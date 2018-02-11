---
title: Programowanie Reaktywne - Zabawa z czasem - Buffer.
date: 2018-02-08
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-buffer
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-buffer/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-buffer/post-big.jpg
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
  - Buffer
short: Dużo tych operatorów na klasie Observable powiązanych z czasem można znaleźć w bibliotece Rx-ów. Dzisiaj zajmiemy się dość ciekawym tworem, dzięki któremu możemy operować strumieniami niczym światłami drogowymi...
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Buffer][post]][post-big]{:.post-left-image}

Dużo tych operatorów na klasie **Observable**{:.color_1} powiązanych z czasem można znaleźć w bibliotece **Rx-ów**. Dzisiaj zajmiemy się dość ciekawym tworem, dzięki któremu możemy operować strumieniami niczym światłami drogowymi...

## Observable.Buffer
Bufor działa jak zapora pomiędzy danymi do publikacji a samą publikacją. Gdzie analogia do świateł? 
Dojeżdżając do skrzyżowania, jeżeli mamy szczęście to jest zielone i jedziemy. Natomiast jeśli trafimy na ten gorszy czas to wówczas jesteśmy "zbuforowani" do czasu, gdy światła ponownie nas przepuszczą.

Podobnie jest z **Observable.Buffer**{:.color_1}, gromadzi on pule do publikacji i wypuszcza ją, dopiero gdy upłynie określony czas.

Najpierw przygotujemy sobie dane, to znaczy będziemy generować samochody dojeżdżające do świateł. Co 500ms nowy samochód.

{% highlight csharp linenos %}
_observableCarList = Observable.Interval(TimeSpan.FromMilliseconds(500));

_intervalSubscribent = _observableCarList.Subscribe(
  carId =>
	{
	  Console.WriteLine($"New Car {carId} ");
	});
{% endhighlight %}

Skoro już samochody mamy zapewnione to pora zainicjować buffor:
{% highlight csharp linenos %}
var wait = TimeSpan.FromSeconds(2);
var period = TimeSpan.FromSeconds(5);

_bufferObservable = Observable.Buffer(_observableCarList, wait, period);
{% endhighlight %}

Przy pomocy operatora **Observable.Buffer**{:.color_1} tworzymy nowy obiekt do obserwowania. Jako parametry podajemy opóźnienie pierwszej publikacji strumienia samochodu (wait).

Drugi parametr **period** określa co ile będą publikowane kolejne partie samochodów na strumień.

Pozostaje jeszcze obsłużyć strumień samochodów. Czyli je przepuszczać, gdy światło będzie zielone i zatrzymywać, gdy będzie zielone:

{% highlight csharp linenos %}
_bufferSubscribent = _bufferObservable.Subscribe(
  newCars =>
	{
	  try
		{
		  Console.WriteLine("Green light!");

			foreach (var carId in newCars)
			{
				Console.WriteLine($"\t\tPass car {carId}.");
				Thread.Sleep(100);
			}

			Console.WriteLine("Red light!");
			Console.WriteLine();
		}
		catch (Exception e)
		{
			Console.WriteLine(e);
		}
	},
() => Console.WriteLine("Completed"));
{% endhighlight %}

[![Reactive Extensions - Buffer][image1]][image1-big]{:.post-right-image}

W pętli dodałem opóźnienie w celach demonstracyjnych tak by symulować przejeżdżanie samochodów.

Zawartość **newCars** będzie zawierała wygenerowaną sekwencję danych(samochodów) w danej chwili. Jeżeli coś się wydarzy nie przewidzianego to wówczas cała lista zostanie utracona!

## Zakończenie
Taki kulawy przykład myślę, że przynajmniej po części pozwoli na zrozumienie **Observable.Buffer**{:.color_1}. Oczywiście metoda zawiera wiele braci i sióstr. Jednak zapoznałem Was tylko z jedną. Proponuję poeksperymentować tak jak Ja to zrobiłem w tym przykładzie.
Zapraszam na **[GitHub-a]**!

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Interval][previous]**

Następny: **[Programowanie Reaktywne - Zabawa z czasem - Delay][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-delay


[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-buffer/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-buffer/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-buffer/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-buffer/image1-big.jpg
