---

title: 'Domain-Driven Development &#8211; &#8222;nadejszła wiekopomna chłiła&#8221;'
date: 2017-11-13T23:40:24+00:00
author: Krzysztof Owsiany
layout: post

permalink: /domain-driven-design-nadejszla-wiekopomna-chliala/
published: false

image: /assets/images/2017/11/blogging-photo-3271.jpg
categories:
  - Bez kategorii
  - Domain-Driven Design
tags:
  - Code Review
  - DDD
  - Domain Expert
  - Domain Model
  - Domain-Driven Design
  - GIT
  - GitHub
  - MVVM
  - Visual Studio Code
short: Chwilami rozmyślałem na temat projektu, jaki chciałbym zmaltretować. Wyszło przy tym kilka ciekawych pomysłów. Jednak do realizacji podejmę się projektu prostego, rozwiązującego mój mały problemik.
---
Długo tutaj mnie nie było, wiele się działo, zmiana pracy, konferencje, wyjazdy. Blog-abstynencja.
    
Chwilami rozmyślałem na temat projektu, jaki chciałbym zmaltretować. Wyszło przy tym kilka ciekawych pomysłów. Jednak do realizacji podejmę się projektu prostego, rozwiązującego mój mały problemik.
    
Nie lubię np. tracić czasu na takie działanie jak:

[![Domain Expert][image1]][image1-big]{:.post-right-image}
      
Liznąwszy nieco wiedzy na temat **[Domain-Driven Design][ddd]**, pora wrzucić jakiegoś kota do wora:

* odpalanie gita w konkretnej lokalizacji,
* otwieranie folderu projektu,
* otwieranie konkretnych plików, np. z dokumentacją,
* wchodzenie na konkretne strony internetowe,
* otwieranie terminala w oknie (także z uprawnieniami admina).
    
Dodatkowo fajnie by było jak bym jednym kliknięciem miał od razu uruchomione wszystko co potrzebuję do pracy.

Przykładowo:
* Otwarty edytor **Visual Studio Code** z projektem.
* Otwarta konsola **GIT** dla tego projektu.
* Folder projektu.
* Przeglądarki (Firefox, Chrome, Edge, Opera do testowania frontendu).

pka siedziałaby sobie cicho w Tray-u, aż ją wyciągnę za oszywę do roboty.

Chciałbym oczywiście mieć możliwość definiowania w prosty sposób profili uruchomienia oraz samych wyzwalaczy.

Fajno by też było jak by konfiguracja była archiwizowana (najlepiej gdzieś hen daleko). Tak by nie stracić w razie awarii systemu.

Cele dla stworzenia **MVP** aplikacji:
* Jak najszybciej dodać wyzwalacz.
* Wiele typów wyzwalaczy.
* Jak najszybciej wywołać wyzwalacz.
* Łatwy dostęp do: wyzwalaczy, konfiguracji i profili.
* Prostota i szybkość tutaj jest najważniejsza.
* Automatyczne kopie bezpieczeństwa.
* Przywracanie z kopii.
* Kopie w chmurze: dropbox, google drive, onedrive.

Pomyślałem, że w ramach projektu **[DDD][ddd]**, stworzę sobie właśnie taki sofcik.

Tym samym stałem się Ekspertem Domenowym (ang. **Domain Expert**)…

## Technologia
   
Co do technologii, jako że apka ma działać na Windozie, to skorzystam z języka **C# + WPF**. Oprócz tego zapewne znajdzie się wiele przydatnych bibliotek do logowania, konteneryzacji, **MVVM**.
Aplikacja zbudowana zostanie z wykorzystaniem **[Onion Architecturę][onion]**, tak by wyodrębnić **[warstwę biznesową][ddd-layer]**

Jako młody adept szkolenia przeprowadzonego przez **[Macieja Aniserowicza][procent]** dotyczącego **Testowania Automatycznego**. Nie omieszkam ich tutaj zastosować.
    
Kod wrzuci się na **[GitHub-a][mygithub]**, może ktoś wykona **Code Review**.

{% include_relative books.md %}

[ddd]: {{site.url}}/domain-driven-design-wstep
[onion]: {{site.url}}/architektura-cebuli
[ddd-layer]: {{site.url}}/domain-driven-design-izolacja-przy-pomocy
[procent]: http://devstyle.pl
[mygithub]: https://github.com/krzysztofowsiany

[image1]: /assets/images/2017/11/blogging-photo-9818-200x300.jpg
[image1-big]: /assets/images/2017/11/blogging-photo-9818.jpg