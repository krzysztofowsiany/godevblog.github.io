---
title: Programowanie Reaktywne - Tworzymy dane - Generators.
date: 2018-02-13
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-tworzymy-dane-generators
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-generators/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-generators/post-big.jpg
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
  - Timestamp
  - TimeInterval  
  - Generate
  - Range
  - Factorial
short: Dzisiaj poznamy coś nowego, jednak skorzystamy z czegoś starego. Jako inicjatory generowania danych będziemy korzystać jeszcze wielokrotnie z Timer-ów. Bardzo dobrze sprawdzają się jako taki niewolnik, który będzie robił co mu karzemy. "Daj mi tyle i tyle co tyle".
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Range][post]][post-big]{:.post-left-image}
Dzisiaj poznamy coś nowego, jednak skorzystamy z czegoś starego. Jako inicjatory generowania danych będziemy korzystać jeszcze wielokrotnie z Timer-ów. Bardzo dobrze sprawdzają się jako taki niewolnik, który będzie robił co mu karzemy. "Daj mi tyle i tyle co tyle".

## Observable.Range
Bardzo prostym przykładem generowania danych jest **Range**{:.color_1}. Dlatego nieco go skomplikujemy**:)**{:.color_2}.
Wygenerujemy prostą tabelką zawierającą informacje o **Timestamp-ie**{:.color_2}, **Interval-le**{:.color_2} i generowanej wartości.
Jak można uzyskać taki efekt? Opakowując strumień danych **2x** => **.TimeInterval().Timestamp()**{:.color_1}.
Skutkuje to otrzymywaniem danych z obiektu obserwowanego w postaci:
* **Timestamp**, 
* **Value.Interval**, 
* **Value.Value**.

**Value**{:.color_2} to pierwsze opakowanie przy pomocy **.TimeInterval()**.

{% highlight csharp linenos %}
Console.WriteLine("RangeGenerator");
Console.WriteLine("Timestamp\t\t\tInterval\t\tValue");

var rangeSource = Observable.Range(start, count)
	.TimeInterval()
	.Timestamp();

_rangeSubscription = rangeSource.Subscribe(
	item =>
	{
		Console.WriteLine("{0}\t{1}\t{2}", 
			item.Timestamp, 
			item.Value.Interval, 
			item.Value.Value);
	},
{% endhighlight %}

A co nam daje ten **Range**{:.color_1}? To proste, określamy wartość początkową (start) oraz ilość (count) danych jakie będziemy generować: **Observable.Range(start, count)**{:.color_1}.

{% highlight csharp linenos %}
var rangeGenerator = new RangeGenerator(-100, 200);
{% endhighlight %}

Prosty przykład:

Dane: **start** = 0, **count** = 10

Wynik: **0**, **1**, **2**, **3**, **4**, **5**, **6**, **7**, **8**, **9**

## Observable.Generate
[![Reactive Extensions - Generate][image1]][image1-big]{:.post-right-image}
Jest i kolejny sposób generowania danych, bardziej wyszukany. Pozwala na kilka ciekawych zabiegów:
* **initialState** - wartość początkowa,
* **condition** - warunki jakie możemy określić, jeżeli ich wynikiem będzie **true** to wówczas będą generowane kolejne dane,
* **iterate** - jak w pętli for, należy modyfikować podstawę warunków, tak by generowanie mogło się zakończyć, jest to też podstawa generowanych danych,
* **resultSelector** - wynik iteracji możemy jeszcze zmodyfikować i tutaj można to zrobić, przykład poniżej (Factorial),
* **timeSelector** - jeszcze trzeba zainicjować proces samodzielnego generowania danych, w tym celu ustalamy co ile czasu będzie wykonywany kolejny etap generowania danych.

**Można porównać ten operator do reaktywnej pętli for:).**{:.h-4}

{% highlight csharp linenos %}
private static ulong Factorial(ulong i) => i < 1 ? 1 : i * Factorial(i - 1);

public FactorialGenerator()
{
	Console.WriteLine("Factorial");

	var initialState = 1ul;

	var observable = Observable.Generate(
		initialState,
		condition => condition < 23,
		iterate => iterate + 1,
		resultSelector => Factorial(resultSelector),
		timeSelector => TimeSpan.FromMilliseconds(100)
		).TimeInterval();

	_subscribeGenerator = observable.Subscribe(
		item =>
		{
			Console.WriteLine("{0} -> {1}", item.Interval, item.Value);
		},
{% endhighlight %}

**Factorial** to nic innego jak silnia, zapisana w bardzo skróconej wersji z wykorzystaniem **rekurencji**.

**Z rekurencją trzeba uważać. To żyje własnym życiem! Samo się żywi! Rozmnaża! I czasem nie chce zginąć!**{:.h-allert-1}

Wyniki generowania przy udziale **Silni** można zaobserwować oczywiście w przykładzie na **[GitHub-ie]**.

{% highlight csharp linenos %}
var generator = new FactorialGenerator();
{% endhighlight %}

## Zakończenie
Jak widać w powyższych moich wypocinach. Możemy wygenerować interesujące dane asynchronicznie oraz rozesłać je po najdalszych krańcach programu. A z krańców do centrum przy wykorzystaniu innych reaktywnych mechanizmów. Dalej przetworzyć dystrybuować do kolejnych zainteresowanych. Plotkowanie na całego...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Timestamp/TimeInterval][previous]**

<!--Następny: **[Programowanie Reaktywne - Zabawa z czasem - Delay.][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-timestamp-and-timeinterval
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval

[post]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-generators/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-generators/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-generators/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/tworzymy-dane-generators/image1-big.jpg

[Observable.Interval]: {{site.url}}/programowanie-reaktywne-tworzymy-dane-generators