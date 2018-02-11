---
title: Programowanie Reaktywne - Zabawa z czasem - Interval.
date: 2018-02-07
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-interval
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-interval/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-interval/post-big.jpg
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
  - Interval
short: Po uporządkowaniu pewnych kolejnych spraw. Pora na kolejny obiekt, jaki możemy obserwować. Wchodzący w skład timerów. Tym razem chodzi o uproszczoną wersje Observable.Timer... 
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Scheduler][post]][post-big]{:.post-right-image}

Po uporządkowaniu pewnych kolejnych spraw. Pora na kolejny obiekt, jaki możemy obserwować. Wchodzący w skład timerów. 
Tym razem chodzi o uproszczoną wersje **Observable.Timer**... 

## Observable.Interval
Jeżeli nie ma potrzeby opóźnienia wyzwolenia pierwszego powiadomienia do obserwatorów. Wówczas można skorzystać z prostszej formy timer o nazwie **Interval**{:.color_1}. 

Przyjmuje co najmniej jeden parametr i jest to czas co ile będą wyzwalane powiadamianie subskrybentów. Wartość ta jest typu **TimeSpan**.

{% highlight csharp linenos %}
private static void AddSubscribent(List<IDisposable> subscribents, 
  IObservable<long> observable)
{
  var subscribent = observable
    .Subscribe(
      index => { Console.WriteLine($"Index: {index}"); },
      exception => { Console.WriteLine($"Exception: {exception}"); },
      () => { Console.WriteLine("Completed"); });

      subscribents.Add(subscribent);
}
{% endhighlight %}

[![Reactive Extensions - Interval][image1]][image1-big]{:.post-left-image}

Drugi parametr to Scheduler, o którym trochę pisałem w poście: [Programowanie Reaktywne - Kto za tym stoi? - Sheduler]. Podobnie jak poprzednio możemy określić kto będzie odpowiedzialny za obsługę całego bałaganu.

Kod jest bardzo prosty dlatego też pozwoliłem sobie zapisać całe ciało delegatów odpowiednio dla każdej z metod (**OnNext**{:.color_1}, **OnError**{:.color_1}, **OnCompleted**{:.color_1}) w jednej linii.

Oczywiście tak jak poprzednio zachowujemy obserwatorów w liście, do późniejszego usunięcia.

{% highlight csharp linenos %}
var observableInterval = Observable.Interval(TimeSpan.FromMilliseconds(200));

var observableIntervalSheduler = Observable.Interval(
  TimeSpan.FromMilliseconds(2000), 
  TaskPoolScheduler.Default);

AddSubscribent(subscribents, observableInterval);
AddSubscribent(subscribents, observableIntervalSheduler);
{% endhighlight %}

W celach demonstracyjnych tworzymy dwa obserwowane obiekty, jeden, korzystając z **TaskPoolScheduler** w celu wymuszenia korzystania z **TaskPool**.

Będą one publikowały w różnych odstępach czasu.

## Zakończenie
Nowa metoda nie wnosi nic nowego, jedynie upraszcza kod w stosunku do **Observable.Timer-a**{:.color_1}.

Jednak im mniej kodu, tym lepiej:)...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Nie zapominaj - Subscribe][previous]**

Następny: **[Programowanie Reaktywne - Zabawa z czasem - Buffer][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-nie-zapominaj-subscribe
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-buffer

[Programowanie Reaktywne - Kto za tym stoi? - Sheduler]: {{site.url}}/programowanie-reaktywne-kto-za-tym-stoi-sheduler

[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-interval/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-interval/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-interval/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-interval/image1-big.jpg

[linq]: https://msdn.microsoft.com/en-us/library/bb308959.aspx
[ms]: http://microsoft.com
[Reactive Extensions]: https://msdn.microsoft.com/en-us/library/hh242985(v=vs.103).aspx