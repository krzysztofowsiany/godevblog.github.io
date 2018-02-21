---
title: Programowanie Reaktywne - Kombinatorzy - Ambiguous.
date: 2018-02-21
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-kombinatorzy-ambiguous
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-ambiguous/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-ambiguous/post-big.jpg
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
  - Ambiguous
short: Krótko, bardzo krótko dzisiaj. A wszystko przez nadchodzące devwarsztaty.pl. Będę debiutował. Stres, strach przed oczami... Bla bla bla pora trochę napisać o Rx tak mało ostatnio poruszałem ten temat na tym blogu;) Dzisiaj kolejny operator związany z kombinowaniem. Zapraszam!
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Ambiguous][post]][post-big]{:.post-right-image}
Krótko, bardzo krótko dzisiaj. A wszystko przez nadchodzące **[devwarsztaty.pl]**. Będę debiutował. Stres, strach przed oczami...
Bla bla bla pora trochę napisać o **Rx** tak mało ostatnio poruszałem ten temat na tym blogu;)
Dzisiaj kolejny operator związany z kombinowaniem. Zapraszam!

## Ambiguous
Kto szybszy ten lepszy. Bywa czasem tak że współzawodnictwo jest nam bardzo na rękę. Z innej strony możemy korzystać ze powielonymi strumieniami danych. Wówczas nie wiadomo który wybrać. Jaki obsługiwać a może nie obsługiwać. W tej sytuacji dzisiejszy bohater **Observable.Amb**{:.color_1} jest odpowiedni. Wybiera strumie który najszybciej dostarcza dane, pozostałe pomija.

Ale najpierw mały refaktor, przeniosłem metodę tworzenia generatorów **CreateGenerator**{:.color_2} do do fabryczki.
{% highlight csharp linenos %}
namespace RXLib.Factories
{
	public static class GeneratorFactory
	{
		public static IObservable<int> CreateGenerator(int initialState, int conditionValue, int incrementValue, int periodValue)
		{
			var period = TimeSpan.FromMilliseconds(periodValue);

			var generator = Observable.Generate(
				initialState,
				condition => condition <= conditionValue,
				iterate => iterate + incrementValue,
				resultSelector => resultSelector,
				timeSelector => period
			);
{% endhighlight %}

[![Reactive Extensions - Ambiguous][image1]][image1-big]{:.post-left-image}
Samo użycie **Observable.Amb**{:.color_1} jest banalnie proste, podajemy po prostu listę strumieni jako parametry.
Metody **Amb** i gotowe. Po zapisie na nowego dostawcę treści. Możemy wypisać cóż tam się na nim znajduje.
Publikowane treści oczywiście powinny być tego samego typu.

-**Bo inaczej jak u diabła mam wybrać z pośród wszystkich dostarczonych źródełek - powiedział Amb po czym rzucił wyjątkiem, aż sie wszystko w sofcie posypało...**{:.color_2}

{% highlight csharp linenos %}
var observableGenerator1 = GeneratorFactory.CreateGenerator(0, 100, 1, 30);
var observableGenerator2 = GeneratorFactory.CreateGenerator(1000, 1050, 1, 20);
var observableGenerator3 = GeneratorFactory.CreateGenerator(10000, 10020, 1, 40);

var observableAmbiguous = Observable.Amb(observableGenerator1, observableGenerator2, observableGenerator3);

var subscribent = observableAmbiguous.Subscribe(
  item =>
  {
    Console.WriteLine($"Amb: {item}");
  },
  exception => Console.WriteLine(exception));
{% endhighlight %}

Bardzo banalna metoda, jednak pozwala unikać duplikacji. :)

## Zakończenie
To był fast-post. :) Niekiedy takie muszą być. Czasem mam myśli, że już się wyprztykałem i nic więcej nie na piszę. A chce dostarczyć wartość i to może być w takiej sytuacji trudne. Nie mniej jednak liczę skrycie, że ktoś kiedyś wyciągnie coś z tych moich publikacji.
Dzięki i zapraszam na kolejne...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Kombinatorzy - Start With][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Merge][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-kombinatorzy-start-wtih
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-merge

[post]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-ambiguous/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-ambiguous/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-ambiguous/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/kombinatorzy-ambiguous/image1-big.jpg
