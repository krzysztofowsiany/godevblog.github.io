---
title: PictOgr - mój CQRS -3-
date: 2017-04-12
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-moj-cqrs-3
image: /assets/images/2017/04/pictogr-moj-cqrs-3/event2.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - Event Sourcing
  - EventBus
  - PictOgr
short: Niniejszy wpis dotyczy implementacji Event Sourcingu w moim CQRSie. Jest to kolejna szyna wykorzystywana na różne sposoby. Można np. zachować (jeżeli system cały system oparty jest o CQRS/ES) stan aplikacji w poszczególnych etapach jej życia. Zapis stanów musi odbyć sie np. w bazie danych.
---
[![CQRS][image1]][image1-big]{:.post-left-image}
Niniejszy wpis dotyczy implementacji **Event Sourcingu** w moim **CQRSie**. Jest to kolejna szyna wykorzystywana na różne sposoby.

Można np. zachować (jeżeli system cały system oparty jest o **CQRS/ES**) stan aplikacji w poszczególnych etapach jej życia. Zapis stanów musi odbyć sie np. w bazie danych. Nie mniej jednak pozwoli to na przedstawienie historii od **A** do **Z** cyklu życia.

Dokładnie po wykonaniu każdej z komend jak zmienia się model aplikacji. Zdarzenia wyzalane są z komend.

Zastosowanie zdarzeń pozwoli na powiadamianie różnych obszarów aplikacji o zmianie stanu aplikacji.

## Zdarzenia i szyna zdarzeń
**IEvent** interfejs bazowy dla wszystkich zapytań, klas implementująca zostanie przekazana do zarejestrowanych obserwatorów.
    
Interfejs zdarzeń.
{% highlight csharp linenos %}
namespace PictOgr.Core.CQRS.Event
{
	public interface IEvent
	{
	}
}
{% endhighlight %}

**IEventHandler** - podobnie jak poprzednio (**IQueryHandler**), implementując ten kontrakt tworzymy kod przetwarzający logikę.
    
Interfejs handlera zdarzeń.
{% highlight csharp linenos %}
namespace PictOgr.Core.CQRS.Event
{
	public interface IEventHandler&lt;TEvent&gt; where TEvent : IEvent
	{
		void Handle(TEvent @event);
	}
}
{% endhighlight %}

**@event** - jak wiadomo event to słowo kluczowe języka c#, jednak można to obejść wykorzystując znak małpki **‚@’**, nakazujemy kompilatorowi, iż nie chcemy skorzystać ze słowa kluczowego **event**, a jedynie użyć jako nazway zmiennej.

**IEventBus**, kontrakt dla szyny zdarzeń, w tym przypadku klasa implementująca musi zawierać trzy metody:
* **Register** - służy do rejestrowania obserwatora zdarzenia,
* **UnRegister** - analogicznie tą metodą wyrzucamy obserwatora zdarzeń,
* **Publish** - dzięki tej metodzie przekazujemy wszystkim słuchaczom zdarzenie.
    
Interfejs szyny zdarzeń.
{% highlight csharp linenos %}
namespace PictOgr.Core.CQRS.Bus.Event
{
	using CQRS.Event;

	public interface IEventBus
	{
		void Register&lt;TEvent&gt;(IEventHandler&lt;TEvent&gt; eventHandler) where TEvent : IEvent;

		void UnRegister&lt;TEvent&gt;(IEventHandler&lt;TEvent&gt; eventHandler) where TEvent : IEvent;

		void Publish&lt;TEvent&gt;(TEvent @event) where TEvent : IEvent;
	}
}
{% endhighlight %}

**EventBus** to implementacja interfejsu **IEventBus**.
    
Implementacja szyny zdarzeń.
{% highlight csharp linenos %}
namespace PictOgr.Core.CQRS.Bus.Event
{
	using System;
	using System.Collections.Generic;
	using Autofac.Extras.NLog;
	using CQRS.Event;

	public class EventBus : IEventBus
	{
		private readonly ILogger logger;

		private static Dictionary&lt;Type, List&lt;object&gt;&gt; eventList = new Dictionary&lt;Type, List&lt;object&gt;&gt;();

		public EventBus(ILogger logger)
		{
			this.logger = logger;
		}

		public void Register&lt;TEvent&gt;(IEventHandler&lt;TEvent&gt; eventHandler) where TEvent : IEvent
		{
			List&lt;object&gt; eventHandlers;

			if (!eventList.ContainsKey(typeof(TEvent)))
			{
				eventList.Add(typeof(TEvent), new List&lt;object&gt;());
			}

			if (!eventList.TryGetValue(typeof(TEvent), out eventHandlers))
			{
				return;
			}

			try
			{
				if (!eventHandlers.Contains(eventHandler))
				{
					eventHandlers.Add(eventHandler);
				}
			}
			catch (Exception e)
			{
				logger.Error(e);
			}
		}

		public void UnRegister&lt;TEvent&gt;(IEventHandler&lt;TEvent&gt; eventHandler) where TEvent : IEvent
		{
			List&lt;object&gt; eventHandlers;

			if (!eventList.TryGetValue(typeof(TEvent), out eventHandlers))
			{
				throw new TypeUnloadedException(nameof(TEvent));
			}

			try
			{
				eventHandlers.Remove(eventHandler);

				if (eventHandlers.Count == 0)
				{
					eventList.Remove(typeof(TEvent));
				}
			}
			catch (Exception e)
			{
				logger.Error(e);
			}
		}

		public void Publish&lt;TEvent&gt;(TEvent @event) where TEvent : IEvent
		{
			List&lt;object&gt; eventHandlers;
			if (!eventList.TryGetValue(typeof(TEvent), out eventHandlers))
			{
				throw new TypeUnloadedException(nameof(TEvent));
			}

			try
			{
				foreach (var eventHandler in eventHandlers)
				{
					(eventHandler as IEventHandler&lt;TEvent&gt;)?.Handle(@event);
				}
			}
			catch (Exception e)
			{
				logger.Error(e);
			}
		}
	}
}
{% endhighlight %}

Lista eventList = new Dictionary<Type, List<object>>();

Jest to lista zdarzeń, do której zostaną, która to dopiero będzie powiązana z listą obserwatorów.
[![CQRS][event2]][event2-big]{:.post-right-image}

[**IEvent** => { **IEventHandler**, **IEventHandler**, **IEventHandler**, etc.}]
Metoda **Register**, sprawdza czy IEventHanlder jest już zarejestrowany, jeśli nie to dodaje do listy.
**UnRegister**, sprawdza czy IEventHandler jest na liście, jeżeli jest to usuwa.
**Publish** - iteruje po wszystkich IEvent, oraz podległych IEventHandlerach i publikuje zdarzenie.

## Testy
Klasę testu zaczynamy od ustawienia (**TearUp**) podstawowych/najczęściej używanych w testach obiektów jak **container**, **fakeEvent**, **eventFakeInvoke**, **fakeEventHandler**.
    
Klasa do testowania zdarzeń.
{% highlight csharp linenos %}
namespace PictOgr.Tests.Core.CQRS.Events
{
	using System.Collections.Generic;
	using System;
	using Autofac;
	using FakeItEasy;
	using PictOgr.Core.AutoFac;
	using PictOgr.Core.CQRS.Bus.Event;
	using PictOgr.Core.CQRS.Event;
	using Shouldly;
	using Xunit;

	public class EventdBusTest : IDisposable
	{
		private readonly IContainer container;
		private readonly IEvent eventFromInvoke;
		private readonly IEvent fakeEvent;
		private readonly IEventHandler&lt;IEvent&gt; fakeEventHandler;

		public EventdBusTest()
		{
			container = Container.CreateBuilder().Build();

			fakeEvent = A.Fake&lt;IEvent&gt;();

			fakeEventHandler = A.Fake&lt;IEventHandler&lt;IEvent&gt;&gt;();

			A.CallTo(() =&gt; fakeEventHandler.Handle(A&lt;IEvent&gt;._))
				  .Invokes((IEvent ev) =&gt;
				  {
					  eventFromInvoke = ev;
				  });
		}
{% endhighlight %}

Na końcu konstruktora tworzymy **fake** dla metody **Handler**, tak by pobierać **event** jaki jest do niej przekazywany jako parametr, tak na zaś do assertów.

Pierwszy teścik taki symboliczny, czy faktycznie **EventBus** to **EventBus** prosto z **AutoFac**-a.

Test poprawności pobierania szyny zdarzeń z kontenera AutoFac.
{% highlight csharp linenos %}
[Fact]
public void test_event_bus_are_correct_resolved()
{
	using (var scope = container.BeginLifetimeScope())
	{
		var eventBus = scope.Resolve&lt;IEventBus&gt;();

		eventBus.ShouldBeOfType&lt;EventBus&gt;();
	}
}
{% endhighlight %}

Jak się powodzi to lecimy dalej.

A tutaj to sprawdzimy czy szyna zdarzeń po publikacji (**Publish**) oszukanego zdarzenia (**fakeEvent**) rzuci wyjąteczkiem **TypeUnloadedException**.
    
Próba publikacji zdarzenia, na pustą szynę, rzuca wyjątkiem.
{% highlight csharp linenos %}
[Fact]
public void event_bus_publish_should_throw_excetion()
{
	using (var scope = container.BeginLifetimeScope())
	{
		var eventBus = scope.Resolve&lt;IEventBus&gt;();

		var fakeEvent = A.Fake&lt;IEvent&gt;();

		Should.Throw&lt;TypeUnloadedException&gt;(() =&gt; { eventBus.Publish(fakeEvent); });
	}
}
{% endhighlight %}

A no bo **POWINNA**!

Teraz to już powinno być dobrze, pierwsza publikacja i odebranie prawidłowego **IEvent**, część kodu zawarta w **TearUp**, tak że tutaj prościutko.
    
Próba publikacji zdarzenia z wyrejestrowanie, powinna się powieść.
{% highlight csharp linenos %}
[Fact]
public void event_bus_register_should_add_event_handler()
{
	using (var scope = container.BeginLifetimeScope())
	{
		var eventBus = scope.Resolve&lt;IEventBus&gt;();

		eventBus.Register(fakeEventHandler);
		eventBus.Publish(fakeEvent);
		eventBus.UnRegister(fakeEventHandler);

		eventFromInvoke.ShouldBeSameAs(fakeEvent);
	}
}
{% endhighlight %}

Odebrany **IEvent** musi być taki sam jak ten publikowany!

A tutaj sobie sprawdzimy jak działa **Register** i **UnRegister**.
    
Rzucanie wyjątkiem dla zarejestrowanego a następnie wyrejestrowanego hanldera.
{% highlight csharp linenos %}
public void event_bus_register_and_unregister_should_throw_exception_when_publish()
{
    using (var scope = container.BeginLifetimeScope())
    {
        var eventBus = scope.Resolve&lt;IEventBus&gt;();
 
        eventBus.Register(fakeEventHandler);
        eventBus.UnRegister(fakeEventHandler);
 
        Should.Throw&lt;TypeUnloadedException&gt;(() =&gt; { eventBus.Publish(fakeEvent); });
        eventFromInvoke.ShouldBeNull();
    }
}
{% endhighlight %}

Zarejestrowany **IEventHandler** i wyrejestrowany po publikacji wali wyjątkiem **TypeUnloadedException**!

Ostatni tłusty teścik rejestruje aż 100 IEventHandlerów, po czym publikuje do nich **fakeEvent**-a.
    
Rejestrowanie 100 handlerów, i sprawdzanie czy otrzymują 100 prawidłowych zdarzeń.
{% highlight csharp linenos %}
[Fact]
public void event_bus_register_many_handlers_should_add_event_handler()
{
	using (var scope = container.BeginLifetimeScope())
	{
		var count = 100;
		var eventBus = scope.Resolve&lt;IEventBus&gt;();
		var eventHanlders = new List&lt;IEventHandler&lt;IEvent&gt;&gt;();
		var events = new List&lt;IEvent&gt;();

		for (var i = 0; i &lt; count; i++)
		{
			var eventHanlder = A.Fake&lt;IEventHandler&lt;IEvent&gt;&gt;();
			eventHanlders.Add(eventHanlder);

			A.CallTo(() =&gt; eventHanlder.Handle(A&lt;IEvent&gt;._))
				.Invokes((IEvent ev) =&gt;
				{
					events.Add(ev);
				});

			eventBus.Register(eventHanlder);
		}

		eventBus.Publish(fakeEvent);

		for (var i = 0; i &lt; count; i++)
		{
			eventBus.UnRegister(eventHanlders[i]);
		}

		foreach (var @event in events)
		{
			@event.ShouldBeSameAs(fakeEvent);
		}
	}
}
{% endhighlight %}

Tym samym powinno dojść 100 oszukanych eventów zapisanych do listy.

Na końcu to już wyrejestrowanie handlerków, i sprawdzenie czy faktycznie te 100 eventów jest oszukanych (**fakeEvent**).

## Na koniec
[![CQRS][event]][event-big]{:.post-left-image}
Co prawda więcej w poście kodu niż treści, ale myślę, że zrozumiały tekst.

W kolejnym poście połączymy **ES** z **CQRS**, oraz dodamy zapowiadane na ten post walidatory.

**Dziękuję za wytrwałość i zachęcam do komentowania.**{:h-1}

{% include_relative dsp.md %}

[event]: /assets/images/2017/04/pictogr-moj-cqrs-3/event.png
[event-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/event-big.png

[event2]: /assets/images/2017/04/pictogr-moj-cqrs-3/event2.png
[event2-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/event2-big.png

[image1]: /assets/images/2017/04/pictogr-moj-cqrs-3/image1.jpg
[image1-big]: /assets/images/2017/04/pictogr-moj-cqrs-3/image1-big.jpg
