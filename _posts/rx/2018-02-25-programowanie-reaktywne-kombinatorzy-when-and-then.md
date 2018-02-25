---
title: Programowanie Reaktywne - Kombinatorzy - When-And-Then.
date: 2018-02-24
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-when-and-then
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-when-and-then/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-when-and-then/post-big.jpg
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
  - When-And-Then
short: Nie tak dawno przedstawiałem zamek błyskawiczny (Zip). Istnieje jeszcze jedna możliwość pozwalająca na łączenie znacznie więcej w jedną całość. Tak by publikacja danych na połączony strumień odbywała się dopiero gdy dostaniemy wszystkie próbki z źródłowych strumieni.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - When-And-Then][post]][post-big]{:.post-left-image}
Nie tak dawno przedstawiałem zamek błyskawiczny (**Zip**{:.color_2}). Istnieje jeszcze jedna możliwość pozwalająca na łączenie znacznie więcej w jedną całość. Tak by publikacja danych na połączony strumień odbywała się dopiero gdy dostaniemy wszystkie próbki z źródłowych strumieni.

## Observable.When-And-Then
Do zbudowanie plecionki z dowolnej ilości strumieni (minimum jednego), wykorzystujemy operator **Observable.When**{:.color_1}. Nie występuje on sam jest tutaj dodatkowo dwa dodatkowe pod operatory:
* **And**{:.color_1} - służy do dołączania kolejnych strumieni poprzez dopisanie **.Add(strumień)**{:.color_1},
* **Then**{:.color_1} - ostatnia operacja łączy wyniki w klasę. Zbiera wszystkie porcje danych od strumieni i publikuje wynik.  

Z tych elementów możemy tworzyć plecionkę...

Poniższy fragment to przygotowanie kilu dystrybutorów, do testu. Jest tutaj nowa metoda rozszerzająca **BreakWhenKey**{:.color_1} opisana nieco niżej.
{% highlight csharp linenos %}
var observableStream1 = GeneratorFactory.CreateGenerator(0, 100, 1, 100);
var observableStream2 = GeneratorFactory.CreateGenerator(0, 100, 1, 60);
var observableStream3 = GeneratorFactory.CreateGenerator(0, 100, 1, 120);
var observableProvider = new ObservableProvider();

observableProvider.ConsoleKey.BreakWhenKey(ConsoleKey.Enter);
{% endhighlight %}

Po przygotowaniu strumieni bazowych należy je ze sobą spleść. Przykład poniżej przedstawia powiązanie strumieni różnego typu.
Dwa dystrybutory pochodzą z **ObservableProvider**{:.color_2}.
Dzięki użyciu **ConsoleKey**{:.color_2} mamy możliwość częściowego kontrolowania kiedy **Then**{:.color_1} wykona dystrybucję nowych danych.
Drugim warunkiem jest **TimeCounter**{:.color_2} ale to tylko dlatego, że dostarcza danych co **1s**{:.color_1}. 
{% highlight csharp linenos %}
var whenAndThenSequence = Observable.When(observableStream1
  .And(observableStream2)
  .And(observableStream3)
  .And(observableProvider.ConsoleKey)
  .And(observableProvider.TimeCounter)
  .Then((first, second, third, consoleKey, time) =>
      new {
        One = first,
        Two = second,
        Three = third,
        Key = consoleKey.Key,
        Time = time
      })
);
{% endhighlight %}

[![Reactive Extensions - When-And-Then][image1]][image1-big]{:.post-right-image}

Wychodząc od pierwszego strumienia **observableStream1**{:.color_1} dodajemy kolejne (ile chcemy). Korzystając z operatora **Add(strumyk)**{:.color_1}
Ostatnim etapem jest użycie **Then**{:.color_1} i tutaj należy pamiętać. Tyle ile strumieni dodamy tyle trzeba przygotować parametrów w lambdzie. A sama budowa obiektu już zależy od nas jak będzie wyglądał.

Ostatni fragment kodu, dotyczy nowej metody, która rozszerza strumyk **ObservableConsoleKey**{:.color_2}.
**BreakWhenKey**{:.color_1} po prostu zapisuje się do dystrybutora i dodaje warunek zakończenia publikacji wciśniętych klawiszów gdy wciśniemy określony przez **exitKey**{:.color_1} klawisz.
{% highlight csharp linenos %}
public static class HelpingExtensions
{
  public static IDisposable BreakWhenKey(this ObservableConsoleKey source, System.ConsoleKey exitKey)
  {
    var subscription = source
      .Subscribe(key =>
      {
        if (key.Key != exitKey)
        {
          return;
        }

        source.Stop();
{% endhighlight %}

## Zakończenie
Plecionka jaką zbudujemy przy wykorzystaniu powyższych operatorów, może być przydatna gdy chcemy złączyć wiele strumieni i uzyskiwać jeden. 

Może mieć też zastosowanie nieco inne, po splocie może się przydać gdy kolejny raz już przyjdzie się "powiesić" na wskutek walki ze środowiskami ;)....

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Switch][previous]**

<!--Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-switch
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-when-and-then/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-when-and-then/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-when-and-then/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-when-and-then/image1-big.jpg