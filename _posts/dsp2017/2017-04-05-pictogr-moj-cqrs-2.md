---
id: 589
title: 'PictOgr - mój CQRS -2-'
date: 2017-04-05T00:20:53+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/04/05/pictogr-moj-cqrs-2/
image: /assets/images/2017/04/metro.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
  - Query
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Command Query Responsibility Segregation - 2 -
    </h1>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/04/metro.png"><img class="alignleft wp-image-685 size-medium" src="http://godev.gemustudio.com/assets/images/2017/04/metro-300x200.png" alt="CQRS" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/04/metro-300x200.png 300w, http://godev.gemustudio.com/assets/images/2017/04/metro-768x512.png 768w, http://godev.gemustudio.com/assets/images/2017/04/metro-1024x683.png 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>Po omówieniu komend pora na przejście do zapytań. Ich celem jest odczytywanie danych i z wracanie w odpowiedniej do wymagania formie.
    </p>
    

      Do wykonywania zapytań posłuży szyna zapytań. Dzięki jej zastosowaniu wywołanie zapytania odbywać się może w dowolnym miejscu aplikacji ze wstrzykniętą odpowiednią zależnością.
    </p>
    

      Wykonanie handlera zapytania odbędzie się zawsze w tym samym środowisku (szyna), zawsze będzie opakowane tym samym algorytmem i nie trzeba tutaj się martwić np. o stosowanie wyjątków, logi, gdyż w trakcie wykonywania przez szynę zapytania będzie to standardowo obsłużone.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Zapytania i szyna zapytań
    </h1>
    
    <p>
      Interfejs bazowy dla zapytań, musi zawierać typ generyczny jaki zostanie zwrócony.
    </p>
    
    <p>
      **IQuery** baza dla wszystkich zapytań
    </p>
    
    <p>
      **TResult** - typ generyczny, określający zwracany wynik wykonania zapytania.
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs zapytań.">namespace PictOgr.Core.CQRS.Query
{
	public interface IQuery&lt;TResult&gt;
	{
	}
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      **IQueryHandler** - podobnie jak poprzednio (**ICommandHandler**), implementując ten kontrakt tworzymy kod przetwarzający logikę, a następnie zwracany jako typ generyczny **TResult**.
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs handlera zapytania.">namespace PictOgr.Core.CQRS.Query
{
	public interface IQueryHandler&lt;in TQuery, out TResult&gt; where TQuery : IQuery&lt;TResult&gt;
	{
		TResult Execute(TQuery query);
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      **IQueryBus**, kontrakt dla szyny danych, analogicznie jak dla komend z tą różnicą, iż trzeba uwzględnić typ generyczny** TResult**.
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs szyny zapytań.">using PictOgr.Core.CQRS.Query;

namespace PictOgr.Core.CQRS.Bus
{
	public interface IQueryBus
	{
		TResult Process&lt;TQuery, TResult&gt;(TQuery query) where TQuery : IQuery&lt;TResult&gt;;
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      **QueryBus** to implementacja interfejsu **IQueryBus**.
    </p>
    
    <pre class="lang:c# decode:true" title="Implementacja szyny zapytań.">using System;
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

		public TResult Process&lt;TQuery, TResult&gt;(TQuery query) where TQuery : IQuery&lt;TResult&gt;
		{
			if (query == null)
			{
				throw new ArgumentNullException(nameof(query));
			}

			var queryHandle = container.Resolve&lt;IQueryHandler&lt;TQuery, TResult&gt;&gt;();

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
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <h4 style="text-align: justify;">
      Proc<a href="http://godev.gemustudio.com/assets/images/2017/04/pałąc_kultury_i_nauki_2.png"><img class="alignleft wp-image-688 " src="http://godev.gemustudio.com/assets/images/2017/04/pałąc_kultury_i_nauki_2-200x300.png" alt="" width="152" height="228" srcset="http://godev.gemustudio.com/assets/images/2017/04/pałąc_kultury_i_nauki_2-200x300.png 200w, http://godev.gemustudio.com/assets/images/2017/04/pałąc_kultury_i_nauki_2-768x1152.png 768w, http://godev.gemustudio.com/assets/images/2017/04/pałąc_kultury_i_nauki_2-683x1024.png 683w, http://godev.gemustudio.com/assets/images/2017/04/pałąc_kultury_i_nauki_2.png 1280w" sizes="(max-width: 152px) 100vw, 152px" /></a>es przetwarzania komendy można przedstawić w następujący sposób:
    </h4>
    
    <p>
      &nbsp;
    </p>
    
    <ol>
      <li style="text-align: justify;">
        Przekazanie zapytania do szyny przy pomocy wywołania metody <b>Process</b>.
      </li>
      <li style="text-align: justify;">
        Jeżeli przekazane zapytanie jest pusta, to rzuca wyjątkiem **ArgumentNullException**,
      </li>
      <li style="text-align: justify;">
        Wyciągnięcie z kontenera (Autofac) handlera dla przekazanego zapytania.
      </li>
      <li style="text-align: justify;">
        Jeżeli handler jest pusty to rzuca wyjątek **Exception**.
      </li>
      <li style="text-align: left;">
        Tworzenie typu zwracanego z domyślnymi wartościami.
      </li>
      <li style="text-align: justify;">
        Wywołanie zapytania poprzez metodę **Execute** w bloku **try&#8230;catch**.
      </li>
      <li style="text-align: justify;">
        Jeżeli wywołanie się nie powiedzie to zostanie zapisany log błędu.
      </li>
      <li style="text-align: justify;">
        Zwracanie wyniku przetwarzania zapytania.
      </li>
    </ol>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Pierwsze zapytanie
    </h1>
    

      Poniżej znajduje się pierwsza implementacja zapytania **GetApplicationInformation**, jako typ generyczny wykorzystana jest klasa **ApplicationInformation**, i to właśnie taki obiekt zostanie zwrócony po wykonaniu zapytania.
    </p>
    
    <pre class="lang:c# decode:true" title="Implementacja zapytania pobierani informacji o aplikacji.">using PictOgr.Core.CQRS.Query;
using PictOgr.Core.Models;

namespace PictOgr.Core.Queries
{
	public class GetApplicationInformation : IQuery&lt;ApplicationInformation&gt;
	{
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Za logikę wykonania zapytania odpowiedzialny jest handler **GetApplicationInformationHandler**. Jego celem jest pobranie z **Assembly** aktualnej wersji programu, a następnie zwrócenie jako klasę **ApplicationInformation** wyniku wykonania zapytania w metodzie **Execute**.
    </p>
    
    <pre class="lang:c# decode:true" title="Implementacja handlera zapytania pobierania informacji o aplikacji (wersja).">using System.Reflection;
using PictOgr.Core.CQRS.Query;
using PictOgr.Core.Models;

namespace PictOgr.Core.Queries
{
	public class GetApplicationInformationHandler : IQueryHandler&lt;GetApplicationInformation, ApplicationInformation&gt;
	{
		public ApplicationInformation Execute(GetApplicationInformation query)
		{
			var version = Assembly.GetExecutingAssembly().GetName().Version;

			return new ApplicationInformation($"{version.Major}.{version.Minor}.{version.Build}");
		}
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Model jaki jest zwracany po wykonaniu zapytania **GetApplicationInformation**.
    </p>
    
    <pre class="lang:c# decode:true" title="Model informacji aplikacji.">namespace PictOgr.Core.Models
{
	public class ApplicationInformation
	{
		public ApplicationInformation(string version)
		{
			Version = version;
		}

		public string Version { get; private set; }
	}
}</pre>
    
    <p>
      Użycie zapytania pobierania informacji aplikacji wygląda następująco:
    </p>
    
    <p>
      <em>var applicationInformation = QueryBus.Process<GetApplicationInformation, ApplicationInformation>(new GetApplicationInformation());</em>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Testy
    </h1>
    

      Automatyczne tworzenie obiektów przez **Autofac** przyczynia się do potrzeby nadpisania handlera dla testowanego zapytania.
    </p>
    

      Tak<a href="http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy.png"><img class="size-medium wp-image-690 alignleft" src="http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy-300x200.png" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy-300x200.png 300w, http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy-768x512.png 768w, http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy-1024x683.png 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a> jak w przypadku komend, należy przygotować mocka dla interfejsu **IQueryHandler**.
    </p>
    

      Dodatkowo określamy co ma zwracać metoda **Execute**, a dokładniej, z jakiego delegata ma skorzystać po jej wywołaniu.
    </p>
    

      Dlatego każdy test korzystający z klasy **QueryBaseTests**, musi zaimplementować delegata. To pozwoli na dowolną imitację działania logiki zapytań.
    </p>
    
    <p>
      Po przygotowaniu obiektu **fake** dla handlera, ponownie rejestrujemy w kontenerze.
    </p>
    
    <p>
      Po tej operacji oryginalna metoda **Execute** z handlera jest już nadpisana, i możemy śmiało testować logikę wykonywanych zapytań.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <pre class="lang:c# decode:true" title="Baza do testowania zapytań.">namespace PictOgr.Tests.Core.CQRS.Queries
{
    using System;
    using Autofac;
    using FakeItEasy;
    using PictOgr.Core.AutoFac;
    using PictOgr.Core.CQRS.Bus;
    using PictOgr.Core.CQRS.Query;

    public class QueryBaseTests&lt;TQuery, TResult&gt; where TQuery : IQuery&lt;TResult&gt;
    {
        protected IQueryBus queryBus;

        protected Func&lt;TResult&gt; handleMethod;

        public QueryBaseTests()
        {
            var builder = Container.CreateBuilder();

            var fakeHandler = A.Fake&lt;IQueryHandler&lt;TQuery, TResult&gt;&gt;();

            A.CallTo(() =&gt; fakeHandler.Execute(A&lt;TQuery&gt;._)).ReturnsLazily(() =&gt; handleMethod.Invoke());

            builder.Register(c =&gt; fakeHandler).AsImplementedInterfaces();

            var container = builder.Build();

            queryBus = container.Resolve&lt;IQueryBus&gt;();
        }
    }
}
</pre>
    
    <p>
      &nbsp;
    </p>
    

      Implementacja pierwszego testu, do generowania losowych ciągów znaków została wykorzystana biblioteka **AutoFixture**, spowoduje to losowość w trakcie uruchamiania testu.
    </p>
    

      Do prawidłowego działania testu należy ustawić delegat **handleMethod** (podobnie jak w przypadku testowania komend). W tym przypadku wykorzystujemy lambdę, i ustawiamy klasę jaka zostanie zwrócona przy wywołaniu metody **Process** z handlera dla szyny zapytań.
    </p>
    
    <pre class="lang:c# decode:true" title="Testowanie zapytania pobierania informacji aplikacji.">namespace PictOgr.Tests.Core.CQRS.Queries
{
    using PictOgr.Core.Models;
    using PictOgr.Core.Queries;
    using Ploeh.AutoFixture;
    using Shouldly;
    using Xunit;

    public class GetApplicationInformationTest : QueryBaseTests&lt;GetApplicationInformation, ApplicationInformation&gt;
    {
        private readonly Fixture fixture;

        public GetApplicationInformationTest()
        {
            fixture = new Fixture();
        }

        [Fact]
        public void get_application_version_should_return_the_random_string()
        {
            var version = fixture.Create&lt;string&gt;();
            handleMethod = () =&gt; new ApplicationInformation(version);

            var applicationInformation = queryBus.Process&lt;GetApplicationInformation, ApplicationInformation&gt;(new GetApplicationInformation());

            applicationInformation.Version.ShouldBe(version);
        }
    }
}
</pre>
    
    <p>
      Po wykonaniu zapytania można sprawdzić wynik przy pomocy asercji:<em>** **applicationInformation.Version.ShouldBe(version);</em>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Na koniec
    </h1>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy_filar.png"><img class="size-medium wp-image-691 alignright" src="http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy_filar-200x300.png" alt="" width="200" height="300" srcset="http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy_filar-200x300.png 200w, http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy_filar-768x1152.png 768w, http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy_filar-683x1024.png 683w, http://godev.gemustudio.com/assets/images/2017/04/stadion_narodowy_filar.png 1280w" sizes="(max-width: 200px) 100vw, 200px" /></a>Po implementacji komend i zapytań, mamy do dyspozycji bardzo potężny mechanizm, który można wykorzystać jako filar do budowy wielu aplikacji.
    </p>
    

      Wcześniej nigdy nie korzystałem z tego podejścia, nie myślałem nawet o takiej formie.
    </p>
    

      Moja interpretacja i implementacja zapewne odbiega od ideału.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Kolejnym krokiem będzie wykorzystanie **Event Sourcing**, i być może dodanie walidatorów, jednak to jest już temat na kolejny post.
    </p>
    
    <p>
      Rozważam, możliwość wyodrębnienie a projektu <a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/">**PictOgr**</a>, implementacji **CQRS**, tak by w przyszłości można było wielokrotnie wykorzystywać efekty mojej pracy.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      **Dziękuję za wytrwałość i zachęcam do komentowania.**
    </h3>
    
{% include_relative dsp.md %}