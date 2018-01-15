---
title: PictOgr - mój CQRS -2-
date: 2017-04-05
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-moj-cqrs-2
image: /assets/images/2017/04/pictogr-moj-cqrs-3/metro.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
  - Query
short: Po omówieniu komend pora na przejście do zapytań. Ich celem jest odczytywanie danych i z wracanie w odpowiedniej do wymagania formie. Do wykonywania zapytań posłuży szyna zapytań. Dzięki jej zastosowaniu wywołanie zapytania odbywać się może w dowolnym miejscu aplikacji ze wstrzykniętą odpowiednią zależnością.
---
[![CQRS][metro]][metro-big]{:.post-right-image}
Po omówieniu komend pora na przejście do zapytań. Ich celem jest odczytywanie danych i z wracanie w odpowiedniej do wymagania formie.

Do wykonywania zapytań posłuży szyna zapytań. Dzięki jej zastosowaniu wywołanie zapytania odbywać się może w dowolnym miejscu aplikacji ze wstrzykniętą odpowiednią zależnością.

Wykonanie handlera zapytania odbędzie się zawsze w tym samym środowisku (szyna), zawsze będzie opakowane tym samym algorytmem i nie trzeba tutaj się martwić np. o stosowanie wyjątków, logi, gdyż w trakcie wykonywania przez szynę zapytania będzie to standardowo obsłużone.

## Zapytania i szyna zapytań
Interfejs bazowy dla zapytań, musi zawierać typ generyczny jaki zostanie zwrócony.

**IQuery** baza dla wszystkich zapytań.

**TResult** - typ generyczny, określający zwracany wynik wykonania zapytania.
    
Interfejs zapytań.
{% highlight csharp linenos %}
namespace PictOgr.Core.CQRS.Query
{
	public interface IQuery<TResult>
	{
	}
}
{% endhighlight %}
    
**IQueryHandler** - podobnie jak poprzednio (**ICommandHandler**), implementując ten kontrakt tworzymy kod przetwarzający logikę, a następnie zwracany jako typ generyczny **TResult**.
    
Interfejs handlera zapytania.
{% highlight csharp linenos %}
namespace PictOgr.Core.CQRS.Query
{
	public interface IQueryHandler<in TQuery, out TResult> where TQuery : IQuery<TResult>
	{
		TResult Execute(TQuery query);
	}
}
{% endhighlight %}
    
**IQueryBus**, kontrakt dla szyny danych, analogicznie jak dla komend z tą różnicą, iż trzeba uwzględnić typ generyczny **TResult**.

Interfejs szyny zapytań.
{% highlight csharp linenos %}
using PictOgr.Core.CQRS.Query;

namespace PictOgr.Core.CQRS.Bus
{
	public interface IQueryBus
	{
		TResult Process<TQuery, TResult>(TQuery query) where TQuery : IQuery<TResult>;
	}
}
{% endhighlight %}

**QueryBus** to implementacja interfejsu **IQueryBus**.
    
Implementacja szyny zapytań.
{% highlight csharp linenos %}
using System;
using Autofac;
using Autofac.Extras.NLog;
using PictOgr.Core.CQRS.Query;

namespace PictOgr.Core.CQRS.Bus
{
	public class QueryBus : IQueryBus
	{
		private readonly ILifetimeScope container;
		private readonly ILogger logger;

		public QueryBus(ILifetimeScope container, ILogger logger)
		{
			this.container = container;
			this.logger = logger;
		}

		public TResult Process<TQuery, TResult>(TQuery query) where TQuery : IQuery<TResult>
		{
			if (query == null)
			{
				throw new ArgumentNullException(nameof(query));
			}

			var queryHandle = container.Resolve<IQueryHandler<TQuery, TResult>>();

			if (queryHandle == null)
			{
				throw new Exception($"Not found handler for Query: '{query.GetType().FullName}'");
			}

			var result = default(TResult);

			try
			{
				result = queryHandle.Execute(query);
			}
			catch (Exception e)
			{
				logger.Error(e);
			}

			return result;
		}
	}
}
{% endhighlight %}

[![Testy CQRS.][palac]][palac-big]{:.post-left-image}

Proces przetwarzania komendy można przedstawić w następujący sposób:
Przekazanie zapytania do szyny przy pomocy wywołania metody **Process**.
Jeżeli przekazane zapytanie jest pusta, to rzuca wyjątkiem **ArgumentNullException**,
Wyciągnięcie z kontenera (Autofac) handlera dla przekazanego zapytania.
Jeżeli handler jest pusty to rzuca wyjątek **Exception**.
Tworzenie typu zwracanego z domyślnymi wartościami.
Wywołanie zapytania poprzez metodę **Execute** w bloku **try&#8230;catch**.
Jeżeli wywołanie się nie powiedzie to zostanie zapisany log błędu.
Zwracanie wyniku przetwarzania zapytania.

## Pierwsze zapytanie
Poniżej znajduje się pierwsza implementacja zapytania **GetApplicationInformation**, jako typ generyczny wykorzystana jest klasa **ApplicationInformation**, i to właśnie taki obiekt zostanie zwrócony po wykonaniu zapytania.
    
Implementacja zapytania pobierani informacji o aplikacji.
{% highlight csharp linenos %}
using PictOgr.Core.CQRS.Query;
using PictOgr.Core.Models;

namespace PictOgr.Core.Queries
{
	public class GetApplicationInformation : IQuery<ApplicationInformation>
	{
	}
}
{% endhighlight %}

Za logikę wykonania zapytania odpowiedzialny jest handler **GetApplicationInformationHandler**. Jego celem jest pobranie z **Assembly** aktualnej wersji programu, a następnie zwrócenie jako klasę **ApplicationInformation** wyniku wykonania zapytania w metodzie **Execute**.
    
Implementacja handlera zapytania pobierania informacji o aplikacji (wersja).
{% highlight csharp linenos %}
using System.Reflection;
using PictOgr.Core.CQRS.Query;
using PictOgr.Core.Models;

namespace PictOgr.Core.Queries
{
	public class GetApplicationInformationHandler : IQueryHandler<GetApplicationInformation, ApplicationInformation>
	{
		public ApplicationInformation Execute(GetApplicationInformation query)
		{
			var version = Assembly.GetExecutingAssembly().GetName().Version;

			return new ApplicationInformation($"{version.Major}.{version.Minor}.{version.Build}");
		}
	}
}
{% endhighlight %}
    
Model jaki jest zwracany po wykonaniu zapytania **GetApplicationInformation**.
    
Model informacji aplikacji.
{% highlight csharp linenos %}
namespace PictOgr.Core.Models
{
	public class ApplicationInformation
	{
		public ApplicationInformation(string version)
		{
			Version = version;
		}

		public string Version { get; private set; }
	}
}
{% endhighlight %}
    
Użycie zapytania pobierania informacji aplikacji wygląda następująco:

{% highlight csharp linenos %}
var applicationInformation = QueryBus.Process<GetApplicationInformation, ApplicationInformation>(new GetApplicationInformation());
{% endhighlight %}

## Testy
[![Testy CQRS.][stadion-narodowy]][stadion-narodowy-big]{:.post-left-image}
Automatyczne tworzenie obiektów przez **Autofac** przyczynia się do potrzeby nadpisania handlera dla testowanego zapytania.

Tak jak w przypadku komend, należy przygotować mocka dla interfejsu **IQueryHandler**.
    
Dodatkowo określamy co ma zwracać metoda **Execute**, a dokładniej, z jakiego delegata ma skorzystać po jej wywołaniu.

Dlatego każdy test korzystający z klasy **QueryBaseTests**, musi zaimplementować delegata. To pozwoli na dowolną imitację działania logiki zapytań.

Po przygotowaniu obiektu **fake** dla handlera, ponownie rejestrujemy w kontenerze.

Po tej operacji oryginalna metoda **Execute** z handlera jest już nadpisana, i możemy śmiało testować logikę wykonywanych zapytań.

Baza do testowania zapytań.
{% highlight csharp linenos %}
namespace PictOgr.Tests.Core.CQRS.Queries
{
    using System;
    using Autofac;
    using FakeItEasy;
    using PictOgr.Core.AutoFac;
    using PictOgr.Core.CQRS.Bus;
    using PictOgr.Core.CQRS.Query;

    public class QueryBaseTests<TQuery, TResult> where TQuery : IQuery<TResult>
    {
        protected IQueryBus queryBus;

        protected Func<TResult> handleMethod;

        public QueryBaseTests()
        {
            var builder = Container.CreateBuilder();

            var fakeHandler = A.Fake<IQueryHandler<TQuery, TResult>>();

            A.CallTo(() => fakeHandler.Execute(A<TQuery>._)).ReturnsLazily(() => handleMethod.Invoke());

            builder.Register(c => fakeHandler).AsImplementedInterfaces();

            var container = builder.Build();

            queryBus = container.Resolve<IQueryBus>();
        }
    }
}
{% endhighlight %}
    
Implementacja pierwszego testu, do generowania losowych ciągów znaków została wykorzystana biblioteka **AutoFixture**, spowoduje to losowość w trakcie uruchamiania testu.

Do prawidłowego działania testu należy ustawić delegat **handleMethod** (podobnie jak w przypadku testowania komend). W tym przypadku wykorzystujemy lambdę, i ustawiamy klasę jaka zostanie zwrócona przy wywołaniu metody **Process** z handlera dla szyny zapytań.
    
Testowanie zapytania pobierania informacji aplikacji.
{% highlight csharp linenos %}
namespace PictOgr.Tests.Core.CQRS.Queries
{
    using PictOgr.Core.Models;
    using PictOgr.Core.Queries;
    using Ploeh.AutoFixture;
    using Shouldly;
    using Xunit;

    public class GetApplicationInformationTest : QueryBaseTests<GetApplicationInformation, ApplicationInformation>
    {
        private readonly Fixture fixture;

        public GetApplicationInformationTest()
        {
            fixture = new Fixture();
        }

        [Fact]
        public void get_application_version_should_return_the_random_string()
        {
            var version = fixture.Create<string>();
            handleMethod = () => new ApplicationInformation(version);

            var applicationInformation = queryBus.Process<GetApplicationInformation, ApplicationInformation>(new GetApplicationInformation());

            applicationInformation.Version.ShouldBe(version);
        }
    }
}
{% endhighlight %}

Po wykonaniu zapytania można sprawdzić wynik przy pomocy asercji: **applicationInformation.Version.ShouldBe(version);**.

## Na koniec
[![PictOgr - mój CQRS][stadion-narodowy-filar]][stadion-narodowy-filar-big]{:.post-right-image}
Po implementacji komend i zapytań, mamy do dyspozycji bardzo potężny mechanizm, który można wykorzystać jako filar do budowy wielu aplikacji.
    
Wcześniej nigdy nie korzystałem z tego podejścia, nie myślałem nawet o takiej formie.

Moja interpretacja i implementacja zapewne odbiega od ideału.

Kolejnym krokiem będzie wykorzystanie **Event Sourcing**, i być może dodanie walidatorów, jednak to jest już temat na kolejny post.

Rozważam, możliwość wyodrębnienie a projektu **[PictOgr]**, implementacji **CQRS**, tak by w przyszłości można było wielokrotnie wykorzystywać efekty mojej pracy.

**Dziękuję za wytrwałość i zachęcam do komentowania.**{:.h-1}
    
{% include_relative dsp.md %}

[PictOgr]: {{site.url}}/pictogr-pomysl

[stadion-narodowy]: /assets/images/2017/04/pictogr-moj-cqrs-3/stadion-narodowy.png
[stadion-narodowy-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/stadion-narodowy-big.png

[palac]: /assets/images/2017/04/pictogr-moj-cqrs-3/palac.png
[palac-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/palac-big.png

[metro]: /assets/images/2017/04/pictogr-moj-cqrs-3/metro.png
[metro-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/metro-big.png

[stadion-narodowy-filar]: /assets/images/2017/04/pictogr-moj-cqrs-3/stadion-narodowy-filar.png
[stadion-narodowy-filar-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/stadion-narodowy-filar-big.png