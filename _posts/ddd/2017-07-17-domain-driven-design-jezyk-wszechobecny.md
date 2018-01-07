---
title: 'Domain-Driven Design &#8211; Język Wszechobecny.'
date: 2017-07-17T20:25:14+00:00
author: gocom
layout: post
permalink: /domain-driven-design-jezyk-wszechobecny/
dslc_post_template:
  - default
image: /assets/images/2017/07/blogging-photo-9933.jpg
categories:
  - Bez kategorii
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
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p>
      <img class="size-medium wp-image-1633 alignleft" src="http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-9933-300x200.jpg" alt="Domain-Driven Design" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-9933-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-9933-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-9933.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" />
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px; font-family: arial, helvetica, sans-serif;"><span style="font-weight: 400;">Odwiecznym problemem jaki napotykają na swojej drodze dwie ścierające się siły: zlecający i wykonawca, jest wzajemna komunikacji i zrozumienie. Problem narasta gdy obie persony obracają się w odseparowanych środowiskach. Przykładem takiej sytuacji jest klient (</span><b>Ekspert Domenowy, eng. Domain Expert</b><span style="font-weight: 400;">) definiujący wymagania aplikacji i wykonawca (np.: zespół programistów, programista).</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 16px; font-family: arial, helvetica, sans-serif;">Dobrym przykładem takiej sytuacji jest często komunikacja pomiędzy kobietą i mężczyzną wprowadzająca zamęt, poprzez niejednoznaczne rozumienie wypowiadanych słów.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 16px; font-family: arial, helvetica, sans-serif;">Specyfika obszarów zainteresowania zawodowego obu osób przeważnie jest tak odległa, iż wzajemne zrozumienie/przekazanie specyfikacji produktu do wykonania skutkuje powstaniem wielu nieścisłości i zgrzytów. Obie osoby zazwyczaj rozmawiają z wykorzystaniem odmiennych zestawów definicji nie mających ze sobą zbyt wiele wspólnego.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2>
      Język Wszechobecny (eng. Ubiquitous Language)
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px; font-family: arial, helvetica, sans-serif;"><span style="font-weight: 400;">Z pomocą przychodzi metoda wytwarzania oprogramowania </span><a href="http://godev.gemustudio.com/2017/07/13/domain-driven-design-wstep/"><b>Domain-Driven Design</b></a><span style="font-weight: 400;">. Otóż nie jest to jedynie architektura. Zawiera w sobie wiele definicji co do kultury pracy w projekcie zarówno od strony definiującego/weryfikującego wymagania. a także ich realizatora.</span></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <img class="wp-image-1630 size-full aligncenter" style="font-family: arial, helvetica, sans-serif; text-align: justify; margin: 0 auto;" src="http://godev.gemustudio.com/assets/images/2017/07/g8266.png" alt="Domain-Driven Design - Ubiquitous Language" width="592" height="286" srcset="http://godev.gemustudio.com/assets/images/2017/07/g8266.png 592w, http://godev.gemustudio.com/assets/images/2017/07/g8266-300x145.png 300w" sizes="(max-width: 592px) 100vw, 592px" />
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px; font-family: arial, helvetica, sans-serif;"><span style="font-weight: 400;">Jednym z jej aspektów jest wykreowanie tak zwanego </span><b>Języka Wszechobecnego (eng. Ubiquitous Language)</b><span style="font-weight: 400;">, zmieniającego sposób komunikacji pomiędzy osobą wymagającą, a realizującą. Wprowadza wspólnie ustalony zestaw słów/definicji  w formie żargonu. Tym samym podnosi się jakość wzajemnej komunikacji poprzez zrozumienie istoty wymagań i problemów jakie zaistnieją w trakcie realizacji projektu.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px; font-family: arial, helvetica, sans-serif;"><span style="font-weight: 400;">Opracowanie słownictwa </span><b>Języka Wszechobecnego</b><span style="font-weight: 400;"> poprzez wspólną analizę dziedziny i dojście  do konsensusu nazewnictwa poszczególnych elementów, pozytywnie wpływa  na współpracę i kulturę pracy  w zespole.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px; font-family: arial, helvetica, sans-serif;"><span style="font-weight: 400;"><a href="http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-1191.jpg"><img class="size-medium wp-image-1636 alignright" src="http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-1191-200x300.jpg" alt="Ubiquitous Language" width="200" height="300" srcset="http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-1191-200x300.jpg 200w, http://godev.gemustudio.com/assets/images/2017/07/blogging-photo-1191.jpg 600w" sizes="(max-width: 200px) 100vw, 200px" /></a>Słownictwo języka wszechobecnego powinno bazować na </span><b>Modelu Domeny (eng. Domain Model)</b><span style="font-weight: 400;">. Skutkuje to wykorzystaniem zdefiniowanych pojęć, w każdym aspekcie projektu. Od modelowania klas po dokumentację i komunikację dotyczącą projektu. Zespół powinien weryfikować wprowadzone pojęcia w celu eliminacji błędnych sformułowań. Dobrą praktyką jest wypowiadanie pojęć na głos, łatwiej będzie wówczas wyłapać dziwne sformułowania.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px; font-family: arial, helvetica, sans-serif;"><b>Język Wszechobecny (eng. Ubiquitous Language)</b><span style="font-weight: 400;"> jest ściśle związany z </span><b>Modelem Domeny/Dziedziny (eng. Domain Model) </b><span style="font-weight: 400;">, dlatego wprowadzanie zmian w żargonie niesie ze sobą potrzebę zmiany modelu i odwrotnie.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 16px; font-family: arial, helvetica, sans-serif;">Projektując i budując aplikację często napotykamy na problemy związane z  określeniem punktu wspólnego tematyki jakiej poruszał projekt.  W pewnym sensie także nazewnictwo zostało narzucone przez przełożonych bądź w przeciwną stronę.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: center;">
      <span style="font-size: 14px;"><strong>Nadmieniam, tutaj iż głoszę swój osobisty punkt widzenia i sposób prezentacji wiedzy. A jako że nie jestem nieomylny, to mogą i zapewne będą zdarzać się błędy&#8230;</strong></span>
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