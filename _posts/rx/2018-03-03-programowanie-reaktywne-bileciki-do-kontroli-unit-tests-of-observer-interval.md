---
title: Programowanie Reaktywne - Bileciki do kontroli - Unit Tests of Observer Interval.
date: 2018-03-03
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-observer-interval
published: true
comments: true        
image: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-observer-interval/post.jpg
image_big: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-observer-interval/post-big.jpg
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
  - Interval
  - UnitTest
  - Tests
  - TDD
  - Test-Driven Development
short: Dzisiaj postanowiłem kontynuować wczorajszą tematykę. Czyli testowanie. W przypadku Rx-ów nie jest to takie proste. Ze względu na potrzebę kontroli nad procesem publikowania danych na strumień.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - TestScheduler][post]][post-big]{:.post-left-image}
Dzisiaj postanowiłem kontynuować wczorajszą tematykę. Czyli testowanie. W przypadku **Rx-ów**{:.color_1} nie jest to takie proste. Ze względu na potrzebę kontroli nad procesem publikowania danych na strumień. Jedna z metod została opisana w poprzednim poście. Dzisiaj nieco inny cel testów.

## TestScheduler.Start
[![Reactive Extensions - UnitTest][image1]][image1-big]{:.post-right-image}
Sam test nie czego sobie ładny i klarowny, dzięki zrzucie śmieci do osobnej klasy: **IntervalObserverTestsFixture**{:.color_1}. Ustawiamy dzisiejszych bohaterów czyli: 

* **created**{:.color_1} - sekunda w której ma nastąpić utworzenie producenta treści,
* **subscribed**{:.color_1} - w tej jednostce czasu następuje zapis na strumień (fikcyjny),
* **disposed**{:.color_1} - w jakim czasie nastąpi zakończenie działalności dystrybutora.

Oczywiście wszystkie wartości powinny być w tej samej jednostce: **sekunda**.

{% highlight csharp linenos %}
  //arrange
  _fixture.SetSimulationData(created, subscribed, disposed);

  //act
  var result = act();

  //assert__simulation_notification
  _fixture.assert__simulation_notification(result);
}

private IList<Recorded<Notification<long>>> act()
{
  return _fixture.act();
{% endhighlight %}

Po przygotowaniu wykonujemy test, i zwrotnie otrzymujemy nagranie z przebiegu działalności dystrybutora. *Czarna skrzynka, i stenogramy;).*

Możemy wówczas sprawdzić jak wyglądała historia strumyczka.
{% highlight csharp linenos %}
public void SetSimulationData(int created, int subscribed, int disposed)
{
  _disposed = disposed;
  _created = created;
  _subscribed = subscribed;

  var period = TimeSpan.FromSeconds(1);

  _sourceObservableInterval = Observable.Interval(period, _testScheduler)
    .Take(_disposed);
{% endhighlight %}

Oczywiście przy tworzeniu strumienia musimy podać **TestScheduler**{:.color_1}, tak jak w poprzednim poście.
Ucinamy do testów ilość publikowanej treści przy pomocy **.Take**{:.color_2}.

Wprowadzone wartości sekundowe będą potrzebne w metodzie testującej poniżej.

{% highlight csharp linenos %}
public IList<Recorded<Notification<long>>> act()
{
  var notificationRecorded = _testScheduler.Start(() => _sourceObservableInterval,
    TimeSpan.FromSeconds(_created).Ticks,
    TimeSpan.FromSeconds(_subscribed).Ticks,
    TimeSpan.FromSeconds(_disposed).Ticks);

  return notificationRecorded.Messages;
{% endhighlight %}

A tutaj już dzieje się, przy pomocy operatora **Start**{:.color_1} określamy o jakim czasie ma nastąpić dane działanie: **created**, **subscribed**, **disposed**. 

Dzięki zastosowaniu interwału wyzwalania publikacji danych nas strumień co **1s** możemy także tutaj posługiwać się wartościami całkowitymi. Jednak metoda **Start**{:.color_2} przyjmuje wartości typu **TimeStamp**. Jest też na samym szczycie wywołania rodzynek, lambda na utworzony wcześniej strumień: **_sourceObservableInterval**{:.color_2}.

Na koniec co innego pozostało jak sprawdzić czy wszystko zachowało się prawidłowo. Należy powołać komisję śledczą na czele z **Shouldly**{:.color_1} i zbadać zawartość czarnej skrzynki.

{% highlight csharp linenos %}
var shouldBeValue = _disposed - 1;
shouldBeValue -= _subscribed;

result.Count.ShouldBe(shouldBeValue);

long index = 0;
foreach (var item in result)
{
  item.Value.Value.ShouldBe(index++);
{% endhighlight %}

W pierwszej asercji sprawdzamy ilość zachowanych publikacji na strumień, powinno ich być o **1 mniej** niż ustalona ilość pobranych wartości ze strumienia (gdyż, jako ostatni przychodzi **OnCompleted**).

Sprawdzić należy także dane jakie są dostarczane do odbiorców. Do tego potrzebne było podwójne użycie **Value.Value**, gdyż pierwszy Value zawiera w sobie nazwę metody jaka została wywołana. Temat poruszany w rozdziale o **[metadanych]**.

## Zakończenie
Testowanie **Rx-ów** to dość specyficzny temat, i warto by było jak naj mnie korzystać z takich testów. Dlatego warto było by odseparować w możliwy jak największy sposób logikę dotykaną przez odbiorców treści do osobnych klas. 
Dobrym tutaj podejściem było by pisanie testów przed implementacją, i nawet nie korzystanie z samych właściwości **Rx-owych**.

**Niech kod będzie z Wami!.**{:.h-3}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Transformers - OfType and Cast][previous]**

<!--Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-interval
[next]: {{site.url}}/programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-interval

[post]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-observer-interval/post.jpg
[post-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-observer-interval/post-big.jpg

[image1]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-observer-interval/image1.jpg
[image1-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-observer-interval/image1-big.jpg


[metadanych]: {{site.url}}/programowanie-reaktywne-transformers-metadata