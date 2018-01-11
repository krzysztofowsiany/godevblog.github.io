---
id: 1079
title: 'PictOgr &#8211; delegowanie wykonania akcji do modelu widoku.'
date: 2017-05-14T23:03:49+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/05/14/pictogr-delegowanie-wykonania-akcji-modelu-widoku/
image: /assets/images/2017/05/IMG_9837-2.jpg
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
  - RelayCommand
  - WPF
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">

      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_0061.jpg"><img class="alignright wp-image-1098 size-medium" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_0061-300x200.jpg" alt="PictOgr - delegowanie wykonania akcji do modelu widoku" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_0061-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0061-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0061-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>Nie zawsze dobrym rozwiązaniem jest budowanie komendy dla każdej operacji
    </p>
    

      wykonywanej na widoku, wręcz może okazać się uciążliwe przekazanie danych z formularza do  komendy. W takiej sytuacji z pomocą przychodzą delegaty.
    </p>
    

      Implementacja interfejsu <strong>ICommand</strong> niesie ze sobą potrzebę deklaracji dwóch metod <strong>Execute</strong>, <strong>CanExecute </strong>oraz zdarzenie <strong>CanExecuteChanged</strong>.
    </p>
    

      Jako że w  programowaniu nie istnieje jedno rozwiązanie problemu i w tym  przypadku można delegować wykonanie metod <strong>Execute</strong> oraz <strong>CanExecute</strong> do modelu widoku.
    </p>
    
    <pre class="lang:c# decode:true" title="Komenda RelayCommand z delegacją logiki działania na zewnątrz obiektu.">using System;
using System.Windows.Input;

namespace PictOgr.MVVM.Base
{
	public class RelayCommand&lt;TParam&gt; : ICommand where TParam : class
	{
		private readonly Action&lt;TParam&gt; execute;
		private readonly Func&lt;TParam, bool&gt; canExecute;

		public RelayCommand(Action&lt;TParam&gt; execute, Func&lt;TParam, bool&gt; canExecute = null)
		{
			this.execute = execute;
			this.canExecute = canExecute;
		}

		public event EventHandler CanExecuteChanged
		{
			add { CommandManager.RequerySuggested += value; }
			remove { CommandManager.RequerySuggested -= value; }
		}

		public bool CanExecute(object parameter)
		{
			return canExecute == null || canExecute(parameter as TParam);
		}

		public void Execute(object parameter)
		{
			execute(parameter as TParam);
		}
	}

	public class RelayCommand : RelayCommand&lt;object&gt;
	{
		public RelayCommand(Action&lt;object&gt; execute, Func&lt;object, bool&gt; canExecute = null)
			: base(execute, canExecute)
		{
		}
	}
}
</pre>
    

      Podczas tworzenia instancji na bazie klasy <strong>RelayCommand  </strong>przekazujemy do niej dwa delegaty: <strong>execute</strong>, <strong>canExecute</strong>.
    </p>
    

      Wykonanie metody <strong>CanExecute</strong> nie zawsze jest istotne dlatego też w celu uproszczenia wykluczenia delegowania dla  tej metody powstała  klasa <strong>RelayCommand</strong> rozszerzająca klasę bazową  o tej samej nazwie i już określonym typie generycznym (object). Dzięki temu możemy przy tworzeniu nowej komendy wykorzystać prostą składnię: <span style="color: #3355ff;"><strong>new RelayCommand(executeDelegate);</strong></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="background: #ffff9c; padding: 5pt; text-align: left;">
      Przykład wykorzystania RelayCommand
    </h1>
    

      Przy budowaniu widoku konfiguracji dla PictOgra, wykorzystany został mechanizm RelayCommand do ustawiania wzorca ścieżki z dostępnych komponentów nazw.
    </p>
    
    <pre class="lang:c# decode:true" title="Przykład wykorzystania RelayCommand.">using System.Windows.Input;
using Autofac.Extras.NLog;
using CQRS.Bus.Query;
using PictOgr.MVVM.Base;

namespace PictOgr.MVVM.Configuration.ViewModels
{
	public class ConfigurationViewModel : BaseViewModel
	{
		private string pathFormat;

		public string PathFormat
		{
			get { return pathFormat; }
			set
			{
				pathFormat = value;
				OnPropertyChanged(nameof(PathFormat));
			}
		}

		public ICommand AddNameModuleCommand { get; private set; }

		public ConfigurationViewModel(IQueryBus queryBus, ILogger logger) : base(queryBus, logger)
		{
			PathFormat = string.Empty;

			AddNameModuleCommand = new RelayCommand(AddNameModule);
		}

		private void AddNameModule(object parameter)
		{
			var nameModule = parameter.ToString();

			PathFormat += nameModule;
		}
	}
}
</pre>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_0712.jpg"><img class="alignleft wp-image-1102 size-medium" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_0712-300x200.jpg" alt="PictOgr" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_0712-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0712-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0712-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    

      Tak przygotowany kod pozwala obsłużyć dowolną ilość modułów nazwy jakie będą  zaimplementowane  w aplikacji.
    </p>
    

      <strong>RelayCommand  </strong>pozwolił na delegacje  tego  mechanizmu do modelu widoku i operowaniu bezpośrednio z wykorzystaniem dostępnych właściwości.
    </p>
    

      Właściwość <strong>PathFormat</strong>, wyświetla bieżący wzorzec nazwy w widoku konfiguracji.
    </p>
    

      Każdy dodany nowy moduł nazwy (Button), wykorzystuje komendę <strong>AddNameModuleCommand</strong> z parametrem przechowującym identyfikator modułu nazwy.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="background: #ffff9c; padding: 5pt; text-align: left;">
      Testowanie RelayCommand
    </h1>
    
    <p>
      Poniżej znajduje się proste testy sprawdzające działanie klasy <strong>RelayCommand</strong> w projekcie  <strong>E2E</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Testowanie RelayCommand.">using PictOgr.MVVM.Base;
using Shouldly;
using Xunit;

namespace PictOgr.E2E
{
	public class RelayCommandTest
	{
		private string executeParam;
		private readonly RelayCommand relayCommand;
		private bool canExecute;

		public RelayCommandTest()
		{
			relayCommand = new RelayCommand(ExecuteDelegate, CanExecute);
		}

		private bool CanExecute(object parameter)
		{
			var testString = parameter.ToString();
			
			canExecute = !string.IsNullOrWhiteSpace(testString);

			return canExecute;
		}

		private void ExecuteDelegate(object parameter)
		{
			executeParam = parameter.ToString();
		}

		[Fact]
		public void execute_relaycommand_should_set_param_and_can_execute()
		{
			var testString = "ok";

			relayCommand.CanExecute(testString);
			relayCommand.Execute(testString);

			executeParam.ShouldBe(testString);
			canExecute.ShouldBeTrue();
		}

		[Fact]
		public void execute_relaycommand_should_not_set_param_and_can_execute()
		{
			var testString = string.Empty;

			relayCommand.CanExecute(testString);

			canExecute.ShouldBeFalse();
		}
	}
}</pre>
    
    <h3 style="text-align: center;">
      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_0022.jpg"><img class="aligncenter size-medium wp-image-1099" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_0022-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_0022-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0022-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0022-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </h3>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="background: #ffff9c; padding: 5pt; text-align: left;">
      Zakończenie
    </h1>
    

      Mechanizm <strong>RelayCommand</strong> w większości przypadków niweluje potrzebę tworzenia innych klas komend, skraca to kodowanie i powoduje powstawanie mniej błędów.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      <strong>Dziękuję za wytrwałość i zachęcam do komentowania.</strong>
    </h3>
    
{% include_relative dsp.md %}