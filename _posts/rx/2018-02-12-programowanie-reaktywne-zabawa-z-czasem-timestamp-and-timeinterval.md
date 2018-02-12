---
title: Programowanie Reaktywne - Zabawa z czasem - Timestamp/TimeInterval.
date: 2018-02-12
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-timestamp-and-timeinterval
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timestamp-and-timeinterval/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timestamp-and-timeinterval/post-big.jpg
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
  - Timestamp
  - TimeInterval  
  - Extension Methods
short: To już ostatni post z rodziny timer-owatych. Omówione zostaną dwa proste operatory. Ale co ważniejsze, zaimplementujemy kolejne dwa własne. Rx oparty jest o rozszerzone metody, dlatego bardzo łatwo jest dodać kolejne potrzebne "stworki".
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Extension Methods][post]][post-big]{:.post-right-image}
To już ostatni post z rodziny timer-owatych. Omówione zostaną dwa proste operatory. Ale co ważniejsze, zaimplementujemy kolejne dwa własne. Rx oparty jest o rozszerzone metody, dlatego bardzo łatwo jest dodać kolejne potrzebne "stworki".

## TimeInterval, Timestamp
Pierwszy fragment kodu dotyczy oznaczania danych na strumieniu interwałem czasowym. Dzięki takiemu działaniu, można zaobserwować ile czasu upłynęło pomiędzy poszczególnymi danymi publikowanymi do obserwatorów.
Po takiej konwersji otrzymujemy nie jedną, a dwa pola:
* **Value** - to wartość podawana przez strumień bazowy,
* **Interval** - okres jaki upłynął od ostatniego przetwarzania strumienia.

Przykład oczywiście na [GitHub-ie] w projekcie o nazwie **StampAndInterval**{:.color_1}, a fragment poniżej.
{% highlight csharp linenos %}
var observableInterval = Observable.Interval(TimeSpan.FromSeconds(1));

_subscribeTimeInterval = observableInterval
	.TimeInterval()
	.Subscribe(
		x => Console.WriteLine("TimeInterval \t\t{0} \t{1}", x.Value, x.Interval)
	);

_subscribeTimestamp = observableInterval
	.Timestamp()
	.Subscribe(
		x => Console.WriteLine("Timestamp \t\t{0} \t{1}", x.Value, x.Timestamp)
	);
{% endhighlight %}

[![Reactive Extensions - Extension Methods][image1]][image1-big]{:.post-left-image}
Już wcześniej w postach korzystaliśmy z operatora opakowującego strumienie tak by uzyskać oprócz danych np. stempel czasowy. Do tego celu posłużyliśmy się operatorem: **.Timestamp()**{:.color_1}. Po opakowaniu otrzymujemy dwie właściwości: 
* **Value** - to wartość podawana przez strumień bazowy,
* **Timestamp** - czas danych publikowanych na strumień.

## Extension Methods
Zajmiemy się teraz odwróceniem działania Timestamp(), TimeInterval(). W tym celu należy nieco się napocić, i zaimplementować własne rozszerzenia do interfejsu **IObservable**{:.color_1}.

{% highlight csharp linenos %}
public static class RXExtensions
{
	public static IObservable<TSource> RemoveTimeInterval<TSource>(this IObservable<TimeInterval<TSource>> source)
	{
		return source.Select(x => x.Value);
	}

	public static IObservable<TSource> RemoveTimestamp<TSource>(this IObservable<Timestamped<TSource>> source)
	{
		return source.Select(x => x.Value);
	}
}
{% endhighlight %}

Po implementacji metod, należy nie marnować kodu i go użyć. Strumień w tym przypadku musi już posiadać odpowiednie opakowanie.
W pierwszym przykładzie: **RemoveTimestamp**{:.color_1}, należy opakować oczywiście **Timestamp-em**. I tak właśnie się dzieje w pierwszym przykładzie poniżej.

{% highlight csharp linenos %}
var observableInterval = Observable.Interval(TimeSpan.FromSeconds(1)).Timestamp();

_subscribeWithoutTimestamp = observableInterval
	.RemoveTimestamp()
	.Subscribe(
		x => Console.WriteLine("Remove Timestamp \t{0}", x)
	);
{% endhighlight %}

Analogicznie postąpimy z drugim przykładem, z tą różnicą że będziemy korzystać z operatorów dotyczących **TimeInterval**{:.color_2}.
Odpowiednio **.TimeInterval()**{:.color_1} i **.RemoveTimeInterval()**{:.color_1}.

{% highlight csharp linenos %}
var observableInterval = Observable.Interval(TimeSpan.FromSeconds(1)).TimeInterval();

_subscribeWithoutTimeInterval = observableInterval
	.RemoveTimeInterval()
	.Subscribe(
		x => Console.WriteLine("Remove TimeInterval \t{0}", x)
	);
{% endhighlight %}

## Zakończenie
Kończąc tą partie postów dotyczących czasu. Mam nadzieję, iż przysłużyłem się komuś moją malutką wiedzą na ten temat. 
W kolejnych poznawać będziemy inne mechanizmy, operatory jakie dostarczają biblioteki **Reactive Extensions**{:.color_1}. Zapraszam do śledzenia. I dziękuję za obecność.

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Throttle][previous]**

<!--Następny: **[Programowanie Reaktywne - Zabawa z czasem - Delay.][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-throttle
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval

[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timestamp-and-timeinterval/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timestamp-and-timeinterval/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timestamp-and-timeinterval/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timestamp-and-timeinterval/image1-big.jpg

[Observable.Interval]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-timestamp-and-timeinterval