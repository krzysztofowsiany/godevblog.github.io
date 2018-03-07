---
title: Programowanie Reaktywne - Kombinatorzy - Start With.
date: 2018-02-20
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-start-with
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-start-with/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-start-with/post-big.jpg
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
  - StartWith
short: Dzisiaj kolejny operatorek pozwalający na kombinowanie ze strumieniami. Tym razem taki co to potrafi się wepchnąć do kolejki i być na początku. Jak to i w życiu bywa co nie jest odpowiednim zachowanie. Jednak w przypadku programowania z wykorzystaniem Rx-ów jak najbardziej.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Start With][image1]][image1-big]{:.post-left-image}
Dzisiaj kolejny operatorek pozwalający na kombinowanie ze strumieniami. Tym razem taki co to potrafi się wepchnąć do kolejki i być na początku. Jak to i w życiu bywa co nie jest odpowiednim zachowanie. Jednak w przypadku programowania z wykorzystaniem **Rx-ów** jak najbardziej.

## StartWith
Dzisiejszy bohater pozwala na wrzucenie danych na sam początek strumienia. Można w ten sposób kontrolować konkretnie co znajduje się na początku.

Poniższa metoda **GetTimeListSamples** tworzy listę obiektów typy **Time**{:.color_1}. Po utworzeniu listy zwracamy ją i będziemy wpychać na sam początek kolejeczki.
{% highlight csharp linenos %}
private static List<Time> GetTimeListSamples()
{
  var timeList = new List<Time>();

  for (short i = 10; i < 20; i++)
  {
    timeList.Add(new Time {Hours = i, Minutes = i, Seconds = i});
  }
{% endhighlight %}

[![Reactive Extensions - Start With][post]][post-big]{:.post-right-image}

Wynikiem powyższej metody jest **timeList**{:.color_1}, która zostanie wstrzyknięta między **Subscribe**{:.color_2}, a dystrybutorem timer-owatym **TimeCounter**{:.color_2}.
Służy do tego **StartWith**{:.color_1} przyjmująca w tym przypadku uprzednio wygenerowaną listę. Ważne by była to list rozszerzająca interfejs **IEnumberable**{:.color_1}.

{% highlight csharp linenos %}
var timeList = GetTimeListSamples();

  var subscribent = observableProvider
    .TimeCounter
    .StartWith(timeList)
    .
    .
    .
    .Subscribe(
    time =>
    {
      Console.WriteLine(time);
{% endhighlight %}

Inna tważ **StartWith**{:.color_1} przyjmuje parametry jako **params**{:.color_1}. Czyli tyle ile chcemy, tyle wrzucamy.

{% highlight csharp linenos %}
.StartWith(
    new Time { Hours = 1, Minutes = 10 },
    new Time { Hours = 2, Minutes = 20 },
    new Time { Hours = 3, Minutes = 10, Seconds = 20 },
    new Time { Hours = 4, Minutes = 10 }
  )
  .Subscribe(
    time =>
    {
      Console.WriteLine(time);
{% endhighlight %}

Oczywiście w tym przypadku wszystkie wepchane obiekty **Time** zostaną wypchnięte na strumie od razu. I dopiero po tej operacji zostanie uruchomiony normalny cykl zaimplementowany w klasie **TimeCounter**{:.color_2}.

## Zakończenie
**StartWith** może się okazać bardzo przydatnym operatorem, jeżeli będziemy chcieli mieć pewien rodzaj kontroli nad tym co ma znaleźć się na początku strumienia. W przeciwnym przypadku nie wiedzę zbyt przydatnego zastosowania. 
Jednak warto wiedzieć, że można taką manipulację wykonać. 
Jak zawsze zapraszam na **[GitHub]******.
Do zaczytaczyska :).


{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Repeat][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Ambiguous][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-repeat
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-ambiguous

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-start-with/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-start-with/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-start-with/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-start-with/image1-big.jpg