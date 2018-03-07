---
title: Programowanie Reaktywne - Marudzimy - Skip.
date: 2018-02-15
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-marudzimy-skip
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/marudzimy-skip/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/marudzimy-skip/post-big.jpg
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
  - TimeInterval  
  - Generate
  - Skip
  - SkipLast
  - SkipWhile
  - SkipUntil
short: Po wczorajszym sowitym poście, dzisiaj trochę przystopujemy. Będzie krócej. Poruszymy tematykę marudzenia ;). Marudzić można na dwa sposoby. Albo że się coś chcę albo nie! Na początek pomarudzimy że czegoś nie chcemy, zapraszam!
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Take][post]][post-big]{:.post-left-image}
Po wczorajszym sowitym poście, dzisiaj trochę przystopujemy. Będzie krócej. Poruszymy tematykę marudzenia ;). Marudzić można na dwa sposoby. Albo że się coś chcę albo nie!

Na początek pomarudzimy że czegoś nie chcemy, zapraszam!

## Skip - tego nie chce tamtego też...
Na samym początku zapewnimy sobie źródłowe strumienie na jakie bęziemy mogli się zapisywać. Skorzystamy w tym przypadku z biblioteki **RXLib**{:.color_2} opisanej w [poprzednim poście][previous]. Drugim źródełkiem będzie prosty **[generator]**.
{% highlight csharp linenos %}
private static void InitializeGenerators()
{
  _observableProvider = new ObservableProvider();

  var initialState = 0;

  _generator = Observable.Generate(
    initialState,
    condition => condition < GenerateItemCount,
    iterate => iterate + 1,
    resultSelector => resultSelector,
    timeSelector => TimeSpan.FromMilliseconds(100)
  );
{% endhighlight %}

Generator bardzo prosty, wypluje co **100ms**{:.color_2} cyferkę zwiększaną o 1, do uzyskania wartości 20.

Ze strumieniem pochodzącym z generatora mamy powiązane dwie marudy. 
Pierwsza maruda nie chce ostatnich dziesięciu publikowanych treści. Do tego celu między strumień (_generator), a zapis(Subscribe) dodajemy żądania marudy (**SkipLast**{:.color_1}). 
Określamy jednocześnie ilu ostatnich publikacji od obiektu obserwowanego nie chcemy.

{% highlight csharp linenos %}
private static void AddSkipLastSubscribent()
{
  _skipLastSubscribent = _generator
    .SkipLast(10)
    .Subscribe(
      item =>
      {
        Console.WriteLine($"SkipeLast 10 items from {GenerateItemCount}: {item}");
{% endhighlight %}

[![Reactive Extensions - Take][image1]][image1-big]{:.post-right-image}

Druga maruda zależna od strumienia wyplutego przez generator, nie będzie nic robić puki ten właśnie strumień nie przestanie swojego rozpowszechniania treści.
**"Zacznę działać, ale najpierw niech tamten skończy"**.

Podobnie jak poprzednio wstrzykujemy marudę (**SkipUntil**{:.color_1}) między strumień, a zapis na strumień. Uwaga zapis wykonujemy na strumień publikujący licznik czasu (z poprzedniego posta).
I przy pomocy **SkipUntil**{:.color_1} określamy jaki inny obiekt publikujący musi przejść w stan **OnCompleted** by ruszył tyłek.

{% highlight csharp linenos %}
private static void AddSkipUntilSubscribent()
{
  _observableProvider.TimeCounter
    .SkipUntil(_generator)
    .Subscribe(
      time =>
      {
        Console.WriteLine($"SkipUntil, ignore: {time}");
{% endhighlight %}

Pozostałe marudy już nie będą zależne od **_generator**{:.color_2}. 

Pierwszy bardzo prosty **Skip**{:.color_1}. Po prostu nie chce tych początkowych elementów. Podając konkretne kryteria liczbowe. Wstrzykujemy jak poprzednio;).
{% highlight csharp linenos %}
private static void AddSkipSubscribent()
{
  _observableProvider.TimeCounter
    .Skip(10)
    .Subscribe(
      time =>
      {
        Console.WriteLine($"Skip (10): {time}");
{% endhighlight %}

Na koniec ten szczególnie wybredny (**SkipWhile**{:.color_1}). Co to kręci nosem na żywca (w czasie rzeczywistym). 
"Zobaczę to zdecyduję, teraz to jeszcze nie wiem".

Przebiera według określonych warunków co skonsumuje co nie. Ten poniżej nic nie będzie robił przez pierwszą minutę.
{% highlight csharp linenos %}
private static void AddSkipWhileSubscribent()
{
  _observableProvider.TimeCounter
    .SkipWhile(x => x.Minutes == 0)
    .Subscribe(
      time =>
      {
        Console.WriteLine($"SkipWhile, ignore first minute: {time}");
{% endhighlight %}

## Zakończenie
Dzisiaj to tyle marudzenia, jutro ponownie przedstawię kolejne marudy. 
Czasem marudzenie jest przydatne. Daje większe możliwości;).

PS: Dzisiaj 13 post, być może pechowy. Kto wie co będzie jutro...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Tworzymy dane - Własna klasa publikująca][previous]**

Następny: **[Programowanie Reaktywne - Marudzimy - Take][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-tworzymy-dane-wlasna-klasa-publikujaca
[next]: {{site.url}}/programowanie-reaktywne-marudzimy-take

[post]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-skip/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-skip/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-skip/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/marudzimy-skip/image1-big.jpg

[generator]: {{site.url}}/programowanie-reaktywne-tworzymy-dane-generators


