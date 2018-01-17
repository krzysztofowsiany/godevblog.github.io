---
title: PictOgr - delegowanie wykonania akcji do modelu widoku.
date: 2017-05-14
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-delegowanie-wykonania-akcji-modelu-widoku
image: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/post.jpg
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
  - RelayCommand
  - WPF
short: Nie zawsze dobrym rozwiązaniem jest budowanie komendy dla każdej operacji wykonywanej na widoku, wręcz może okazać się uciążliwe przekazanie danych z formularza do  komendy. W takiej sytuacji z pomocą przychodzą delegaty.
---
[![PictOgr - delegowanie wykonania akcji do modelu widoku.][post]][post-big]{:.post-right-image}
Nie zawsze dobrym rozwiązaniem jest budowanie komendy dla każdej operacji wykonywanej na widoku, wręcz może okazać się uciążliwe przekazanie danych z formularza do  komendy. W takiej sytuacji z pomocą przychodzą delegaty.
Implementacja interfejsu **ICommand** niesie ze sobą potrzebę deklaracji dwóch metod **Execute**, **CanExecute** oraz zdarzenie **CanExecuteChanged**.
Jako że w  programowaniu nie istnieje jedno rozwiązanie problemu i w tym  przypadku można delegować wykonanie metod **Execute** oraz **CanExecute** do modelu widoku.
    
Komenda RelayCommand z delegacją logiki działania na zewnątrz obiektu.

{% highlight csharp linenos %}
using System;
using System.Windows.Input;

namespace PictOgr.MVVM.Base
{
	public class RelayCommand<TParam> : ICommand where TParam : class
	{
		private readonly Action<TParam> execute;
		private readonly Func<TParam, bool> canExecute;

		public RelayCommand(Action<TParam> execute, Func<TParam, bool> canExecute = null)
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

	public class RelayCommand : RelayCommand<object>
	{
		public RelayCommand(Action<object> execute, Func<object, bool> canExecute = null)
			: base(execute, canExecute)
		{
		}
	}
}
{% endhighlight %}

Podczas tworzenia instancji na bazie klasy **RelayCommand  **przekazujemy do niej dwa delegaty: **execute**, **canExecute**.

Wykonanie metody **CanExecute** nie zawsze jest istotne dlatego też w celu uproszczenia wykluczenia delegowania dla  tej metody powstała  klasa **RelayCommand** rozszerzająca klasę bazową  o tej samej nazwie i już określonym typie generycznym (object). Dzięki temu możemy przy tworzeniu nowej komendy wykorzystać prostą składnię: 
**new RelayCommand(executeDelegate);**{:.color_1}

## Przykład wykorzystania RelayCommand
Przy budowaniu widoku konfiguracji dla PictOgra, wykorzystany został mechanizm RelayCommand do ustawiania wzorca ścieżki z dostępnych komponentów nazw.
    
Przykład wykorzystania RelayCommand.

{% highlight csharp linenos %}
using System.Windows.Input;
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
{% endhighlight %}
    
[![PictOgr.][image1]][image1-big]{:.post-left-image}
Tak przygotowany kod pozwala obsłużyć dowolną ilość modułów nazwy jakie będą  zaimplementowane  w aplikacji.

**RelayCommand** pozwolił na delegacje  tego  mechanizmu do modelu widoku i operowaniu bezpośrednio z wykorzystaniem dostępnych właściwości.

Właściwość **PathFormat**, wyświetla bieżący wzorzec nazwy w widoku konfiguracji.

Każdy dodany nowy moduł nazwy (Button), wykorzystuje komendę **AddNameModuleCommand** z parametrem przechowującym identyfikator modułu nazwy.

## Testowanie RelayCommand
Poniżej znajduje się proste testy sprawdzające działanie klasy **RelayCommand** w projekcie  **E2E**.
    
Testowanie RelayCommand.


[![PictOgr.][image2]][image2-big]{:.post-right-image}

## Zakończenie
Mechanizm **RelayCommand** w większości przypadków niweluje potrzebę tworzenia innych klas komend, skraca to kodowanie i powoduje powstawanie mniej błędów.

**Dziękuję za wytrwałość i zachęcam do komentowania**.
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/post.jpg
[post-big]: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/post-big.jpg

[image1]: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/image1.jpg
[image1-big]: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/image1-big.jpg

[image2]: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/image2.jpg
[image2-big]: /assets/images/2017/05/pictogr-delegowanie-wykonania-akcji-modelu-widoku/image2-big.jpg