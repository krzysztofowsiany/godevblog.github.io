---
title: Architektura cebuli
date: 2017-04-05
author: Krzysztof Owsiany
layout: post
published: true
permalink: /architektura-cebuli
image: /assets/images/2017/04/architektura-cebuli/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - Architektura
  - dajsiepoznac2017
  - DSP2017
  - Onion
short: Rozwarstwienie aplikacji to także większy porządek => większa czytelność => łatwiejsze utrzymanie. Zachęcam do budowania aplikacji w oparciu o cebulkę!
---
## Clean Architecture
[![Architektura cebuli][post]][post-big]{:.post-right-image}
Jest to ogólne pojęcie określające architekturę tworzenia sytemu z uwzględnieniem kilku czynników:
* niezależność od framework&#8217;a/bibliotek,
* testowalność z wykluczeniem bazy danych i interfejsu użytkownika, a także innych zewnętrznych komponentów,
* niezależność względem interfejsu użytkownika, podmiana nie wpływa na pozostałą część systemu,
* niezależność względem wykorzystanej bazy danych, dzięki temu można dowolnie podmieniać system bazy danych bez ingerencji w działanie aplikacji,
* odseparowanie modelu biznesowego od świata zewnętrznego.
    
Układ w formie tarczy/okręgów, przedstawia budowę architektury.
    
Zależności pomiędzy warstwami(okręgami), budowane są jednokierunkowo, to znaczy, iż warstwa podrzędna nie wie nic o warstwie nadrzędnej tym samym implementacja warstwy zewnętrznej nie może być wykorzystywana przez warstwę wewnętrzną.
    
![Clean Architecture][clean-architecture]
    
Na powyższym obrazku zależności określone są poprzez strzałki, przykładowo:
* Warstwa **Entities** jest niezależna od żadnej warstwy, i przeważnie określa modele domenowe, warstwa wyżej **Uses Cases** jest zależna od warstwy **Entities** i aktywnie ją wykorzystuje.
* Dodatkowo ilość warstw w aplikacji nie jest z góry określona i może być zupełnie inna niż na przykładzie. Ważne jest zachowanie reguł **Clean Architecture**.
    
##  Onion Architecture
**[Jeffrey Palermo][jeffreypalermo]** przyrównał **Clean Architecture** do cebuli: **&#8222;A good, clean architecture is built like an onion&#8221;**

Na obrazku poniżej przestawiona jest owa architektura.

[![Onion Architecture][onion-architecture]][jeffreypalermo]{:.post-left-image}
    
Warstwy bliżej centrum cebuli, nie wiedzą nic o warstwach jakie otaczają, i nie jest im to potrzebne, spełniają przypisaną im rolę i tyle.

Powiązanie z interfejsem użytkownika jest dość luźne i odbywa się za pośrednictwem **REST/SOAP**.

Baza danych nie jest najważniejszym elementem sytemu a jedynie jest wykorzystywane przez infrastrukturę aplikacji.

W powyższym przypadku w samym centrum znajdują się modele domenowe (**Domain-Driven Design**).

Takie podejście pozwala na łatwiejsze przetestowanie aplikacji pod kątem funkcjonowania.

Pewne elementy aplikacji np. logi, dostęp do plików/bazy, usługi zewnętrzne, funkcjonują poza bazową funkcjonalnością aplikacji. Dzięki temu łatwiej jest pisać testy gdyż narzut technologiczny wynikający ze stosowania pewnego typu rozwiązania (biblioteki), nie jest tutaj wykorzystywany.

**Rozwarstwienie aplikacji to także większy porządek => większa czytelność => łatwiejsze utrzymanie. Zachęcam do budowania aplikacji w oparciu o cebulkę!**{:.h-1}
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/04/architektura-cebuli/post.jpg
[post-big]: /assets/images/2017/04/architektura-cebuli/post-big.jpg

[onion-architecture]: /assets/images/2017/04/architektura-cebuli/onion-architecture.png

[clean-architecture]: /assets/images/2017/04/architektura-cebuli/clean-architecture.jpg

[jeffreypalermo]: http://jeffreypalermo.com/blog/the-onion-architecture-part-1