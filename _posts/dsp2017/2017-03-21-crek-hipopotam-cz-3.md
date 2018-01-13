---
title: C#rek - hipopotam cz.3.
date: 2017-03-21
author: Krzysztof Owsiany
layout: post
published: true
permalink: /crek-hipopotam-cz-3
image: /assets/images/2017/03/crek-hipopotam-cz-3/post.png
categories:
  - Daj Się Poznać 2017
tags:
  - 'C#rek'
  - dajsiepoznac2017
  - DSP2017
  - Visual Studio 2015
short:  C#rek trochę już obyty z GUJI, rozmyślając o zielonych migdałach, czasem też o programowaniu. Po wielu chwilach doszedł do wniosku, iż programowanie jest to ciężki kawałek chleba, ale warto poświęcić jedną, czy dwie kąpiele błotne na rzecz nauki.
---
[![C#rek][post]][post-big]{:.post-right-image}
C#rek trochę już obyty z GU**J**I, rozmyślając o zielonych migdałach, czasem też o programowaniu. Po wielu chwilach doszedł do wniosku, iż programowanie jest to ciężki kawałek chleba, ale warto poświęcić jedną, czy dwie kąpiele błotne na rzecz nauki. Szkoda tylko, że jest tak osamotniony w swych poczynaniach, w okolicy żadnego ogra o podobnych pomyślunkach.

## Pułapki - Breakpoint
Hipek ma mały problem z balami i czasem te wredne istoty gryzą niemiłosiernie. Jest jednak na to rozwiązanie można pozastawiać pułapki. C#rek wie co to pułapki, nie raz łapał żaby.

[![C#rek][menu_breakpoints]][menu_breakpoints-big]{:.post-left-image}

Jednak na spaślaku trzeba to robić dobrze, wykorzystać można do tego kilka magicznych sztuczek.
    
Obieramy miejsce w kodziku, gdzie tą pułapke chcemy zastawić i zaklęciem **F9**, lub poprzez machnięcie lewym pośladkiem gryzonia (LPM), w menu **Debug**. W miejscu gdzie pułapka ma być postawiona celujemy w **Toogle Breakpoint**.

Od razu tutaj można rzec, iż innym przydatnym zaklęciem **Crtl+Shift+F9** zdejmujemy wszystkie pułapki **Delete All Breakpoints.**

Podkreślić tutaj trzeba bardzo ważną sprawę, można polować na robala w tym celu użyć trzeba kilku ciekawych zaklęć:
* **F10** - dzięki temu zaklęciu można śledzić robala krok po kroku idąc główną ścieżką,
* **F11** - podobnie jak wyżej tutaj możemy deptać po piętach robalom, jednak w tym przypadku możemy wchodzić w zakamarki (metody),
* **F5** - pozwala uruchomić śledzenie, ale także zrobić szybkiego susa do kolejnej pułapki.
    
# Lista pułapek - Breakpoints
[![Breakpoints][breakpoints]][breakpoints-big]{:.post-left-image}
C#rek ma małą pamięć, dlatego przyda się tutaj lista pułapek, można ją przywołać zaklęciem **Crtl+D, B.**
    
Pokaże się ładna lista, gdzie można różne cuda robić, **wyłączać, włączać, kasować, wyszukiwać, dodawać** pułapki i wszystko na widoku.
    
Taki robalomonitoring, gdzie, kiedy, co, itd. Warto korzystać.
    
## Podglądy - Autos, Immediate Window, Locals
Podczas śledzenia przydać się może nieco informacji do nawigacji, tak by po omacku nie szukać robali.

Trza tu wymienić następujące zaklęcia:    
* **Crtl+D, I** - Immediate Window - konsola z możliwością wykonywania poleceń, np. podgląd, wystarczy wpisać nazwę zmiennej i potwierdzić enterem,

[![Immediate Window][immediate]][immediate-big]{:.post-center-image} 

* **Crtl+D, A** - Autos - wgląd do zmiennych w całej aplikacji,

[![Autos][autos]][autos-big]{:.post-center-image}

* **Crtl+D, L** - Locals - to lokalne podglądy informacji, można je porozwijać, by dowiedzieć się więcej (bieżący zakres),

[![Locals][locals]][locals-big]{:.post-center-image}

* **Crtl+D, W** - Watch - wybierać można własne informacje do podglądu, dostępne są po wduszeniu prawego przycisku gryzonia na zmienną i wybraniu &#8222;Add Watch&#8221;,
* **Crtl+Alt+W, 2, **Crtl+Alt+W, 3,  **Crtl+Alt+W, 4, **Crtl+Alt+W, 5** - otwarcie okiennicy pozostałych okien **Watch**, jakby komu było mało jednej.

[![Watch][watch]][watch-big]{:.post-center-image}
    
Po tej obszernej wiedzy, warto by poćwiczyć nowe zaklęcia/umiejętności.

## Koniec o hipopotamie
To ostatni wpis hipopotamowy, mam nadzieję, że forma i treść oraz wartość intelektualna, jaką chciałem przedstawić rozbawi i nauczy.

Proszę o komentowanie, czy jest to dobra forma, czy też nie?
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/03/crek-hipopotam-cz-3/post.png
[post-big]: /assets/images/2017/03/crek-hipopotam-cz-3/post-big.png

[menu_breakpoints]: /assets/images/2017/03/crek-hipopotam-cz-3/menu_breakpoints.png
[menu_breakpoints-big]: /assets/images/2017/03/crek-hipopotam-cz-3/menu_breakpoints-big.png

[breakpoints]: /assets/images/2017/03/crek-hipopotam-cz-3/breakpoints.png
[breakpoints-big]: /assets/images/2017/03/crek-hipopotam-cz-3/breakpoints-big.png

[autos]: /assets/images/2017/03/crek-hipopotam-cz-3/autos.png
[autos-big]: /assets/images/2017/03/crek-hipopotam-cz-3/autos-big.png

[locals]: /assets/images/2017/03/crek-hipopotam-cz-3/locals.png
[locals-big]: /assets/images/2017/03/crek-hipopotam-cz-3/locals-big.png

[immediate]: /assets/images/2017/03/crek-hipopotam-cz-3/immediate.png
[immediate-big]: /assets/images/2017/03/crek-hipopotam-cz-3/immediate-big.png

[watch]: /assets/images/2017/03/crek-hipopotam-cz-3/watch.png
[watch-big]: /assets/images/2017/03/crek-hipopotam-cz-3/watch-big.png