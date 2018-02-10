---
title: Programowanie Reaktywne - Zabawa z czasem - Sample.
date: 2018-02-10
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-sample
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-sample/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-sample/post-big.jpg
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
  - Sample
short: Zapewne każdy naukowiec lubi się bawić próbkami. Jako programista także jestem naukowce. Testuję, próbuje. Eksperymentuje cały czas z nowymi IT-wynalazkami. Takie życie, takie hobby...
---
{% include_relative preface.md %}

## Wstęp
Zapewne każdy naukowiec lubi się bawić próbkami. Jako programista także jestem naukowce. Testuję, próbuje. Eksperymentuje cały czas z nowymi **IT-wynalazkami**. Takie życie, takie hobby...

## Sample
[![Reactive Extensions - Sample][post]][post-big]{:.post-right-image}
Biblioteczka Rxowa pozwala nam także, na pobieranie próbek ze strumieni. Stop, jakie pobieranie przecież to programowanie reaktywne. Próbki dostajemy prosto z dystrybutora. Trzeba tylko namiary zostawić. 

Próbki pobierzemy z pewnego źródła (co 10ms), jakim jest **Observable.Interval**, ale to już znamy;)

{% highlight csharp linenos %}
var observable = Observable.Interval(TimeSpan.FromMilliseconds(10));
{% endhighlight %}

W celach demonstracyjnych napisałem prostą klasie **PickASample**{:.color_2}, gdzie większość magii dzieje się w konstruktorze.

Słowo kluczowe **Sample**{:.color_1}, przyjmujące oczywiście parametr **TimeSpan**. Nakładamy tym samym filtr na bazowy strumień i publikujemy w nowym strumieniu jedną dostarczoną przez bazowego dostawcę dane co określony czas. 

**Observable.Interval -> Sample -> próbka**{:.h-2}

Na nowy strumień musimy się zapisać jednak wcześniej wykonujemy mały trik. Korzystamy z **.Timestamp()**. Skutkuje to opakowaniem danych pochodzących ze strumienia stemplem czasowym (takich operacji jest więcej, ale o tym w dalszych postach **;)**). Dzięki takiemu zabiegowi mam i index + czas, w jakim zostały rozesłane. Efekt jest widoczny w przykładzie w projekcie **Sample** na repozytorium wyzwania: **[GitHub]**.

{% highlight csharp linenos %}
public PickASample(IObservable<long> observable, int seconds)
{
	_seconds = seconds;

	var timeSpan = TimeSpan.FromSeconds(seconds);

	_simpleObservable = observable
		.Sample(timeSpan)
		.Timestamp()
		.Subscribe(
			timestamp =>
			{
				Console.WriteLine($"Sample every {_seconds}[s]: {timestamp}.");
			},			
{% endhighlight %}

[![Reactive Extensions - Sample][image1]][image1-big]{:.post-left-image}

W celach informacyjnych zapisane zostały sekundy w klasie. Tak by potem identyfikować wyniki w odniesieniu do konkretnych obiektów **PickASample**.

Na koniec warto byłoby użyć jeszcze klasy do stworzenia obiektu.
Oczywiście zapisujemy obiekty do późniejszego niszczenia (IDisposable).

{% highlight csharp linenos %}
var sampleList = new List<IDisposable>
{
	new PickASample(observable, 1),
	new PickASample(observable, 3),
	new PickASample(observable, 5)
};
{% endhighlight %}

Zapisanych będzie trzech odbiorców. Z odpowiednio ustawionymi czasami pobierania próbek na **1s**, **3s**, **5s**.

## Zakończenie
Wyniki działania zamieszczonych fragmentów kodu, najlepiej sprwdzić odpalając cały projekt z **[GitHub-a]**. Zapraszam.

Strzelił mi dzisiaj do głowy niecny plan. By nagrać serie video na **[YT]** o podobnej tematyce. Ale czy to dojdzie do skutku. Być może to temat kolejnego wyzwania...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Delay][previous]**

<!--Następny: **[Programowanie Reaktywne - Kto za tym stoi? - Sheduler.][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-delay
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval

[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-sample/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-sample/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-sample/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-sample/image1-big.jpg
