---
title: Programowanie Reaktywne - Kombinatorzy - Switch.
date: 2018-02-24
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-switch
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-switch/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-switch/post-big.jpg
categories:
  - Programowanie Reaktywne
  - '30 day challenge'
  - Programowanie
  - Reactive Extensions
tags:
  - Reactive Extensions
  - Observer
  - Observable
  - Programowanie Reaktywne
  - Rx
  - Switch
short: Swego czasu był taki film gdzie głównie bohaterowie zamieniają się między sobą swoimi zasobami. W przypadku Rx-ów do czynienia mamy z metodą pozwalając przetaczać na inną usługę w przypadku gdy pierwsza zawieszę.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Switch][post]][post-big]{:.post-right-image}
Swego czasu był taki film gdzie głównie bohaterowie zamieniają się między sobą swoimi zasobami. W przypadku **Rx-ów** do czynienia mamy z metodą pozwalając przetaczać na inną usługę w przypadku gdy pierwsza zawieszę.

## Observable.Switch
Samą implementację rozpoczynam od stworzenia listy generatorów. Lista ta będzie niezbędna w procesie budowania **Switch-a**{:.color_1}. Listę trzeba uprzednio przekonwertować na odpowiedni typ. W tym przypadku będzie to typ: ```IObservable<IObservable<Randomizer>>```. Do konwertowania wykorzystujemy wbudowaną funkcjonalność w **Rx-ach**: **ToObservable**{:.color_1}.

{% highlight csharp linenos %}
var randomedList = new List<IObservable<Randomed>>();
randomedList.Add(ObservableRandomizer.Create(0, 100));
randomedList.Add(ObservableRandomizer.Create(1000, 2000));
randomedList.Add(ObservableRandomizer.Create(0, 100));

for (var i = 0; i < randomedList.Count; i++)
{
  randomedList[i].DefaultPrint($"Randomizer{i}");
}

var observableRandomedList = randomedList.ToObservable();

var observableSequence = observableRandomedList.Switch();

var subscription1 = observableSequence.DefaultPrint("Switch");
{% endhighlight %}

Po wykonaniu tej operacji możemy dokonać zapisu na nowo powstały strumień np. przy pomocy metody **DefaultPrint**{:.color_2}. 
Tworzenie **Observable.Switch**{:.color_1} można wykonać w dwojaki sposób:
* **Observable.Switch(poszczególne sekwencje oddzielone średnikiem)**,
* **.Switch()** ten sposób określamy korzystanie z nowej funkcjonalności bezpośrednio na przekonwertowanej do typu **IObservable**.

[![Reactive Extensions - Switch][image1]][image1-big]{:.post-left-image}

Ale czym jest ten **Switch**{:.color_1}. Otóż odpowiedzialny jest on za wybór strumienia jaki będzie wykorzystany do publikacji wyników pochodzących od dystrybutora powstałego na wskutek działania metody **Switch**.
Jego główne założenie, mówi że publikowane są dane jedynie z najświeższego strumienia jaki został podpięty.

Do projektu z **Rx-ami** dodałem nową klasę  **Randomed**{:.color_2}, która to będzie zawierała informacje generowane przez wątek na jakim uruchomiona jest publikacja.

{% highlight csharp linenos %}
namespace RXLib.Randomizer
{
	public class Randomed
	{
		public int Value { get; set; }
		public long Ticks { get; set; }

		public Randomed()
		{
			Value = 0;
			Ticks = 0;
		}

		public override string ToString()
		{
			return $"{Ticks}->{Value}";
		}
{% endhighlight %}

Dodatkowo stworzyłem całą klasę o nazwie: **ObservableRandomizer**{:.color_1} zawierającą poniższy wątek jaki odpowiedzialny jest za publikowanie danych po sieci.

{% highlight csharp linenos %}
private void StartThread()
{
  _threadInProgress = true;

  _thread = new Thread(ThreadMethod);
  _thread.Start();
}

private void ThreadMethod()
{
  while (_threadInProgress)
  {
    var delay = new Random(DateTime.Now.Millisecond).Next(200, 1000);
    Thread.Sleep(delay);

    _randomed.Ticks = DateTime.Now.Ticks;
    _randomed.Value = new Random(DateTime.Now.Millisecond).Next(_from, _to);

    Publish();
  }
}
{% endhighlight %}

Owe działania odbywają się w wątkach. Dlatego, że aplikacja ma działać samodzielnie. Przygotowując a następnie publikując dane.

## Zakończenie
W trakcie rozwoju programu dotyczącego **Switch**. Napisałem dwie klasy pomocnicze, jednak nie są one obecnie wykorzystywane.
Pierwsza z nich dodaje do strumienia **Timestamp**, a następnie go wyświetla.

{% highlight csharp linenos %}
public static IDisposable PrintWithTimestamp<T>(this IObservable<T> source, string identify)
{
  var subscription = source
    .Timestamp()
    .Subscribe(
      item =>
{% endhighlight %}

Analogicznie działa druga metoda o nazwie: **PrintWithTimeInterval**{:.color_1}. Jedyna różnica jaka tutaj się znajduje to korzystanie w tym przypadku z **TimeInterval**{:.color_1}

{% highlight csharp linenos %}
public static IDisposable PrintWithTimeInterval<T>(this IObservable<T> source, string identify)
{
  var subscription = source
    .TimeInterval()
    .Subscribe(
      item =>
{% endhighlight %}

{% include_relative end.md %}

W obecnym projekcie na chwilę obecną nie owe metody nie są wykorzystywane. Ich implementację napisałem w trakcie pracy nad dzisiejszym aktorem czyli metodą **Switch**{:.olor_1}.

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Zip][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - When-And-Then][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-zip
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-when-and-then

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-switch/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-switch/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-switch/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-switch/image1-big.jpg