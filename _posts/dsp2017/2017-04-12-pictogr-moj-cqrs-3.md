---
id: 768
title: 'PictOgr &#8211; mój CQRS -3-'
date: 2017-04-12T21:43:58+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/04/12/pictogr-moj-cqrs-3/
image: /assets/images/2017/04/event.png
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
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Command Query Responsibility Segregation &#8211; 3 &#8211;
    </h1>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/04/IMG-2015-08-03-8084.jpg"><img class="alignleft wp-image-818 size-medium" src="http://godev.gemustudio.com/assets/images/2017/04/IMG-2015-08-03-8084-300x200.jpg" alt="CQRS" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/04/IMG-2015-08-03-8084-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/04/IMG-2015-08-03-8084-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/04/IMG-2015-08-03-8084-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a> <a href="http://godev.gemustudio.com/assets/images/2017/04/event.png"><br /> </a>Niniejszy wpis dotyczy implementacji <strong>Event Sourcingu</strong> w moim <strong>CQRSie</strong>. Jest to kolejna szyna wykorzystywana na różne sposoby.
    </p>
    

      Można np. zachować (jeżeli system cały system oparty jest o <strong>CQRS/ES</strong>) stan aplikacji w poszczególnych etapach jej życia. Zapis stanów musi odbyć sie np. w bazie danych. Nie mniej jednak pozwoli to na przedstawienie historii od <strong>A</strong> do <strong>Z</strong> cyklu życia
    </p>
    

      Dokładnie po wykonaniu każdej z komend jak zmienia się model aplikacji. Zdarzenia wyzalane są z komend.
    </p>
    

      Zastosowanie zdarzeń pozwoli na powiadamianie różnych obszarów aplikacji o zmianie stanu aplikacji.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Zdarzenia i szyna zdarzeń
    </h1>
    
    <p>
      <strong>IEvent</strong> interfejs bazowy dla wszystkich zapytań, klas implementująca zostanie przekazana do zarejestrowanych obserwatorów.
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs zdarzeń.">namespace PictOgr.Core.CQRS.Event
{
	public interface IEvent
	{
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>IEventHandler</strong> &#8211; podobnie jak poprzednio (<strong>IQueryHandler</strong>), implementując ten kontrakt tworzymy kod przetwarzający logikę.
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs handlera zdarzeń.">namespace PictOgr.Core.CQRS.Event
{
	public interface IEventHandler&lt;TEvent&gt; where TEvent : IEvent
	{
		void Handle(TEvent @event);
	}
}</pre>
    

      <strong>@event</strong> &#8211; jak wiadomo event to słowo kluczowe języka c#, jednak można to obejść wykorzystując znak małpki <strong>‚@’</strong>, nakazujemy kompilatorowi, iż nie chcemy skorzystać ze słowa kluczowego <strong>event</strong>, a jedynie użyć jako nazway zmiennej.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>IEventBus</strong>, kontrakt dla szyny zdarzeń, w tym przypadku klasa implementująca musi zawierać trzy metody:
    </p>
    
    <ul>
      <li>
        <strong>Register</strong> &#8211; służy do rejestrowania obserwatora zdarzenia,
      </li>
      <li>
        <strong>UnRegister</strong> &#8211; analogicznie tą metodą wyrzucamy obserwatora zdarzeń,
      </li>
      <li>
        <strong>Publish</strong> &#8211; dzięki tej metodzie przekazujemy wszystkim słuchaczom zdarzenie.
      </li>
    </ul>
    
    <pre class="lang:c# decode:true" title="Interfejs szyny zdarzeń.">namespace PictOgr.Core.CQRS.Bus.Event
{
	using CQRS.Event;

	public interface IEventBus
	{
		void Register&lt;TEvent&gt;(IEventHandler&lt;TEvent&gt; eventHandler) where TEvent : IEvent;

		void UnRegister&lt;TEvent&gt;(IEventHandler&lt;TEvent&gt; eventHandler) where TEvent : IEvent;

		void Publish&lt;TEvent&gt;(TEvent @event) where TEvent : IEvent;
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    

      <strong>EventBus</strong> to implementacja interfejsu <strong>IEventBus</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Implementacja szyny zdarzeń.">namespace PictOgr.Core.CQRS.Bus.Event
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
}</pre>
    

      <em>Lista eventList = new Dictionary<Type, List<object>>();</em>
    </p>
    

      Jest to lista zdarzeń, do której zostaną, która to dopiero będzie powiązana z listą obserwatorów.<a href="http://godev.gemustudio.com/assets/images/2017/04/event2.png"><img class="alignright wp-image-820 size-medium" src="http://godev.gemustudio.com/assets/images/2017/04/event2-300x200.png" alt="CQRS" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/04/event2-300x200.png 300w, http://godev.gemustudio.com/assets/images/2017/04/event2-768x512.png 768w, http://godev.gemustudio.com/assets/images/2017/04/event2-1024x683.png 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    

      [<strong>IEvent</strong> => { <strong>IEventHandler</strong>, <strong>IEventHandler</strong>, <strong>IEventHandler</strong>, etc.}]
    </p>
    

      Metoda <strong>Register</strong>, sprawdza czy IEventHanlder jest już zarejestrowany, jeśli nie to dodaje do listy.
    </p>
    

      <strong>UnRegister</strong>, sprawdza czy IEventHandler jest na liście, jeżeli jest to usuwa.
    </p>
    

      <strong>Publish</strong> &#8211; iteruje po wszystkich IEvent, oraz podległych IEventHandlerach i publikuje zdarzenie.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Testy
    </h1>
    

      Klasę testu zaczynamy od ustawienia (<strong>TearUp</strong>) podstawowych/najczęściej używanych w testach obiektów jak <strong>container</strong>, <strong>fakeEvent</strong>, <strong>eventFakeInvoke</strong>, <strong>fakeEventHandler</strong>.
    </p>
    
    <pre class="lang:c# decode:true " title="Klasa do testowania zdarzeń.">namespace PictOgr.Tests.Core.CQRS.Events
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
		}</pre>
    

      Na końcu konstruktora tworzymy <strong>fake</strong> dla metody <strong>Handler</strong>, tak by pobierać <strong>event</strong> jaki jest do niej przekazywany jako parametr, tak na zaś do assertów.
    </p>
    

      Pierwszy teścik taki symboliczny, czy faktycznie <strong>EventBus</strong> to <strong>EventBus</strong> prosto z <strong>AutoFac</strong>-a.
    </p>
    
    <pre class="lang:c# decode:true " title="Test poprawności pobierania szyny zdarzeń z kontenera AutoFac.">[Fact]
public void test_event_bus_are_correct_resolved()
{
	using (var scope = container.BeginLifetimeScope())
	{
		var eventBus = scope.Resolve&lt;IEventBus&gt;();

		eventBus.ShouldBeOfType&lt;EventBus&gt;();
	}
}</pre>
    

      Jak się powodzi to lecimy dalej.
    </p>
    

      A tutaj to sprawdzimy czy szyna zdarzeń po publikacji (<strong>Publish</strong>) oszukanego zdarzenia (<strong>fakeEvent</strong>) rzuci wyjąteczkiem <strong>TypeUnloadedException</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Próba publikacji zdarzenia, na pustą szynę, rzuca wyjątkiem.">[Fact]
public void event_bus_publish_should_throw_excetion()
{
	using (var scope = container.BeginLifetimeScope())
	{
		var eventBus = scope.Resolve&lt;IEventBus&gt;();

		var fakeEvent = A.Fake&lt;IEvent&gt;();

		Should.Throw&lt;TypeUnloadedException&gt;(() =&gt; { eventBus.Publish(fakeEvent); });
	}
}</pre>
    

      A no bo <strong>POWINNA</strong>!
    </p>
    

      Teraz to już powinno być dobrze, pierwsza publikacja i odebranie prawidłowego <strong>IEvent</strong>, część kodu zawarta w <strong>TearUp</strong>, tak że tutaj prościutko.
    </p>
    
    <pre class="lang:c# decode:true " title="Próba publikacji zdarzenia z wyrejestrowanie, powinna się powieść.">[Fact]
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
}</pre>
    

      Odebrany <strong>IEvent</strong> musi być taki sam jak ten publikowany!
    </p>
    

      A tutaj sobie sprawdzimy jak działa <strong>Register</strong> i <strong>UnRegister</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Rzucanie wyjątkiem dla zarejestrowanego a następnie wyrejestrowanego hanldera.">public void event_bus_register_and_unregister_should_throw_exception_when_publish()
{
    using (var scope = container.BeginLifetimeScope())
    {
        var eventBus = scope.Resolve&lt;IEventBus&gt;();
 
        eventBus.Register(fakeEventHandler);
        eventBus.UnRegister(fakeEventHandler);
 
        Should.Throw&lt;TypeUnloadedException&gt;(() =&gt; { eventBus.Publish(fakeEvent); });
        eventFromInvoke.ShouldBeNull();
    }
}</pre>
    

      Zarejestrowany <strong>IEventHandler</strong> i wyrejestrowany po publikacji wali wyjątkiem <strong>TypeUnloadedException</strong>!
    </p>
    

      Ostatni tłusty teścik rejestruje aż 100 IEventHandlerów, po czym publikuje do nich <strong>fakeEvent</strong>-a.
    </p>
    
    <pre class="lang:c# decode:true " title="Rejestrowanie 100 handlerów, i sprawdzanie czy otrzymują 100 prawidłowych zdarzeń.">[Fact]
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
}</pre>
    

      Tym samym powinno dojść 100 oszukanych eventów zapisanych do listy.
    </p>
    

      Na końcu to już wyrejestrowanie handlerków, i sprawdzenie czy faktycznie te 100 eventów jest oszukanych (<strong>fakeEvent</strong>).
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Na koniec<a href="http://godev.gemustudio.com/assets/images/2017/04/event.png"><img class="alignright wp-image-819 size-thumbnail" src="http://godev.gemustudio.com/assets/images/2017/04/event-150x150.png" alt="CQRS" width="150" height="150" /></a>
    </h1>
    

      Co prawda więcej w poście kodu niż treści, ale myślę, że zrozumiały tekst.
    </p>
    

      W kolejnym poście połączymy <strong>ES</strong> z <strong>CQRS</strong>, oraz dodamy zapowiadane na ten post walidatory.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      <strong>Dziękuję za wytrwałość i zachęcam do komentowania.</strong>
    </h3>
    
{% include_relative dsp.md %}