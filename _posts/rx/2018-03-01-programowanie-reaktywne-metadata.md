---
title: Programowanie Reaktywne - Transformers - Metadata.
date: 2018-03-01
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-transformers-metadata
published: true
comments: true        
image: /assets/images/2018/03/programowanie-reaktywne/transformers-metadata/post.jpg
image_big: /assets/images/2018/03/programowanie-reaktywne/transformers-metadata/post-big.jpg
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
  - Materialize
  - Dematerialize
short: Dzisiejszym bohaterem zostaje ostatnia para Transformers-ów. Są oni ze sobą ściśle powiązani. Można śmiało powiedzieć, żę występują między nimi relacje rodzinne. Rodzic i dziecko. Zapraszam do dalszego czytania w celu zgłębienia tajemnic rodzinnych;).
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Materialize][post]][post-big]{:.post-right-image}
Dzisiejszym bohaterem zostaje ostatnia para Transformers-ów. 
Są oni ze sobą ściśle powiązani. Można śmiało powiedzieć, żę występują między nimi relacje rodzinne. Rodzic i dziecko.
Zapraszam do dalszego czytania w celu zgłębienia tajemnic rodzinnych;).

## Materialize i Dematerialize
Przygotowałem trzy przykłady. Na początek przygotujemy strumienie, i przekażemy je do metod zawierających mięsko.

{% highlight csharp linenos %}
var subscribents = new List<IDisposable>();
var observableProvider = new ObservableProvider();
var observableStream = GeneratorFactory.CreateGenerator(0, 5, 1, 300);

Console.WriteLine("Press any keys (Enter to end stream).");

MetadataCreateGenerator(subscribents, observableStream);
MetadataManual(subscribents);
MetadataConsoleKey(subscribents, observableProvider);
{% endhighlight %}

[![Reactive Extensions - Dematerialize][image1]][image1-big]{:.post-left-image}
W każdym z poniższych przykładów został użyty operator rodzica: **Materialize**{:.color_1}. A dlaczego nazwałem go rodzicem? 
Tak samo jak dziecko musi mieć swojego rodzica podobnie jest z drugą metodą **Dematerialize**{:.color_1}.

Podsumowując by użyć **Dematerialize**{:.color_1} należy najpierw skorzystać z **Materialize**{:.color_1}.

Powyższe metody wyświetlają dane w formie **metadanych**{:.color_1}. Czyli ukazują w przypadku **Materialize**{:.color_1} metodę jaka jest wywoływana oraz dane jakie zawiera. Oczywiście to jakie dane są wyświetlane zależy od strumienia. Jeżeli na strumień wrzucane są np. klasy. To wówczas nie otrzymamy jedynie nazwę klasy.

Druga metoda **Dematerialize**{:.color_1} sięga głębiej i wyświetla jedynie parametry przekazane do metod: **OnNext**, **OnError**, **OnCompleted**.

Poniższy przykład dotyczy wykorzystania prezentacji w kontekście strumienia **ConsoleKey**{:.color_2}.
{% highlight csharp linenos %}
private static void MetadataConsoleKey(ICollection<IDisposable> subscribents, ObservableProvider observableProvider)
{
  subscribents.Add(
    observableProvider.ConsoleKey
      .Materialize()
      .DefaultPrint("MaterializeConsoleKey"));

  subscribents.Add(observableProvider.ConsoleKey
    .Materialize()
    .Dematerialize()
    .DefaultPrint("DematerializeConsoleKey"));

  subscribents.Add(observableProvider.ConsoleKey
    .Select(x => x.Key)
    .DefaultPrint("ConsoleKey"));
{% endhighlight %}

Po wduszeniu klawisza na klawiaturze, wyświetli się dwie formy metadanych oraz faktyczny klawisz jaki został wduszony.

Drugi przykład jest prostszy i bazuje na strumieniu pochodzącym z Generatora. 
W tym przypadku podobnie wyświetlone zostaną dane oraz metadane.
{% highlight csharp linenos %}
private static void MetadataCreateGenerator(ICollection<IDisposable> subscribents,IObservable<int> observableStream)
{
  subscribents.Add(observableStream.Materialize()
    .DefaultPrint("MaterializeCreateGenerator"));

  subscribents.Add(observableStream
    .Materialize()
    .Dematerialize()
    .DefaultPrint("DematerializeCreateGenerator"));
{% endhighlight %}

Ostatni z przykładów jaki przygotowałem dotyczy manualnie generowanego strumienia. 
I tutaj możemy zaobserwować jak zostanie potraktowany wyjątek i wywołanie **OnError**{:.color_2}.

{% highlight csharp linenos %}
private static void MetadataManual(ICollection<IDisposable> subscribents)
{
  var source = new Subject<string>();

  source.Materialize()
    .DefaultPrint("MaterializeManual");

  source.Materialize()
    .Dematerialize()
    .DefaultPrint("DematerializeManual");

  source.OnNext("Tekst 1");
  source.OnNext("Tekst 2");

  source.OnError(new Exception("Wyjątek"));
  source.OnCompleted();
{% endhighlight %}

W powyższym przykładzie wykorzystane zostały wszystkie metody jakie zostały zaimplementowane z interfejsu: **IObserver**{:.color_1}.

## Zakończenie
Powyższe operatory mogą być bardzo przydatne do analizy problemów. Można zalogować jakie typy danych zostały wtłoczone na strumień. 
W innym kontekście nie widzę zastosowania: **Materialize**{:.color_1}, **Dematerialize**{:.color_1}.

Dziękuję za czytactwo i zapraszam do śledzenia moich blogowych poczynań...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Transformers - OfType and Cast][previous]**

Następny: **[Programowanie Reaktywne - Bileciki do kontroli - Unit Tests of Interval][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-transformers-of-type-and-cast
[next]: {{site.url}}/programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-interval

[post]: /assets/images/2018/03/programowanie-reaktywne/transformers-metadata/post.jpg
[post-big]: /assets/images/2018/03/programowanie-reaktywne/transformers-metadata/post-big.jpg

[image1]: /assets/images/2018/03/programowanie-reaktywne/transformers-metadata/image1.jpg
[image1-big]: /assets/images/2018/03/programowanie-reaktywne/transformers-metadata/image1-big.jpg