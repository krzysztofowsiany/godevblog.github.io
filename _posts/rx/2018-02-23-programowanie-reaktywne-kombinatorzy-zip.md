---
title: Programowanie Reaktywne - Kombinatorzy - Zip.
date: 2018-02-23
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-zip
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-zip/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-zip/post-big.jpg
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
  - Zip
short: To już dwudziesty raz się spotykamy odnośnie Rx-owatych. Tydzień pomału dobiega końca. Taki i zbliżamy się do zakończenia serii postów dotyczących kombinatorów. Okazuje się, że rozpisałem się bardzo w tej podgrupie. W najgorszym wypadku nie zakończę na 30 postach :).
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Zip][post]][post-big]{:.post-right-image}
Kontynuując tematykę kombinatorów. Dzisiaj o pewnym znanym słówku, bardzo popularnym formacie kompresji danych. Nie wiem jakim cudem trafił do **Rx-owej** rodziny. Być morze przytaczam złą aluzję. Ale o tym nieco dalej.

## Observable.Zip
Z angielskiego **Zip**{:.color_1} znaczy tyle co zamek błyskawiczny. I tym porównaniu możemy doszukać się aluzji. Działanie operatora **Observable.Zip**{:.color_1} dokładnie można zrozumieć jako zamykanie zamka. Tym samym łączymy lewą i prawą część. 
Utworzony zostaje nowy strumień (zamknięty zamek).

Jednak na samym początku szarpnąłem się i stworzyłem dwie klasy pomocnicze **PrintExtensions**{:.color_2}, oraz **ConvertingExtensions**{:.color_2}. Śledząc internety natrafiłem na takie **Extension Methods** dzięki którym znacznie łatwiej i czytelniej jest wyświetlać dane w konsoli.

Przy pomocy **DefaultPrint**{:.color_1} możemy w szybki sposób dokonać zapisu na strumień i wyświetlać skutki działania dystrybutora danych.
{% highlight csharp linenos %}
public static IDisposable DefaultPrint<T>(this IObservable<T> source, string identify)
{
  var subscription = source.Subscribe(
    item =>
    {
      Console.WriteLine("{0}\t\titem: {1}", identify, item);
    },
    exception =>
    {
      Console.WriteLine("{0}\t\texception: {1}", identify, exception);
    },
    () =>
    {
      Console.WriteLine("{0}\t\tcompleted", identify);
    });
{% endhighlight %}

Druga klasa natomiast dotyczy konwertowania danych. W tym konkretnym przypadku **ToCharacter**{:.color_1} wykonujemy zamianę danych typu long na ciąg znaków. 
Wykonujemy taką operację przez wyselekcjonowanie i zamianę wykonaną przy pomocy **char.ConvertFromUtf32**{:.color_1}.

{% highlight csharp linenos %}
public static class ConvertingExtensions
{
  public static IObservable<string> ToCharacter(this IObservable<long> source)
  {
    return source.Select(item => char.ConvertFromUtf32((int)item));
{% endhighlight %}

[![Reactive Extensions - Zip][image1]][image1-big]{:.post-left-image}
Przechodząc do meritum dzisiejszego posta, przedstawiam poniżej wycinek kodu zawierający dwa obiekty publikujące cyklicznie dane. Jeden z nich będzie dostarczał dane typu long (observableIntervalForNumbers). Natomiast drugi przy pomocy wspomnianej wcześniej metodzie **ToCharacter**{:.color_2} dostarczał będzie znaki.

W przypadku **Observable.Zip**{:.color_2}, nie musimy się martwić o to, że dane są różnego typu. Nowy strumień będzie dostarczał je w dwóch odpowiednio nazwanych polach (**Index**, **Character**).

{% highlight csharp linenos %}
var observableIntervalForNumbers = Observable.Interval(TimeSpan.FromMilliseconds(10))
  .Take(256);

var observableIntervalForChars = Observable.Interval(TimeSpan.FromMilliseconds(50))
  .Take(256)
  .ToCharacter();

var subscription1 = observableIntervalForNumbers
  .Zip(observableIntervalForChars, (leftItem, rightItem) => new
  {
    Index = leftItem,
    Character = rightItem
  })
  .DefaultPrint("Zip test");
{% endhighlight %}

Na samym końcu korzystając z metody **DefaultPrint**{:.color_1} wyrzucamy interesujące dane znajdujące się w źródełku.
Używanie **Zip**{:.color_2} jest bardzo proste, z głównego strumienia wywołujemy metodę i w parametrach podajemy drugi strumień z jakim będzie zip-owany. Jako drugi parametr podajemy lambdę, której celem będzie utworzenie obiektu z obu łączonych właściwości.

## Zakończenie
Co jest ciekawe publikowanie na zip-owany strumień nastąpi dopiero gdy oba źródłowe strumienie wyślą swoją jednostkę danych.
**Zip**:.color_2} poczeka, aż z obu strumieni dotrą dane.

To tyle w ten piątkowy wieczór. Po przeczytaniu posta mam cichą nadzieję, że od tej pory zamek błyskawiczny będzie miał też bardzie przyzwoite zastosowanie.

**Kod z Wami!**{:.color_1}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Merge][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Switch][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-merge
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-switch

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-zip/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-zip/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-zip/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-zip/image1-big.jpg