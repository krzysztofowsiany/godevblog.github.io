---
title: Domain-Driven Design - Izolacja przy pomocy warstw.
date: 2017-07-24T16:50:49+00:00
author: Krzysztof Owsiany
layout: post
permalink: domain-driven-design-izolacja-przy-pomocy-warstw
published: true
comments: true
image: /assets/images/2017/07/domain-driven-design-izolacja-przy-pomocy-warstw/post.jpg
categories:
  - Domain-Driven Design
  - Programowanie
tags:
  - DDD
  - Domain-Driven Design
  - high-cohesion
  - loose-coupling

short: Poprawne modelowanie dziedziny skutkuje bezwzględnym wymaganiem dotyczą jej izolacji od reszty systemu. Z pomocą przychodzi architektura warstwowa wyodrębniająca z aplikacji spójne ze sobą pod względem działania obszary. Zebrane w ten sposób funkcjonalności są składowymi warstw.
---
{% include_relative preface.md %}

## Wstęp
[![loose-coupling][post]][post-big]{:.post-left-image}
Poprawne modelowanie dziedziny skutkuje bezwzględnym wymaganiem dotyczą jej izolacji od reszty systemu. Z pomocą przychodzi architektura warstwowa wyodrębniająca z aplikacji spójne ze sobą pod względem działania obszary. Zebrane w ten sposób funkcjonalności są składowymi warstw. Przy czym bazowy zestaw warstw został zdefiniowany i zawiera:

* **interfejsu Użytkownika** (ang. **User Interface**) - warstwa ta odpowiedzialna jest za kontakt ze światem zewnętrznym. Służy obsłudze funkcjonalności aplikacji przez użytkownika. Oczywiście warstwa ta może także być w formie **API** (**Application Programming Interface**). Czyli usługi udostępnionej innym aplikacjom, Np. **WebSerwisy**, **WebSockety**. Warstwa **Interfejsu  Użytkownika** korzysta z publicznych interfejsów upublicznionych w warstwach niższego rzędu.    
* **Aplikacji** (ang. **Application**) - jest to warstwa pośrednicząca między warstwą interfejsu, a warstwą dziedziny, wszelkie operacje deleguje do warstwy domeny, sama może posiadać stan jednak nie posiada logiki biznesowej. Jest niezbędna gdyż zarządza zadaniami jakie są zlecane z warstwy użytkownika do aplikacji. Tak jak warstwa **Interfejsu Użytkownika** posiada dostęp do warstw niższego rzędu.
[![Architektura warstwowa][image1-big]][image1-big]{:.post-center-image}
* **Dziedziny/Modelu** (ang. **Domain**) - warstwa gdzie implementujemy **Logikę Biznesową** (ang. **Bussines  Logic**). Dostarcza najbardziej wartościową funkcjonalność (**wartość biznesową**), jest rdzeniem aplikacji. Korzysta z warstwy niżej (**infrastruktury**) w charakterze magazynu danych. Powinna zawierać w sobie implementację głównej funkcjonalności programu. Dzięki separacji od działań związanych ze środowiskiem w jakim uruchamiana jest aplikacja. Dużo łatwiej jest testować działanie warstwy, a także przenosić czystą formę algorytmów ustaloną z **Ekspertem Domenowym** (ang. **Domain  Expert**).
* **Infrastruktury** (ang. **Infrastructure**) - jest to warstwa służąca do kontaktu z systemem w jakim uruchamiany jest program. Pośredniczy w korzystaniu z funkcji systemowych/usług zewnętrznych, np.:: baza danych, zapis do plików, dostęp do urządzeń zewnętrznych, zdalnych usług. Jak sama nazwa wskazuje cała infrastruktura jaka znajduje się w środowisku uruchomieniowym programu. Świadczy usługi na  rzecz warstw wyższego rzędu.

Każda z wymienionych warstw izoluje specyficzną dla siebie funkcjonalność. Pozwoliło to nie tylko odseparować **Model Dziedziny** (ang. **Domain Model**), co także uporządkować składowe elementy aplikacji.

Warstwy powinny być zależne jedynie od warstwy niższej, jednocześnie luźno powiązane z warstwami wyżej.
[![high-cohesion][image2]][image2-big]{:.post-left-image}
    
Oznacza to, iż aplikacja cechuje się: dużą spójnością (ang. **high-cohesion**), słabym związaniem (ang. **loose-coupling**).

Jakie zachodzi pomiędzy: warstwami, interfejsami, obiektami. 
    

Zależnie od złożoności systemu, istnieje możliwość dodania kolejnych warstw w celu większego rozproszenia funkcjonalności. Należy jednak pamiętać iż, w sytuacji nadmiernego przyrostu ilości warstw rośnie także złożoność aplikacji. Ta sytuacja z kolei utrudnia utrzymanie aplikacji.

Architekturę warstwową opisywałem także w poście: **[Architektura cebuli][onion]**.
    
Oczywiście nie są to wszystkie możliwe sposoby na wyizolowanie **Modelu Dziedziny** (ang. **Domain Model**)  w aplikacji…
  
**Nadmieniam, tutaj iż głoszę swój osobisty punkt widzenia i sposób prezentacji wiedzy. A jako że nie jestem nieomylny, to mogą i zapewne będą zdarzać się błędy...**


{% include_relative books.md %}

---
Wcześniejszy artykuł: **[Domain-Driven Design - Izolacja przy pomocy warstw.][previous]**

Następny artykuł: **[Domain-Driven Design - Podstawowe części składowe.][next]**

---
[previous]: {{site.url}}/domain-driven-design-izolacja-przy-pomocy-warstw
[next]: {{site.url}}/domain-driven-design-podstawowe-czesci-skladowe

[onion]: {{site.url}}/architektura-cebuli

[post]: /assets/images/2017/07/domain-driven-design-izolacja-przy-pomocy-warstw/post.jpg
[post-big]: /assets/images/2017/07/domain-driven-design-izolacja-przy-pomocy-warstw/post-big.jpg

[image1-big]: /assets/images/2017/07/domain-driven-design-izolacja-przy-pomocy-warstw/image1-big.png

[image2]: /assets/images/2017/07/domain-driven-design-izolacja-przy-pomocy-warstw/image2.jpg
[image2-big]: /assets/images/2017/07/domain-driven-design-izolacja-przy-pomocy-warstw/image2-big.jpg