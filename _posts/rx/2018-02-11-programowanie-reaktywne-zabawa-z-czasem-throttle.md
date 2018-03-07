---
title: Programowanie Reaktywne - Zabawa z czasem - Throttle.
date: 2018-02-11
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-throttle
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-throttle/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-throttle/post-big.jpg
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
  - Throttle
  - ToObservable
short: Jazda z koksem... Dzisiaj poruszymy tematykę - kolejnego operatora związanego z czasem. Hurra... Znowu. To jednak już przed ostatnia część związana z czasem... Zapraszam ponownie do krainy reaktywnej magii.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Throttle][post]][post-big]{:.post-left-image}
Jazda z koksem... Dzisiaj poruszymy tematykę - kolejnego operatora związanego z czasem. Hurra... :| Znowu?? To jednak już przed ostatnia część związana z czasem... Zapraszam ponownie do krainy reaktywnej magii.

## Observable.Throttle
Dzisiaj mamy ciekawy obiekt. Jego zachowanie bywa często przydatne, zwłaszcza gdy chcemy wykryć sytuację bezczynności użytkownika. 

Publikowanie treści na strumieniu wyzwalane jest w tym przypadku gdy zostanie wykryta bezczynność na bazowym strumieniu powyżej określonego czasu.

W tym celu przygotowałem projekt o nazwie **Throttle**{:.color_1} znajdujący się na **[GitHub]**.

Zbudowałem sztuczny twór samoczynnie blokujący i zwalniający proces publikowania treści do strumienia z wykorzystaniem pętli i opóźnienia **Throw.Sleep**.

{% highlight csharp linenos %}
public IObservable<int> Stream => GetStream().ToObservable();

private IEnumerable<int> GetStream()
{
	var i = 0;

	while (!_end)
	{
		while (!_publish)
		{
			Thread.Sleep(100);
		}

		Console.Write($"{i},");

		yield return i++;

		Thread.Sleep(100);
	}
}
{% endhighlight %}

[![Reactive Extensions - Throttle][image1]][image1-big]{:.post-right-image}

Jak widać na powyższym fragmencie, pętla **while**{:.color_2} odpowiada za publikowanie danych na strumień. Natomiast pole **_publish**{:.color_2} - określa czy publikować treści, czy czekać na zmianę statusu.

Dla uproszczenia konwersję z **IEnumerable => IObservable**{:.color_1} wykonują w klasie pod właściwością: **Stream**{:.color_2}.
Do tego celu wykorzystałem rozszerzenie **ToObservable**{:.color_1} z Rx-ów. Pozwalające właśnie na taką zamianę.

Kolejny fragment to użycie **[Observable.Interval]**{:.color_2} do zmiany statusu publikacji danych na strumieniu dla **Observable.Throttle**{:.color_2}. Dodatkowo wyświetlanych jest trochę informacji na temat zmiany. 
{% highlight csharp linenos %}
var switcherTimeSpan = TimeSpan.FromSeconds(5);
var switcher = Observable.Interval(switcherTimeSpan);
_switcherSubscribe = switcher.Subscribe(x =>
	{
	_publish = !_publish;

	var swithcTo = _publish ? "publish (unlock stream)" : "not publish (lock stream)";

	Console.WriteLine();
	Console.WriteLine($"Switch to {swithcTo}");
	Console.WriteLine();
	},
	Console.WriteLine,
	() => { Console.WriteLine("Switcher completed"); });
}

{% endhighlight %}

Uprościłem także kod samego **Subscribe**, poprzez bezpośrednie wykorzystanie **Console.WriteLine**{:.color_2} jako **OnError**{:.color_2} bez konieczności użycia **lambdy**.

Ostatni fragment to już wykorzystanie klasy **StreamPublisher**{:.color_2}. Zapisanie się na strumień przy pomocy **Throttle**{:.color_1}. I logowanie tych operacji. Także tutaj skorzystałem z **Timestamp**{:.color_2} w celu opakowania danych stemplem czasowym.

{% highlight csharp linenos %}
var streamPublisher = new StreamPublisher();

var throttle = streamPublisher.Stream.Throttle(TimeSpan.FromMilliseconds(500));

var throttleSubscribe = throttle.Timestamp().Subscribe(
	x => Console.WriteLine("Last item {0}: {1}", x.Value, x.Timestamp),
	Console.WriteLine,
	() => Console.WriteLine("Throttle completed"));
{% endhighlight %}
Tym samym jeżeli na strumień będą publikowane dane i publikacja zostanie wstrzymana na więcej niż **500ms**. To wówczas **Throttle**{:.color_1} wyświetli ostatnio wysłaną danę.

## Zakończenie
Zapraszam do zabawy z przykładem jaki zamieściłem na **[GitHub]**. Samodzielnego poeksperymentowania. Analizy. Krytykowania błędów autora ;). Przecież nie jestem Alfą i Omegą.

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Sample][previous]**

Następny: **[Programowanie Reaktywne - Zabawa z czasem - Timestamp/TimeInterval.][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-sample
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-timestamp-and-timeinterval

[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-throttle/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-throttle/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-throttle/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-throttle/image1-big.jpg

[Observable.Interval]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval