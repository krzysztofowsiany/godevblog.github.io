---
title: Programowanie Reaktywne - Marudzimy - Take.
date: 2018-02-16
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-marudzimy-take
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/marudzimy-take/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/marudzimy-take/post-big.jpg
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
  - TimeInterval  
  - Generate
  - Take
  - TakeLast
  - TakeWhile
  - TakeUntil
short: Krakałem, krakałem o pechu i wykrakałem. Miało być tak szybko z drugim marudą, a tu się pojawiły problemy jakich wcześniej nie przewidziałem. Otóż drugi maruda działa na innej zasadzie. Marudzi ale przy braniu. I tutaj pojawił się problem. Bierzemy pierwsze kilka publikacji na strumień.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Skip][image1]][image1-big]{:.post-left-image}
Krakałem, krakałem o pechu i wykrakałem. Miało być tak szybko z drugim marudą, a tu się pojawiły problemy jakich wcześniej nie przewidziałem.
Otóż drugi maruda działa na innej zasadzie. Marudzi ale przy braniu. I tutaj pojawił się problem. Bierzemy pierwsze kilka publikacji na strumień. I kasował swoją subskrypcję, co ciekawe w momencie wyzwalania przez publikację metody **OnNext**{:.color_2}, tym samym dochodziło do jednoczesnego dostępu do tej samej kolekcji przez **ForEach**{:.color_2} i **Dispose**{:.color_2}.
Po nierównej walce, obrałem obejście problemu i skorzystałem jedynie ze strumieni generowanych przez **Observable.Generator**{:.color_1}:).

## Take - chcę tylko to i to, tamtego już nie...
Tworzymy dwa bardzo podobne do siebie [generatory]. Po co jest potrzebny ten drugi dowiemy się trochę niżej.
Będą one produkować dane co **100ms**{:.color_2} i **400ms**{:.color_2}. Kto się zapisze to dostanie;)
{% highlight csharp linenos %}
private static void InitializeGenerators()
{
  var initialState = 0;

  _generator1 = Observable.Generate(
    initialState,
    condition => condition < GenerateItemCount,
    iterate => iterate + 1,
    resultSelector => resultSelector,
    timeSelector => TimeSpan.FromMilliseconds(100)
  );

  _generator2 = Observable.Generate(
    initialState,
    condition => condition < GenerateItemCount,
    iterate => iterate + 1,
    resultSelector => resultSelector,
    timeSelector => TimeSpan.FromMilliseconds(400)
  );
{% endhighlight %}

I o to nasz pierwszy maruda (**TakeLast**{:.color_1}), dla niego liczy się tylko ten **X**{:.color_1} ostatnich publikowanych na strumień danych. Można by żec, ignorant:). Czeka, czeka, aż pojawi się to co che. Zgarnie swoją wybredną pulę danych.
{% highlight csharp linenos %}
private static void AddTakeLastSubscribent()
{
  _generator1
    .TakeLast(10)
    .Subscribe(
      item =>
      {
        Console.WriteLine($"TakeLast 10 items from {GenerateItemCount}: {item}");
{% endhighlight %}

[![Reactive Extensions - Skip][post]][post-big]{:.post-right-image}

**TakeWhile**{:.color_1} ten ma swoje zasady. Jak strumień ich nie spełnia to nie chce danych. Jest bardzo wybredny.
Oczywiście marudy należy wpiąć między strumień a subskrypcję. Jak bardzo wybredny to zależy od nas. Należy pamiętać jednak, że jeżeli choć raz coś mu nie spasuje to się i dan nogę!
{% highlight csharp linenos %}
private static void AddTakeWhileSubscribent()
{
  _generator1
    .TakeWhile(x => x < 5)
    .Subscribe(
      item =>
      {
        Console.WriteLine($"TakeWhile, show only some first generated data: {item}");
{% endhighlight %}

Szybki Bill (**Take**{:.color_1}), od razu zgarnia dane od dystrybutorów. Jednak wybiera tylko pierwsze sztuki. To wredna bestia jak dostanie co chce, wypisze z subskrypcji **8}**{:.color_1} i tyle go widzieli...
{% highlight csharp linenos %}
private static void AddTakeSubscribent()
{
  _generator1
    .Take(10)
    .Subscribe(
      item =>
      {
        Console.WriteLine($"Take (10): {item}");
{% endhighlight %}

Na koniec ostatni i to tutaj właśnie potrzebny jest ten drugi generator (**_generator2**{:.color_1}).
Odbiera dane puki **_generator1**{:.color_2} publikuje. Jeżeli pierwszy padnie. To wówczas **TakeUntil**{:.color_1} już nie chce. I oczywiście wypisze się z listy subskrybentów.
{% highlight csharp linenos %}
private static void AddTakeUntilSubscribent()
{
  _generator2
    .TakeUntil(_generator1)
    .Subscribe(
      item =>
      {
        Console.WriteLine($"TakeUntil, generator1 publishing: {item}");
{% endhighlight %}

## Zakończenie
Dzisiejszy zestaw operatorów, dość podobny do tych z poprzedniego posta. Jedne ignorują drugie biorą. Lustrzane odbicia.
Trochę napsuły mi dzisiaj krwi. Walczyłem, walczyłem, a potem zmieniłem taktykę i pokonałem problem. Warto czasem zrobić krok do tyłu by zobaczyć problem z innej perspektywy i rozwiązać go podążając inną drogą. :). Done.

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Marudzimy - Skip][previous]**

<!--Następny: **[Programowanie Reaktywne - Zabawa z czasem - Delay.][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-marudzimy-skip
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval

[post]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-take/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-take/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-take/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-take/image1-big.jpg

[generatory]: {{site.url}}/programowanie-reaktywne-tworzymy-dane-generators


