---
title: Programowanie Reaktywne - Kombinatorzy - Repeat.
date: 2018-02-19
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-repeat
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-repeat/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-repeat/post-big.jpg
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
  - Repeat
short: Dzisiaj ponownie poruszymy temat kombinowania na strumieniach. Tym razem posłużymy się operatorem Repeat. Jak sama nazwa wskazuję będziemy się powtarzać :). Operatory są dość proste co nie znaczy, że nie są potężnym narzędziem w całej rodzinie Rx-ów. 
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Repeat][image1]][image1-big]{:.post-right-image}
Dzisiaj ponownie poruszymy temat kombinowania na strumieniach. Tym razem posłużymy się rozszeżeniem **Repeat**{:.color_1}. Jak sama nazwa wskazuję będziemy się powtarzać :).
Operatory są dość proste co nie znaczy, że nie są potężnym narzędziem w całej rodzinie **Rx-ów**{:.color_1}. 

## Repeat
Przy pomocy tego rozszerzenia możemy zaoszczędzić nieco czasu przy kodowaniu. W odniesieniu do poprzedniego posta na temat **Concat** i wykorzystania pętli do wygenerowania połączonej sekwencji strumieni. Dzisiaj wystarczyło wykorzystać powtarzacz z parametrem: **Repeat(ile razy powtórzyć)**{:.color_1}.

Dodatkowo dzisiejsze przykłady są uboższe w ilość kodu, dzięki zniwelowaniu wykorzystania zmiennej przechowującej sekwencję strumieni.
{% highlight csharp linenos %}
var twoSecondsTimeSpan = TimeSpan.FromSeconds(2);
var fiveSecondsTimeSpan = TimeSpan.FromSeconds(2);

var observableSequenceTenTimes =
  Observable.Range(1, 5)
  .Delay(fiveSecondsTimeSpan)
  .Repeat(10)
  .Subscribe(item =>
    {
      Console.WriteLine($"Only ten times: {item}");
    },
    exception => Console.WriteLine(exception));
{% endhighlight %}

[![Reactive Extensions - Repeat][post]][post-big]{:.post-left-image}

Dodatkowo posłużyłem się operatorem **Delay**{:.color_2} jak już wiadomo z postów dotyczących timer-owatych.
Efektem będzie **5**{:.color_2} sekundowe oczekiwanie między poszczególnymi porcjami danych od połączonych strumieni.

Drugi przypadek jest bardziej rozbudowany, i zawiera w sobie wymyślny (losowy ;)) algorytm sekwencji źródeł danych dla obserwatorów. Między poszczególnymi sekwencjami także wykorzystałem  **Delay**{:.color_2}.

Co tutaj jest takiego wyjątkowego? **Repeat**{:.color_1} bez parametrów, czyli ciągłe powtarzanie zbudowanej sekwencji.
Można  to z powodzeniem wykorzystać przy sterowaniu lampkami na choince w Boże Narodzenie przy pomocy **PC** ;).
{% highlight csharp linenos %}
var observableSequenceContinually =
  Observable.Range(1, 5)
  .Delay(twoSecondsTimeSpan)
  .Concat(CreateGenerator(100, 200, 10, 500))
  .Delay(twoSecondsTimeSpan)
  .Concat(Observable.Range(100, 5))
  .Delay(twoSecondsTimeSpan)
  .Concat(CreateGenerator(1000000, 2000000, 10000, 100))
  .Delay(fiveSecondsTimeSpan)
  .Repeat()
    .Subscribe(item =>
      {
        Console.WriteLine($"Continually: {item}");
      },
      exception => Console.WriteLine(exception));
{% endhighlight %}

Ten skrócony zapis jest bardzo elegancki.

## Zakończenie
Kończąc na dzisiaj wnioskiem powtarzajmy do skutku aż zapamiętamy co chcieliśmy przyswoić. Żartuję. Jednak powtarzanie zachowuje się nieco inaczej aniżeli np. **Interval**{:.color_2}. Samo w sobie publikuje już konkretny algorytm i w ten sposób możemy dostarczyć do naszego programu pewien szkielet sterowania zachowaniem. 

Dziękuję i zapraszam do dalszego czytania:).

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Concat][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-start-with

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-repeat/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-repeat/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-repeat/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-repeat/image1-big.jpg