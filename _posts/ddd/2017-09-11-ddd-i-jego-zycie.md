---
title: Domain-Driven Design - DDD i jego życie.
date: 2017-09-11T08:47:48+00:00
author: Krzysztof Owsiany
layout: post
permalink: ddd-i-jego-zycie
published: true
image: /assets/images/2017/09/ddd-i-jego-zycie/post.jpg
categories:
  - Domain-Driven Design
tags:
  - Aggregates
  - Agregaty
  - DDD
  - Domain Model
  - Domain-Driven Design
  - Fabryki
  - Factories
  - Repository
  - Repozytoria
short: Domain-Driven Design charakteryzuje komponenty wykorzystywane przy budowie złożonych modelów dziedziny (ang. Domain Model). Jednak owe komponenty wchodzą w skład większego bytu, posiadają swój cykl życia.
---
{% include_relative preface.md %}

## Wstęp

[![Domain-Driven Design][post]][post-big]{:.post-left-image}
Domain-Driven Design charakteryzuje komponenty wykorzystywane przy budowie złożonych modelów dziedziny (ang. **Domain Model**).

Jednak owe komponenty wchodzą w skład większego bytu, posiadają swój cykl życia.

Podobnie jak istota żywa, rodzą się, funkcjonują, umierają i niekiedy pozostawiają po sobie ślad w historii.

W całym tym cyklu życia niezbędne jest wsparcie z zewnątrz. I Tutaj z pomocą przychodzą wzorce:
* agregaty (ang. **aggregates**),
* fabryki (ang. **factories**),
* repozytoria (ang. **repositories**).
    
Stosowanie powyższych wzorców porządkuje modele i tym samym umożliwia łatwiejsze zarządzanie mnogością obiektów.

## Agregaty
[![Domain-Drive Design - Aggregates][image1]][image1-big]{:.post-right-image}

Jest to zbiór powiązanych ze sobą obiektów, dzięki temu można traktować je jako jedna całość (jeden obiekt). Agregat (ang. **aggregate**) zbudowany jest z dwóch części:
* **korzenia** (ang. **Aggregate Root**) &#8211; jedna z encji (ang. **entity**) wchodząca w skład zbioru obiektów,
* **granicy** (ang. **Boundary**) &#8211; definiuje zawartość agregatu, czyli jakie obiekty będą się znajdować w jego obrębie.
    
Agregat (ang. **aggregate**) otacza granicą swoje obiekty. Dostęp do obiektów możliwy jest jedynie w obrębie granicy. Dostęp do agregatu odbywa się poprzez korzeń.

Zmienia się także podejście do tożsamości encji (ang. **entity**). Za wyjątkiem korzenia pozostałe encje muszą posiadać tożsamość ale w obrębie granicy agregatu. Inna sytuacja jest w przypadku korzenia, który to musi identyfikować agregat (ang. **aggregate**) w całym Modelu Domeny (ang. **Domain Model**).
    
Dostęp z poza granicy agregatu jest zabroniony z wykluczeniem korzenia agregatu (ang. **Aggregate Root**).

Jedyną możliwością dostępu do wewnętrznych obiektów agregatu odbywa się poprzez chwilowe przekazanie kopii obiektu.

Jak zbudować agregat?: 1. Wyznaczyć grupę encji/wartości (ang. **entity/value object**). 2. Tym samym wyznaczyć granicę agregatu (ang. **aggregate**). 3. Z encji (ang. **entity**) wybrać jedną odpowiednią do pełnienia roli korzenia agregatu (ang. **Aggregate Root**). 4. Ustanowić dostęp do wewnętrznych obiektów poprzez korzeń.

## Fabryki
[![Domain-Driven Design - Factories][image2]][image2-big]{:.post-left-image}

Kolejny z wzorców dzięki którym, tworzenie rozbudowanych agregatów będzie łatwiejsza i nie pozwoli na ich rozhermetyzowanie to fabryka (ang. **factory**). Fabryka jak sama nazwa wskazuje to obiekt którego, celem jest wytworzenie produktu jaki zamawiamy lub jego odtworzenie. Jest ona ściśle powiązana z konkretnym typem obiektu i jeżeli zachodzi potrzeba przeniesienia odpowiedzialności tworzenia tego obiektu, bez wahania należy to zrobić. Do tworzenia agregatów także należy wykorzystać fabrykę ściśle powiązaną z korzeniem agregatu (ang. **Aggregate Root**).
    
Agregat składa się z wielu encji i obiektów wartości, przy pomocy fabryki upraszczamy tworzenie tych wewnętrznych bytów. Cała logika związana z kreacją znajduje się w klasie fabryki.

Sama konstrukcja fabryki to nic innego jak znane do tej pory wzorce kreacyjne:
* metoda wytwórcza (ang. **factory method**),
* fabryka abstrakcyjna (ang. **abstract factory**),
* budowniczy (ang. **builder**).
    
Jednak w pewnych sytuacjach wykorzystanie fabryki (ang. **factory**) jest nadmiarowe:
* wszystkie atrybuty obiektu są publiczne,
* klasa jest typem,
* tworzenie obiektu jest proste,
* w konstruktorze nie zawiera logiki obiektu,
* konstruktor jest atomowy (wszystkie informacje niezbędne do wykonania obiektu znajdują się w konstruktorze).
    
W przypadku tworzenia obiektów wartości (ang. **value object**) tworzenie obiektów jest prostsze, aniżeli dla encji (ang. **entity**). Wynika to z faktu posiadania przez encje tożsamości. Unikalny identyfikator encji może być wygenerowany przez fabrykę, ale także do niej przekazany. Przekazywanie identyfikatora to przykład użycia fabryki do odtwarzania encji. Nie można generować na nowo, gdyż zmieni się tożsamość (będzie to inna encja). Jak zwykle wszystko zależy od kontekstu bieżącego zastosowania fabryki.
    
## Repozytoria
[![Domain-Driven Design - Repositories][image3]][image3-big]{:.post-right-image}

Wzorzec manipulacji obiektami trwale zachowanymi przy pomocy zaimplementowanych działań w warstwie infrastruktury. Repozytorium (ang. **repository**) to wzorzec hermetyzujacy działania na trwałych obiektach w swoim obrębie. Żądania jakie obsługuje wzorzec repozytorium (ang. **repository**). Zawierają w sobie zestaw kryteriów według jakich zostanie przeprowadzona selekcja obiektów.
    
Mechanizm obsługi zapisanych trwale obiektów pozwala odciążyć Model Dziedziny (ang. **Domain Model**) z procesu manipulacji zapisem/odczytem danych. Udostępniając tym samym prosty interfejs wykorzystywany przy zapisie/odczycie danych.

Repozytoria powiązane są ściśle z obiektami jakie obsługują. Korzysta z wzorca fabryki, a także wykonuje mapowanie ze szkieletu obiektów wczytanych z mechanizmu przechowywania trwałych danych (np. baza danych) na agregaty/encje/obiekty wartości zawarte w Modelu Dziedziny (ang. **Domain Model**).

Z repozytoriów powinny korzystać jedynie korzenie agregatów (ang. **Aggregate Root**) z zapotrzebowaniem na zapis/odczyt danych.

Korzyści ze stosowania repozytoriów (ang. **repositories**):
* udostępnienie prostego interfejsu manipulacji obiektami,
* odseparowanie Modelu Dziedziny (ang. **Domain Model**) od technologii przechowywania trwałych danych,
* możliwość testowania Modelu Dziedziny (ang. **Domain Model**) poprzez sztuczną implementacje interfejsów repozytoriów.

## Zakończenie
Budowanie aplikacji na bazie **Domain-Driven Design**, wymusza na projgramiście trzymanie się pewnych konwencji, wzorców. Jednak skutki wykorzystania będą przynosić korzyści jakie dostarcza to podejście. Powodują, że warto się pochylić nad tym tematem i rozwinąć w sobie zdolność do wykorzystywania **DDD**.

Po takiej porcji wiedzy rozmyślam (w końcu) nad zastosowaniem w prostym projekcie. Oraz przedstawieniu swoich poczynań w kolejnych postach dotyczących **DDD**.

{% include_relative books.md %}
---
Wcześniejszy artykuł: **[Domain-Driven Design - Podstawowe części składowe.][previous]**

Następny artykuł: **[Domain-Driven Design - &#8222;Nadejszła wiekopomna chłiła&#8221;.][next]**

---
[previous]: {{site.url}}/domain-driven-design-podstawowe-czesci-skladowe
[next]: {{site.url}}/domain-driven-design-nadejszla-wiekopomna-chliala


[post]: /assets/images/2017/09/ddd-i-jego-zycie/post.jpg
[post-big]: /assets/images/2017/09/ddd-i-jego-zycie/post-big.jpg

[image1]: /assets/images/2017/09/ddd-i-jego-zycie/image1.jpg
[image1-big]: /assets/images/2017/09/ddd-i-jego-zycie/image1-big.jpg

[image2]: /assets/images/2017/09/ddd-i-jego-zycie/image2.jpg
[image2-big]: /assets/images/2017/09/ddd-i-jego-zycie/image2-big.jpg

[image3]: /assets/images/2017/09/ddd-i-jego-zycie/image1.jpg
[image3-big]: /assets/images/2017/09/ddd-i-jego-zycie/image1-big.jpg