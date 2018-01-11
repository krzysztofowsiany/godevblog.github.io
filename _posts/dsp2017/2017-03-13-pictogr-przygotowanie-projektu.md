---
title: PictOgr - przygotowanie projektu.
date: 2017-03-13T19:54:02+00:00
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-przygotowanie-projektu
image: /assets/images/2017/03/pictogr-przygotowanie-projektu/post.jpg
categories:
  - Daj Się Poznać 2017
  - Fotografia
tags:
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
short: Najsam przód trzeba by sobie przygotować projekcik, dlatego raz dwa + nazwa i VS wygenerował mi się WPFik. Następnie fajnie byłoby kontrolować wersje kiedy i jak pasuje kod. 
---

## Repo
Najsam przód trzeba by sobie przygotować projekcik, dlatego raz dwa + nazwa i VS wygenerował mi się WPFik. Następnie fajnie byłoby kontrolować wersje kiedy i jak pasuje kod.

W katalożku **[PictOgr-a][pictogr-idea]** odpalam basha i frunę:
* wydaję sobie komende **git init**,
* dopinam GitHuba **git remote add origin https://github.com/krzysztofowsiany/pictogr**,
* zaciągam GitHubem wklepując **git fetch**,
* i cacy.

[![PictOgr - przygotowanie projektu][image1]][github-pictogr]
    
Moja robota w drzewie git:
* **master->dev**,
* **dev**-ka rozwijam sobie na bieżąco rozwijając taski w pod gałązkach, jak mi wpadnie do głowy potrzeba wydania wersji to wrzucam sobie w **master**.
    
Po powrocie do przyszłości może się też pojawić gałązka **testing**, tj. **maser->testing->dev**.

Potem już tylko podpinanie pliczków, ignorowanie i integracja z repo.

## Zabawa w bibliotekarza
[PictOgr-a][pictogr-idea] potrzebuje wsparcia, trzeba było udać się do biblioteki i godzinami studiować zawartość.
    
Ale udało się wyłuskać kilka pozycji obowiązkowych w miejscu o nazwie &#8222;**Package Manager Console**&#8221;.

### Dla projektu kilka &#8222;książek&#8221; z biblioteki:
* **AutoFac** - kontenerek na obiekty, (**Install-Package Autofac, [Autofac]**),
* **LiteDb** - bazka dla nieznających S-kuela, (**Install-Package LiteDb, [LiteDb]**),
* **log4net** - zapis popełnionych błędów i innych informacji, (**Install-Package log4net, [log4net]**),
* **photo.exif** - czytanie nagłówka EXIF z pliczków graficznych, (**Install-Package photo.exif, [photo.exif]**).
    
### Do teścików będę potrzebował poniższego zestawu:
* **FakeItEasy** - do udawania obiektów w testach, (**Install-Package FakeItEasy, [FakeItEasy]**),
* **xUnit** - baza do teścików, dodatkowo VS wymaga runnera, (**Install-Package xUnit, [xUnit]**), 
* **Shouldly** - upiększone asercje w oparciu o Fluent Pattern, (**Install-Package Shouldly, [Shouldly]**).
    
To tyle na chwilę obecną, w trakcie rozwoju, zapewne dojdą kolejne biblioteczki.

## Testowanie Ogra
![Testowanie][image2]
Testować trzeba dużo, a w zasadzie szybciej niż się cokolwiek zrobi. Słaby jestem w tym chciałbym to zmienić.Dlatego przeznaczę cały project na to ;).
    
Będzie się zwał **PictOgr.Tests** i całe mięsko tam będzie się znajdować.
    
Nie jestem Krzysztof Kolumb (choć Krzysztof) i hameryki nie odkryję na nowo, chcę się tego nauczyć, a to jest dobry pomysł, a i ludzie będą paczeć na mój kod.


**Ty! Pacz!**{:.tdd-green}
**Nie ma testów!**{:.tdd-red}
**HA!**{:.tdd-green}
**HA!**{:.tdd-red}
**HA!**{:.tdd-green}
**Co za burak!**{:.tdd-red}
**HA!**{:.tdd-green}
**HA!**{:.tdd-red}
**HA!**{:.tdd-green}
      
## Struktura Ogra
[![Struktura Ogra][image3]][image3-big]{:.post-left-image}
Początkowo słaba ta strukturka tylko 3 projekciki. A toteż mało czasu człowiek ma tylko 24h i projekt mozolnie pcha się do przodu jak ślimak.
    
Jak to dobrze, że jestem devem i mam 48h na dobę.

**PictOgr** - główny projekt, WPFki podstawowego widoku.
**PictOgr.Core** - przydatne zestawy funkcji, jak pobieranie mięcha dla kontenera **AutoFac**.
**PictOgr.Tests** - testy, testy, moje testy aplikacji nic po za tym.

## I the End
Pokusiłem się o implementację:
* **CQRS**,
* **AutoFac**,
* **Testów**.
    
Jest to kod rozwojowy i jak się rozwinie to wówczas będzie czas na post.

Ale to w kolejnym skrobaniu tekstu na &#8222;Daj Się Poznać 2017&#8221;.
    
{% include_relative dsp.md %}

[github-pictogr]: https://github.com/krzysztofowsiany/pictogr
[pictogr-idea]: {{site.url}}/pictogr-pomysl

[Shouldly]: http://docs.shouldly-lib.net
[Autofac]: https://autofac.org
[LiteDb]: http://www.litedb.org
[FakeItEasy]: https://fakeiteasy.github.io
[log4net]: https://logging.apache.org/log4net
[photo.exif]: https://github.com/fraxedas/photo
[xUnit]: https://xunit.github.io

[post]: /assets/images/2017/03/pictogr-przygotowanie-projektu/post.jpg
[post-big]: /assets/images/2017/03/pictogr-przygotowanie-projektu/post-big.jpg

[image1]: /assets/images/2017/03/pictogr-przygotowanie-projektu/image1.jpg

[image2]: /assets/images/2017/03/pictogr-przygotowanie-projektu/image2.jpg

[image3]: /assets/images/2017/03/pictogr-przygotowanie-projektu/image3.png
[image3-big]: /assets/images/2017/03/pictogr-przygotowanie-projektu/image3-big.png