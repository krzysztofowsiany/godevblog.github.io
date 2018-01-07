---
title: Domain-Driven Design - &#8222;Nadejszła wiekopomna chłiła&#8221;.
date: 2017-11-13T23:40:24+00:00
author: Krzysztof Owsiany
layout: post
permalink: domain-driven-design-nadejszla-wiekopomna-chliala
published: true
image: /assets/images/2017/11/domain-driven-design-nadejszla-wiekopomna-chliala/post.jpg
categories:
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
{% include_relative preface.md %}

## Wstęp
[![Domain-Driven Design][post]][post-big]{:.post-left-image}
Długo tutaj mnie nie było, wiele się działo, zmiana pracy, konferencje, wyjazdy. Blog-abstynencja.

Liznąwszy nieco wiedzy na temat **[Domain-Driven Design][ddd]**, pora wrzucić jakiegoś kota do wora:

## O projekcie
Chwilami rozmyślałem na temat projektu, jaki chciałbym zmaltretować. Wyszło przy tym kilka ciekawych pomysłów. Jednak do realizacji podejmę się projektu prostego, rozwiązującego mój mały problemik.
    
Nie lubię np. tracić czasu na takie działanie jak:

* odpalanie gita w konkretnej lokalizacji,
* otwieranie folderu projektu,
* otwieranie konkretnych plików, np. z dokumentacją,
* wchodzenie na konkretne strony internetowe,
* otwieranie terminala w oknie (także z uprawnieniami admina).
    
Dodatkowo fajnie by było jak bym jednym kliknięciem miał od razu uruchomione wszystko co potrzebuję do pracy.
Przykładowo:

1. Otwarty edytor **Visual Studio Code** z projektem.
2. Otwarta konsola **GIT** dla tego projektu.
3. Folder projektu.
4. Przeglądarki (Firefox, Chrome, Edge, Opera do testowania frontendu).

pka siedziałaby sobie cicho w Tray-u, aż ją wyciągnę za oszywę do roboty.

Chciałbym oczywiście mieć możliwość definiowania w prosty sposób profili uruchomienia oraz samych wyzwalaczy.

Fajno by też było jak by konfiguracja była archiwizowana (najlepiej gdzieś hen daleko). Tak by nie stracić w razie awarii systemu.
[![Domain Expert][image1]][image1-big]{:.post-right-image}
Cele dla stworzenia **MVP** aplikacji:
1. Jak najszybciej dodać wyzwalacz.
2. Wiele typów wyzwalaczy.
3. Jak najszybciej wywołać wyzwalacz.
4. Łatwy dostęp do: wyzwalaczy, konfiguracji i profili.
5. Prostota i szybkość tutaj jest najważniejsza.
6. Automatyczne kopie bezpieczeństwa.
7. Przywracanie z kopii.
8. Kopie w chmurze: dropbox, google drive, onedrive.

Pomyślałem, że w ramach projektu **[DDD][ddd]**, stworzę sobie właśnie taki sofcik.

Tym samym stałem się Ekspertem Domenowym (ang. **Domain Expert**).

## Technologia
   
Co do technologii, jako że apka ma działać na Windozie, to skorzystam z języka **C# + WPF**. Oprócz tego zapewne znajdzie się wiele przydatnych bibliotek do logowania, konteneryzacji, **MVVM**.
Aplikacja zbudowana zostanie z wykorzystaniem **[Onion Architecturę][onion]**, tak by wyodrębnić **[warstwę biznesową][ddd-layer]**

Jako młody adept szkolenia przeprowadzonego przez **[Macieja Aniserowicza][procent]** dotyczącego **Testowania Automatycznego**. Nie omieszkam ich tutaj zastosować.
    
Kod wrzuci się na **[GitHub-a][mygithub]**, może ktoś wykona **Code Review**.

{% include_relative books.md %}

---
Wcześniejszy artykuł: **[Domain-Driven Design - DDD i jego życie.][previous]**

---
[previous]: {{site.url}}/ddd-i-jego-zycie


[ddd]: {{site.url}}/domain-driven-design-wstep
[onion]: {{site.url}}/architektura-cebuli
[ddd-layer]: {{site.url}}/domain-driven-design-izolacja-przy-pomocy
[procent]: http://devstyle.pl
[mygithub]: https://github.com/krzysztofowsiany


[post]: /assets/images/2017/11/domain-driven-design-nadejszla-wiekopomna-chliala/post.jpg
[post-big]: /assets/images/2017/11/domain-driven-design-nadejszla-wiekopomna-chliala/post-big.jpg

[image1]: /assets/images/2017/11/domain-driven-design-nadejszla-wiekopomna-chliala/image1.jpg
[image1-big]: /assets/images/2017/11/domain-driven-design-nadejszla-wiekopomna-chliala/image1-big.jpg