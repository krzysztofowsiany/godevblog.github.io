---
title: Programowanie Reaktywne - Tworzymy dane - Własna klasa publikująca.
date: 2018-02-14
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-tworzymy-dane-wlasna-klasa-publikujaca
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/post-big.jpg
categories:
  - Programowanie Reaktywne
  - '30 day challenge'
  - Programowanie
  - Reactive Extensions
  - C#
  - Rx
tags:
  - Reactive Extensions
  - Observer
  - Observable
  - Programowanie Reaktywne
  - Rx
  - Timestamp
  - TimeInterval  
  - Generate
  - Custom observable class
  - Własna klasa publikująca
short: Z okazji Walentynek dzisiaj pojawi się głównie w kodzie coś ekstra. Zapraszam do kompilacji i obserwacji. Natomiast post poświęcony będzie budowaniu własnej klasy publikującej dane. W tym celu idąc krok dalej stworzyłem bibliotekę RXlib z jakiej będziemy jeszcze korzystać. 
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Custom observable class][post]][post-big]{:.post-right-image}
Z okazji Walentynek dzisiaj pojawi się głównie w kodzie coś ekstra. Zapraszam do kompilacji i obserwacji. Natomiast post poświęcony będzie budowaniu własnej klasy publikującej dane. W tym celu idąc krok dalej stworzyłem bibliotekę **RXlib**{:.color_1} z jakiej będziemy jeszcze korzystać. 
Idea jest dość prosta. Główny strumień dystrybuujący dane to **Interval**{:.color_2}.

Co **100ms** będzie on powiadamiał podpiętych do niego odbiorców. Natomiast to właśnie do tych odbiorców będziemy się subskrybować i odbierać dane.

## IObservable<T>
Dysponując takim generycznym interfejsem (IObservable<T>). Możemy stworzyć własną klasę dystrybuującą dane na strumień. W tym konkretnym przypadku stworzymy licznik czasu. I jako typ rozsyłany wykorzystamy klasę **Time**{:.color_1}.

Klasa będzie przechowywała **sekundy**, **minuty**, **godziny**. Dodatkowo by łatwo wyświetlać nadpisałem **ToString**{:.color_1}.

{% highlight csharp linenos %}
public class Time
{
	public Time()
	{
		Seconds = 0;
		Minutes = 0;
		Hours = 0;
	}

	public short Seconds { get; set; }
	public short Minutes { get; set; }
	public long Hours { get; set; }

	public override string ToString()
	{
		return $"{Hours}:{Minutes:00}:{Seconds:00}";
	}
}
{% endhighlight %}

Skąd tutaj **IDisposable**? Przyda się gdy już wszystko będziemy zwijać i kończyć działanie programu.
Najważniejsze co jest wymagane w przypadku budowania własnej klasy do obserwowania, to lista obserwujących: **_observers**{:.color_1}.

Do konstruktora wstrzykujemy obiekt obserwowalny powstały przy użyciu **Observable.Interval**{:.color_2}. Będzie wyzwalał publikację danych ma strumień zapisanych na naszą listę **_observers**{:.color_1} obserwatorów.

{% highlight csharp linenos %}
public class ObservableTimeCounter : IObservable<Time>, IDisposable
{
	private const int MinutesLimit = 59;
	private const int HourLimit = 59;

	private List<IObserver<Time>> _observers;
	private Time _time;
	private IDisposable _tickerSubscription;

	public ObservableTimeCounter(IObservable<long> ticker)
	{
		_observers = new List<IObserver<Time>>();
		_time = new Time();

		SubscribeOnTicker(ticker);
	}

	public IDisposable Subscribe(IObserver<Time> observer)
	{
		if (!_observers.Contains(observer))
		{
			_observers.Add(observer);
		}

		return new Unsubscriber<Time>(_observers, observer);
	}
{% endhighlight %}

[![Reactive Extensions - Własna klasa publikująca][image1]][image1-big]{:.post-left-image}

Do zapisu subskrybentów służy metoda **Subscribe**{:.color_1}. Jest ona narzucana przez interfejs i musimy ją zaimplementować (a jak inaczej subskrybować...).

Działanie proste jak obiekt obserwujący nie został jeszcze dodany do listy to dodajemy. 

Zwracamy interfejs **IDisposable**, dzięki takiej konstrukcji mogliśmy wielokrotnie niszczyć obiekty obserwatorów w poprzednich postach.

Ale skąd tutaj u diabła wziąć typ **IDisposable**? Trzeba wykazać się sprytem i stworzyć kolejny obiekt: **Unsubscriber**{:.color_1}.

Przez implementację interfejsu IDisposable, możemy zwrócić stworzony tak obiekt w **Subscribe**. A nowy obiekt zawiera odwołanie do obserwatora, oraz listy obserwatorów zawartych w obiekcie jaki będzie obserwowany. Dzięki takiemu zabiegowi będzie mogli się wypisać z **_observers**{:.color_2}.
{% highlight csharp linenos %}
public class Unsubscriber<T> : IDisposable
{
	private List<IObserver<T>> _observers;
	private IObserver<T> _observer;

	public Unsubscriber(List<IObserver<T>> observers, IObserver<T> observer)
	{
		_observers = observers;
		_observer = observer;
	}

	public void Dispose()
	{
		if (_observer != null && _observers.Contains(_observer))
		{
			_observers.Remove(_observer);
{% endhighlight %}

Typ generyczny zastosowany został po to by nie tworzyć do każdej kolejnej klasy publikującej osobnych klas do odpisywania z listy. 
Generyczny typo powoduje uniwersalność tego rozwiązania. Czyli mniej kodu:).

A co z naszym ticker-em. Otóż będzie on służył akurat w tym przypadku do kalkulacji zmiennej _time co **1s**{:.color_2}.
Służy do tego metoda **CalculateTime**{:.color_1}.
Nie jest ona zbyt ciekawa, zwiera w sobie po prostu zwiększanie pól: sekund, minut, godzin. 
I zerowanie odpowiedniego pola po przekroczeniu granicznej wartości. Czyli: 60 s => 1 min, 60 min => 1 h.

{% highlight csharp linenos %}
private void SubscribeOnTicker(IObservable<long> ticker)
{
	_tickerSubscription = ticker.Subscribe(
		index =>
		{
			if (index % 10 != 0) return;

			CalculateTime();
		},
		Console.WriteLine,
		OnComplete
	);
}
{% endhighlight %}

Na samym końcu metody **CalculateTime**{:.color_2} znajduje się wywołanie metody **Publish**{:.color_1} odpowiedzialnej za wysłanie na strumień aktualnej zmiennej **_time**{:.color_2}. 

A dzieje się to bardzo prosto, skoro mamy listę zapisanych obserwatorów **_observers**{:.color_2} to dzięki dobrodziejstwu **LINQ** wyciąga do każdego obiektu łapę i dusi na publiczne metody **OnNext**{:.color_1}. 
{% highlight csharp linenos %}
private void Publish()
{
	_observers.ForEach(observer => observer.OnNext(_time));
}

Na koniec jeżeli zajdzie potrzeba, i strumień inicjujący (Interval) przejdzie w stan **Completed**. To użyje poniższej metody  **OnComplete**{:.color_1} i dokona żywota wszystkich subskrybentów.
private void OnComplete()
{
	_observers.ForEach(observer => observer.OnCompleted());

	_observers.Clear();
}
{% endhighlight %}

## ObservableProvider
[![Reactive Extensions - Własna klasa publikująca][image2]][image2-big]{:.post-right-image}
Ten post to też początek życia dostawcy obiektów do obserwowania. W tym celu zacząłem pisać klasę pozwalającą na korzystanie z różnych dystrybutorów.

Obecnie zawiera w sobie główny obiekt **_ticker**{:.color_1}. Będzie on wyzwalaczem dla pozostałych obiektów.

**ObservableProvider**{:.color_1} dostarcza na chwilę obecną dwa obiekty do subskrybowania. Pierwszy z nich to opisywany wyżej **ObservableTimeCounter**{:.color_1}. Natomiast drugi (**ObservableValentinesDay**{:.color_1}) został dopisany specjalnie z okazji Walentynek. Zapraszam do przetestowania:).

{% highlight csharp linenos %}
public class ObservableProvider : IDisposable
{
	public ObservableTimeCounter TimeCounter { get; private set; }
	public ObservableValentinesDay ValentinesDay { get; private set; }

	private IObservable<long> _ticker;
	
	public ObservableProvider()
	{
		InitializeTicker();

		Initialize();
	}

	private void Initialize()
	{
		TimeCounter = new ObservableTimeCounter(_ticker);
		ValentinesDay = new ObservableValentinesDay(_ticker);
	}
{% endhighlight %}
Na bazie klasy należy stworzyć obiekt dostawcy, i korzystać z pól dostawców treści.

## Zakończenie
Na koniec warto by w końcu coś zrobić z tą biblioteką. Po dowiązaniu do projektu **OwnObservable**{:.color_1}. Tworzymy obiekt dostawcy i zapisujemy się do dwóch dostępnych dostawców treści: **TimeCounter**{:.color_2}, **ValentinesDay**{:.color_2}.
{% highlight csharp linenos %}
static void Main(string[] args)
{
	var observableProvider = new ObservableProvider();

	observableProvider.TimeCounter.Subscribe(time =>
	{
		Console.ForegroundColor = ConsoleColor.White;
		Console.WriteLine(time);
	});

	observableProvider.ValentinesDay.Subscribe(valentinesDayMessage =>
	{
		Console.ForegroundColor = valentinesDayMessage.Color;
		Console.WriteLine(valentinesDayMessage.Message);
	});
{% endhighlight %}

**Voilà.**{:color_1} 

**Szczęśliwego dnia Walentego. Dziękuję i zapraszam na [GitHub].**{:.h-2}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Tworzymy dane - Generators][previous]**

Następny: **[Programowanie Reaktywne - Marudzimy - Skip][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-tworzymy-dane-generators
[next]: {{site.url}}/programowanie-reaktywne-marudzimy-skip

[post]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/image1-big.jpg

[image2]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/image2.jpg
[image2-big]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-wlasna-klasa-publikujaca/image2-big.jpg