---
title: Programowanie Reaktywne - Kombinatorzy - Combine Latest.
date: 2018-02-26
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-combine-latest
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-combine-latest/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-combine-latest/post-big.jpg
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
  - Combine Latest
short: Dziwny ten kombinator, jak już zostanie odblokowany przez otrzymanie przynajmniej po jednej porcji danych od głównych źródełek. To wówczas już publikuje w raz z taktem najszybszego dystrybutora.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Combine Latest][post]][post-big]{:.post-right-image}
Tak to już koniec tej mini serii o kombinatorach. Wyszło dziewięć postów. Całkiem sporo. 

Wszystkie kody oczywiście znajdują się na **[GitHub-ie]**. Myślę, że w ten sposób łatwiej będzie zrozumieć działanie **Rx-ów**{:.color_2}. Uruchomić i analizować co tam się ciekawego dzieje. A jeszcze lepiej poeksperymentować.

## Observable.CombineLatest
Dziwny ten kombinator, jak już zostanie odblokowany przez otrzymanie przynajmniej po jednej porcji danych od głównych źródełek. To wówczas już publikuje w raz z taktem najszybszego dystrybutora.
Jak nie ma od innych danych. To powiela ostatnią porcyjkę.

[![Reactive Extensions - Combine Latest][image1]][image1-big]{:.post-left-image}

Bazując na przykładzie dotyczącym **[When-And-Then][previous]** powstał poniższy kodzik.
Dzięki użyciu strumienia **ConsoleKey**{:.color_1} nic się ciekawego nie dzieje puki nie wciśniemy różnego od **Enter** klawisza na klawiaturze.

Wduszenie spowoduje odblokowanie i popłynie strumień danych.

Łącznikiem wszystkich nadrzędnych źródełek jest tutaj **CombineLatest**{:.color_1}. 
Można mu podać wiele strumieni w parametrach. 
Jednak trzeba pamiętać, że ilość parametrów powinna być odzwierciedlona w takiej samej ilości także parametrów w lambdzie znajdującej się na końcu użycia **CombineLatest**{:.color_1}.
{% highlight csharp linenos %}
var observableStream1 = GeneratorFactory.CreateGenerator(0, 100, 1, 500);
var observableStream2 = GeneratorFactory.CreateGenerator(1000, 1100, 1, 2000);
var observableStream3 = GeneratorFactory.CreateGenerator(10000, 11000, 1, 250);
var observableProvider = new ObservableProvider();

observableProvider.ConsoleKey.BreakWhenKey(ConsoleKey.Enter);

var combineLatestStream = observableStream1.CombineLatest(
  observableStream2,
  observableStream3,
  observableProvider.ConsoleKey,
  (a, b, c, d) => new
  {
    A = a,
    B = b,
    C = c,
    D = d.Key
  });

var combineLatestSubscribent = combineLatestStream.DefaultPrint("CombineLatest");
{% endhighlight %}

Wykorzystujemy dane od wszystkich strumieni i tworzymy nowy obiekt. 

Znaczy to tyle, że raz odblokowany strumień, płynie już nieustannie powielając mniej aktualne dane. 

Wszyscy maszerują razem...

## Zakończenie
Kończąc przygodę z kombinowaniem zastanawiam się jaką tematykę podjąć dalej. Jeszcze wcale nie było słowa na temat przechwytywania zdarzeń. Zastępując tym samym użycie **+/-=**{:.color_1} **new**{:.color_2} **EventHandler...**{:.color_1}. 

Ale o tym głębiej będę się zastanawiał jutro.
Dzisiaj dziękuję za poświęcony czas.

**Kod z Wami!**{:.color_1}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - When-And-Then][previous]**

Następny: **[Programowanie Reaktywne - Transformers - Select][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-when-and-then
[next]: {{site.url}}/programowanie-reaktywne-transformers-select

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-combine-latest/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-combine-latest/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-combine-latest/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-combine-latest/image1-big.jpg