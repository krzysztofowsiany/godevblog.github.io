---
title: Programowanie Reaktywne - Zabawa z czasem - Timer.
date: 2018-02-03
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-timer
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timer/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timer/post-big.jpg
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
  - Timer
short: Wielokrotnie w swoim życiu stosowałem dwojakiego rodzaju wyzwalacze w celu cyklicznego wykonywania pewny czynności. Mowa tutaj o wykorzystaniu Timera lub Thread. Pierwszy z nich polega na utworzeniu klasy, która będzie cyklicznie co określony czas wyzwalała event.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Timer][post]][post-big]{:.post-right-image}
Wielokrotnie w swoim życiu stosowałem dwojakiego rodzaju wyzwalacze w celu cyklicznego wykonywania pewny czynności. 
Mowa tutaj o wykorzystaniu **Timera** lub **Thread**.
Pierwszy z nich polega na utworzeniu klasy, która będzie cyklicznie co określony czas wyzwalała **event**.

Natomiast druga opcja to wykorzystanie wątku + pętli. 
Do pętli wrzucamy to co chcemy cyklicznie wykonywać, wzbogacone o opóźnienie czasowe np. **Thread.Sleep(100)**{:.color_1}.

Ale hola miało być o reaktywnym programowaniu! 


## Observable.Timer
W tej sytuacji z pomocą przychodzi Reactive Extensions oraz bogaty zestaw strumieni do cyklicznego wyzwalania reakcji na obserwatorach.

Pierwszy z nich dość prosty to **Timer**.

Tak teraz pora na pierwszy kodzik wykorzystujący Reactive Extensions. Jest on dostępny na repozytorium [GitHub].

Jak stworzyć taki strumień do obserwowania? Jak go obserwować?

Tworzenie prostego strumienia dla Timer-a.
{% highlight csharp linenos %}
public TimerDueTimeAndPeriod(TimeSpan dueTime, TimeSpan period)
{
	_className = this.GetType().Name;

	_timerObservable = Observable.Timer(dueTime, period);
{% endhighlight %}

Zmienna **_className** wykorzystana jest jedynie do celów identyfikacji, wyrzucanych na konsole treści;).

A tak się zapisujemy na timer-ek.
{% highlight csharp linenos %}
_lambdaSubscribe = timerObservable.Subscribe(index =>
{
    Console.WriteLine($"[{_className}] : From lambda: {index}");
});
{% endhighlight %}

Dzięki tej zmiennej: **_lambdaSubscribe** kasujemy zapis obserwatora na strumień publikowany przez obiekt obserwowany.

**index** to identyfikator publikowania treści dla subskrybentów. Po każdej publikacji zwiększany jest o 1.

Korzystamy tutaj z **lambdy**{:.color_1} jednak nic nie stoi na przeszkodzie, by skorzystać z normalnej metody.
{% highlight csharp linenos %}
    _methodSubscribe = timerObservable.Subscribe(OnTimer);
}

private void OnTimer(long index)
{
	Console.WriteLine($"[{_className}] : From lambda: {index}");
}
{% endhighlight %}

[![Reactive Extensions - Timer][image1]][image1-big]{:.post-left-image}
Zmienna **_methodSubscribe** jest nam potrzebna do późniejszego zniszczenia subskrybowanego strumienia.

Powyższe fragmenty kodu znajdują się w klasie: **TimerDueTime**.

To najprostsze użycie Timera ma jedną wadę. Wykona się tylko raz po upływie określonego czasu **dueTime**.

Ale zawsze można coś zaradzić. Przecież mamy takie coś jak przeciążanie operatorów:D
{% highlight csharp linenos %}
public TimerDueTimeAndPeriod(TimeSpan dueTime, TimeSpan period)
{
	_className = this.GetType().Name;

	_timerObservable = Observable.Timer(dueTime, period);
{% endhighlight %}

Dochodzi kolejny parametr **period**, określa powtarzanie publikacji co określony czas (nie należy zapomnieć, iż rozpocznie się to dopiero po upłynięciu dueTime).

Tym sposobem mamy do dyspozycji ładny timer-ek z wykorzystaniem **RX-ów**{:.color_1}.

## Zakończenie
Pierwsze koty za płoty. Myślę, że na dzisiaj wystarczy. Jednak nie jest to Całkowie wyczerpanie tematów **Timer**-ów. W kolejnym poście opiszę czym są **Schedulery**{:.color_1}, czyli kolejny parametr, jaki możemy przekazać w metodzie **Observable.Timer(...)**{:.color_1}.

Zapraszam na **[GitHub]** do przejrzenia mojej "twórczości".

**Czym innym, jak nie współczesną poezją jest programowanie?**{:.h-4}
**Jako dowód: także w tym procederze, nie jest rzadkością pytanie.**{:.h-4}
**Co autor miał na myśli - twórczości interpretowanie.**{:.h-4}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Wstęp.][previous]**

Następny: **[Programowanie Reaktywne - Kto za tym stoi? - Scheduler.][next]**

------

[previous]: {{site.url}}/programowanie-reaktywne-wstep
[next]: {{site.url}}/programowanie-reaktywne-kto-za-tym-stoi-scheduler

[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timer/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timer/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timer/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-timer/image1-big.jpg

[linq]: https://msdn.microsoft.com/en-us/library/bb308959.aspx
[ms]: http://microsoft.com
[Reactive Extensions]: https://msdn.microsoft.com/en-us/library/hh242985(v=vs.103).aspx