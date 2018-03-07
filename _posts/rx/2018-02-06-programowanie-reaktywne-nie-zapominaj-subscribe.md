---
title: Programowanie Reaktywne - Nie zapominaj - Subscribe.
date: 2018-02-06
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-nie-zapominaj-subscribe
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/nie-zapominaj-subscribe/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/nie-zapominaj-subscribe/post-big.jpg
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
  - Subscribe
  - OnNext
  - OnError
  - OnComplete
  - Timer
short: Trochę czasu już upłynęło... Warto by było przyswoić pewne dodatkowe informacje procesie zapisu na strumienie. Przykłady przedstawione do tej pory w postach są bardzo uproszczone. var observableTimer = Observable.Timer(_dueTime, _period, scheduler);
---
{% include_relative preface.md %}

## Wstęp
Trochę czasu już upłynęło... Warto by było przyswoić pewne dodatkowe informacje procesie zapisu na strumienie.

Przykłady przedstawione do tej pory w postach są bardzo uproszczone:

{% highlight csharp linenos %}
var observableTimer = Observable.Timer(_dueTime, _period, scheduler);

observableTimer.Subscribe(index =>
{
    Console.WriteLine($"Lambda: {index}");
});
{% endhighlight %}

## Subskrybowanie
[![Reactive Extensions - Subscribe][post]][post-big]{:.post-left-image}
Metoda zapisu przyjmuje (ale nie musi) trzy delegaty:
* **OnNext** - jest to ciało delegatu wykonywanego w trakcie publikowania przez obiekt obserwowany treści. To tutaj dzieje się nasza zaimplementowana magia,
* **OnError** - oczywiście zdarzyć się może, że nie będzie można zapisać się do strumienia, wówczas zostanie wyzwolony delegat z błędem. Warto by było także skorzystać z tej możliwości,
* **OnCompleted** - ostatni trywialny delegat, informuje, gdy strumień się zakończy. W przypadku **Timer-a**. Ta sytuacja nie nastąpi.

Zapis do strumienia niesie ze sobą pewne niebezpieczeństwo. Istnieje ryzyko wyłożenia subskrypcji zależne od implementacji zawartej w **=>(lambda)**. 
Nasz wspaniały idealny kod może rzucić wyjątkiem. Wówczas **OnNext** przestanie być wyzwalane. Dlatego warto by uchwycić co nieco w ciele delegatu.

Nowa klasa **StreamTimer** zawiera metodę do zapisu.

{% highlight csharp linenos %}
public void Subscribe(Action<long> onNext)
{
  var newSubscribent = _timerObservable.Subscribe(
    onNext,
    OnError,
    OnCompleted
    );

  _subscribents.Add(newSubscribent);
}

private void OnCompleted()
{
  Console.WriteLine("Completed");
}

private void OnError(Exception ex)
{
  Console.WriteLine(ex);
}

public void Dispose()
{
  _subscribents.ForEach(x => x.Dispose());
}
{% endhighlight %}

Dzięki klasie stworzony został timer i w nim domyślnie obsługa **OnError**{:.color_1} i **OnCompleted**{:.color_1}.
Czyli już nie ma co się nimi martwić.

Kolejny fragment pokazuje jak zapisywać obserwatorów.
Pierwszy przykład od linii:1. Nie będzie powodował problemu dlatego pozwoliłem sobie napisać w najprostszej postaci.

{% highlight csharp linenos %}
timer.Subscribe(index =>
{
  Console.WriteLine($"YEAH {index}");
});

timer.Subscribe(index =>
{
  try
  {
    throw new Exception("TRAH!");
  }
  catch (Exception e)
  {
    Console.WriteLine(e);
  }
});

timer.Subscribe(index =>
{
  throw new Exception("TRAH!");
});
{% endhighlight %}

[![Reactive Extensions - Subscribe][image1]][image1-big]{:.post-right-image}

Linia:6 zawiera w sobie mechanizm obsługi wyjątków, a to dlatego, że rzucamy jednym w przeciwnym wypadku aplikacja zostałaby zatrzymana.
W linii:18 zaczyna się fragment kodu, który spowoduje wywalenie programu. W repozytorium jest on za komentowany tak by program się uruchamiał i działał.

## Zakończenie
Warto byłoby wspomnieć także, o sprzątaniu po sobie. Czyli używaniu **Dispose**. Najpierw zapisujemy zapisanego subskrybenta. Tak by potem na koniec można było ich wszystkich wywalić na zbity r__.

{% highlight csharp linenos %}
  _subscribents.Add(newSubscribent);
}

public void Dispose()
{
  _subscribents.ForEach(x => x.Dispose());
}
{% endhighlight %}

W linii: 1 zapisujemy a w 6 niszczymy.

Mam nadzieję, że ponownie przybliżyłem **Reactive Extensions**:).

**Pamiętajcie! Łapcie wyjątki puki gorące!**{:.h-allert-1}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kto za tym stoi? - Scheduler.][previous]**

Następny: **[Programowanie Reaktywne - Zabawa z czasem - Interval][next]**

------

[previous]: {{site.url}}/programowanie-reaktywne-kto-za-tym-stoi-scheduler
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval

[post]: /assets/images/2018/02/programowanie-reaktywne/nie-zapominaj-subscribe/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/nie-zapominaj-subscribe/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/nie-zapominaj-subscribe/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/nie-zapominaj-subscribe/image1-big.jpg

[linq]: https://msdn.microsoft.com/en-us/library/bb308959.aspx
[ms]: http://microsoft.com
[Reactive Extensions]: https://msdn.microsoft.com/en-us/library/hh242985(v=vs.103).aspx