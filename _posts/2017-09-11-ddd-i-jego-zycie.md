---
id: 1772
title: 'Domain-Driven Design &#8211; i jego życie'
date: 2017-09-11T08:47:48+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1772
permalink: /2017/09/11/ddd-i-jego-zycie/
dslc_post_template:
  - default
image: /images/2017/09/blogging-photo-1381.jpg
categories:
  - Bez kategorii
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
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h2>
      Wstęp
    </h2>
    
    <p>
      Poprzedni artykuł dotyczący składowych elementów wykorzystywanych w <a title="Domain-Driven Design - podstawowe części składowe." href="http://godev.gemustudio.com/2017/08/17/domain-driven-design-podstawowe-czesci-skladowe/">Domain-Driven Development</a>, charakteryzuje komponenty wykorzystywane przy budowie złożonych modelów dziedziny (ang. <strong>Domain Model</strong>).
    </p>
    
    <p>
      Jednak owe komponenty wchodzą w skład większego bytu, posiadają swój cykl życia.
    </p>
    
    <p>
      Podobnie jak istota żywa, rodzą się, funkcjonują, umierają i niekiedy pozostawiają po sobie ślad w historii.
    </p>
    
    <p>
      W całym tym cyklu życia niezbędne jest wsparcie z zewnątrz. I Tutaj z pomocą przychodzą wzorce:
    </p>
    
    <ul>
      <li>
        agregaty (ang. <strong>aggregates</strong>),
      </li>
      <li>
        fabryki (ang. <strong>factories</strong>),
      </li>
      <li>
        repozytoria (ang. <strong>repositories</strong>).
      </li>
    </ul>
    
    <p>
      Stosowanie powyższych wzorców porządkuje modele i tym samym umożliwia łatwiejsze zarządzanie mnogością obiektów.
    </p>
    
    <h2>
      Agregaty
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/09/blogging-photo-1112.jpg"><img class="alignright size-medium wp-image-1775" src="http://godev.gemustudio.com/images/2017/09/blogging-photo-1112-300x200.jpg" alt="Domain-Drive Design - Aggregates" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/09/blogging-photo-1112-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/09/blogging-photo-1112-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/09/blogging-photo-1112.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a> Jest to zbiór powiązanych ze sobą obiektów, dzięki temu można traktować je jako jedna całość (jeden obiekt). Agregat (ang. <strong>aggregate</strong>) zbudowany jest z dwóch części:
    </p>
    
    <ul>
      <li>
        <strong>korzenia</strong> (ang. <strong>Aggregate Root</strong>) &#8211; jedna z encji (ang. <strong>entity</strong>) wchodząca w skład zbioru obiektów,
      </li>
      <li>
        <strong>granicy</strong> (ang. <strong>Boundary</strong>) &#8211; definiuje zawartość agregatu, czyli jakie obiekty będą się znajdować w jego obrębie.
      </li>
    </ul>
    
    <p>
      Agregat (ang. <strong>aggregate</strong>) otacza granicą swoje obiekty. Dostęp do obiektów możliwy jest jedynie w obrębie granicy. Dostęp do agregatu odbywa się poprzez korzeń.
    </p>
    
    <p>
      Zmienia się także podejście do tożsamości encji (ang. <strong>entity</strong>). Za wyjątkiem korzenia pozostałe encje muszą posiadać tożsamość ale w obrębie granicy agregatu. Inna sytuacja jest w przypadku korzenia, który to musi identyfikować agregat (ang. <strong>aggregate</strong>) w całym Modelu Domeny (ang. <strong>Domain Model</strong>).
    </p>
    
    <p>
      Dostęp z poza granicy agregatu jest zabroniony z wykluczeniem korzenia agregatu (ang. <strong>Aggregate Root</strong>).
    </p>
    
    <p>
      Jedyną możliwością dostępu do wewnętrznych obiektów agregatu odbywa się poprzez chwilowe przekazanie kopii obiektu.
    </p>
    
    <p>
      Jak zbudować agregat?: 1. Wyznaczyć grupę encji/wartości (ang. <strong>entity/value object</strong>). 2. Tym samym wyznaczyć granicę agregatu (ang. <strong>aggregate</strong>). 3. Z encji (ang. <strong>entity</strong>) wybrać jedną odpowiednią do pełnienia roli korzenia agregatu (ang. <strong>Aggregate Root</strong>). 4. Ustanowić dostęp do wewnętrznych obiektów poprzez korzeń.
    </p>
    
    <h2>
      Fabryki
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/09/blogging-photo-1322.jpg"><img class="alignleft wp-image-1793" src="http://godev.gemustudio.com/images/2017/09/blogging-photo-1322-300x200.jpg" alt="Domain-Driven Design - Factories" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/09/blogging-photo-1322-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/09/blogging-photo-1322-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/09/blogging-photo-1322.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>Kolejny z wzorców dzięki którym, tworzenie rozbudowanych agregatów będzie łatwiejsza i nie pozwoli na ich rozhermetyzowanie to fabryka (ang. <strong>factory</strong>). Fabryka jak sama nazwa wskazuje to obiekt którego, celem jest wytworzenie produktu jaki zamawiamy lub jego odtworzenie. Jest ona ściśle powiązana z konkretnym typem obiektu i jeżeli zachodzi potrzeba przeniesienia odpowiedzialności tworzenia tego obiektu, bez wahania należy to zrobić. Do tworzenia agregatów także należy wykorzystać fabrykę ściśle powiązaną z korzeniem agregatu (ang. <strong>Aggregate Root</strong>).
    </p>
    
    <p>
      Agregat składa się z wielu encji i obiektów wartości, przy pomocy fabryki upraszczamy tworzenie tych wewnętrznych bytów. Cała logika związana z kreacją znajduje się w klasie fabryki.
    </p>
    
    <p>
      Sama konstrukcja fabryki to nic innego jak znane do tej pory wzorce kreacyjne:
    </p>
    
    <ul>
      <li>
        metoda wytwórcza (ang. <strong>factory method</strong>),
      </li>
      <li>
        fabryka abstrakcyjna (ang. <strong>abstract factory</strong>),
      </li>
      <li>
        budowniczy (ang. <strong>builder</strong>).
      </li>
    </ul>
    
    <p>
      Jednak w pewnych sytuacjach wykorzystanie fabryki (ang. <strong>factory</strong>) jest nadmiarowe:
    </p>
    
    <ul>
      <li>
        wszystkie atrybuty obiektu są publiczne,
      </li>
      <li>
        klasa jest typem,
      </li>
      <li>
        tworzenie obiektu jest proste,
      </li>
      <li>
        w konstruktorze nie zawiera logiki obiektu,
      </li>
      <li>
        konstruktor jest atomowy (wszystkie informacje niezbędne do wykonania obiektu znajdują się w konstruktorze).
      </li>
    </ul>
    
    <p>
      W przypadku tworzenia obiektów wartości (ang. <strong>value object</strong>) tworzenie obiektów jest prostsze, aniżeli dla encji (ang. <strong>entity</strong>). Wynika to z faktu posiadania przez encje tożsamości. Unikalny identyfikator encji może być wygenerowany przez fabrykę, ale także do niej przekazany. Przekazywanie identyfikatora to przykład użycia fabryki do odtwarzania encji. Nie można generować na nowo, gdyż zmieni się tożsamość (będzie to inna encja). Jak zwykle wszystko zależy od kontekstu bieżącego zastosowania fabryki.
    </p>
    
    <h2>
      Repozytoria
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/09/blogging-photo-9308.jpg"><img class="alignright size-medium wp-image-1795" src="http://godev.gemustudio.com/images/2017/09/blogging-photo-9308-300x200.jpg" alt="Domain-Driven Design - Repositories" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/09/blogging-photo-9308-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/09/blogging-photo-9308-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/09/blogging-photo-9308.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>Wzorzec manipulacji obiektami trwale zachowanymi przy pomocy zaimplementowanych działań w warstwie infrastruktury. Repozytorium (ang. <strong>repository</strong>) to wzorzec hermetyzójacy działania na trwałych obiektach w swoim obrębie. Żądania jakie obsługuje wzorzec repozytorium (ang. <strong>repository</strong>). Zawierają w sobie zestaw kryteriów według jakich zostanie przeprowadzona selekcja obiektów.
    </p>
    
    <p>
      Mechanizm obsługi zapisanych trwale obiektów pozwala odciążyć Model Dziedziny (ang. <strong>Domain Model</strong>) z procesu manipulacji zapisem/odczytem danych. Udostępniając tym samym prosty interfejs wykorzystywany przy zapisie/odczycie danych.
    </p>
    
    <p>
      Repozytoria powiązane są ściśle z obiektami jakie obsługują. Korzysta z wzorca fabryki, a także wykonuje mapowanie ze szkieletu obiektów wczytanych z mechanizmu przechowywania trwałych danych (np. baza danych) na agregaty/encje/obiekty wartości zawarte w Modelu Dziedziny (ang. <strong>Domain Model</strong>).
    </p>
    
    <p>
      Z repozytoriów powinny korzystać jedynie korzenie agregatów (ang. <strong>Aggregate Root</strong>) z zapotrzebowaniem na zapis/odczyt danych.
    </p>
    
    <p>
      Korzyści ze stosowania repozytoriów (ang. <strong>repositories</strong>):
    </p>
    
    <ul>
      <li>
        udostępnienie prostego interfejsu manipulacji obiektami,
      </li>
      <li>
        odseparowanie Modelu Dziedziny (ang. <strong>Domain Model</strong>) od technologii przechowywania trwałych danych,
      </li>
      <li>
        możliwość testowania Modelu Dziedziny (ang. <strong>Domain Model</strong>) poprzez sztuczną implementacje interfejsów repozytoriów.
      </li>
    </ul>
    
    <h2>
      Zakończenie
    </h2>
    
    <p>
      Budowanie aplikacji na bazie <strong>Domain-Driven Design</strong>, wymusza na projgramiście trzymanie się pewnych konwencji, wzorców. Jednak skutki wykorzystania będą przynosić korzyści jakie dostarcza to podejście. Powodują, że warto się pochylić nad tym tematem i rozwinąć w sobie zdolność do wykorzystywania <strong>DDD</strong>.
    </p>
    
    <p>
      Po takiej porcji wiedzy rozmyślam (w końcu) nad zastosowaniem w prostym projekcie. Oraz przedstawieniu swoich poczynań w kolejnych postach dotyczących <strong>DDD</strong>.
    </p>
    
    <p>
      Ponownie polecam poniższe książki.
    </p>
    
    <p>
      <a href="http://ebookpoint.pl/view/90752/domdri.htm"> <img src="https://static01.helion.com.pl/global/okladki/326x466/0ec470d7102b93516012ee4849dc3a41,domdri.jpg" alt="Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym. Eric Evans." width="70" height="100" /> <strong>Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym. Eric Evans.</strong> </a>
    </p>
    
    <p>
      <a href="http://ebookpoint.pl/view/90752/dddaro.htm"> <img src="https://static01.helion.com.pl/global/okladki/326x466/91bb872731d822a7c801afc2b4e9b8cc,dddaro.jpg" alt="DDD dla architektów oprogramowania, Vaughn Vernon." width="70" height="100" /> <strong>DDD dla architektów oprogramowania, Vaughn Vernon.</strong> </a>
    </p>
    
    <p>
      <em>Są to linki afiliacyjne.</em>
    </p>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>