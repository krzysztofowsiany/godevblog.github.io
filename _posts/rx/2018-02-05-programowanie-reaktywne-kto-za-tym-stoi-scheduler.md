---
title: Programowanie Reaktywne - Kto za tym stoi? - Scheduler.
date: 2018-02-05
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kto-za-tym-stoi-scheduler
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kto-za-tym-stoi-scheduler/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kto-za-tym-stoi-scheduler/post-big.jpg
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
  - Scheduler
short: A jak funkcjonują ten cały mechanizm obserwowanego i obserwatora? Przecież muszą być obrabiane w pocie czoła przez nasze wspaniałe CPU. Magia dzieje się poza naszym polem widzenia. Biblioteka Rx udostępnia mechanizm harmonogramu.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Scheduler][post]][post-big]{:.post-left-image}
A jak funkcjonują ten cały mechanizm obserwowanego i obserwatora? Przecież muszą być obrabiane w pocie czoła przez nasze wspaniałe CPU... Magia dzieje się poza naszym polem widzenia.

Biblioteka **Rx** udostępnia mechanizm harmonogramu. Odpowiedzialny jest za rozsyłanie powiadomień do subskrybentów.

## Schedulery
Do dyspozycji mamy dość sporą grupę scheduler-ów, skupię się na kilku głównych.

W tym celu napisałem klasę pomocniczą opartą na poznanym już terminie [Timerów][previous] o nazwie **ExampleTimer**{:.color_1}

{% highlight csharp linenos %}
public ExampleTimer(String name, IScheduler scheduler)
{
  Initialize(name);
  _timerObservable = Observable.Timer(_dueTime, _period, scheduler);

  Subscribe();
}

private void Initialize(String name)
{
  _dueTime = TimeSpan.FromSeconds(1);
  _period = TimeSpan.FromSeconds(1);
  _name = name;
}
{% endhighlight %}

**ImmediateScheduler** - bazując na tym zostanie uruchomiony natychmiast na bierz, działa na bieżącym wątku, synchronicznie.

{% highlight csharp linenos %}
new ExampleTimer("ImmediateScheduler", ImmediateScheduler.Instance)
{% endhighlight %}

**CurrentThreadScheduler** - bazuje na bieżącym wątku, i jest normalnie kolejkowań jak każda inna operacja. Tym samym może przylagować, podobnie jak Immediate działa synchronicznie.

{% highlight csharp linenos %}
new ExampleTimer("CurrentThreadScheduler", CurrentThreadScheduler.Instance)
{% endhighlight %}

**NewThreadScheduler** - działa na nowym niezależnym wątku, dobrze nadaje się do długich działań, działa asynchronicznie.

{% highlight csharp linenos %}
new ExampleTimer("NewThreadScheduler", NewThreadScheduler.Default)
{% endhighlight %}

**ThreadPoolScheduler** - publikowanie treści pochodzi z puli wątków działających w tle, przeznaczone do krótkotrwałego używania, asynchronicznie.

{% highlight csharp linenos %}
new ExampleTimer("ThreadPoolScheduler", ThreadPoolScheduler.Instance)
{% endhighlight %}

[![Reactive Extensions - Scheduler][image1]][image1-big]{:.post-right-image}
**TaskPoolScheduler** - akcje wyzwalane są w tym przypadku z puli zadań jest to forma bardzie abstrakcyjna aniżeli pula wątków. Najlepiej wykorzystać w krótkich działaniach jest to też działanie asynchronicznie.

{% highlight csharp linenos %}
new ExampleTimer("TaskPoolScheduler", TaskPoolScheduler.Default)
{% endhighlight %}

Jeżeli nie zdefiniujemy żadnego schedulera, to wówczas zostanie przydzielony automatycznie na podstawie kontekstu tworzenia obiektu obserwowanego.

## Zakończenie
Przeważnie nie ma potrzeby manipulowaniem automatycznego przydzielania Schedulera. Jednak w pewnych sytuacjach można wpłynąć na to jak będzie się zachowywał. 

To na tyle w tym pościku, zapraszam do kolejnych.

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Timer.][previous]**

Następny: **[Programowanie Reaktywne - Nie zapominaj - Subscribe.][next]**

------

[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-timer
[next]: {{site.url}}/programowanie-reaktywne-nie-zapominaj-subscribe

[post]: /assets/images/2018/02/programowanie-reaktywne/kto-za-tym-stoi-scheduler/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kto-za-tym-stoi-scheduler/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kto-za-tym-stoi-scheduler/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kto-za-tym-stoi-scheduler/image1-big.jpg
