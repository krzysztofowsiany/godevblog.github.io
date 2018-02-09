---
title: Programowanie Reaktywne - Zabawa z czasem - Delay.
date: 2018-02-08
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-zabawa-z-czasem-delay
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-delay/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-delay/post-big.jpg
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
  - Delay
short: Dzisiaj na tapetę coś prostego. Bazujując na operatorze Interval. Złapiemy ogon niczym w filmach szpiegowskich. A nawet wiele...
---
{% include_relative preface.md %}

## Wstęp
Dzisiaj na tapetę coś prostego. Bazujując na operatorze Interval. Złapiemy ogon niczym w filmach szpiegowskich. A nawet wiele...

## Observable.Delay
[![Reactive Extensions - Delay][post]][post-big]{:.post-left-image}
Do przepisu będziemy potrzebować już istniejący strumień. Do tego celu najłatwiej użyć **Observable.Interval**{:.color_2}. 

Do głównego strumienia generowanego przez Interval. Dodamy tak zwany ogon. Klasyczna sytuacja z Hollywood. Bohater jedzie samochodem. Nagle uświadamia sobie, że podąża za nim samochód. Przyśpiesza, ogon też przyśpiesza. 

Ale my nie będziemy starali się go zgubić. A jedynie doczepić kilka wagonów do lokomotywy.

Na początek dopisujemy się do **Observable.Interval**{:.color_2}, będzie to nasz obiekt do śledzenia.

{% highlight csharp linenos %}
var subscribeInterval = observableInterval.Subscribe(index =>
{
  Console.WriteLine($"{DateTime.UtcNow} Followed!");
});
			
for (var i = 0; i < 10; i++)
{
  spies.Add(new Spy(observableInterval, rand.Next(3000), $"Spy {i}"));
}
{% endhighlight %}

Następnie tworzymy 10 szpiegów, nadając im nazwę oraz losową wartość  0 - 3000 [ms]. Będzie to odstęp czasowy szpiega od obserwowanego.

{% highlight csharp linenos %}
internal class Spy : IDisposable
{
	private string _spyName;
	private IDisposable _spySubscribe;

	public Spy(IObservable<long> observableInterval, int time, string spyName)
	{
		_spyName = spyName;

		var delay = TimeSpan.FromMilliseconds(time);
		_spySubscribe = observableInterval.Delay(delay)
			.Subscribe(
			index =>
			{
				Console.WriteLine($"{DateTime.UtcNow} {_spyName}");
			},
			exception =>
{% endhighlight %}

[![Reactive Extensions - Delay][image1]][image1-big]{:.post-right-image}
Do śledzenia wykorzystamy **Observable.Delay**{:.color_1}. Ten operator spowoduje publikowanie wiadomości w określonym odstępie czasu od bazowego głównego strumienia. Podawanym jako parametr typu TimeSpan. Następnie wystarczy już tylko oczywiście zapisać się na strumień nowego dystrybutora.

Tak samo za pociągiem podążają wagony, z małym nagięcie. Wagony są do siebie nawzajem podczepiane. Tutaj **Delay**{:.color_2} doczepia się do bazowego "wodza".

## Zakończenie
Mam cichą nadzieję, że moje aluzje, przykłady pomogą w zrozumieniu poruszanej tematyki. A wręcz jej nie utrudnią. 

Pomalutku dostrzegam pewien problem, otóż przy nadmiernym korzystaniu z tych wszystkich mechanizmów, jakie dostarczają **Rx**{:.color_2}. Może się okazać, że będziemy mieli nowy **Callback Hell**{:.color_1}. Jak zawsze sprawdza się znana zasada. Można wszystko, ale w umiarze.

Zapraszam do przeanalizowania projektu **Delay**{:.color_2}, na [GitHub].


{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Zabawa z czasem - Buffer][previous]**

<!--Następny: **[Programowanie Reaktywne - Kto za tym stoi? - Sheduler.][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-buffer
[next]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval


[post]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-delay/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-delay/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-delay/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/zabawa-z-czasem-delay/image1-big.jpg
