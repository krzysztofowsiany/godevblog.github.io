---
title: Programowanie Reaktywne - Wstęp.
date: 2018-02-03
author: Krzysztof Owsiany
layout: post
permalink: programowanie-reaktywne-wstep
published: true
comments: true        
image: /assets/images/2018/02/programowanie-reaktywne-wstep/post.jpg
image_big: /assets/images/2018/02/programowanie-reaktywne-wstep/post-big.jpg
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
short: Od dawien dawna, tworzenie oprogramowania zwłaszcza związanego z graficznymi interfejsami użytkownika (na potrzeby uproszczenia będę odnosił się właśnie do problemów z GUI). Boryka się z problemem, zacinania, lagów, przechodzenia programów w stan nieokreślony aż do momentu zakończenia przetwarzania pewnego obszaru w kodzie.
---
{% include_relative preface.md %}

## Wstęp
[![Wyścig do sekcji krytycznej!][post]][post-big]{:.post-left-image}
Od dawien dawna, tworzenie oprogramowania zwłaszcza związanego z graficznymi interfejsami użytkownika (na potrzeby uproszczenia będę odnosił się właśnie do problemów z GUI). 
Boryka się z problemem, zacinania, lagów, przechodzenia programów w stan nieokreślony aż do momentu zakończenia przetwarzania pewnego obszaru w kodzie.

Z pomocą przyszła wielowątkowość... 
Do dyspozycji mamy pewną zmienną ilość rdzeni w procesorze. Daje to możliwość odseparowania wykonywania czasochłonnych operacji na inny wątek i tym samym nieblokowanie GUI.

Niestety nie ma róży bez kolców. I tak jest w przypadku wielowątkowości. Programowanie jest trudniejsze i niesie ze sobą wiele pułapek wynikających z potrzeby jednoczesnego dostępu do tzw. sekcji krytycznej.

## Programowanie reaktywne
I o to nowa myśl i idea przychodzi z pomocą: Programowanie reaktywne. 
Jest to jeden z paradygmatów programowania opierający się kontrolowanie przepływu w programach przy pomocy asynchronicznych strumieni. Owe strumienie są miejscem styku, do którego są publikowane dane oraz z którego poprzez zapisanie się na listę rozsyłane są komunikaty do zainteresowanych obserwatorów. 

Drążąc głębiej tematykę, jest to po prostu implementacja wzorca projektowego Obserwator. Gdzie implementujemy dwóch aktorów: Obserwatora i Obserwowanego. Wówczas obserwowany poprzez swoje działanie rozsyła komunikaty do wszystkich zapisanych na wewnętrznej liście obserwatorów.

*Taki wzorcowy Big Brother*{:.h-3}

[![Reactive Extensions!][image1]][image1-big]{:.post-right-image}
Słynna firma z [Redmond][ms] udostępnia nam już istniejący mechanizm owego wzorca, jaki możemy implementować we własnych rozwiązaniach o nazwie **[Reactive Extensions] (RX)**. Na bazie tej biblioteki mamy możliwość użycia kilku sztuczek:
* pozbycie się problematycznych eventów (**+/-= new EventXXXX()**{:.color_1}) z kodu,
* wykorzystanie jako odmierzacze czasu (Timery), lub wątki (Thread),
* implementację własnych rozwiązań na bazie interfejsów **IObservable**{:.color_1}, **IObserver**{:.color_1}.

*Więcej o sztuczkach w kolejnych postach*.

A wszystko to z wykorzystaniem słynnego **[LINQ]**{:.color_1} oraz **lambdy**{:.color_1}.

Biblioteczki jakie należy zainstalować by korzystać z **Reactive Extensions** w przypadku Visual Studio:

* **Install-Package System.Reactive**{:.color_1},
* **Install-Package System.Reactive.Linq**{:.color_1},
* **Install-Package System.Reactive.Core**{:.color_1},
* **Install-Package System.Reactive.Providers**{:.color_1}.

W zasadzie pierwsza pozycja powinna zainstalować wymagane zależności.

## Zakończenie
Trochę teorii się przyda. W kolejnych postach będę przekazywał bardziej praktyczne przykłady okraszone kodzikiem....

Zapraszam do śledzenia, komentowania.

{% include_relative end.md %}

[post]: /assets/images/2018/02/programowanie-reaktywne-wstep/post.jpg
[post-big]: /assets/images/2018/02/programowanie-reaktywne-wstep/post-big.jpg

[image1]: /assets/images/2018/02/programowanie-reaktywne-wstep/image1.jpg
[image1-big]: /assets/images/2018/02/programowanie-reaktywne-wstep/image1-big.jpg

[linq]: https://msdn.microsoft.com/en-us/library/bb308959.aspx
[ms]: http://microsoft.com
[Reactive Extensions]: https://msdn.microsoft.com/en-us/library/hh242985(v=vs.103).aspx