---
title: Programowanie Reaktywne - Kombinatorzy - Merge.
date: 2018-02-22
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-merge
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-merge/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-merge/post-big.jpg
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
  - Merge
short: To już dwudziesty raz się spotykamy odnośnie Rx-owatych. Tydzień pomału dobiega końca. Taki i zbliżamy się do zakończenia serii postów dotyczących kombinatorów. Okazuje się, że rozpisałem się bardzo w tej podgrupie. W najgorszym wypadku nie zakończę na 30 postach :).
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Merge][post]][post-big]{:.post-right-image}
To już dwudziesty raz się spotykamy odnośnie **Rx-owatych**{:.color_2}. Tydzień pomału dobiega końca. Taki i zbliżamy się do zakończenia serii postów dotyczących kombinatorów. Okazuje się, że rozpisałem się bardzo w tej podgrupie. W najgorszym wypadku nie zakończę na 30 postach :).

## Observable.Merge
Jakże dobrze znany ten termin jest programistom. Zapewne wiele razy spotkaliśmy podczas pracy z **GIT-em**{:.color_2}. Tutaj jednak nie będziemy konfliktować.
Operator **Observable.Merge**{:.color_1} przeznaczony jest do łączenia wielu strumieni. Połączeni razem dystrybutorzy tworzą nowy twór (jak w Power Rangers).

**Tego samego typu strumienie musisz mieć. Inaczej ciemna strona Mocy odrodzi się.**{:.h-1}

Użyłem tutaj małego triku w celu wykorzystania innego typu strumienia do **Observable.Merge**{:.color_1}. Przy pomocy małego selekta i rzutowania uzyskałem strumień taki sam jak generowane przez **GeneratorFactory.CreateGenerator**{:.color_2}.

{% highlight csharp linenos %}
var observableProvider = new ObservableProvider();
  var observableGenerator1 = GeneratorFactory.CreateGenerator(0, 100, 1, 100);
  var observableGenerator2 = GeneratorFactory.CreateGenerator(1000, 2000, 2, 600);
  var observableGenerator3 = GeneratorFactory.CreateGenerator(10000, 15000, 51, 1000);

  Console.WriteLine("Press any keys, enter to end ConsoleKey stream.");

  var observableMerge1 = Observable.Merge(
    observableProvider.ConsoleKey.Select(x => (int)x.Key),
    observableGenerator1,
    observableGenerator2,
    observableGenerator3
    );
{% endhighlight %}

Złączone w ten sposób strumienie, tworzą jeden. Do niego wystarczy się już tylko zapisać i czerpać dane ze źródełka.
{% highlight csharp linenos %}
var consoleKeySubscribent = observableProvider.ConsoleKey.Subscribe(
  key =>
  {
    if (key.Key != ConsoleKey.Enter)
    {
      return;
    }

    observableProvider.ConsoleKey.Stop();

    Console.WriteLine("Press any key to stop program.");
  });

var subscribent1 = observableMerge1.Subscribe(
  item =>
  {
    Console.WriteLine($"Merge1: {item}");
  },
{% endhighlight %}

[![Reactive Extensions - Merge][image1]][image1-big]{:.post-left-image}

Dodatkowo oczywiście, zapis na strumień klawiszy pochodzący z konsoli spowoduje nam możliwość jego przerwania przy pomocy **Stop()**{:.color_2}.

Oczywiście wiele dróg prowadzi do rozwiązania problemu, zwłaszcza jak mamy takie elastyczne możliwości składania kodu jak w **Rx-ach**{:.color_2}.
Podobny efekt uzyskamy wykorzystują poniższy przykład.

{% highlight csharp linenos %}
var observableMerge2 = GeneratorFactory.CreateGenerator(-1000, 0, 1, 10);
    observableMerge2
      .Merge(observableGenerator1)
      .Merge(observableGenerator2)
      .Merge(observableGenerator3);

    var subscribent2 = observableMerge2.Subscribe(
      item =>
      {
        Console.WriteLine($"Merge2: {item}");
      },
      exception => Console.WriteLine(exception));
{% endhighlight %}

Zapewne ten zapis jest bardziej seksy. 

## Zakończenie
**Observable.Merge**{:.color_1} jest jak bar. Gdzie wiele strumieni spotyka się wieloma odbiorcami. Konsumenci i producenci razem w jednym miejscu. Łączy ich jeden główny powód **"%"**.

Kończę by sobie już wstydu oszczędzić. 

**Kod z Wami!.**{:.h-3}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Ambiguous][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Zip][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-ambiguous
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-zip

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-merge/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-merge/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-merge/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-merge/image1-big.jpg