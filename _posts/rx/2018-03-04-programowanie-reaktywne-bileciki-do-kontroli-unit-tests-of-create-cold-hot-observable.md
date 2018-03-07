---
title: Programowanie Reaktywne - Bileciki do kontroli - Unit Tests of Create Cold/Hot Observable.
date: 2018-03-04
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable
published: true
comments: true        
image: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/post.jpg
image_big: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/post-big.jpg
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
  - UnitTest
  - Tests
  - TDD
  - Test-Driven Development
  - Create Hot Observable
  - Create Cold Observable
short: W ostatnim poście wyzwania poruszę ponownie tematykę związaną z testowanie. Dzisiaj wejdziemy jeszcze głębiej i przetestujemy dokładniej co się dzieje w trakcie odbierania danych od dystrybutora. Zapraszam do czytania.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - CreateHotObservable][post]][post-big]{:.post-left-image}
W ostatnim poście wyzwania poruszę ponownie tematykę związaną z testowanie. Dzisiaj wejdziemy jeszcze głębiej i przetestujemy dokładniej co się dzieje w trakcie odbierania danych od dystrybutora. Zapraszam do czytania.

## CreateColdObservable i CreateHotObservable
Na tapetę wybrałem dzisiaj dwa sposoby tworzenia obiektów obserwowanych:

* **CreateColdObservable**{:.color_1} - dzięki tej metodzie możemy utworzyć strumień, z wykorzystaniem porcji nagrań, tak jak poprzednio w poście opisywałem użycie **Recorded<Notification<...**{:.color_1}. Właśnie z wykorzystaniem tej klasy możemy przygotować historię publikowania treści przez strumień. Publikowanie jest względem dokonania zapisu na strumień,
* **CreateHotObservable**{:.color_1} - działa tak samo jak metoda wyżej, z tą różnicą, iż zaczyna od momentu utworzenia strumienia. 

Rozwinięcie powiązania z tworzeniem lub zapisem, znajduje się w dalszej części postu.

W tym kontekście napisałem dwa testy.
Zobaczcie jakie ładne i klarowne. Widać same dobre rzeczy. Całe przekręty, szachrajstwa zostały schowane w klasie dodatkowej: **CreateObservableTestsFixture**{:.color_1}.

Pierwszy teścik weryfikuje działanie gorącego tworzenia dystrybutora.
{% highlight csharp linenos %}
[Fact]
public void return_sequence_of_notifications__when__subscribe_to_hot_observable()
{
  //arrange
  _fixture.SetSimulationDataForHotObservable();

  //act
  var result = act();

  //assert
  _fixture.assert__simulation_notification_of_hot_observable(result);
{% endhighlight %}

[![Reactive Extensions - CreateColdObservable][image1]][image1-big]{:.post-right-image}

Jak i w poprzednich postach wykorzystałem tutaj **AAA**{:.color_1}:
* **A**{:.color_1}range - przygotowanie do testowania,
* **A**{:.color_1}ct - odpalenie funkcjonalności jaką należy przetestować,
* **A**{:.color_1}ssert - dowodzimy, że test przeszedł.

Drugi test bardzo podobny do pierwszego, w zasadzie różni się tylko użyciem metod do przygotowania, i weryfikacji wyników testu.
{% highlight csharp linenos %}
[Fact]
public void return_sequence_of_notifications__when__subscribe_to_cold_observable()
{
  //arrange
  _fixture.SetSimulationDataForColdObservable();

  //act
  var result = act();

  //assert
  _fixture.assert__simulation_notification_of_cold_observable(result);
{% endhighlight %}

To tyle o samych testach, pora zabrać się za krojenie mięcha.

W procesie przygotowania strumienia danych opartego o **HotObservable**{:.color_1} należy wskazać parametr do metody wytwarzającej. Oczywiście metoda **CreateHotObservable**{:.color_1} jest zawarta w klasie już poznanej: **TestScheduler**{:.color_2}.

Tworzenie źródełka wykonujemy przy pomocy kreacji historii rekordów. W każdym z tworzonych rekordów **Recorded**{:.color_1} określamy jakiego typu będzie powiadomienie, a następnie wypełniamy czasem w jakim ma nastąpić publikacja na strumień oraz danymi jakie mają być publikowane.
Określamy także czym jest wpis:

* dane - **CreateOnNext**{:.color_1},
* wyjątek - **CreateOnError**{:.color_1},
* koniec strumienia - **CreateOnCompleted**{:.color_1}.

{% highlight csharp linenos %}
_sourceObservableInterval = _testScheduler.CreateHotObservable(
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnError<int>(new Exception())),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnError<int>(new ArgumentException())),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnCompleted<int>())
{% endhighlight %}

Dla poszczególnych metod należy dodatkowo podać wymagane parametry np: wyjątek jaki ma zostać rzucony w danym miejscu.
Doskonale tutaj widać potencjał. Skoro możemy konkretnie przygotować sekwencję występujących po sobie publikacji danych na strumień, to wówczas możemy także to zweryfikować.

Drugi przykład jest bardzo podobny, dotyczy jednak **CreateColdObservable**{:.color_1}
{% highlight csharp linenos %}
_sourceObservableInterval = _testScheduler.CreateColdObservable(
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
  new Recorded<Notification<int>>(TimeSpan.FromSeconds(second++).Ticks, Notification.CreateOnNext(value++)),
{% endhighlight %}

Metoda **act**{:.color_1} będzie bardzo podobna do tej z poprzedniego postu. Odpalamy funkcjonowanie strumienia, i określamy w jakich kryteriach będzie wykonywana dystrybucja danych.

Metoda korzysta z wcześniej przygotowanego strumienia: **_sourceObservableInterval**{:.color_1}.
{% highlight csharp linenos %}
public IList<Recorded<Notification<int>>> act()
{
  var notificationRecorded = _testScheduler.Start(() => _sourceObservableInterval,
    0,
    0,
    TimeSpan.FromSeconds(_disposed).Ticks);

  return notificationRecorded.Messages;
}
{% endhighlight %}

[![Reactive Extensions - TestScheduler][image2]][image2-big]{:.post-left-image}

Dla obu przypadków będzie to to samo działanie.

Pora zweryfikować działanie. Sprawdzić czy stworzony strumień zostanie prawidłowo rozesłany.
Weryfikujemy w tym celu kilka właściwości nagranych wiadomości:
* czy ilość dodanych etapów na strumień jest równa ilości otrzymanych, z pominięciem **OnCompleted** (-1)
{% highlight csharp linenos %}
private void assert__for_messages_count(IList<Recorded<Notification<int>>> messages)
{
  var shouldBeValue = _disposed - 1;
  messages.Count.ShouldBe(shouldBeValue);
{% endhighlight %}

* czy łączny czas jaki strumień żył jest odpowiedni, ilość elementów razy jednostka czasu na element,
{% highlight csharp linenos %}
_testScheduler.Clock.ShouldBe(_disposed * TimeSpan.FromSeconds(1).Ticks);
{% endhighlight %}

* weryfikacja czasów poszczególnych publikacji, tutaj mamy dwie możliwości, dla **hot** i **cold**.
{% highlight csharp linenos %}
private void assert__for_messages_time_hot(IList<Recorded<Notification<int>>> messages)
{
  for (var i = 0; i < _disposed - 1; i++)
  {
    messages[i].Time.ShouldBe(TimeSpan.FromSeconds(i + 1).Ticks);
{% endhighlight %}

Wersja **hot** różni się tym, że czas wyliczany jest relatywny w odniesieniu do utworzenia strumienia. Natomiast **cold** odnosi się do momentu subskrypcji. 

{% highlight csharp linenos %}
private void assert_for_messages_time_cold(IList<Recorded<Notification<int>>> messages)
{
  for (var i = 0; i < _disposed - 1; i++)
  {
    messages[i].Time.ShouldBe(TimeSpan.FromSeconds(i + 1).Ticks + 1);
{% endhighlight %}

Dodanie 1 tick-a, właśnie pochodzi z tej różnicy w funkcjonowaniu. 
Opóźnienie między utworzeniem, a subskrypcją w tym konkretnym przypadku gdzie obie wartością ustawione na 0 (metoda **Start**). Wynosi właśnie 1 tick.

* weryfikowanie rodzaju rekordu, użyłem w tym kontekście metod: **ShouldBeOnNext**{:.color_1} i **ShouldBeOnError**{:.color_1}.
{% highlight csharp linenos %}
private void assert__for_messages(IList<Recorded<Notification<int>>> messages)
{
  var index = 0;
  var value = 0;
  messages[index++].Value.ShouldBeOnNext(value++);
  messages[index++].Value.ShouldBeOnNext(value++);
  messages[index++].Value.ShouldBeOnNext(value++);
  messages[index++].Value.ShouldBeOnError(typeof(Exception));
  messages[index++].Value.ShouldBeOnNext(value++);
  messages[index++].Value.ShouldBeOnNext(value++);
  messages[index++].Value.ShouldBeOnError(typeof(ArgumentException));
  messages[index++].Value.ShouldBeOnNext(value++);
  messages[index++].Value.ShouldBeOnNext(value++);
{% endhighlight %}
Należy tutaj oczywiście zweryfikować całą zawartość strumienia, czy publikowane dane są odpowiednie.

Oczywiście wszystkie te weryfikacje warto zebrać w całość. I stosując się do zasady **DRY**{:.color_1}, wykorzystać co się da do niecnych celów.
{% highlight csharp linenos %}
public void assert__simulation_notification_of_cold_observable(IList<Recorded<Notification<int>>> messages)
{
  assert_for_messages_time_cold(messages);

  assert__for_messages_count(messages);
  assert__for_test_scheduler_clock();
  assert__for_messages(messages);
}
{% endhighlight %}

Różnica pomiędzy obiema metodami w odniesieniu do gorącego i zimnego jest w metodach: **assert_for_messages_time_cold**, **assert__for_messages_time_hot** jak same nazwy wskazują.
{% highlight csharp linenos %}
public void assert__simulation_notification_of_hot_observable(IList<Recorded<Notification<int>>> messages)
{
  assert__for_messages_time_hot(messages);
{% endhighlight %}

Ludzie powiedzą: 
- jak to przecież **ShouldBeOnNext**{:.color_1} i **ShouldBeOnError**{:.color_1} nie ma w bibliotece **Shouldly**{:.color_1}...
- racja niema. To sobie napisałem je sam :p.

**DRY** mi tak kazał. Połączyłem weryfikowanie w całość.
{% highlight csharp linenos %}
public static void ShouldBeOnNext<T>(this Notification<T> value, T expectedValue)
{
  value.Kind.ShouldBe(NotificationKind.OnNext);
  value.HasValue.ShouldBeTrue();
  value.Exception.ShouldBeNull();
  value.Value.ShouldBe(expectedValue);
{% endhighlight %}

Pierwsza sprawdza czy powiadomienie jest typu **OnNext**{:.color_1}. W tym celu sprawdzam:
* **Kind** - typ to **NotificationKind.OnNext**,
* **HasValue** - OnNext powinien mieć wartość,
* **Exception** - nie powinno być wyjątku,
* **Value** - i oczywiście wartość powinna być taka jak zapodałem w metodzie.


{% highlight csharp linenos %}
public static void ShouldBeOnError<T>(this Notification<T> value, Type type)
{
  value.Kind.ShouldBe(NotificationKind.OnError);
  value.HasValue.ShouldBeFalse();
  value.Exception.ShouldBeOfType(type);
{% endhighlight %}

Druga metoda sprawdza czy jest to **OnError**{:.color_1}:
* **Kind** - typ to **NotificationKind.OnError**,
* **HasValue** - OnError nie powinien zawierać żadnej wartości,
* **Exception** - za to powinien rzucić jakiś wyjąteczek.

## Zakończenie
A poco ci tyle asercji, powinna być jedna na klasę. 
No tak jedna, i jest jedna w kontekście weryfikacji strumienia jest jedna asercja, a że składa się na nią tyle czynników to już nie moja wina.

Ale poco zaglądasz do pomocniczej klasy, zobacz co robi test i czy działa, nie grzeb tam bo tam jest bałagan.

Kończąc na dzisiaj, mam nadzieje, że moje przemyślenia i wypociny do czegoś się komuś przydadzą. 

Ja dzięki cało miesięcznej pracy z **Rx-ami** nauczyłem się bardzo wiele, nie tylko z samej biblioteki. Ale także z samego pisania i wytrwałości.

Jestem obecnie skłonny choć w małym stopniu poczuć się jak **[Gutek]** w jego rocznym celu pisania postów co dzień. **Wielki szacunek, za zrealizowanie tego celu!**{:.color_2}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Bileciki do kontroli - Unit Tests of Observer Interval][previous]**

<!--Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-observer-interval
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat

[post]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/post.jpg
[post-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/post-big.jpg

[image1]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/image1.jpg
[image1-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/image1-big.jpg

[image2]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/image2.jpg
[image2-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable/image2-big.jpg

[Gutek]: https://blog.gutek.pl