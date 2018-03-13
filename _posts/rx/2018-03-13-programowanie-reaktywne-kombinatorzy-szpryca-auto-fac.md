---
title: Programowanie Reaktywne - Szpryca - AutoFac.
date: 2018-03-13
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-szpryca-auto-fac
published: true
comments: true        
image: /assets/images/2018/03/programowanie-reaktywne/szpryca-auto-fac/post.jpg
image_big: /assets/images/2018/03/programowanie-reaktywne/szpryca-auto-fac/post-big.jpg
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
  - AutoFac
  - Dependency Injection
short: Ludzie lubią ułatwiać sobie życie. Programiści to też podobno ludzie ;) dlatego pewnie postępują podobnie. Czasem z lenistwa, innym razem z własnych nieprzymuszonych chęci. Branża IT nieustannie się rozwija. Powstają takie wspaniałości jak wstrzykiwanie zależności;) Warto było by i w rodzinie Rx-owatych dostawać to co się chce i kiedy się chce.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - AutoFac][post]][post-big]{:.post-right-image}
Ludzie lubią ułatwiać sobie życie. Programiści to też podobno ludzie ;) dlatego pewnie postępują podobnie.
Czasem z lenistwa, innym razem z własnych nieprzymuszonych chęci. 
Branża IT nieustannie się rozwija. Powstają takie wspaniałości jak wstrzykiwanie zależności;)

Warto było by i w rodzinie **Rx-owatych**{:.color_2} dostawać to co się chce i kiedy się chce.

## AutoFac
Hmm posłużę się tutaj moją ulubioną biblioteką do wstrzykiwania szprycy w konstruktorach. **[AutoFac]**.
Nie ma róży bez kolców... By ktoś miał lepiej inny musi mieć gorzej. Dlatego wszystkie wstrzykiwane środki trzeba wcześniej przygotować.
**Kontener trzeba załadować przed podróżą**{:.color_1}.
Przykładowo rejestrujemy obiekt **[Interval]**. Niestety w tej formie możemy dokonać jedynie jednorazowej rejestracji. 
Wynika to z faktu, że musimy zidentyfikować ten tworzony obiekt, i dzieje się to poprzez **IObservable**{:.color_1}<**long**{:.color_1}>. 
{% highlight csharp linenos %}
var builder = new ContainerBuilder();

builder
  .Register(c => Observable.Interval(TimeSpan.FromMilliseconds(100)))
  .As<IObservable<long>>()
  .SingleInstance();

builder.RegisterType<ObservableTimeCounter>().SingleInstance();

builder.RegisterType<Clock>();
builder.RegisterType<Part>();
{% endhighlight %}

Rejestrujemy także w ten sposób kilka innych obiektów, np. **ObservableTimeCounter**{:.color_1}, **Clock**{:.color_1}, **Part**{:.color_1}.

Obiekty **Rx-owe**{:.color_2} będą wstrzykiwane wielokrotnie, dlatego dobrze by je było zrobić jako **Singleton-y**{:.color_1}.

Jak już sobie porejestrujemy obiekty. To można je powyciągać.
{% highlight csharp linenos %}
var container = InitContainer();

container.Resolve<Clock>();

for (var i = 0; i < 7; i++)
{
  container.Resolve<Part>();
}
{% endhighlight %}

Dla przykładu użyjemy obiektu **Clock**{:.color_1} do wyświetlania zegara.
Oraz kilu obiektów **Part**{:.color_1}. Ale dzięki **singleton-kom** możemy wielokrotnie się podpinać pod zarejestrowane czasowe wyzwalacze.

A jak poprosić o obiekt **Rx-a**{:.color_2}. Tak jak każdy inny:p, wykorzystując uchwyt do zarejestrowanego w kontenerze obiektu.
{% highlight csharp linenos %}
public Clock(ObservableTimeCounter interval, Object obj)
{
  _obj = obj;

  interval.Subscribe(time =>
  {
    lock (_obj)
    {
      Console.SetCursorPosition(Console.WindowWidth - 8, 0);
{% endhighlight %}

[![Reactive Extensions - Dependency Injection][image1]][image1-big]{:.post-left-image}

Wstrzyknięty został obiekt **ObservableTimeCounter**{:.color_1}, można już się zarejestrować.

Jest tutaj jeszcze jeden trik, jaki musiałem zastosować ze względu na pisanie na konsole.
**Obiekt**{:.color_1}, wstrzykiwany może być wykorzystywany w wielu miejsca. A służ on blokowaniu dostępu do określonego obszaru sekcji krytycznej.

W przeciwnym wypadku byłby niezły bajzel. Im więcej byśmy dodali obiektów, tym częściej działy by się cuda na ekranie konsoli. A to dlatego, że działania na konsoli: np.:

* **Console.SetCursorPosition**{:.color_1} - ustawienie pozycji kursora,
* **Console.WriteLine**{:.color_1} - wypisanie na konsole danych.

Łącznie nie są to działania atomowe.
I poprzez korzystanie ze strumienia i wielu subskrypcjom sekwencja wykonania działań na konsoli, może być losowa.
Dzięki zablokowaniu działania na konsoli. Sytuacja została w prosty sposób ogarnięta.
Jednak nie jest to dobra praktyka i ma na celu jedynie prezentację działania **Rx-ów**{:.color_2} i **AutoFac-a**{:.color_2}.
{% highlight csharp linenos %}
public Part(IObservable<long> interval, Object obj)
{
  _obj = obj;
  _guid = Guid.NewGuid().ToString().Substring(0, 5);
  _top = count;
  count++;

  interval.Subscribe(OnNext);
{% endhighlight %}


## Zakończenie
Oczywiście istnieje inne wyjście z problemu rejestrowania wielu obiektów np. **Interval**.
Ale o tym myślę przy następnej okazji.

**Kod z Wami!**{:.h-3}

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Bileciki do kontroli - Unit Tests of Create Cold/Hot Observable][previous]**

<!--Następny: **[Programowanie Reaktywne - Kombinatorzy - Start With][next]**-->

------
[previous]: {{site.url}}/programowanie-reaktywne-bileciki-do-kontroli-unit-tests-of-create-cold-hot-observable
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat

[post]: /assets/images/2018/03/programowanie-reaktywne/szpryca-auto-fac/post.jpg
[post-big]: /assets/images/2018/03/programowanie-reaktywne/szpryca-auto-fac/post-big.jpg

[image1]: /assets/images/2018/03/programowanie-reaktywne/szpryca-auto-fac/image1.jpg
[image1-big]: /assets/images/2018/03/programowanie-reaktywne/szpryca-auto-fac/image1-big.jpg

[AutoFac]: https://autofac.org/

[Interval]: {{site.url}}/programowanie-reaktywne-zabawa-z-czasem-interval

[Singleton-y]: https://pl.wikipedia.org/wiki/Singleton_(wzorzec_projektowy)