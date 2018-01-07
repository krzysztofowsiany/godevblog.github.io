---
title: 'Garbage Collector &#8211; Wysypisko śmieci.'
date: 2017-05-14T22:58:28+00:00
author: Krzysztof Owsiany
layout: post
published: true
permalink: wysypisko-smieci
image: /assets/images/2017/05/wysypisko-smieci/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - 'C#'
  - dajsiepoznac2017
  - DSP2017
  - Garbage Collection
  - GC
  - 'Mark&Sweep'
short: Nasz wspaniały język C#, znosi z nas prawie pełną odpowiedzialność za sprzątanie po sobie. Można by rzec, iż mamy zatrudnioną sprzątaczkę i nawet nie wiemy, kiedy magicznie bałagan znika. Oczywiści mowa tutaj o Garbage Collector...
---
[![Garbage Collector][post]][post-big]{:.post-left-image}
 
Nasz wspaniały język C#, znosi z nas prawie pełną odpowiedzialność za sprzątanie po sobie.

Można by rzec, iż mamy zatrudnioną sprzątaczkę i nawet nie wiemy, kiedy magicznie bałagan znika. Oczywiści mowa tutaj o **Garbage Collector**.

Jeszcze dzisiaj pamiętam trudność, i obowiązek kontrolowania wycieków pamięci, gdy pisałem oprogramowanie z wykorzystaniem języka C++.

Z drugiej strony człowiek był bardziej odpowiedzialny za to co się działo w kodzie.

Teraz w dobie ogromnych pamięci RAM, **GC**, często można  zapomnieć o wyciekach pamięci.

## Działanie
[![Garbage Collector][image1]][image1-big]{:.post-right-image}
Alokowanie pamięci odbywa się niejako w dwóch miejscach:
* na **stosie (Stack)** &#8211; zarządzaniem zajmuje się **CLR** (Common Language Runtime), i zawiera referencje do faktycznie utworzonych obiektów na stercie,
* na **sterta (Heap)** &#8211;  zarządzaniem zajmuje się GC.

Śmietnik działa  bardzo sprytnie, w pierwszej fazie (**Mark**) znakuje obiekty jakie są używane -> istnieją powiązane z obiektem referencje (**Stack -> Heap**{:.color_1}),  po czym  zaznacza je.

Tak oznaczone obiekty nie zostaną usunięte w fazie drugiej (**Sweep**).
    
**Tym sposobem dochodzimy do nazwy stosowanego w GC algorytmu -> Mark & Sweep.**{: .highlight-1}

Aplikacje składają  się z wielu obiektów, i proces czyszczenia może trwać dość długo, zależnie od ilości obiektów. Dlatego nie jest on często uruchamiany.

 Automatyczne wyzwoleni **GC** następuje w sytuacji gdy zostanie przekroczony pewien zakres pamięci.

## Generacje

**GC** kategoryzuje obiekty według ich wieku powstania, tym samym przydzielane są do odpowiednich pokoleń oznaczanych odpowiednio **0, 1, 2**.

Zmiana pokolenia następuje podczas uruchomienia **GC**, awans w pokoleniu następuje gdy obiekt nie nadaje się do zniszczenia.

[![Garbage Collector][image2]][image2-big]{:.post-left-image}
Jeżeli obiekt jest potrzebny i są do niego powiązane referencje ze stosu na stertę to wówczas jest on ważny i podbijana jest jego ranka od 0 do 2.

Do generacji przydzielany jest budżet, dla 0 przyjmuje się wielkość **256 KB**, w przypadku przekroczenia podczas  alokowanie nowego obiektu następuje uruchomienie czyszczenia na generacji 0, w tym czasie istnieje duża szansa, iż część obiektów nadaje się do zniszczenia lub awansu na wyższe pokolenie.

Po przeczyszczeniu następuje ponowna próba alokacji jeżeli się nie powiedzie to automatycznie obiekt awansuje do wyższej generacji.

Generacja zerowa jest miejscem gdzie obiekty są najczęściej tworzone i niszczone, dlatego też jej wielkość **256 KB**, jest obszarem, który powinien z łatwością zmieścić się w pamięci  **L2 &#8211; cache procesora**.

**C.D.N.**

{% include_relative dsp.md %}

[post]:  /assets/images/2017/05/wysypisko-smieci/post.jpg
[post-big]:  /assets/images/2017/05/wysypisko-smieci/post.jpg

[image1]: /assets/images/2017/05/wysypisko-smieci/image1.jpg
[image1-big]: /assets/images/2017/05/wysypisko-smieci/image1-big.jpg

[image2]: /assets/images/2017/05/wysypisko-smieci/image2.jpg
[image2-big]: assets/images/2017/05/wysypisko-smieci/image2-big.jpg