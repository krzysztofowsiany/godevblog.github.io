---
title: PictOgr - cebulka + moje pierwsze DDD.
date: 2017-04-26
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-cebulka-pierwsze-ddd
image: /assets/images/2017/04/pictogr-cebulka-pierwsze-ddd/post.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - CQRS
  - dajsiepoznac2017
  - DDD
  - DSP2017
  - Onion
  - PictOgr
short: Udało się ugotować cebulkę, projekt wygląda znacznie lepiej aniżeli wcześniej. I dodatkowo ma większe możliwości. Stworzyłem też moje pierwsze DDD (Domain-Driven Design), ostatnio zachorowałem...
---
[![Clean Architecture][post]][post-big]{:.post-right-image}
Udało się ugotować cebulkę, projekt wygląda znacznie lepiej aniżeli wcześniej. I dodatkowo ma większe możliwości.
Stworzyłem też moje pierwsze **DDD (Domain-Driven Design)**, ostatnio zachorowałem w tym kierunku (tak jak CQRS i Onion), i pragnę zgłębiac temat&#8230;

Zmiana architektury na tak wczesnym etapie projektu nie była zbyt bolesna. Tym bardziej, iż CQRS został wyodrębniony wcześniej.

**Jest to moje pierwsze praktyczne zetknięcie z Clean Architecture (lamer).**

**PictOgr** obecnie składa się z 7 projektów tak jak to widać na pierwszym zrzucie.

## Zmiany
![Onion Architecture][pictogr-infrastructure]{:.post-left-image}    
     
Wydzieliłem warstwę domeny w projekcie Core.    

Infrastructure zawiera wykorzystane usług, **CQRS**, implementacje repozytoriuów, **Autofac**, **DTO**, **AutoMapper**, i inne potrzebne elementy, bardziej szczegółowy wykaz na drugim zrzucie.

GUI aplikacji znajdować się będzie w projekcie **MVVM**, czyli XAMLe, **ViewModele** oraz moduły dla **Autofaca**.

Dodałem też projekt, w którym znajdą się testy integracyjne o nazwie E2E.

**Zmiana architektury niesie ze sobą kilka zmian dotyczących mechanizmów działania aplikacji!**

## Użycie eventa do zamykania okien
Na pierwszy ogień, klasa implementująca (**IEvent**) zdarzenie zamykania aplikacji.

Zdarzenie zamykania aplikacji.
{% highlight csharp linenos %}
using CQRS.Event;

namespace PictOgr.Infrastructure.Events
{
	public class ExitApplicationEvent : IEvent
	{
	    public ExitApplicationEvent(int exitCode)
	    {
	        
	    }
	}
}
{% endhighlight %}

Powyższa klasa jest wykorzystywana przez powiązanego Handlera o nazwie **ExitApplicationEventHandler**.

Jej celem  jest wywołanie przekazanego **delegata** do zamykania apikacji w metodzie **Handle**. To spowoduje zamknięcie okienka.
    
Handler zdarzenia zamykania aplikacji.
{% highlight csharp linenos %}
using System;
using CQRS.Event;

namespace PictOgr.Infrastructure.Events
{
    public class ExitApplicationEventHandler : IEventHandler&lt;ExitApplicationEvent&gt;
    {
        private readonly Action action;

        public ExitApplicationEventHandler(Action action)
        {
            this.action = action;
        }

        public void Handle(ExitApplicationEvent @event)
        {
            action();
        }
    }
}
{% endhighlight %}

Rejestrowanie handlera i przekazanie delegato do zamknięcia okienka.
    
Rejestrowanie handlera do zdarzenia zamykania aplikacji.
{% highlight csharp linenos %}
eventBus.Register(new ExitApplicationEventHandler(() =>
{
	Close();
}));
{% endhighlight %}
    
Pozostaje jedynie w odpowiedniej komendzie **ExitApplicationHandler** wykonać publikacje zdarzenia **ExitApplicationEvent **do szyny zdarzeń.

Efektem jest zamknięcie wszystkich okienek w których zarejestrowany jest handler **ExitApplicationEventHandler** (kod wyżej).
    
Publikowanie zdarzenia na szynę w handlerze comendy zamykania aplikacji.
{% highlight csharp linenos %}
public void Handle(ExitApplication command)
{
    _logger.Info("Exit application.");
    _eventBus.Publish(new ExitApplicationEvent(command.ExitCode));
    System.Environment.Exit(command.ExitCode);
}
{% endhighlight %}

## Wykorzystanie usług w zapytaniach CQRSa
Do przekazywania danych pomiędzy aplikacją, a modelem wykorzystana będzie odrębna klasa określana jako **DTO (Data Transfer Object)**.
Dzięki takiemu odseparowaniu aplikacja nic nie wie o modelu domeny jaki zaimplementujemy w aplikacji.
    
Klasa informacji o aplikacji, DTO - Data Transfer Object, do przekazania informacji od modelu domenowego.
{% highlight csharp linenos %}
namespace PictOgr.Infrastructure.DTO
{
	public class ApplicationInformationDto
	{
		public string Version { get; set; }
	}
}
{% endhighlight %}
    
Dane pomiędzy modelem domeny a klasą DTO muszą być przekazane, i można to zrobić pod górkę poprostu przepisaując właściwości z wykorzystaniem klasy pośredniczącej (np. jakiegoś Adaptera), lub zywkorzytaniem biblioteczki **[AutoMapper]**.

Poniżej znajduje się konfiguracja AutoMappera dla klas **ApplicationInformation** <=> **ApplicationInformationDto**.
    
Mapowanie obiektu domeny na obiekt DTO.
{% highlight csharp linenos %}    
using AutoMapper;
using PictOgr.Core.Domain;
using PictOgr.Infrastructure.DTO;

namespace PictOgr.Infrastructure.Mappers
{
	public static class AutoMapperConfig
	{
		public static IMapper Initialize() =&gt; new MapperConfiguration(config =&gt;
		{
			config.CreateMap<ApplicationInformation, ApplicationInformationDto>();
			config.CreateMap<ApplicationInformationDto, ApplicationInformation>();

		}).CreateMapper();
	}
}
{% endhighlight %}

Konfiguracje ustawiamy dwu kierunkowo oznacza to iż będzie można mapować dane w obu kierunkach:
* **ApplicationInformation** = **ApplicationInformationDto**{:.color_1},
* **ApplicationInformationDto**{:.color_1} = **ApplicationInformation**.

Do pobierania danych z domeny użyjemy tym razem usługi, do jej implementacji wykorzytsamy interfejsik **IApplicaitonService**, zawierający definicję metody pobierania informacji o aplikacji.

Interfejsik dla usług aplikacji.
{% highlight csharp linenos %}
using PictOgr.Infrastructure.DTO;

namespace PictOgr.Infrastructure.Services.ApplicationService
{
	public interface IApplicationService
	{
		ApplicationInformationDto GetApplicationInformation();
	}
}
{% endhighlight %}
    
Interfejs **IApplicaitonService**, jest zaimplementowany przez poniższą klasę **ApplicationService**.
    
Usługa aplikacji implementująca swój interfejsik.
{% highlight csharp linenos %}
using AutoMapper;
using PictOgr.Core.Domain;
using PictOgr.Core.Repositories;
using PictOgr.Infrastructure.DTO;

namespace PictOgr.Infrastructure.Services.ApplicationService
{
	public class ApplicationService : IApplicationService
	{
		private readonly IApplicationInformationRepository _applicationInformationRepository;
		private readonly IMapper _mapper;

		public ApplicationService(
			IApplicationInformationRepository applicationInformationRepository,
			IMapper mapper)
		{
			_applicationInformationRepository = applicationInformationRepository;
			_mapper = mapper;
		}

		public ApplicationInformationDto GetApplicationInformation()
		{
			var applicationInformation = _applicationInformationRepository.GetApplicationInformation();

			return _mapper.Map&lt;ApplicationInformation, ApplicationInformationDto&gt;(applicationInformation);
		}
	}
}
{% endhighlight %}

W klasie usługi po pobraniu danych z repozytorium odbywa się mapowanie:
{% highlight csharp linenos %}
return _mapper.Map<ApplicationInformation, ApplicationInformationDto>(applicationInformation);
{% endhighlight %}
Efektem jest przeniesienie danych z obiektu domenowego do obiektu DTO.
    
## Użycie modelu domeny do pobrania informacji o aplikacji
Pierwszy obiekt w moim modelu domeny. To klasa z informacjami o aplikacji.

Bardzo banalna, różni się w zasadzie od klasy z nią powiązanej (**DTO**), wykorzystaniem konstruktora i możliwością ustawienia właściwości **Version** jedynie właśnie z tego konstruktora (lub metod klasy).
    
Obiekt domeny zawierający informacje o aplikacji.
{% highlight csharp linenos %}
namespace PictOgr.Core.Domain
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
    
Jest tutaj też interfejsik z **repozytorium** pobierania informacji o aplikacji, owe repozytorium będzie implementowane dopiero w warstiwe wyżej (**Infrastrukture**). Repozytorium jest ściśle związane z modelem **ApplicationInformation**.
    
Interfejsik repozytorium pobierania informacji o aplikacji.
{% highlight csharp linenos %}
using PictOgr.Core.Domain;

namespace PictOgr.Core.Repositories
{
	public interface IApplicationInformationRepository
	{
		ApplicationInformation GetApplicationInformation();
	}
}
{% endhighlight %}
    
Jedna metoda pobierania informacji jest implementowana w klasie repozytorium **ApplicationInformationRepository**, implementuje ona interfejs z modelu domeny **IApplicaitonInformationRepository**, i dostarcza informacji o aplikacji.
    
Implementacja repozytorium pobierania danych o aplikacji (warstwa infrastruktury).
{% highlight csharp linenos %}
using System.Reflection;
using PictOgr.Core.Domain;
using PictOgr.Core.Repositories;

namespace PictOgr.Infrastructure.Repositories
{
	public class ApplicationInformationRepository: IApplicationInformationRepository
	{
		public ApplicationInformation GetApplicationInformation()
		{
			var version = Assembly.GetExecutingAssembly().GetName().Version;
			return new ApplicationInformation($"{version.Major}.{version.Minor}.{version.Build}");
		}
	}
}
{% endhighlight %}
    
Na chwilę obecną jest to tylko wersja plikacji, jednak z czasem może ulec rozbudowie o więcej ciekawych infomracji.
**To tyle z dużych zmian w projekcie, myślę iż teraz pujdzie już znacznie lepiej (dla oka = GUI).**

## Zakończenie
Tak wiem jest to prosty przykład, zapewne wogule nie powinno się robić w ten sposób. Jednak się uczę, i taki przykład dostarcza mi dużo doświadczenia.

Dlatego też postanowiłem zrobić to w ten sposób, być może ktoś dzięki temu wpisowi zrozumie coś wiecej&#8230;

## **Dziękuję za wytrwałość i zachęcam do komentowania.**
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/04/pictogr-cebulka-pierwsze-ddd/post.png
[post-big]: /assets/images/2017/04/pictogr-cebulka-pierwsze-ddd/post-big.png

[onion]: /assets/images/2017/04/pictogr-cebulka-pierwsze-ddd/onion.png
[onion-big]: /assets/images/2017/04/pictogr-cebulka-pierwsze-ddd/onion-big.png

[pictogr-infrastructure]: /assets/images/2017/04/pictogr-cebulka-pierwsze-ddd/pictogr-infrastructure.png

[AutoMapper]: http://automapper.org

