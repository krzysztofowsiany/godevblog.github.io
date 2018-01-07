---
title: Domain-Driven Design - Wstęp.
date: 2017-07-13T10:25:43+00:00
author: Krzysztof Owsiany
layout: post
permalink: domain-driven-design-wstep
published: true
comments: true
image: /assets/images/2017/07/domain-driven-design-wstep/post.jpg
categories:
  - Domain-Driven Design
  - Programowanie
tags:
  - DDD
  - Domain-Driven Design
short: Niniejszym otwieram cykl postów związanych z rozkminianiem architektury wytwarzania oprogramowania o nazwie DDD => Domain-Driven Design. Jest to temat jaki od pewnego czasu dręczy mnie, i chcę rozwinąć swoje zdolności w tym konkretnym obszarze.
---
{% include_relative preface.md %}

## Wstęp
[![Domain-Driven Design][post]][post-big]{:.post-right-image}
Niniejszym otwieram cykl postów związanych z rozkminianiem architektury wytwarzania oprogramowania o nazwie **DDD => Domain-Driven Design**. Jest to temat jaki od pewnego czasu dręczy mnie, i chcę rozwinąć swoje zdolności w tym konkretnym obszarze.

W tym celu zaopatrzyłem się w dwie pozycje:
    
|[![Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym. Eric Evans.][domdri-image]][domdri]{:.book-image}|[Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym. Eric Evans.][domdri]|
|[![DDD dla architektów oprogramowania, Vaughn Vernon.][dddaro-image]][dddaro]{:.book-image}|[DDD dla architektów oprogramowania, Vaughn Vernon.][dddaro]|
    
## Czym jest Domain-Driven Design?
Jest to podejście do budowania aplikacji, w którym zaczynamy od stworzenia tak zwanego **Modelu Domeny** (eng. **Domain Model**). Sam model nie jest niczym innym jak wyodrębnionym głównym zachowaniem aplikacji jaki ma zostać zaimplementowany.
    
Aplikacja zbudowana jest z wielu elementów:
* interfejs użytkownika,
* obsługa wejść/wyjść,
* obsługa bazy danych,
* inne usługi wspierające tworzenie aplikacji.

**Model Domeny/Dziedziny** (eng. **Domain Model**) nie zawiera tego bagażu, to czysta implementacja wartości (**wartość biznesowa**) jaką ma dawać aplikacja. Stworzona w sposób niezależny i łatwa do przetestowania.
     
W celu jej implementacji programista musi rozumieć co jest najważniejszą wartością w oprogramowaniu jakie ma wykonać. Dlatego musi kontaktować się z osobą posiadającą **największą wiedzę** na temat funkcjonalności tworzonej aplikacji. Osoba taka określana jest jako** Ekspert Domenowy  (eng. Domain Expert)**,może to być np. klient.

Często pojawia się problem z wymianą informacji (niejednokrotnie się z nim zetknąłem). Dotyczy problemów językowych występujących w komunikacji pomiędzy programistą, a ekspertem domenowym. Osoby te zazwyczaj wywodzą się z innych środowisk i pojęcia jakimi operują nie są zrozumiałem lub znaczą coś zupełnie innego dla strony przeciwnej.

[![DDD][image1]][image1-big]{:.post-left-image}

Rozwiązaniem problemu jest stosowanie tak zwanego **[języka wszechobecnego (eng. Ubiquitous Language)][unbiquitous]**.
Zawierającego wspólnie wypracowane pojęcia dzięki, którym zarówno ekspert domenowy zrozumie programistę jak i odwrotnie.

Jest to technika trudna, wymagająca w implementacji odpowiedniego projektowania i nakładająca na programistę dodatkowy narzut pracy związany z **klepaniem kodu**.

Do budowy aplikacji opartej o **Domain-Driven Design** wykorzystać można wielowarstwową architekturę aplikacji. W ten sposób model domenowy zostanie wyodrębniony do własnej warstwy.
    
Nadmieniam, tutaj iż głoszę swój osobisty punkt widzenia i sposób prezentacji wiedzy. A jako że nie jestem nieomylny, to mogą i zapewne będą zdarzać się błędy...

----
Następny artykuł: **[Domain-Driven Design - Język Wszechobecny.][next]**

----

[next]: {{site.url}}/domain-driven-design-jezyk-wszechobecny

[unbiquitous]: {{site.url}}/domain-driven-design-jezyk-wszechobecny

[domdri]: http://ebookpoint.pl/view/90752/domdri.htm
[domdri-image]: https://static01.helion.com.pl/global/okladki/326x466/0ec470d7102b93516012ee4849dc3a41,domdri.jpg

[dddaro]: http://ebookpoint.pl/view/90752/dddaro.htm
[dddaro-image]: https://static01.helion.com.pl/global/okladki/326x466/91bb872731d822a7c801afc2b4e9b8cc,dddaro.jpg

[post]: /assets/images/2017/07/domain-driven-design-wstep/post.jpg
[post-big]: /assets/images/2017/07/domain-driven-design-wstep/post-big.jpg

[image1]: /assets/images/2017/07/domain-driven-design-wstep/image1.jpg
[image1-big]: /assets/images/2017/07/domain-driven-design-wstep/image1-big.jpg