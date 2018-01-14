---
title: PictOgr - mój CQRS -1-
date: 2017-03-29
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-moj-cqrs-1
image: /assets/images/2017/03/pictogr-moj-cqrs-1/post.jpg
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - Command
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
short: Zachciało mi się&#8230; nauczyć czegoś przydatnego i noweg. Padło na separację operacji pobierania i zmieniania danych. W tym celu pokusiłem się o własną implementację CQRS. Wszystkie komponenty składowe ładowane przez Autofaca w odseparowanym module.
---
[![PictOgr - mój CQRS.][post]][post-big]{:.post-left-image}
Zachciało mi się&#8230; nauczyć czegoś przydatnego i noweg. Padło na separację operacji pobierania i zmieniania danych. W tym celu pokusiłem się o własną implementację **CQRS**. Wszystkie komponenty składowe ładowane przez Autofaca w odseparowanym module.
    
Funkcjonalność w połączeniu z **MVVM** funkcjonuje dobrze, a i ja się czegoś nowego nauczyłem.

Tym samym dzielę się ze światem, informacjami na tema rozwoju [PictOgr-a].

Zważywszy, iż mam duży bagaż doświadczeń (nie koniecznie dobrych), i zmiana podejścia do budowania aplikacji z wykluczeniem **code-behind** jest dla mnie bardzo ekscytująca. W końcu od ponad 20 lat uwielbiam się rozwijać w IT, a to kolejna okazja.

## Struktura w projekcie
[![PictOgr - mój CQRS.][mycqrs]][mycqrs-big]{:.post-right-image}
Struktura mojego CQRSa w projekcie wygląda tak jak na przedstawionym obrazku.

Rozdzieliłem bazę do budowania komend i zapytań w podfolderze **CQRS** wraz z odpowiednimi nazwami:
* **Bus** - implementqacja szynu dla komend i zapytań zawierająca interfejs szyny komend (**ICommandBus**) i zapytań(**IQueryBus**) w raz z ich implementacją (**CommandBus**, **QueryBus**),
* **Command** - kontrakty komend w skład których wchodzi interfejs: **ICommand** i **ICommandHandler**,
* **Query** - kontrakty dla zapytań i tu wyodrębnić można: **IQuery**, **IQueryHandler**.

Wszystkie komponenty bazowe CQRS-a tworzone są w module **CQRSModule**.

## Komendy i szyna komend
Pora nieco omówić implementację komend, do budowy zostały wykorzystane następujace kontrakty:
* **ICommand** - bazowy interfejs dla każdej komendy nie posiada żadnego szkieletu, poprzez implementację określamy dane jakie należy przezkazać do handler-a komendy,
Interfejs komend.
{% highlight csharp linenos %}    
namespace PictOgr.Core.CQRS.Command
{
	public interface ICommand
	{
	}
}
{% endhighlight %}

* **ICommandHandler** - interfejs jaki należy zaimplementować w klasie handler-a, tego typu komenda nie otrzymuje żadnych danych,
* **ICommandHandler**<**ICommand**> - tworząc implementację na bazie tego kontraktu, przekazać należy dane, które to następnie zostaną przetworzone przez handlera.

Interfejs handlerów komend.
{% highlight csharp linenos %}    
namespace PictOgr.Core.CQRS.Command
{
	public interface ICommandHandler
	{
	}

	public interface ICommandHandler<in TCommand> : ICommandHandler 
      where TCommand : ICommand
	{
		void Handle(TCommand command);
	}
}
{% endhighlight %}

* **ICommandBus** to kontrakt dotyczący szyny komend, na którą będą wrzucane komendy i przetwarzane.

Interfejs szyny komend.
{% highlight csharp linenos %}
using PictOgr.Core.CQRS.Command;

namespace PictOgr.Core.CQRS.Bus
{
	public interface ICommandBus
	{
		void SendCommand<TCommand>(TCommand command)
          where TCommand : ICommand;
	}
}
{% endhighlight %}
    
Implementacja szyny komend **CommandBus**.
   
Szyna komend.
{% highlight csharp linenos %}
using System;
using Autofac;
using Autofac.Extras.NLog;
using PictOgr.Core.CQRS.Command;

namespace PictOgr.Core.CQRS.Bus
{
	public class CommandBus : ICommandBus
	{
		private readonly ILifetimeScope container;
		private readonly ILogger logger;

		public CommandBus(ILifetimeScope container, ILogger logger)
		{
			this.container = container;
			this.logger = logger;
		}

		public void SendCommand<TCommand>(TCommand command) 
        where TCommand : ICommand
		{
			if (command == null)
			{
				throw new ArgumentNullException(nameof(command));
			}

			var commandHandler = container.ResolveOptional<ICommandHandler<TCommand>>();

			if (commandHandler == null)
			{
				throw new Exception(
          $"Not found handler for Command: '{command.GetType().FullName}'");
			}

			try
			{
				commandHandler.Handle(command);
			}
			catch (Exception e)
			{
				logger.Error(e);
			}
		}
	}
}
{% endhighlight %}

Proces przetwarzania komendy można przedstawić w następujący sposób:
* Przekazanie komendy do szyny przy pomocy wywołania metody **SendCommand**.
* Jeżeli przekazana komenda jest pusta, to rzuca wyjątkiem **ArgumentNullException**,
* Wyciągnięcie z kontenera (Autofac) handlera dla przekazanej komendy.
* Jeżeli handler jest pusty to rzuca wyjątek **Exception**.
* Wywołanie komendy poprzez metodę **Handle** w bloku **try&#8230;catch**.
* Jeżeli wywołanie się nie powiedzie to zostanie zapisany log błędu.
    
## Pierwsza komenda
Pierwsza komenda jaka została zaimplementowana **ExitApplication** dotyczy zamykanai aplikacji.

Dane jakie zostają przekazane to kod wyjścia.

Komenda zamykania aplikacji.
{% highlight csharp linenos %}
using PictOgr.Core.CQRS.Command;

namespace PictOgr.Core.Commands
{
	public class ExitApplication : ICommand
	{
		public int ExitCode { get; private set; }

		public ExitApplication(int exitCode)
		{
			ExitCode = exitCode;
		}
	}
}
{% endhighlight %}

Kod błędu wykorzystany jest przez handlera **ExitApplicationHandler**, jest on wymagany przez metodę **System.Environment.Exit(ExitCode)**.
    
Dodatkowo zapisywany jest log informujący. iż aplikacja została zamknięta.

Handler zamykania aplikacji.
{% highlight csharp linenos %}
using Autofac.Extras.NLog;
using PictOgr.Core.CQRS.Command;

namespace PictOgr.Core.Commands
{
	public class ExitApplicationHandler : ICommandHandler<ExitApplication>
	{
		private readonly ILogger logger;

		public ExitApplicationHandler(ILogger logger)
		{
			this.logger = logger;
		}

		public void Handle(ExitApplication command)
		{
			logger.Info("Exit application.");
			System.Environment.Exit(command.ExitCode);
		}
	}
}
{% endhighlight %}

Kod poniżej przedstawia, użycie komendy zamykania aplikacji, w komendach wywoływanych przez widok MVVM.

Do obiektu **ExitApplicationCommand** została wstrzyknięta szyna komend.

Użycie komendy ExitApplication.
{% highlight csharp linenos %}
using System;
using PictOgr.Core.Commands;
using PictOgr.Core.CQRS.Bus;
using ICommand = System.Windows.Input.ICommand;

namespace PictOgr.SplashScreen.Commands
{
	public class ExitApplicationCommand : ICommand
	{
		private readonly ICommandBus commandBus;

		public ExitApplicationCommand(ICommandBus commandBus)
		{
			this.commandBus = commandBus;
		}

		public bool CanExecute(object parameter)
		{
			return true;
		}

		public void Execute(object parameter)
		{
			commandBus.SendCommand<ExitApplication>(new ExitApplication(0));
		}

		public event EventHandler CanExecuteChanged;
	}
}
{% endhighlight %}

Uzycie komendy **ExitApplication**, sprowadza sie do 1 linijki kodu *commandBus.SendCommand<ExitApplication>(new ExitApplication(0));*

## Testy
Do przetestowania działania komend w ujęciu testów jednostkowych wymagane jest przysłonięcie metody **Handle**.

W tym celu napisałem specjalną klasę matkę z mockiem (zaznaczone linie 18-27 w kodzie).

Ponieważ w projekcie został zastosowany mechanizm automatycznego rejstrowania obiektów w Autofacku, należy podmienić (ponownie zarejestrować) komendę jaką chcemy przetestować.

Dodatkowo stosuję tutaj typ generyczny, tak by użyc klasy bazowej dla większej ilości testów.

Baza do testowania komend.
{% highlight csharp linenos %}
namespace PictOgr.Tests.Core.CQRS.Commands
{
    using System;
    using Autofac;
    using FakeItEasy;
    using PictOgr.Core.AutoFac;
    using PictOgr.Core.CQRS.Bus;
    using PictOgr.Core.CQRS.Command;

    public class CommandBaseTests<T> where T : ICommand
    {
        protected ICommandBus commandBus;
        protected Action<ICommand> handleMethod;

        public CommandBaseTests()
        {
            var builder = Container.CreateBuilder();

            var fakeHandler = A.Fake<ICommandHandler<T>>();

            A.CallTo(() => fakeHandler.Handle(A<T>._))
                .Invokes((T command) =>
                {
                    handleMethod?.Invoke(command);
                });

            builder.Register(c => fakeHandler).AsImplementedInterfaces();

            var container = builder.Build();

            commandBus = container.Resolve<ICommandBus>();
        }
    }
}
{% endhighlight %}

Metoda **handleMethod** jest to delegat jaki musi być przypisany w teście.

Powyższa implementacja jest rozszeżana we właściwym kodzie testu **ExitApplicationCommandTest**.

Przesłnięcie metody handleMethod, pozwala na pobranie kodu wyjścia z wywoływanej komendy.

Kod następnie jest przepisany do zmiennej lokalnej, i wówczas możemy już wykonać asercję: *exitCode.ShouldBe(expectedValue);*

Testowanie komendy Exit.
{% highlight csharp linenos %}
namespace PictOgr.Tests.Core.CQRS.Commands
{
    using PictOgr.Core.Commands;
    using SplashScreen.Commands;
    using Shouldly;
    using Xunit;

    public class ExitApplicationCommandTest : CommandBaseTests<ExitApplication>
    {
        private readonly int expectedValue = 123;
        private int exitCode;

        public ExitApplicationCommandTest()
        {
            handleMethod = command =>
            {
                var exitApplication = command as ExitApplication;
                exitCode = exitApplication.ExitCode;
            };
        }

        [Fact]
        public void exit_application_command_should_be_handled_by_command_bus()
        {
            commandBus.SendCommand<ExitApplication>(new ExitApplication(expectedValue));

            exitCode.ShouldBe(expectedValue);
        }

        [Fact]
        public void window_command_exit_application_should_be_handle_by_command_bus()
        {
            var exitApplicationCommand = new ExitApplicationCommand(commandBus);

            exitApplicationCommand.Execute(null);

            exitCode.ShouldBe(0);
        }
    }
}
{% endhighlight %}

Drugi test jaki został zaimplementowany to sprawdzenie działania komendy wywołanej z widoku w celu zamknięcia aplikacji.

W tym przypadku dane jakie zostają przekazane do komendy ustalane są w klasie **ExitApplicationCommand**, i kod prawidłowego wyjścia jest równy 0.

Dlatego asercję należy wykonać do wartości 0.

[![MyCQRS - Travis][mycqrs-travis]][mycqrs-travis-big]{:.post-left-image}

To tyle jeśli chodzi o zaimplementowany przeze mnie fragment **CQRS** dotyczący komend, w następnej części przedstawię implementację zapytań.

Zastanawiam się także nad wykorzystaniem **ES** w projekcie, oraz reorganizacją projektu w celu wyodrębnienie CQRSa do osobnej biblioteki.

**Jeżeli ktoś wytrzymał do końca to dziękuję za uwagę i zapraszam do dalszego śledzenia bloga.**{:.h-1}

{% include_relative dsp.md %}

[PictOgr-a]: {{site.url}}/pictogr-pomysl

[post]: /assets/images/2017/03/pictogr-moj-cqrs-1/post.jpg
[post-big]: /assets/images/2017/03/pictogr-moj-cqrs-1/post-big.jpg

[image1]: /assets/images/2017/03/pictogr-moj-cqrs-1/image1.jpg
[image1-big]: /assets/images/2017/03/pictogr-moj-cqrs-1/image1-big.jpg

[mycqrs]: /assets/images/2017/03/pictogr-moj-cqrs-1/mycqrs.png
[mycqrs-big]: /assets/images/2017/03/pictogr-moj-cqrs-1/mycqrs-big.png

[mycqrs-travis]: /assets/images/2017/03/pictogr-moj-cqrs-1/mycqrs-travis.png
[mycqrs-travis-big]: /assets/images/2017/03/pictogr-moj-cqrs-1/mycqrs-travis-big.png