---
id: 1652
title: 'Domain-Driven Design &#8211; izolacja przy pomocy warstw.'
date: 2017-07-24T16:50:49+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1652
permalink: /2017/07/24/domain-driven-design-izolacja-przy-pomocy-warstw/
dslc_post_template:
  - default
image: /images/2017/07/blogging-photo-1365.jpg
categories:
  - Bez kategorii
  - Domain-Driven Design
  - Programowanie
tags:
  - DDD
  - Domain-Driven Design
  - high-cohesion
  - loose-coupling
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-family: arial, helvetica, sans-serif; font-size: 16px;"><a href="http://godev.gemustudio.com/images/2017/07/blogging-photo-1365.jpg"><img class="size-medium wp-image-1660 alignleft" src="http://godev.gemustudio.com/images/2017/07/blogging-photo-1365-300x200.jpg" alt="loose-coupling" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/07/blogging-photo-1365-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/07/blogging-photo-1365-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/07/blogging-photo-1365.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>Poprawne modelowanie dziedziny skutkuje bezwzględnym wymaganiem dotyczą jej izolacji od reszty systemu. Z pomocą przychodzi architektura warstwowa wyodrębniająca z aplikacji spójne ze sobą pod względem działania obszary. Zebrane w ten sposób funkcjonalności są składowymi warstw. Przy czym bazowy zestaw warstw został zdefiniowany i zawiera:</span>
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <span style="font-size: 16px;"><b style="font-family: arial, helvetica, sans-serif;">Interfejsu Użytkownika</b><span style="font-weight: 400;"> (ang. </span><b style="font-family: arial, helvetica, sans-serif;">User Interface</b><span style="font-weight: 400;">) &#8211; warstwa ta odpowiedzialna jest za kontakt ze światem zewnętrznym. Służy obsłudze funkcjonalności aplikacji przez użytkownika. Oczywiście warstwa ta może także być w formie </span><b style="font-family: arial, helvetica, sans-serif;">API</b><span style="font-weight: 400;"> (</span><b style="font-family: arial, helvetica, sans-serif;">Application Programming Interface</b><span style="font-weight: 400;">). Czyli usługi udostępnionej innym aplikacjom, Np. </span><b style="font-family: arial, helvetica, sans-serif;">WebSerwisy</b><span style="font-weight: 400;">, </span><b style="font-family: arial, helvetica, sans-serif;">WebSockety</b><span style="font-weight: 400;">. Warstwa </span><b style="font-family: arial, helvetica, sans-serif;">Interfejsu  Użytkownika</b><span style="font-weight: 400;"> korzysta z publicznych interfejsów upublicznionych w warstwach niższego rzędu.</span></span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <ul>
      <li style="font-weight: 400; text-align: justify;">
        <span style="font-family: arial, helvetica, sans-serif; font-size: 16px;"><b>Aplikacji</b><span style="font-weight: 400;"> (ang. </span><b>Application</b><span style="font-weight: 400;">) &#8211; jest to warstwa pośrednicząca między warstwą interfejsu, a warstwą dziedziny, wszelkie operacje deleguje do warstwy domeny, sama może posiadać stan jednak nie posiada logiki biznesowej. Jest niezbędna gdyż zarządza zadaniami jakie są zlecane z warstwy użytkownika do aplikacji. Tak jak warstwa </span><b>Interfejsu Użytkownika </b><span style="font-weight: 400;">posiada dostęp do warstw niższego rzędu.</span></span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/07/4layer_application.png"><img class="aligncenter wp-image-1677 size-medium" src="http://godev.gemustudio.com/images/2017/07/4layer_application-300x211.png" alt="Architektura warstwowa" width="300" height="211" srcset="http://godev.gemustudio.com/images/2017/07/4layer_application-300x211.png 300w, http://godev.gemustudio.com/images/2017/07/4layer_application.png 565w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <ul>
      <li style="font-weight: 400; text-align: justify;">
        <span style="font-family: arial, helvetica, sans-serif; font-size: 16px;"><b>Dziedziny/Modelu</b><span style="font-weight: 400;"> (ang. </span><b>Domain</b><span style="font-weight: 400;">) &#8211;  warstwa gdzie implementujemy </span><b>Logikę Biznesową</b><span style="font-weight: 400;"> (ang. </span><b>Bussines  Logic</b><span style="font-weight: 400;">). Dostarcza najbardziej wartościową funkcjonalność (</span><b>wartość biznesową</b><span style="font-weight: 400;">), jest rdzeniem aplikacji. Korzysta z warstwy niżej (</span><b>infrastruktury</b><span style="font-weight: 400;">) w charakterze magazynu danych. Powinna zawierać w sobie implementację głównej funkcjonalności programu. Dzięki separacji od działań związanych ze środowiskiem w jakim uruchamiana jest aplikacja. Dużo łatwiej jest testować działanie warstwy, a także przenosić czystą formę algorytmów ustaloną z </span><b>Ekspertem Domenowym</b><span style="font-weight: 400;"> (ang. </span><b>Domain  Expert</b><span style="font-weight: 400;">).</span></span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <ul>
      <li style="font-weight: 400; text-align: justify;">
        <span style="font-family: arial, helvetica, sans-serif; font-size: 16px;"><b>Infrastruktury</b><span style="font-weight: 400;"> (ang. </span><b>Infrastructure</b><span style="font-weight: 400;">) &#8211; jest to warstwa służąca do kontaktu z systemem w jakim uruchamiany jest program. Pośredniczy w korzystaniu z funkcji systemowych/usług zewnętrznych, np.:: baza danych, zapis do plików, dostęp do urządzeń zewnętrznych, zdalnych usług. Jak sama nazwa wskazuje cała infrastruktura jaka znajduje się w środowisku uruchomieniowym programu. Świadczy usługi na  rzecz warstw wyższego rzędu.</span></span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-family: arial, helvetica, sans-serif; font-size: 16px;"><span style="font-weight: 400;">Każda z wymienionych warstw izoluje specyficzną dla siebie funkcjonalność. Pozwoliło to nie tylko odseparować </span><b>Model Dziedziny</b><span style="font-weight: 400;"> (ang. </span><b>Domain Model</b><span style="font-weight: 400;">), co także uporządkować składowe elementy aplikacji.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-family: arial, helvetica, sans-serif; font-size: 16px;">Warstwy powinny być zależne jedynie od warstwy niższej, jednocześnie luźno powiązane z warstwami wyżej.<a href="http://godev.gemustudio.com/images/2017/07/blogging-photo-1398.jpg"><img class="size-medium wp-image-1680 alignright" src="http://godev.gemustudio.com/images/2017/07/blogging-photo-1398-300x200.jpg" alt="high-cohesion" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/07/blogging-photo-1398-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/07/blogging-photo-1398-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/07/blogging-photo-1398.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a> </span>
    </p>
    
    <p>
      <span style="font-size: 16px;"><span style="font-weight: 400; font-family: arial, helvetica, sans-serif;">Oznacza to, iż aplikacja cechuje się: </span>dużą spójnością (ang. <b style="font-family: arial, helvetica, sans-serif;">high-cohesion</b>), <span style="font-family: arial, helvetica, sans-serif;">słabym związaniem (ang. </span><b style="font-family: arial, helvetica, sans-serif;">loose-coupling</b><span style="font-family: arial, helvetica, sans-serif;">).</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-family: arial, helvetica, sans-serif; font-size: 16px;">Jakie zachodzi pomiędzy: warstwami, interfejsami, obiektami. </span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-family: arial, helvetica, sans-serif; font-size: 16px;">Zależnie od złożoności systemu, istnieje możliwość dodania kolejnych warstw w celu większego rozproszenia funkcjonalności. Należy jednak pamiętać iż, w sytuacji nadmiernego przyrostu ilości warstw rośnie także złożoność aplikacji. Ta sytuacja z kolei utrudnia utrzymanie aplikacji.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-family: arial, helvetica, sans-serif; font-size: 16px;"><span style="font-weight: 400;">Architekturę warstwową opisywałem także w poście: </span><a href="http://godev.gemustudio.com/2017/04/05/architektura-cebuli/"><span style="font-weight: 400;"><b>Architektura cebuli</b></span></a><span style="font-weight: 400;">.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-family: arial, helvetica, sans-serif; font-size: 16px;"><span style="font-weight: 400;">Oczywiście nie są to wszystkie możliwe sposoby na wyizolowanie </span><b>Modelu Dziedziny</b><span style="font-weight: 400;"> (ang. </span><b>Domain Model</b><span style="font-weight: 400;">)  w aplikacji…</span></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: center;">
      <span style="font-size: 14px; font-family: arial, helvetica, sans-serif;"><strong>Nadmieniam, tutaj iż głoszę swój osobisty punkt widzenia i sposób prezentacji wiedzy. A jako że nie jestem nieomylny, to mogą i zapewne będą zdarzać się błędy&#8230;</strong></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Polecane książki
    </h2>
    
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