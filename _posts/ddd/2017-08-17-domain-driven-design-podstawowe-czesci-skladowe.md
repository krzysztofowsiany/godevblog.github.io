---
title: Domain-Driven Design - Podstawowe części składowe.
date: 2017-08-17T08:16:00+00:00
author: Krzysztof Owsiany
layout: post
permalink: domain-driven-design-podstawowe-czesci-skladowe
published: true
comments: true
image: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/post.jpg
categories:
  - Domain-Driven Design
  - Programowanie
tags:
  - Asocjacje
  - Associations
  - DDD
  - Domain Model
  - Domain-Driven Design
  - Encje
  - Entity
  - high-cohesion
  - loose-coupling
  - Obiekty Wartości
  - Pakiety
  - Services
  - Usługi
  - Value Obiect
short: Do budowy Modelu Dziedziny (ang. Domain Model), wykorzystujemy kilka bazowych składowych powiązanych ze sobą relacjami.
---
{% include_relative preface.md %}

## Wstęp
Do budowy **Modelu Dziedziny** (ang. **Domain Model**), wykorzystujemy kilka bazowych składowych powiązanych ze sobą relacjami.
    
## Asocjacje (ang. associations)
[![Asocjacje (ang. associations)][post]][post-big]{:.post-left-image}
Asocjacja to swoista abstrakcja stanowiąca o związku pomiędzy bytami wchodzącymi w skład **Modelu Dziedziny** (ang. **Domain Model**), jaką twórca uznał za odpowiednią.

O czym należy pamiętać tworząc asocjacje:
* eliminacja zbędnych, im więcej tym model jest bardziej skomplikowany,
* unikanie asocjacji wiele do wiele (unikniemy wielokrotnych relacji),
* określenie kierunku,
* stosowanie kwalifikatorów - skutkuje uproszczeniem relacji w **Modelu Dziedziny** (ang. **Domain Model**).
    
**Kwantyfikatory** - ograniczają kierunek interpretacji **asocjacji** (ang. **associations**).
    
## Encje (ang. entity)
[![Encje (ang. entity)][image1]][image1-big]{:.post-right-image}
Encje określane są także jako **Obiekty Referencyjne** (ang. **Reference Objects)**.
    
Obiekty tego typu muszą być jednoznacznie identyfikowane w **Modelu Dziedziny** (ang. **Domain Model**), posiadają swoją tożsamość niezmienną w czasie.

Powoduje to, iż można owe obiekty porównywać ze sobą w sytuacji gdy atrybuty nie stanowiące o tożsamości obiektu.

**Encja** (ang. **entity**) powinna zawierać w sobie atrybuty związane z tożsamością obiektu, pozwalające na jej porównywanie z innymi bądź wyszukiwanie. Dlatego zależą od kontekstu zachowania obiektu.
    
W sytuacji gdy atrybuty nie identyfikują jednoznacznie obiektu w **Modelu Dziedziny** (ang. **Domain Model**), wprowadza się sztuczne identyfikatory.
    
## Obiekty wartości (ang. value object)
[![Obiekty wartości (ang. value object)][image2]][image2-big]{:.post-left-image}
Obiekty tego typu nie posiadają tożsamości służą przede wszystkim do opisywania rzeczy (określają aspekt dziedziny). Najważniejsze są atrybuty obiektu, a nie tożsamość.

Można zadać pytanie po co mieszać i stosować i **encję** (ang. **entity**) i **obiekty wartości** (ang. **value objects**)?    

A no po to by uprościć sam **Model Dziedziny** (ang. **Domain Model**).

Obiekty bez atrybutów określających ich jednoznaczną identyfikację są łatwiejsze w utrzymaniu. W przeważającej ilości sytuacji nie zachodzi potrzeba zmiany **obiektu wartości** (ang. **value object**). Jednak gdy taka potrzeba występuje to wówczas nie ma możliwości współdzielenia obiekt.
    
Dodatkowo brak tożsamości powoduje brak potrzeby przejmowania się instancjami obiektu, to upraszcza i pozwala na wiele optymalizacji **Modelu Dziedziny** (ang. **Domain Model**).

Sytuacje gdy zmiana **obiektu wartości** (ang. **value object**) jest dopuszczalna:

* gdy tworzenie/usuwanie obiektu będzie kosztowne dla aplikacji,
* gdy obiekt jest często modyfikowany,
* gdy obiekty nie są często współdzielone (najlepiej wcale),
* gdy modyfikacja obiektu wpływały by na spójność **Modelu Dziedziny** (ang. **Domain Model**).
    
**Dobrą praktyką jest konstruowanie obiektów wartości w formie niezmiennej (immutable).**
    
## Usługi (ang. service)
[![Usługi (ang. service)][image3]][image3-big]{:.post-right-image}     
Nie wszystkie składowe elementy **Modelu Dziedziny** (ang. **Domain Model**), opierają się na przechowywaniu wartości, niekiedy zachodzi potrzeba wyodrębnienia operacji. Nie zawierają one żadnego stanu, nie przechowują wartości, a jedynie świadczą działanie. W tej sytuacji można mówić o **usługach** (ang. **services**).

**Usługi** (ang. **service**) są zdefiniowane wyłącznie w kontekście operacji jakie świadczą dla swojego klienta. Są kontraktem zawierającym abstrakcyjne zamierzenia pewnego działania.

Cechy poprawnej **usługi** (ang. **service**):
* odwołują się do **Modelu Dziedziny** (ang. **Domain Model**), jednak nie wchodzą jako część ani **encji** (ang. **entity**), ani też **obiektu wartości** (ang. **value object**),
* wykonywane operacje są bezstanowe - nie przechowujemy wartości w **usłudze** (ang. **service**),
* kontrakt **usługi** (ang. **service**), jest określany przez **Model Dziedziny** (ang. **Domain Model**).

Nazewnictwo **usług** (ang. **service**), opierać się powinno na **Języku Wszechobecnym** (ang. **Ubiquitous Language**).
    
## Moduły/Pakiety (ang. modules)
[![Moduły/Pakiety (ang. modules)][image4]][image4-big]{:.post-left-image}   
Projektowanie **Modelu Dziedziny** (ang. **Domain  Model**) nie jest pozbawione problemów wynikających z nadmiernego rozrastania. W celu uproszczenia i łatwiejszego zrozumienia istoty modelu należy wprowadzić podział na moduły.

Przy podziale należy pamiętać, że: **nie kod jest wydzielany do modułów (ang. modules), a pojęcia dziedziny!**{:.color_1}

Wydzielane **moduły** (ang. **modules**), powinny być:
* luźno ze sobą powiązane (ang. **loose &#8211; coupling**),
* zachować dużą spójność (ang. **high &#8211; cohesion**).
    
Rozdzielenie **modułów** (ang. **modules**), można odnieść do budowy książki. Gdzie **Model Dziedziny** (ang. **Domain Model**), traktujemy jako treść pewnej opowiadanej historii, natomiast **moduły** (ang. **modules**) odzwierciedlają rozdziały.

**Moduły** (ang. **modules**), poprzez swe nazwy zawarte także w **Języku Wszechobecnym** (ang. **Ubiquitous Language**). Powinny stanowić wiedzę dziedzinową.

W raz z rozrostem/rozwojem **Modelu Dziedziny** (ang. **Domain Model**), zachodzi potrzeba refaktoryzacji **modułów** (ang. **modules**). Jednak proces ten może niekiedy powodować dość duże zmiany w kodzie.

Tym samym istnieje ryzyko powstania bałaganu w systemie kontroli wersji oraz konflikty między programistami.<

Częściowym rozwiązaniem problemu jest planowanie/przewidywanie  struktury **modułów** (ang. **modules**). Programiści starają się przewidzieć przed stworzeniem pozostałych części modelu.    

Błędnie zdefiniowane **moduły** (ang. **modules**), powinny zostać poprawione, gdyż brak reakcji będzie powodował nasilenie się problemu w przyszłości.
    
## Na koniec

Budowanie **Modelu Dziedziny** (ang. **Domain Model**), nie jest  sprawą  łatwą i wymaga zmiany sposobu myślenia podczas planowania. Widzę na  swoim przykładzie z jakim trudem przychodzi zrozumienie istoty **Domain-Driven Design**.

Powyższe składowe  elementy, stanowią podstawowe konstrukty jakie powinno się wykorzystywać w procesie tworzenia **Logiki Biznesowej** (ang. **Business Logic**) w tworzonych aplikacjach opartych na **Domain-Driven Design**.

Oczywiście nie jest to wyczerpanie tematu i zachęcam do wielokrotnego zgłębiania wiedzy na ten temat.
    
{% include_relative books.md %}

---
Wcześniejszy artykuł: **[Domain-Driven Design - Izolacja przy pomocy warstw.][previous]**

Następny artykuł: **[Domain-Driven Design - DDD i jego życie.][next]**

---
[previous]: {{site.url}}/domain-driven-design-izolacja-przy-pomocy-warstw
[next]: {{site.url}}/ddd-i-jego-zycie

[post]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/post.jpg
[post-big]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/post-big.jpg

[image1]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image1.jpg
[image1-big]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image1-big.jpg

[image2]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image2.jpg
[image2-big]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image2-big.jpg

[image3]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image3.jpg
[image3-big]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image3-big.jpg

[image4]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image4.jpg
[image4-big]: /assets/images/2017/08/domain-driven-design-podstawowe-czesci-skladowe/image4-big.jpg