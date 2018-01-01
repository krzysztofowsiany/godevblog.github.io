---
id: 1699
title: 'Domain-Driven Design &#8211; podstawowe części składowe'
date: 2017-08-17T08:16:00+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1699
permalink: /2017/08/17/domain-driven-design-podstawowe-czesci-skladowe/
dslc_post_template:
  - default
image: /images/2017/08/blogging-photo-2144.jpg
categories:
  - Bez kategorii
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
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Do budowy <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>), wykorzystujemy kilka bazowych składowych powiązanych ze sobą relacjami.</span>
    </p>
    
    <h2>
      Asocjacje (ang. associations)
    </h2>
    
    <p>
      <img class="size-medium wp-image-1708 alignleft" src="http://godev.gemustudio.com/images/2017/08/blogging-photo-1349-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/08/blogging-photo-1349-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1349-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1349.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" />
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Asocjacja to swoista abstrakcja stanowiąca o związku pomiędzy bytami wchodzącymi w skład <strong>Modelu Dziedziny </strong>(ang. <strong>Domain Model</strong>), jaką twórca uznał za odpowiednią.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">O czym należy pamiętać tworząc asocjacje:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">eliminacja zbędnych, im więcej tym model jest bardziej skomplikowany</span>
      </li>
      <li>
        <span style="font-size: 16px;">unikanie asocjacji wiele do wiele (unikniemy wielokrotnych relacji),</span>
      </li>
      <li>
        <span style="font-size: 16px;">określenie kierunku,</span>
      </li>
      <li>
        <span style="font-size: 16px;">stosowanie kwalifikatorów &#8211; skutkuje uproszczeniem relacji w <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>).</span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Kwantyfikatory</strong> &#8211; ograniczają kierunek interpretacji <strong>asocjacji</strong> (ang. <strong>associations</strong>).</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Encje (ang. entity)
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><a href="http://godev.gemustudio.com/images/2017/08/blogging-photo-1167.jpg"><img class="size-medium wp-image-1713 alignright" src="http://godev.gemustudio.com/images/2017/08/blogging-photo-1167-300x200.jpg" alt="Encje (ang. entity)" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/08/blogging-photo-1167-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1167-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1167.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>Encje określane są także jako <strong>Obiekty Referencyjne (</strong>ang.<strong> Reference Objects)</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Obiekty tego typu muszą być jednoznacznie identyfikowane w <strong>Modelu Dziedziny (</strong>ang. <strong>Domain Model</strong>), posiadają swoją tożsamość niezmienną w czasie.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Powoduje to, iż można owe obiekty porównywać ze sobą w sytuacji gdy atrybuty nie stanowiące o tożsamości obiektu.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Encja (ang. entity) </strong>powinna zawierać w sobie atrybuty związane z tożsamością obiektu, pozwalające na jej porównywanie z innymi bądź wyszukiwanie. Dlatego zależą od kontekstu zachowania obiektu.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">W sytuacji gdy atrybuty nie identyfikują jednoznacznie obiektu w <strong>Modelu Dziedziny (</strong>ang.<strong> Domain Model)</strong>, wprowadza się sztuczne identyfikatory.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Obiekty wartości (ang. value object)
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">O<a href="http://godev.gemustudio.com/images/2017/08/blogging-photo-1165.jpg"><img class="size-medium wp-image-1715 alignleft" src="http://godev.gemustudio.com/images/2017/08/blogging-photo-1165-300x200.jpg" alt="Obiekty wartości (ang. value object)" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/08/blogging-photo-1165-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1165-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1165.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>biekty tego typu nie posiadają tożsamości służą przede wszystkim do opisywania rzeczy (określają aspekt dziedziny). Najważniejsze są atrybuty obiektu, a nie tożsamość.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Można zadać pytanie po co mieszać i stosować i <strong>encję</strong> (ang. <strong>entity</strong>) i <strong>obiekty wartości</strong> (ang. <strong>value objects</strong>)?</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">A no po to by uprościć sam <strong>Model Dziedziny</strong> (ang. <strong>Domain Model</strong>).</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Obiekty bez atrybutów określających ich jednoznaczną identyfikację są łatwiejsze w utrzymaniu. W przeważającej ilości sytuacji nie zachodzi potrzeba zmiany <strong>obiektu wartości</strong> (ang. <strong>value object</strong>). Jednak gdy taka potrzeba występuje to wówczas nie ma możliwości współdzielenia obiekt.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Dodatkowo brak tożsamości powoduje brak potrzeby przejmowania się instancjami obiektu, to upraszcza i pozwala na wiele optymalizacji <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>).</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Sytuacje gdy zmiana <strong>obiektu wartości</strong> (ang. <strong>value object</strong>) jest dopuszczalna:</span>
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
        <span style="font-size: 16px;">gdy modyfikacja obiektu wpływały by na spójność <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>).</span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Dobrą praktyką jest konstruowanie obiektów wartości w formie niezmiennej (immutable).</strong></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Usługi (ang. service)
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">N<a href="http://godev.gemustudio.com/images/2017/08/blogging-photo-1572.jpg"><img class="size-medium wp-image-1718 alignright" src="http://godev.gemustudio.com/images/2017/08/blogging-photo-1572-300x200.jpg" alt="Usługi (ang. service)" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/08/blogging-photo-1572-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1572-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/08/blogging-photo-1572.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>ie wszystkie składowe elementy <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>), opierają się na przechowywaniu wartości, niekiedy zachodzi potrzeba wyodrębnienia operacji. Nie zawierają one żadnego stanu, nie przechowują wartości, a jedynie świadczą działanie. W tej sytuacji można mówić o <strong>usługach </strong>(ang. <strong>services</strong>).</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Usługi </strong>(ang. <strong>service</strong>) są zdefiniowane wyłącznie w kontekście operacji jakie świadczą dla swojego klienta. Są kontraktem zawierającym abstrakcyjne zamierzenia pewnego działania.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Cechy poprawnej <strong>usługi </strong>(ang. <strong>service</strong>):</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">odwołują się do <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>), jednak nie wchodzą jako część ani <strong>encji </strong>(ang. <strong>entity</strong>), ani też <strong>obiektu wartości </strong>(ang. <strong>value object</strong>),</span>
      </li>
      <li>
        <span style="font-size: 16px;">wykonywane operacje są bezstanowe &#8211; nie przechowujemy wartości w <strong>usłudze </strong>(ang. <strong>service</strong>),</span>
      </li>
      <li>
        <span style="font-size: 16px;">kontrakt <strong>usługi </strong>(ang. <strong>service</strong>), jest określany przez <strong>Model Dziedziny</strong> (ang. <strong>Domain Model</strong>).</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Nazewnictwo <strong>usług </strong>(ang. <strong>service</strong>), opierać się powinno na <strong>Języku Wszechobecnym</strong> (ang. <strong>Ubiquitous Language</strong>).</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Moduły/Pakiety (ang. modules)
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">P<a href="http://godev.gemustudio.com/images/2017/08/blogging-photo-2144.jpg"><img class="size-medium wp-image-1707 alignleft" src="http://godev.gemustudio.com/images/2017/08/blogging-photo-2144-300x200.jpg" alt="Usługi (ang. service)" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/08/blogging-photo-2144-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/08/blogging-photo-2144-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/08/blogging-photo-2144.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>rojektowanie <strong>Modelu Dziedziny</strong> (ang. <strong>Domain  Model</strong>) nie jest pozbawione problemów wynikających z nadmiernego rozrastania. W celu uproszczenia i łatwiejszego zrozumienia istoty modelu należy wprowadzić podział na moduły.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Przy podziale należy pamiętać, że: <span style="color: #ff5500;"><strong>nie kod jest wydzielany do modułów (ang. modules), a pojęcia dziedziny!</strong></span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Wydzielane <strong>moduły </strong>(ang. <strong>modules</strong>), powinny być:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">luźno ze sobą powiązane (ang. <strong>loose &#8211; coupling</strong>),</span>
      </li>
      <li>
        <span style="font-size: 16px;">zachować dużą spójność (ang. <strong>high &#8211; cohesion</strong>).</span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Rozdzielenie <strong>modułów </strong>(ang. <strong>modules</strong>), można odnieść do budowy książki. Gdzie <strong>Model Dziedziny </strong>(ang. <strong>Domain Model</strong>), traktujemy jako treść pewnej opowiadanej historii, natomiast <strong>moduły </strong>(ang. <strong>modules</strong>) odzwierciedlają rozdziały.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Moduły </strong>(ang. <strong>modules</strong>), poprzez swe nazwy zawarte także w <strong>Języku Wszechobecnym</strong> (ang. <strong>Ubiquitous Language</strong>). Powinny stanowić wiedzę dziedzinową.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">W raz z rozrostem/rozwojem <strong>Modelu Dziedziny</strong> (ang. <strong>Domain Model</strong>), zachodzi potrzeba refaktoryzacji <strong>modułów </strong>(ang. <strong>modules</strong>). Jednak proces ten może niekiedy powodować dość duże zmiany w kodzie.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Tym samym istnieje ryzyko powstania bałaganu w systemie kontroli wersji oraz konflikty między programistami.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Częściowym rozwiązaniem problemu jest planowanie/przewidywanie  struktury <strong>modułów </strong>(ang. <strong>modules</strong>). Programiści starają się przewidzieć przed stworzeniem pozostałych części modelu.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Błędnie zdefiniowane <strong>moduły </strong>(ang. <strong>modules</strong>), powinny zostać poprawione, gdyż brak reakcji będzie powodował nasilenie się problemu w przyszłości.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Na koniec
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Budowanie <strong>Modelu Dziedziny </strong>(ang. <strong>Domain Model</strong>), nie jest  sprawą  łatwą i wymaga zmiany sposobu myślenia podczas planowania. Widzę na  swoim przykładzie z jakim trudem przychodzi zrozumienie istoty <strong>Domain-Driven Design</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Powyższe składowe  elementy, stanowią podstawowe konstrukty jakie powinno się wykorzystywać w procesie tworzenia <strong>Logiki Biznesowej</strong> (ang. <strong>Business Logic</strong>) w tworzonych aplikacjach opartych na <strong>Domain-Driven  Design</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Oczywiście nie jest to wyczerpanie tematu i zachęcam do wielokrotnego zgłębiania wiedzy na ten temat:</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <table class=" aligncenter" style="width: 450px; margin: 0 auto;">
      <tr style="height: 100px;">
        <td style="width: 100px; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/domdri.htm"><img class="aligncenter" src="https://static01.helion.com.pl/global/okladki/326x466/0ec470d7102b93516012ee4849dc3a41,domdri.jpg" alt="Okładka książki Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym" width="72" height="103" /></a>
        </td>
        
        <td style="width: 350px; text-align: center; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/domdri.htm">Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym. Eric Evans.</a>
        </td>
      </tr>
      
      <tr style="height: 100px;">
        <td style="width: 100px; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/dddaro.htm"><img class="aligncenter" src="https://static01.helion.com.pl/global/okladki/326x466/91bb872731d822a7c801afc2b4e9b8cc,dddaro.jpg" alt="Okładka książki DDD dla architektów oprogramowania" width="70" height="100" /></a>
        </td>
        
        <td style="width: 350px; text-align: center; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/dddaro.htm">DDD dla architektów oprogramowania, Vaughn Vernon.</a>
        </td>
      </tr>
    </table>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>