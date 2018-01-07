---
title: Domain-Driven Design - Podstawowe części składowe.
date: 2017-08-17T08:16:00+00:00
author: Krzysztof Owsiany
layout: post
permalink: domain-driven-design-podstawowe-czesci-skladowe
published: false
image: /assets/images/2017/08/blogging-photo-2144.jpg
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
---
{% include_relative preface.md %}

## Wstęp
Do budowy **Modelu Dziedziny** (ang. **Domain Model**), wykorzystujemy kilka bazowych składowych powiązanych ze sobą relacjami.
    
## Asocjacje (ang. associations)
    
    <p>
      <img class="size-medium wp-image-1708 alignleft" src="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1349-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1349-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1349-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1349.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" />
    </p>
    

Asocjacja to swoista abstrakcja stanowiąca o związku pomiędzy bytami wchodzącymi w skład **Modelu Dziedziny **(ang. **Domain Model**), jaką twórca uznał za odpowiednią.

O czym należy pamiętać tworząc asocjacje:
* eliminacja zbędnych, im więcej tym model jest bardziej skomplikowany,
* unikanie asocjacji wiele do wiele (unikniemy wielokrotnych relacji),
* określenie kierunku,
* stosowanie kwalifikatorów &#8211; skutkuje uproszczeniem relacji w **Modelu Dziedziny** (ang. **Domain Model**).
    
strong>Kwantyfikatory** &#8211; ograniczają kierunek interpretacji **asocjacji** (ang. **associations**).
    
## Encje (ang. entity)

      <span style="font-size: 16px;"><a href="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1167.jpg"><img class="size-medium wp-image-1713 alignright" src="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1167-300x200.jpg" alt="Encje (ang. entity)" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1167-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1167-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1167.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>Encje określane są także jako **Obiekty Referencyjne (**ang.** Reference Objects)**.</span>
    </p>
    

      <span style="font-size: 16px;">Obiekty tego typu muszą być jednoznacznie identyfikowane w **Modelu Dziedziny (**ang. **Domain Model**), posiadają swoją tożsamość niezmienną w czasie.</span>
    </p>
    

      <span style="font-size: 16px;">Powoduje to, iż można owe obiekty porównywać ze sobą w sytuacji gdy atrybuty nie stanowiące o tożsamości obiektu.</span>
    </p>
    

      <span style="font-size: 16px;">**Encja (ang. entity) **powinna zawierać w sobie atrybuty związane z tożsamością obiektu, pozwalające na jej porównywanie z innymi bądź wyszukiwanie. Dlatego zależą od kontekstu zachowania obiektu.</span>
    </p>
    

      <span style="font-size: 16px;">W sytuacji gdy atrybuty nie identyfikują jednoznacznie obiektu w **Modelu Dziedziny (**ang.** Domain Model)**, wprowadza się sztuczne identyfikatory.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
## Obiekty wartości (ang. value object)

      <span style="font-size: 16px;">O<a href="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1165.jpg"><img class="size-medium wp-image-1715 alignleft" src="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1165-300x200.jpg" alt="Obiekty wartości (ang. value object)" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1165-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1165-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1165.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>biekty tego typu nie posiadają tożsamości służą przede wszystkim do opisywania rzeczy (określają aspekt dziedziny). Najważniejsze są atrybuty obiektu, a nie tożsamość.</span>
    </p>
    

      <span style="font-size: 16px;">Można zadać pytanie po co mieszać i stosować i **encję** (ang. **entity**) i **obiekty wartości** (ang. **value objects**)?</span>
    </p>
    

      <span style="font-size: 16px;">A no po to by uprościć sam **Model Dziedziny** (ang. **Domain Model**).</span>
    </p>
    

      <span style="font-size: 16px;">Obiekty bez atrybutów określających ich jednoznaczną identyfikację są łatwiejsze w utrzymaniu. W przeważającej ilości sytuacji nie zachodzi potrzeba zmiany **obiektu wartości** (ang. **value object**). Jednak gdy taka potrzeba występuje to wówczas nie ma możliwości współdzielenia obiekt.</span>
    </p>
    

      <span style="font-size: 16px;">Dodatkowo brak tożsamości powoduje brak potrzeby przejmowania się instancjami obiektu, to upraszcza i pozwala na wiele optymalizacji **Modelu Dziedziny** (ang. **Domain Model**).</span>
    </p>
    

      <span style="font-size: 16px;">Sytuacje gdy zmiana **obiektu wartości** (ang. **value object**) jest dopuszczalna:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">gdy tworzenie/usuwanie obiektu będzie kosztowne dla aplikacji,</span>
      </li>
      <li>
        <span style="font-size: 16px;">gdy obiekt jest często modyfikowany,</span>
      </li>
      <li>
        <span style="font-size: 16px;">gdy obiekty nie są często współdzielone (najlepiej wcale),</span>
      </li>
      <li>
        <span style="font-size: 16px;">gdy modyfikacja obiektu wpływały by na spójność **Modelu Dziedziny** (ang. **Domain Model**).</span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    

      <span style="font-size: 16px;">**Dobrą praktyką jest konstruowanie obiektów wartości w formie niezmiennej (immutable).**</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
## Usługi (ang. service)
    

      <span style="font-size: 16px;">N<a href="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1572.jpg"><img class="size-medium wp-image-1718 alignright" src="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1572-300x200.jpg" alt="Usługi (ang. service)" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1572-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1572-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-1572.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>ie wszystkie składowe elementy **Modelu Dziedziny** (ang. **Domain Model**), opierają się na przechowywaniu wartości, niekiedy zachodzi potrzeba wyodrębnienia operacji. Nie zawierają one żadnego stanu, nie przechowują wartości, a jedynie świadczą działanie. W tej sytuacji można mówić o **usługach **(ang. **services**).</span>
    </p>
    

      <span style="font-size: 16px;">**Usługi **(ang. **service**) są zdefiniowane wyłącznie w kontekście operacji jakie świadczą dla swojego klienta. Są kontraktem zawierającym abstrakcyjne zamierzenia pewnego działania.</span>
    </p>
    

      <span style="font-size: 16px;">Cechy poprawnej **usługi **(ang. **service**):</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">odwołują się do **Modelu Dziedziny** (ang. **Domain Model**), jednak nie wchodzą jako część ani **encji **(ang. **entity**), ani też **obiektu wartości **(ang. **value object**),</span>
      </li>
      <li>
        <span style="font-size: 16px;">wykonywane operacje są bezstanowe &#8211; nie przechowujemy wartości w **usłudze **(ang. **service**),</span>
      </li>
      <li>
        <span style="font-size: 16px;">kontrakt **usługi **(ang. **service**), jest określany przez **Model Dziedziny** (ang. **Domain Model**).</span>
      </li>
    </ul>
    

      <span style="font-size: 16px;">Nazewnictwo **usług **(ang. **service**), opierać się powinno na **Języku Wszechobecnym** (ang. **Ubiquitous Language**).</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
## Moduły/Pakiety (ang. modules)
      <span style="font-size: 16px;">P<a href="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-2144.jpg"><img class="size-medium wp-image-1707 alignleft" src="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-2144-300x200.jpg" alt="Usługi (ang. service)" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-2144-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-2144-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/08/blogging-photo-2144.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>rojektowanie **Modelu Dziedziny** (ang. **Domain  Model**) nie jest pozbawione problemów wynikających z nadmiernego rozrastania. W celu uproszczenia i łatwiejszego zrozumienia istoty modelu należy wprowadzić podział na moduły.</span>
    </p>
    

      <span style="font-size: 16px;">Przy podziale należy pamiętać, że: <span style="color: #ff5500;">**nie kod jest wydzielany do modułów (ang. modules), a pojęcia dziedziny!**</span></span>
    </p>
    

      <span style="font-size: 16px;">Wydzielane **moduły **(ang. **modules**), powinny być:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">luźno ze sobą powiązane (ang. **loose &#8211; coupling**),</span>
      </li>
      <li>
        <span style="font-size: 16px;">zachować dużą spójność (ang. **high &#8211; cohesion**).</span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    

      <span style="font-size: 16px;">Rozdzielenie **modułów **(ang. **modules**), można odnieść do budowy książki. Gdzie **Model Dziedziny **(ang. **Domain Model**), traktujemy jako treść pewnej opowiadanej historii, natomiast **moduły **(ang. **modules**) odzwierciedlają rozdziały.</span>
    </p>
    

      <span style="font-size: 16px;">**Moduły **(ang. **modules**), poprzez swe nazwy zawarte także w **Języku Wszechobecnym** (ang. **Ubiquitous Language**). Powinny stanowić wiedzę dziedzinową.</span>
    </p>
    

      <span style="font-size: 16px;">W raz z rozrostem/rozwojem **Modelu Dziedziny** (ang. **Domain Model**), zachodzi potrzeba refaktoryzacji **modułów **(ang. **modules**). Jednak proces ten może niekiedy powodować dość duże zmiany w kodzie.</span>
    </p>
    

      <span style="font-size: 16px;">Tym samym istnieje ryzyko powstania bałaganu w systemie kontroli wersji oraz konflikty między programistami.</span>
    </p>
    

      <span style="font-size: 16px;">Częściowym rozwiązaniem problemu jest planowanie/przewidywanie  struktury **modułów **(ang. **modules**). Programiści starają się przewidzieć przed stworzeniem pozostałych części modelu.</span>
    </p>
    

      <span style="font-size: 16px;">Błędnie zdefiniowane **moduły **(ang. **modules**), powinny zostać poprawione, gdyż brak reakcji będzie powodował nasilenie się problemu w przyszłości.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
## Na koniec

      <span style="font-size: 16px;">Budowanie **Modelu Dziedziny **(ang. **Domain Model**), nie jest  sprawą  łatwą i wymaga zmiany sposobu myślenia podczas planowania. Widzę na  swoim przykładzie z jakim trudem przychodzi zrozumienie istoty **Domain-Driven Design**.</span>
    </p>
    

      <span style="font-size: 16px;">Powyższe składowe  elementy, stanowią podstawowe konstrukty jakie powinno się wykorzystywać w procesie tworzenia **Logiki Biznesowej** (ang. **Business Logic**) w tworzonych aplikacjach opartych na **Domain-Driven  Design**.</span>
    </p>
    

      <span style="font-size: 16px;">Oczywiście nie jest to wyczerpanie tematu i zachęcam do wielokrotnego zgłębiania wiedzy na ten temat:</span>
    </p>
    
  {% include_relative books.md %}

---
Wcześniejszy artykuł: **[Domain-Driven Design - Izolacja przy pomocy warstw.][previous]**

Następny artykuł: **[Domain-Driven Design - DDD i jego życie.][next]**

---
[previous]: {{site.url}}/domain-driven-design-izolacja-przy-pomocy-warstw
[next]: {{site.url}}/ddd-i-jego-zycie
