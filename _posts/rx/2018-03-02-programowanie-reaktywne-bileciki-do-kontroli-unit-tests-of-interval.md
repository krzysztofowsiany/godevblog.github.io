---
title: Programowanie Reaktywne - Bileciki do kontroli - Unit Tests of Interval.
date: 2018-03-02
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-interval
published: true
comments: true        
image: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-interval/post.jpg
image_big: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-interval/post-big.jpg
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
short: 'Wszystko super i fajnie ale gdzie są testy? Co zrobić by przetestować taki strumień zasilany przez Observable.Interval? Przecież testy będą trwały wieczność... Jest na to rada: przeczytaj post do końca;). Ale na początek warto było by wyposażyć się...'
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - Unit Test][post]][post-big]{:.post-left-image}
Wszystko super i fajnie ale gdzie są testy? Co zrobić by przetestować taki strumień zasilany przez **Observable.Interval**{:.color_2}? Przecież testy będą trwały wieczność...
Jest na to rada: przeczytaj post do końca;)
Ale na początek warto było by wyposażyć się w dodatkowe narzędzia:

* **Install-Package Shouldly**{:.color_1} - by asercje były milsze dla oka,
* **Install-Package Microsoft.Reactive.Testing**{:.color_1} - wymagana biblioteka do testowania **Rx-owatych**{:.color_2},
* **Install-Package xUnit**{:.color_1} - bez tej paczuszki to ani rusz w testy;).

## TestScheduler
Jak to w testach bywa, trzeba czasem oszukać system i posłużyć się udawaczami. Tak jest i w przypadku testów.

Aby nie odczuć bólu testowania np.: operatora **Interval**{:.color_2} należy zakupić **DeLorean-a**{:.color_2}.
I między poszczególnymi porcjami dostarczanymi przez dystrybutora odbyć krótką podróż w czasie...

Jest też inne wyjście prostsze. Po prostu należy użyć schedulera: **TestScheduler**{:.color_1}. 
Jak tego można dokonać bez posiadania własnego **DeLorean-a** ukazałem w metodzie **InitializeStream**{:.color_1}.

Przykład oczywiście poniżej oraz w pełnej krasie na **[GitHub-ie]**.

{% highlight csharp linenos %}
public class IntervalTestsFixture
{
  #region arrange
  private IObservable<long> _observableInterval;
  private TestScheduler _testScheduler;
  private IList<long> _expectedSequence;
  
  public void PrepareStream(int count)
  {
    InitializeStream(count);

    InitializeExpectedValues(count);
  }

  private void InitializeStream(int count)
  {
    _testScheduler = new TestScheduler();
    var period = TimeSpan.FromSeconds(1);

    _observableInterval = Observable
      .Interval(period, _testScheduler)
      .Take(count);
  }
{% endhighlight %}

[![Reactive Extensions - Test-Driven Development][image1]][image1-big]{:.post-right-image}

Jak można było dojrzeć w klasie **IntervalTestsFixture**{:.color_1} zawartych jest więcej interesujących linijek. 
Dzięki tej klasie możemy wyzbyć się balastu ciężkich do zrozumienia testów jednostkowych. **[Chwała Ci za to Procencie:)]**.

To może coś przetestujemy. Proszę to ładna klaska zawierająca jedną metodę oraz jej wariacje. Testującą czy **Interval** faktycznie zwraca co ma zwrócić.

Jak widać głównie widzimy to co ma być testowane, a nie to że sąsiadka z naprzeciwka przechadza się nago wieczorami w oknie. Tym się zajmuje wspomniana **IntervalTestsFixture**{:.color_1}. Co by nas zbytnie nie rozpraszało w testowaniu.

{% highlight csharp linenos %}
public class IntervalTests
{
  [Theory]
  [InlineData(0)]
  [InlineData(10)]
  [InlineData(100)]
  [InlineData(1000)]
  [InlineData(100000)]
  public void return_sequence_of_numbers__when__subscribe_to_interval_observable_stream(int count)
  {
    //arrange
    _fixture.PrepareStream(count);

    //act
    var result = act();

    //assert
    _fixture.assert__sequence_of_numbers(result);
  }

  private ICollection<long> act()
  {
    return _fixture.act();
  }
{% endhighlight %}

Ładna co nie? Ale to moja:p Napiszcie sobie sami...

Na koniec smaczek co **act**{:.color_1}.
Do testów potrzebne są wyniki, dlatego też w miejscu gdzie testujemy funkcjonalność zapisujemy się na strumień, i pakujemy wszystko do listy.

{% highlight csharp linenos %}
public ICollection<long> act()
{
  var actualValues = new List<long>();

  _observableInterval.Subscribe(actualValues.Add);

  _testScheduler.Start();

  return actualValues;
{% endhighlight %}

Potem **Shouldly**{:.color_1} sprawdzi czy wszystko jest prawidłowo. Jak nie to poczęstuje nas odpowiednim i gorzkim komunikatem.

## Zakończenie
Testowanie to bardzo ważny aspekt wytarzania oprogramowania.  Dlatego zapewne do napisania mam jeszcze wiele postów o podobnej tematyce. Także w kontekście **Rx-ów**{:.color_1}. Jednak na dzisiaj koniec tego dobrego piąteczek, niedługo koniec wyzwania. A ja już czuję ogromną satysfakcję, a co dopiero w Niedzielę:)

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Transformers - Metadata][previous]**

<!--Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-transformers-metadata
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat

[post]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-interval/post.jpg
[post-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-interval/post-big.jpg

[image1]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-interval/image1.jpg
[image1-big]: /assets/images/2018/03/programowanie-reaktywne/bileciki-do-kontroli-unit-tests-of-interval/image1-big.jpg


[Chwała Ci za to Procent:)]: https://devstyle.pl