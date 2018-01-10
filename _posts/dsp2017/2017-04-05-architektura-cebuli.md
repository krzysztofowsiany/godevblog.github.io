---
id: 663
title: Architektura cebuli
date: 2017-04-05T18:14:01+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/04/05/architektura-cebuli/
image: /assets/images/2017/04/480-Zwiebel-zwiebel-Fotolia-28405313-c-vadim-yerofeyev.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - Architektura
  - dajsiepoznac2017
  - DSP2017
  - Onion
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1 style="background: LIGHTSALMON; padding: 5px;">
      Clean Architecture
    </h1>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/04/480-Zwiebel-zwiebel-Fotolia-28405313-c-vadim-yerofeyev.jpg"><img class="alignleft wp-image-728 size-medium" src="http://godev.gemustudio.com/assets/images/2017/04/480-Zwiebel-zwiebel-Fotolia-28405313-c-vadim-yerofeyev-300x209.jpg" alt="Architektura cebuli" width="300" height="209" srcset="http://godev.gemustudio.com/assets/images/2017/04/480-Zwiebel-zwiebel-Fotolia-28405313-c-vadim-yerofeyev-300x209.jpg 300w, http://godev.gemustudio.com/assets/images/2017/04/480-Zwiebel-zwiebel-Fotolia-28405313-c-vadim-yerofeyev.jpg 480w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    

      Jest to ogólne pojęcie określające architekturę tworzenia sytemu z uwzględnieniem kilku czynników:
    </p>
    
    <ul style="text-align: justify;">
      <li>
        niezależność od framework&#8217;a/bibliotek,
      </li>
      <li>
        testowalność z wykluczeniem bazy danych i interfejsu użytkownika, a także innych zewnętrznych komponentów,
      </li>
      <li>
        niezależność względem interfejsu użytkownika, podmiana nie wpływa na pozostałą część systemu,
      </li>
      <li>
        niezależność względem wykorzystanej bazy danych, dzięki temu można dowolnie podmieniać system bazy danych bez ingerencji w działanie aplikacji,
      </li>
      <li>
        odseparowanie modelu biznesowego od świata zewnętrznego.
      </li>
    </ul>
    
    <p>
      Układ w formie tarczy/okręgów, przedstawia budowę architektury.
    </p>
    
    <p>
      Zależności pomiędzy warstwami(okręgami), budowane są jednokierunkowo, to znaczy, iż warstwa podrzędna nie wie nic o warstwie nadrzędnej tym samym implementacja warstwy zewnętrznej nie może być wykorzystywana przez warstwę wewnętrzną.
    </p>
    
    <p>
      <img class="aligncenter" src="https://8thlight.com/blog/assets/posts/2012-08-13-the-clean-architecture/CleanArchitecture-8b00a9d7e2543fa9ca76b81b05066629.jpg" alt="Clean Architecture" width="772" height="567" />
    </p>
    

      Na powyższym obrazku zależności określone są poprzez strzałki, przykładowo:
    </p>
    

      Warstwa <strong>Entities</strong> jest niezależna od żadnej warstwy, i przeważnie określa modele domenowe, warstwa wyżej <strong>Uses Cases</strong> jest zależna od warstwy <strong>Entities</strong> i aktywnie ją wykorzystuje.
    </p>
    

      Dodatkowo ilość warstw w aplikacji nie jest z góry określona i może być zupełnie inna niż na przykładzie. Ważne jest zachowanie reguł <strong>Clean Architecture</strong>.
    </p>
    
    <h1 style="background: LIGHTSALMON; padding: 5px;">
      Onion Architecture
    </h1>
    

      <strong><a href="http://jeffreypalermo.com/blog/the-onion-architecture-part-1/">Jeffrey Palermo</a></strong> przyrównał <strong>Clean Architecture</strong> do cebuli: <strong><em>&#8222;A good, clean architecture is built like an onion&#8221;</em></strong>.<img class="alignright" src="http://jeffreypalermo.com/files/media/image/WindowsLiveWriter/TheOnionArchitecturepart1_70A9/image%7B0%7D%5B59%5D.png" alt="Onion Architecture" width="366" height="259" />
    </p>
    

      Na obrazku poniżej przestawiona jest owa architektura.
    </p>
    

      Warstwy bliżej centrum cebuli, nie wiedzą nic o warstwach jakie otaczają, i nie jest im to potrzebne, spełniają przypisaną im rolę i tyle.
    </p>
    
    <p>
      Powiązanie z interfejsem użytkownika jest dość luźne i odbywa się za pośrednictwem <strong>REST/SOAP</strong>.
    </p>
    
    <p>
      Baza danych nie jest najważniejszym elementem sytemu a jedynie jest wykorzystywane przez infrastrukturę aplikacji.
    </p>
    
    <p>
      W powyższym przypadku w samym centrum znajdują się modele domenowe (<strong>Domain-Driven Design</strong>).
    </p>
    
    <p>
      Takie podejście pozwala na łatwiejsze przetestowanie aplikacji pod kątem funkcjonowania.
    </p>
    
    <p>
      Pewne elementy aplikacji np. logi, dostęp do plików/bazy, usługi zewnętrzne, funkcjonują poza bazową funkcjonalnością aplikacji. Dzięki temu łatwiej jest pisać testy gdyż narzut technologiczny wynikający ze stosowania pewnego typu rozwiązania (biblioteki), nie jest tutaj wykorzystywany.
    </p>
    
    <h3 style="text-align: center; background: LIGHTSALMON; padding: 5px;">
      Rozwarstwienie aplikacji to także większy porządek => większa czytelność => łatwiejsze utrzymanie. Tak że zachęcam do budowania aplikacji w oparciu o cebulkę!
    </h3>
    
{% include_relative dsp.md %}