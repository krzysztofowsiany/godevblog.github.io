---
title: Programowanie Reaktywne - Łap To! - ConsoleKey.
date: 2018-02-17
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-lap-to-console-key
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne/lap-to-console-key/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne/lap-to-console-key/post-big.jpg
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
  - ConsoleKey
short: Dzisiejszy post jest szczególny, gdyż to 15 post składający się na wyzwanie jakie podjąłem. Półmetek jest. Wiele pracy już zostało włożone, jeszcze więcej przede mną.  Dziękuję wszystkim czytelnikom, i mam nadzieję, że udało mi się komuś pomóc.
---
{% include_relative preface.md %}

## Wstęp
[![Reactive Extensions - ConsoleKey][image1]][image1-big]{:.post-left-image}
Dzisiejszy post jest szczególny, gdyż to 15 post składający się na wyzwanie jakie podjąłem. Półmetek jest. Wiele pracy już zostało włożone, jeszcze więcej przede mną.  Dziękuję wszystkim czytelnikom, i mam nadzieję, że udało mi się komuś pomóc.

Zostałem też sprowadzony do porządku. Nadmiernie obkładałem FB grupę, swoimi publikacjami. Wszystkie osoby jakie uraziłem tym działaniem przepraszam. I znacznie ograniczę wrzucanie swoich wypocin na publiczne grupy w mediach społecznościowych.

## ConsoleKey
Dzisiaj zmienimy trochę podejście, i zaczniemy przechwytywać zdarzenia pochodzące od użytkownika. W tym celu stworzyłem klasę **ObservableConsoleKey**{:.color_1}. Można zapisywać się na jej wewnętrzną listę. Tym samym po uruchomieniu nasłuchu na zdarzenia pochodzące wciskanych przycisków w konsoli. Będziemy mogli reagować.

{% highlight csharp linenos %}
public class ObservableConsoleKey : IObservable<ConsoleKeyInfo>, IDisposable
{
  private bool _catchKeys;
  private List<IObserver<ConsoleKeyInfo>> _observers;
{% endhighlight %}

[![Reactive Extensions - ConsoleKey][post]][post-big]{:.post-right-image}

Publikacja wciśniętych klawiszy na stłumień odbywa się w metodzie **Start**{:.color_1}. Dodatkowo użyłem zmiennej logicznej do kontroli pętli odbierającej dane z klawiatury i dystrybuującej do zapisanych zainteresowanych obiektów.

Przy pomocy publicznej metody **Stop**{:.color_1} możemy przerwać pętlę i tym samym pozwolić na zakończanie programu w konsoli.

{% highlight csharp linenos %}
public void Start()
{
  _catchKeys = true;

  while (_catchKeys)
  {
    var currentKey = Console.ReadKey(true);
    Publish(currentKey);
  }
}

public void Stop()
{
  _catchKeys = false;
{% endhighlight %}
Metoda jest bardzo prosta i w zasadzie zmienia zmienną logiczną **_catchKeys**{:.color_1} na **false**.

Publikowanie wciśniętych klawiszy na strumień jest bardzo proste. Także użyte tutaj zostało **LINQ** i metoda **ForEach**{:.color_2}. Jako parametr w wyzwalanej metodzie **OnNext**{:.color_2} oczywiście przekazujemy przechwycony klawisz z konsoli.
{% highlight csharp linenos %}
private void Publish(ConsoleKeyInfo currentKey)
{
  _observers.ForEach(observer => observer.OnNext(currentKey));
}
{% endhighlight %}

Pozostałe elementy w klasie **ObservableKeyConsole**{:.color_1}, są bardzo podobne do tych użytych w poprzednich klasach generatorów: **ObservableValentinesDay**{:.color_2}, **ObservableTimeCounter**{:.color_2}.

Ostatni fragment kodu dotyczy sposobu użycia nowego publishera. Jest bardzo podobnie do poprzednich z tą różnicą, że do dyspozycji mamy dwie wyżej opisane metody **Start**{:.color_2} i **Stop**{:.color_2}. Dzięki nim możemy sterować zachowaniem obiektu obserwowanego.

Zapis na strumień wykonujemy standardowo.
{% highlight csharp linenos %}
static void Main()
{
  var observableProvider = new ObservableProvider();

  observableProvider.ConsoleKey
    .Subscribe(consoleKey =>
    {
      Console.WriteLine(consoleKey.Key);

      if (consoleKey.Key == ConsoleKey.Enter)
      {
        observableProvider.ConsoleKey.Stop();
      }
    });

  observableProvider.ConsoleKey.Start();
{% endhighlight %}

Wykonujemy tutaj także ekstra sprawdzenie czy wciśnięty klawisz to **Enter** i gdy tak właśnie jest to wówczas zatrzymujemy pętlę przechwytującą klawiaturę konsoli. I tym samym możemy zatrzymać działanie programu w sposób naturalny.

## Zakończenie
Tooooooo bardzoooooo krótki post. Wybrałem temat dość prosty do implementacji. Nie zawsze trzeba klepać multum lini kodu. Czasem trzeba coś prostego stworzyć. I myślę, że jest to bardzo ciekawe rozwiązanie. 

Często czuję tutaj potrzebę użycia kontenera (**AutoFac**). I być może pojawią się posty o takiej tematyce. Wówczas mielibyśmy już dostęp w dowolnym miejscu programu do obiektów obserwowanych. W przypadku **ObservableConsoleKey**{:.color_1} dało by to możliwość korzystania z wprowadzanych na konsolę danych w dowolnym miejscu aplikacji. Ciekawa koncepcja...

{% include_relative end.md %}

------
Wcześniejszy: **[Programowanie Reaktywne - Marudzimy - Take][previous]**

Następny: **[Programowanie Reaktywne - Kombinatorzy - Concat][next]**

------
[previous]: {{site.url}}/programowanie-reaktywne-marudzimy-take
[next]: {{site.url}}/programowanie-reaktywne-kombinatorzy-concat

[post]: /assets/images/2018/02/programowanie-reaktywne/lap-to-console-key/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne/lap-to-console-key/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne/lap-to-console-key/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne/lap-to-console-key/image1-big.jpg

[generatory]: {{site.url}}/programowanie-reaktywne-tworzymy-dane-generators


