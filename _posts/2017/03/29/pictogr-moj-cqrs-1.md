---
id: 582
title: 'PictOgr &#8211; mój CQRS -1-'
date: 2017-03-29T10:18:55+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=582
permalink: /2017/03/29/pictogr-moj-cqrs-1/
image: /assets/images/2017/03/13575771_612844145558374_5342566555726992706_o.jpg
categories:
  - Bez kategorii
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - Command
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Command Query Responsibility Segregation &#8211; 1 &#8211;
    </h1>
    
    <p style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/03/13575771_612844145558374_5342566555726992706_o.jpg"><img class="alignleft wp-image-625 size-medium" src="http://godev.gemustudio.com/assets/images/2017/03/13575771_612844145558374_5342566555726992706_o-300x200.jpg" alt="PictOgr - mój CQRS" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/13575771_612844145558374_5342566555726992706_o-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/03/13575771_612844145558374_5342566555726992706_o-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/03/13575771_612844145558374_5342566555726992706_o-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>Zachciało mi się&#8230; nauczyć czegoś przydatnego i noweg. Padło na separację operacji pobierania i zmieniania danych. W tym celu pokusiłem się o własną implementację <strong>CQRS</strong>. Wszystkie komponenty składowe ładowane przez Autofaca w odseparowanym module.
    </p>
    
    <p style="text-align: justify;">
      Funkcjonalność w połączeniu z <strong>MVVM</strong> funkcjonuje dobrze, a i ja się czegoś nowego nauczyłem.
    </p>
    
    <p style="text-align: justify;">
      Tym samym dzielę się ze światem, informacjami na tema rozwoju <a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/">PictOgr-a</a>.
    </p>
    
    <p style="text-align: justify;">
      Zważywszy, iż mam duży bagaż doświadczeń (nie koniecznie dobrych), i zmiana podejścia do budowania aplikacji z wykluczeniem <strong>code-behind</strong> jest dla mnie bardzo ekscytująca. W końcu od ponad 20 lat uwielbiam się rozwijać w IT, a to kolejna okazja.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Struktura w projekcie
    </h1>
    
    <p style="text-align: justify;">
      Struktura mojego CQRSa w projekcie wygląda tak jak na przedstawionym obrazku.
    </p>
    
    <p style="text-align: justify;">
      Rozdzieliłem bazę do budowania komend i zapytań w podfolderze <strong>CQRS</strong> wraz z odpowiednimi nazwami:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>Bus</strong> &#8211; implementqacja szynu dla komend i zapytań zawierająca interfejs szyny komend (<strong>ICommandBus</strong>) i zapytań(<strong>IQueryBus</strong>) w raz z ich implementacją (<strong>CommandBus</strong>, <strong>QueryBus</strong>),
      </li>
      <li style="text-align: justify;">
        <strong>Command</strong> &#8211; kontrakty komend w skład których wchodzi interfejs: <strong>ICommand</strong> i <strong>ICommandHandler</strong>,
      </li>
      <li style="text-align: justify;">
        <strong>Query</strong> &#8211; kontrakty dla zapytań i tu wyodrębnić można: <strong>IQuery</strong>, <strong>IQueryHandler</strong>.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/03/myCQRS.png"><img class="size-full wp-image-584 aligncenter" src="http://godev.gemustudio.com/assets/images/2017/03/myCQRS.png" alt="" width="268" height="381" srcset="http://godev.gemustudio.com/assets/images/2017/03/myCQRS.png 268w, http://godev.gemustudio.com/assets/images/2017/03/myCQRS-211x300.png 211w" sizes="(max-width: 268px) 100vw, 268px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Wszystkie komponenty bazowe CQRS-a tworzone są w module <strong>CQRSModule</strong>.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Komendy i szyna komend
    </h1>
    
    <p style="text-align: justify;">
       Pora nieco omówić implementację komend, do budowy zostały wykorzystane następujace kontrakty:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>ICommand</strong> &#8211; bazowy interfejs dla każdej komendy nie posiada żadnego szkieletu, poprzez implementację określamy dane jakie należy przezkazać do handler-a  komendy,
      </li>
    </ul>
    
    <pre class="lang:c# decode:true" title="Interfejs komend.">namespace PictOgr.Core.CQRS.Command
{
	public interface ICommand
	{
	}
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>ICommandHandler</strong> &#8211; interfejs jaki należy zaimplementować w klasie handler-a, tego typu komenda nie otrzymuje żadnych danych,
      </li>
      <li style="text-align: justify;">
        <strong>ICommandHandler<ICommand></strong> &#8211; tworząc implementację na bazie tego kontraktu, przekazać należy dane, które to następnie zostaną przetworzone przez handlera.
      </li>
    </ul>
    
    <pre class="lang:c# decode:true" title="Interfejs handlerów komend.">namespace PictOgr.Core.CQRS.Command
{
	public interface ICommandHandler
	{
	}

	public interface ICommandHandler&lt;in TCommand&gt; : ICommandHandler where TCommand : ICommand
	{
		void Handle(TCommand command);
	}
}</pre>
    
    <p style="text-align: justify;">
      <strong> </strong>
    </p>
    
    <p style="text-align: justify;">
      <strong>ICommandBus</strong> to kontrakt dotyczący szyny komend, na którą będą wrzucane komendy i przetwarzane.<strong> </strong>
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs szyny komend.">using PictOgr.Core.CQRS.Command;

namespace PictOgr.Core.CQRS.Bus
{
	public interface ICommandBus
	{
		void SendCommand&lt;TCommand&gt;(TCommand command) where TCommand : ICommand;
	}
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Implementacja szyny komend <strong>CommandBus</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Szyna komend.">using System;
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

		public void SendCommand&lt;TCommand&gt;(TCommand command) where TCommand : ICommand
		{
			if (command == null)
			{
				throw new ArgumentNullException(nameof(command));
			}

			var commandHandler = container.ResolveOptional&lt;ICommandHandler&lt;TCommand&gt;&gt;();

			if (commandHandler == null)
			{
				throw new Exception($"Not found handler for Command: '{command.GetType().FullName}'");
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
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <h4>
      Proces przetwarzania komendy można przedstawić w następujący sposób:
    </h4>
    
    <ol>
      <li>
        Przekazanie komendy do szyny przy pomocy wywołania metody <strong>SendCommand</strong>.
      </li>
      <li>
        Jeżeli przekazana komenda jest pusta, to rzuca wyjątkiem <strong>ArgumentNullException</strong>,
      </li>
      <li>
        Wyciągnięcie z kontenera (Autofac) handlera dla przekazanej komendy.
      </li>
      <li>
        Jeżeli handler jest pusty to rzuca wyjątek <strong>Exception</strong>.
      </li>
      <li>
        Wywołanie komendy poprzez metodę <strong>Handle</strong> w bloku <strong>try&#8230;catch</strong>.
      </li>
      <li>
        Jeżeli wywołanie się nie powiedzie to zostanie zapisany log błędu.
      </li>
    </ol>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Pierwsza komenda
    </h1>
    
    <p style="text-align: justify;">
      Pierwsza komenda jaka została zaimplementowana <strong>ExitApplication</strong> dotyczy zamykanai aplikacji.
    </p>
    
    <p style="text-align: justify;">
      Dane jakie zostają przekazane to kod wyjścia.
    </p>
    
    <pre class="lang:c# decode:true" title="Komenda zamykania aplikacji.">using PictOgr.Core.CQRS.Command;

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
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Kod błędu wykorzystany jest przez handlera <strong>ExitApplicationHandler</strong>, jest on wymagany przez metodę <strong>System.Environment.Exit(ExitCode)</strong>.
    </p>
    
    <p>
      Dodatkowo zapisywany jest log informujący. iż aplikacja została zamknięta.
    </p>
    
    <pre class="lang:c# decode:true" title="Handler zamykania aplikacji.">using Autofac.Extras.NLog;
using PictOgr.Core.CQRS.Command;

namespace PictOgr.Core.Commands
{
	public class ExitApplicationHandler : ICommandHandler&lt;ExitApplication&gt;
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
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      Kod poniżej przedstawia, użycie komendy zamykania aplikacji, w komendach wywoływanych przez widok MVVM.
    </p>
    
    <p style="text-align: justify;">
      Do obiektu <strong>ExitApplicationCommand</strong> została wstrzyknięta szyna komend.
    </p>
    
    <pre class="lang:c# decode:true" title="Użycie komendy ExitApplication.">using System;
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
			commandBus.SendCommand&lt;ExitApplication&gt;(new ExitApplication(0));
		}

		public event EventHandler CanExecuteChanged;
	}
}</pre>
    
    <p style="text-align: justify;">
      Uzycie komendy <strong>ExitApplication</strong>, sprowadza sie do 1 linijki kodu <em>commandBus.SendCommand<ExitApplication>(new ExitApplication(0));</em>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Testy
    </h1>
    
    <p style="text-align: justify;">
      Do przetestowania działania komend w ujęciu testów jednostkowych wymagane jest przysłonięcie metody <strong>Handle</strong>.
    </p>
    
    <p style="text-align: justify;">
      W tym celu napisałem specjalną klasę matkę z mockiem (zaznaczone linie 18-27 w kodzie).
    </p>
    
    <p style="text-align: justify;">
      Ponieważ w projekcie został zastosowany mechanizm automatycznego rejstrowania obiektów w Autofacku, należy podmienić (ponownie zarejestrować) komendę jaką chcemy przetestować.
    </p>
    
    <p style="text-align: justify;">
      Dodatkowo stosuję tutaj typ generyczny, tak by użyc klasy bazowej dla większej ilości testów.
    </p>
    
    <pre class="lang:c# mark:18-27 decode:true" title="Baza do testowania komend.">namespace PictOgr.Tests.Core.CQRS.Commands
{
    using System;
    using Autofac;
    using FakeItEasy;
    using PictOgr.Core.AutoFac;
    using PictOgr.Core.CQRS.Bus;
    using PictOgr.Core.CQRS.Command;

    public class CommandBaseTests&lt;T&gt; where T : ICommand
    {
        protected ICommandBus commandBus;
        protected Action&lt;ICommand&gt; handleMethod;

        public CommandBaseTests()
        {
            var builder = Container.CreateBuilder();

            var fakeHandler = A.Fake&lt;ICommandHandler&lt;T&gt;&gt;();

            A.CallTo(() =&gt; fakeHandler.Handle(A&lt;T&gt;._))
                .Invokes((T command) =&gt;
                {
                    handleMethod?.Invoke(command);
                });

            builder.Register(c =&gt; fakeHandler).AsImplementedInterfaces();

            var container = builder.Build();

            commandBus = container.Resolve&lt;ICommandBus&gt;();
        }
    }
}
</pre>
    
    <p>
      Metoda <strong>handleMethod</strong> jest to delegat jaki musi być przypisany w teście.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      Powyższa implementacja jest rozszeżana we właściwym kodzie testu <strong>ExitApplicationCommandTest</strong>.
    </p>
    
    <p style="text-align: justify;">
      Przesłnięcie metody handleMethod, pozwala na pobranie kodu wyjścia z wywoływanej komendy.
    </p>
    
    <p style="text-align: justify;">
      Kod następnie jest przepisany do zmiennej lokalnej, i wówczas możemy już wykonać asercję: <em>exitCode.ShouldBe(expectedValue);</em>
    </p>
    
    <pre class="lang:c# decode:true " title="Testowanie komendy Exit.">namespace PictOgr.Tests.Core.CQRS.Commands
{
    using PictOgr.Core.Commands;
    using SplashScreen.Commands;
    using Shouldly;
    using Xunit;

    public class ExitApplicationCommandTest : CommandBaseTests&lt;ExitApplication&gt;
    {
        private readonly int expectedValue = 123;
        private int exitCode;

        public ExitApplicationCommandTest()
        {
            handleMethod = command =&gt;
            {
                var exitApplication = command as ExitApplication;
                exitCode = exitApplication.ExitCode;
            };
        }

        [Fact]
        public void exit_application_command_should_be_handled_by_command_bus()
        {
            commandBus.SendCommand&lt;ExitApplication&gt;(new ExitApplication(expectedValue));

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
}</pre>
    
    <p style="text-align: justify;">
      Drugi test jaki został zaimplementowany to sprawdzenie działania komendy wywołanej z widoku w celu zamknięcia aplikacji.
    </p>
    
    <p style="text-align: justify;">
      W tym przypadku dane jakie zostają przekazane do komendy ustalane są w klasie <strong>ExitApplicationCommand</strong>, i kod prawidłowego wyjścia jest równy 0.
    </p>
    
    <p style="text-align: justify;">
      Dlatego asercję należy wykonać do wartości 0.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Koniec<a href="http://godev.gemustudio.com/assets/images/2017/03/13581925_612838085558980_6043402438851061498_o.jpg"><img class="wp-image-631 size-medium alignright" src="http://godev.gemustudio.com/assets/images/2017/03/13581925_612838085558980_6043402438851061498_o-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/13581925_612838085558980_6043402438851061498_o-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/03/13581925_612838085558980_6043402438851061498_o-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/03/13581925_612838085558980_6043402438851061498_o-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </h1>
    
    <p style="text-align: justify;">
      To tyle jeśli chodzi o zaimplementowany przeze mnie fragment <strong>CQRS</strong> dotyczący komend, w następnej części przedstawię implementację zapytań.
    </p>
    
    <p style="text-align: justify;">
      Zastanawiam się także nad wykorzystaniem <strong>ES</strong> w projekcie, oraz reorganizacją projektu w celu wyodrębnienie CQRSa do osobnej biblioteki.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      Jeżeli ktoś wytrzymał do końca to dziękuję za uwagę i zapraszam do dalszego śledzenia bloga.
    </h3>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <div style="text-align: center;">
        <strong>Jest to post przygotowany na potrzeby konkursu &#8222;Daj Się Poznać 2017&#8221; organizowanym przez <a href="http://devstyle.pl">Macieja Aniserowicza</a>.</strong>
      </div>
      
      <div style="text-align: center;">
         <a href="http://devstyle.pl/daj-sie-poznac/" target="_blank" rel="noopener noreferrer"><img class="wp-image-104 size-full alignright" title="Daj Się Poznać 2017" src="http://godev.gemustudio.com/assets/images/2017/02/dsp2017-3.png" alt="" width="68" height="154" /></a>
      </div>
      
      <div style="font-size: 10pt; padding: 10px;">
        <div>
          <strong>Projekt: </strong><a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/">PictOgr</a>.
        </div>
        
        <div>
          <strong>GitHub: </strong><a href="https://github.com/krzysztofowsiany/pictogr">github.com/krzysztofowsiany/pictogr</a>
        </div>
        
        <div>
          <strong>Blog: </strong><a href="http://godev.gemustudio.com">godev.gemustudio.com</a>
        </div>
        
        <div>
          <strong>Snapchat</strong>: <a href="https://www.snapchat.com/add/gocom7" target="_blank" rel="noopener noreferrer">gocom7</a>
        </div>
        
        <div>
          <strong>RSS: </strong><a href="http://godev.gemustudio.com/category/daj-sie-poznac-2017/feed">godev.gemustudio.com/category/daj-sie-poznac-2017/feed</a>
        </div>
        
        <div>
          <strong>Facebook:</strong><a href="https://www.facebook.com/PictOgr-1729700930654225/">www.facebook.com/PictOgr-1729700930654225/</a>
        </div>
        
        <div>
          <strong>Twitter: </strong><a href="https://twitter.com/gemu_gocom">twitter.com/gemu_gocom</a>
        </div>
      </div>
    </div>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>