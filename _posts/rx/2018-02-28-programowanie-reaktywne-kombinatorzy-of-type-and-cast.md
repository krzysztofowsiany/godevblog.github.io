---
title: Programowanie Reaktywne - Transformers - OfType and Cast.
date: 2018-02-28
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-transformers-of-type-and-cast
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/transformers-of-type-and-cast/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/transformers-of-type-and-cast/post-big.jpg
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
  - OfType
  - Cast
short: Jeżeli lubisz sobie porzucać przedmiotami? Albo pobawić się w magika zamieniając chusteczki w gołębie? Ten post jest zdecydowanie dla Ciebie. Jak i w naszym społeczeństwie, tak samo na Cybertron-ie, czasem trzeba czymś cisnąć by wszyscy zrozumieli ideę...
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - OfType][post]][post-big]{:.post-left-image}
Jeżeli lubisz sobie porzucać przedmiotami? Albo pobawić się w magika zamieniając chusteczki w gołębie? Ten post jest zdecydowanie dla Ciebie. Jak i w naszym społeczeństwie, tak samo na Cybertron-ie, czasem trzeba czymś cisnąć by wszyscy zrozumieli ideę...

## OfType i Cast
Biblioteka **Rx-owa** zrodziła w sobie dwa operatory ciskające głazami. 
Niestety nie każdy głaz może zostać rzucony. Musi on być odpowiedniego typu: **object**{:.color_1}.
Jeżeli ten jeden warunek zostanie spełniony to wówczas można rzucić delikwenta.

Na samym początku troche biurokracji, trzeba przygotować bazę wypadową. Tym zajmuje się kod poniżej.

{% highlight csharp linenos %}
static void Main(string[] args)
{
  var subscribents = new List<IDisposable>();

  AddGeneratedStream(subscribents);

  ManualStream(subscribents);
{% endhighlight %}

[![Reactive Extensions - Cast][image1]][image1-big]{:.post-right-image}
Do zobrazowania wykorzystania rzucania, przygotowałem dwa przykłady. Jeden to także coś nowego: **Subject**{:.color_1}.
Z tą klasą możemy zbudować prymitywny manualnie sterowany strumień. Dodatkowo należy wskazać jaki typ będzie znajdował się w strumieniu. 
Następnie korzystamy już ze znanych metod do sterowania: 
* **OnNext**{:.color_2} - wprowadzanie na strumień nowych danych,
* **OnCompleted**{:.color_2} - poinformowaniu o końcu strumienia.,

Do dyspozycji mamy dwóch miotaczy:
* **OfType**{:.color_1} - bardziej doświadczony miotacz, zanim czymś rzuci to sprawdzi czy to czym rzuca jest odpowiedniego typu,
* **Cast**{:.color_1} - nie patrzy łapie i rzuca, jest niebezpieczny czasem może przeforsować się i walnąć wyjątkiem (jak w przykładzie **;)**{:.color_1}).

{% highlight csharp linenos %}
private static void ManualStream(ICollection<IDisposable> subscribents)
{
  var manualStream = new Subject<object>();

  subscribents.Add(manualStream
    .OfType<byte>()
    .DefaultPrint("OfType"));

  subscribents.Add(manualStream
    .Cast<byte>()
    .DefaultPrint("Cast"));

  for (byte i = 0; i < 127; i++)
  {
    manualStream.OnNext(i);
  }

  manualStream.OnNext("4");
  manualStream.OnNext("5");

  manualStream.OnCompleted();
{% endhighlight %}

Powyższy manualnie sterowany przykład, przedstawia użycie miotaczy. Wszystko będzie działać prawidłowo do momentu gdy na strumień wprowadzimy ciąg znaków ("4", "5"). Wówczas **OnType**{:.color_1} przejdzie bez problemu. Natomiast **Cast**{:.color_1} będzie chciał użyć nieodpowiedniego typu i wypluje wyjątek.

Drugi przykład korzysta z **Generator-a**{:.color_1}, jednak jak wcześniej wspomniałem bazą rzutu jest typ **object**{:.color_1}. Dlatego w celach doświadczalnych wykonałem przed rzutowanie z wykorzystaniem **Select**{:.color_2}.

Dzięki takiemu zabiegowi otrzymujemy strumień zawierający typ **object**{:.color_1}.
I tak właśnie możemy już wykorzystać miotaczy...

{% highlight csharp linenos %}
private static void AddGeneratedStream(ICollection<IDisposable> subscribents)
{
  var observableStream = GeneratorFactory.CreateGenerator(100, 200, 1, 50)
    .Select(item => (object) item);

  subscribents.Add(observableStream
    .OfType<int>()
    .DefaultPrint("OfType"));

  subscribents.Add(observableStream
    .Cast<int>()
    .DefaultPrint("Cast"));
{% endhighlight %}

## Zakończenie
Jeżeli ktoś chce się pobawić w łapanie rzuconych piłeczek, to zapraszam do zabawy. W przeciwnym wypadku warto zrobić unik;).

Nie mniej jednak czasem rzucić trzeba by wyładować stres.
Kończąc na dzisiaj, zapraszam do jutra na kolejny post.

**Kod z Wami!.**{:.h-3}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Transformers - Select][previous]**

<!--Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-transformers-select
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat

[post]: /assets/images/2018/02/programowanie-reaktywne/transformers-of-type-and-cast/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/transformers-of-type-and-cast/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/transformers-of-type-and-cast/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/transformers-of-type-and-cast/image1-big.jpg