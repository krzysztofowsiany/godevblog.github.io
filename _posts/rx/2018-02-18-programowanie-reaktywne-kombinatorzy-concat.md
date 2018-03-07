---
title: Programowanie Reaktywne - Kombinatorzy - Concat.
date: 2018-02-18
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-concat
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-concat/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-concat/post-big.jpg
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
  - Concat
short: Dzisiejszy post, tak jak i kilka następnych będzie dotyczył kombinowania. Będziemy korzystać z wielu strumieni publikujących dane tego samego typu do łączenia ich w jedną całość. I dopiero wówczas będzie można...
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Concat][image1]][image1-big]{:.post-right-image}
Dzisiejszy post, tak jak i kilka następnych będzie dotyczył kombinowania. Będziemy korzystać z wielu strumieni publikujących dane tego samego typu do łączenia ich w jedną całość. I dopiero wówczas będzie można się zapisać do tak stworzonego dystrybutora.

## Concat
Na początek bardzo prosty operator, pozwalający na łączyć wiele strumieni w jeden. Działa podobnie jak kolejka **FIFO - First Input First Output**{:.color_1}.

W tym celu stworzyłem prostą metodę pozwalającą na generowanie nowych obiektów do obserwowania w oparciu o **Observable.Generate**{:.color_2}. Będzie nam to potrzebne do łączenia w jeden sekwencyjny strumień.

Jako parametry metody podajemy składowe wymagane do wygenerowania danych przy pomocy **Observable.Generate**{:.color_2}.
{% highlight csharp linenos %}
private static IObservable<int> CreateGenerator(int initialState, int conditionValue, int incrementValue, int periodValue)
{
  var period = TimeSpan.FromMilliseconds(periodValue);

  var generator = Observable.Generate(
    initialState,
    condition => condition <= conditionValue,
    iterate => iterate + incrementValue,
    resultSelector => resultSelector,
    timeSelector => period
  );
{% endhighlight %}

[![Reactive Extensions - Concat][post]][post-big]{:.post-left-image}
Dodatkowo by trochę zróżnicować to so się dzieje, skorzystamy także z prostego operatora **Observable.Range**{:.color_2}.

Posłużyłem się także pętlą, tak by pokazać, że można łączyć wielokrotnie wielu dystrybutorów. Poniższy kod generuje 21 sekwencyjnie ze sobą połączonych strumieni. Ostatecznie wykonujemy zapis na tak stworzony miks.

Publikowanie danych przez strumienie odbędzie się z zachowaniem specyfiki danego dostawcy: 
* **Observable.Range**{:.color_1} - będzie to szło jeden po drugim bez zamierzonego opóźnienia,
* **Observable.Generate**{:.color_1} - w tym przypadku będzie to zależne od **timeSelector-a**{:.color_2), cykl publikowania pójdzie zgodnie z wartością **TimeSpan**.

{% highlight csharp linenos %}
var observableSequence = Observable.Range(0, 5);

for (var i = 0; i < 10; i++)
{
  observableSequence = observableSequence.Concat(CreateGenerator(0, i * 10, 2, 500));
  observableSequence = observableSequence.Concat(Observable.Range(0, 5));
}

observableSequence.Subscribe(Console.WriteLine);
{% endhighlight %}

## Zakończenie
To już kolejny operator jaki przedstawiam. Jest bardzo dużo. Pozwalają na bardzo wiele manipulacji związanych ze strumieniami. Mam nadzieję, że znajdzie się dla nich zastosowanie w twoim kodowaniu. Dzięki za czytanie i zapraszam do kolejnych postów.

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Łap To - ConsoleKey][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Repeat][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-repeat

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-concat/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-concat/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-concat/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-concat/image1-big.jpg