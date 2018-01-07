---
title: Domain-Driven Design - Język Wszechobecny.
date: 2017-07-17T20:25:14+00:00
author: Krzysztof Owsiany
layout: post
permalink: domain-driven-design-jezyk-wszechobecny
published: true
comments: true
image: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/post.jpg
categories:
  - Domain-Driven Design
  - Programowanie
tags:
  - DDD
  - Domain Model
  - Domain-Driven Design
  - Język Wszechobecny
  - Model Domeny
  - Model Dziedziny
  - Ubiquitous Language

short: Odwiecznym problemem jaki napotykają na swojej drodze dwie ścierające się siły. Zlecający vs wykonawca. Wzajemna komunikacji vs zrozumienie. Problem narasta gdy obie persony obracają się w odseparowanych środowiskach.
---
{% include_relative preface.md %}

## Wstęp
[![Domain-Driven Design][post]][post-big]{:.post-left-image}
Odwiecznym problemem jaki napotykają na swojej drodze dwie ścierające się siły: zlecający i wykonawca, jest wzajemna komunikacji i zrozumienie. Problem narasta gdy obie persony obracają się w odseparowanych środowiskach. Przykładem takiej sytuacji jest klient (**Ekspert Domenowy**, eng. **Domain Expert**) definiujący wymagania aplikacji i wykonawca (np.: zespół programistów, programista).

Dobrym przykładem takiej sytuacji jest często komunikacja pomiędzy kobietą i mężczyzną wprowadzająca zamęt, poprzez niejednoznaczne rozumienie wypowiadanych słów.
    
Specyfika obszarów zainteresowania zawodowego obu osób przeważnie jest tak odległa, iż wzajemne zrozumienie/przekazanie specyfikacji produktu do wykonania skutkuje powstaniem wielu nieścisłości i zgrzytów. Obie osoby zazwyczaj rozmawiają z wykorzystaniem odmiennych zestawów definicji nie mających ze sobą zbyt wiele wspólnego.
    
## Język Wszechobecny (eng. Ubiquitous Language)

Z pomocą przychodzi metoda wytwarzania oprogramowania **[Domain-Driven Design][ddd-wstep]**

Otóż nie jest to jedynie architektura. Zawiera w sobie wiele definicji co do kultury pracy w projekcie zarówno od strony definiującego/weryfikującego wymagania. a także ich realizatora.

[![Domain-Driven Design - Ubiquitous Language][image1]][image1-big]{:.post-right-image}

Jednym z jej aspektów jest wykreowanie tak zwanego **Języka Wszechobecnego** (eng. **Ubiquitous Language**), zmieniającego sposób komunikacji pomiędzy osobą wymagającą, a realizującą. Wprowadza wspólnie ustalony zestaw słów/definicji  w formie żargonu. Tym samym podnosi się jakość wzajemnej komunikacji poprzez zrozumienie istoty wymagań i problemów jakie zaistnieją w trakcie realizacji projektu.

Opracowanie słownictwa **Języka Wszechobecnego** poprzez wspólną analizę dziedziny i dojście  do konsensusu nazewnictwa poszczególnych elementów, pozytywnie wpływa  na współpracę i kulturę pracy  w zespole.

[![Ubiquitous Language][image2]][image2-big]{:.post-left-image}
      
Słownictwo języka wszechobecnego powinno bazować na **Modelu Domeny** (eng. **Domain Model**). Skutkuje to wykorzystaniem zdefiniowanych pojęć, w każdym aspekcie projektu. Od modelowania klas po dokumentację i komunikację dotyczącą projektu. Zespół powinien weryfikować wprowadzone pojęcia w celu eliminacji błędnych sformułowań. Dobrą praktyką jest wypowiadanie pojęć na głos, łatwiej będzie wówczas wyłapać dziwne sformułowania.    

**Język Wszechobecny** (eng. **Ubiquitous Language**) jest ściśle związany z **Modelem Domeny/Dziedziny** (eng. **Domain Model**), dlatego wprowadzanie zmian w żargonie niesie ze sobą potrzebę zmiany modelu i odwrotnie

Projektując i budując aplikację często napotykamy na problemy związane z  określeniem punktu wspólnego tematyki jakiej poruszał projekt.  W pewnym sensie także nazewnictwo zostało narzucone przez przełożonych bądź w przeciwną stronę.

    
**Nadmieniam, tutaj iż głoszę swój osobisty punkt widzenia i sposób prezentacji wiedzy. A jako że nie jestem nieomylny, to mogą i zapewne będą zdarzać się błędy...**
    
{% include_relative books.md %}

---
Wcześniejszy artykuł: **[Domain-Driven Design - Wstęp.][previous]**

Następny artykuł: **[Domain-Driven Design - Izolacja przy pomocy warstw.][next]**

---
[previous]: {{site.url}}/domain-driven-design-wstep
[next]: {{site.url}}/domain-driven-design-izolacja-przy-pomocy-warstw

[ddd-wstep]: {{site.url}}/domain-driven-design-wstep

[post]: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/post.jpg
[post-big]: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/post-big.jpg

[image1]: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/image1.png
[image1-big]: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/image1-big.png

[image2]: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/image2.jpg
[image2-big]: /assets/images/2017/07/domain-driven-design-jezyk-wszechobecny/image2-big.jpg