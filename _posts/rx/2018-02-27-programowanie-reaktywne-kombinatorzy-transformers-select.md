---
title: Programowanie Reaktywne - Transformers - Select.
date: 2018-02-27
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-transformers-select
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/transformers-select/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/transformers-select/post-big.jpg
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
  - Select
short: Przyszła pora by troszkę się pobawić Transformers-ami. Autoboty - transformacja... Otwieram tym samym mikro cykl transformacji strumieni prosto z Cybertron-u. Pomijając luźne aluzje, przetwarzanie danych pochodzących od dystrybutorów to...
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Select][post]][post-big]{:.post-right-image}
Przyszła pora by troszkę się pobawić Transformers-ami. Autoboty - transformacja...
Otwieram tym samym mikro cykl transformacji strumieni prosto z **Cybertron-u**{:.color_1}. 

Pomijając luźne aluzje, przetwarzanie danych pochodzących od dystrybutorów to powszechna praktyka i poniższy przy przykład choć trywialny może zaprocentować w przyszłości.

## Observable.Select
[![Reactive Extensions - Select][image1]][image1-big]{:.post-left-image}
Najprostszy operatorek (**Select**{:.color_1}), ale jaki potężny. Dzięki niemu możemy manipulować czasoprzestrzenią dystrybuowanych danych.

Na starcie korzystając z **RxLib**{:.color_2} tworzymy prosty strumień, który to następnie nieco zmodyfikujemy.

A jak działa **Select**{:.color_1}? Jak krowa. Bierze do pyska. Mieli, mieli, mieli i jest mleko:)

Dostaje towar, i opakowuje jak mu zagramy.

Z prostej liczby z zakresu od 0 do 255 stworzymy obiekt zawierający samą liczbę oraz ich binarną i heksadecymalną postać.
{% highlight csharp linenos %}
var observableStream = GeneratorFactory.CreateGenerator(0, 255, 1, 50);

var selectSubscribent = observableStream
  .Select(
    item => new
    {
      Number = item,
      Bits = Convert.ToString(item, 2),
      Hex = Convert.ToString(item, 16).ToUpper()
    }
  ).DefaultPrint("Select");
{% endhighlight %}

Na koniec wszystko wyświetlamy i gotowe.
Prosty przykład jak można zrobić coś z pozornie nieznaczącej liczby. Z poczwarki w motyla...

## Zakończenie
Mieliśmy już przyjemność korzystać z transformacji w postach dotyczących: **[Timestamp/TimeInterval]**.

Wówczas opisałem na szybko działanie, ze względu na potrzebę użycia. Pozostało jeszcze kilka **Autobotów**{:.color_1} po wojnie z **Decepticon-ami**{:.color_1}. Zapraszam do śledzenia :).

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Combine Latest][previous]**

Następny: **[Programowanie Reaktywne - Transformers - OfType and Cast][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-combine-latest
[next]: {{site.url}}/programowanie-reaktywne-transformers-of-type-and-cast

[Timestamp/TimeInterval]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-timestamp-and-timeinterval

[post]: /assets/images/2018/02/programowanie-reaktywne/transformers-select/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/transformers-select/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/transformers-select/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/transformers-select/image1-big.jpg