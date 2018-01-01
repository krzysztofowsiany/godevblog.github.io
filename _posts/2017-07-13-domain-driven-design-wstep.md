---
id: 1586
title: 'Domain-Driven Design &#8211; Wstęp'
date: 2017-07-13T10:25:43+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1586
permalink: /2017/07/13/domain-driven-design-wstep/
dslc_post_template:
  - default
image: /images/2017/07/blogging-photo-16.jpg
categories:
  - Bez kategorii
  - Domain-Driven Design
  - Programowanie
tags:
  - DDD
  - Domain-Driven Design
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p>
      <span style="font-size: 16px;">Niniejszym otwieram cykl postów związanych z rozkminianiem architektury wytwarzania oprogramowania o nazwie <strong>DDD => Domain-Driven Design</strong>. Jest to temat jaki od pewnego czasu dręczy mnie, i chcę rozwinąć swoje zdolności w tym konkretnym obszarze.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <span style="font-size: 16px;">W tym celu zaopatrzyłem się w dwie pozycje:</span>
    </p>
    
    <table class=" aligncenter" style="width: 300px; margin: 0 auto;">
      <tr style="height: 100px;">
        <td style="width: 150px; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/domdri.htm"><img class="aligncenter" src="https://static01.helion.com.pl/global/okladki/326x466/0ec470d7102b93516012ee4849dc3a41,domdri.jpg" alt="Okładka książki Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym" width="72" height="103" /></a>
        </td>
        
        <td style="width: 150px; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/dddaro.htm"><img class="aligncenter" src="https://static01.helion.com.pl/global/okladki/326x466/91bb872731d822a7c801afc2b4e9b8cc,dddaro.jpg" alt="Okładka książki DDD dla architektów oprogramowania" width="70" height="100" /></a>
        </td>
      </tr>
      
      <tr style="height: 100px;">
        <td style="width: 150px; text-align: center; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/domdri.htm">Domain-Driven Design. Zapanuj nad złożonym systemem informatycznym. Eric Evans.</a>
        </td>
        
        <td style="width: 150px; text-align: center; height: 100px;">
          <a href="http://ebookpoint.pl/view/90752/dddaro.htm">DDD dla architektów oprogramowania, Vaughn Vernon.</a>
        </td>
      </tr>
    </table>
    
    <h2 style="text-align: justify;">
      Czym jest Domain-Driven Design?
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Jest to podejście do budowania aplikacji, w którym zaczynamy od stworzenia tak zwanego <strong>Modelu Domeny (eng. Domain Model)</strong>. Sam model nie jest niczym innym jak wyodrębnionym głównym zachowaniem aplikacji jaki ma zostać zaimplementowany.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Aplikacja zbudowana jest z wielu elementów: </span>
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <span style="font-size: 16px;">interfejs użytkownika, </span>
      </li>
      <li style="text-align: justify;">
        <span style="font-size: 16px;">obsługa wejść/wyjść, </span>
      </li>
      <li style="text-align: justify;">
        <span style="font-size: 16px;">obsługa bazy danych,</span>
      </li>
      <li style="text-align: justify;">
        <span style="font-size: 16px;"> inne usługi wspierające tworzenie aplikacji.</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Model Domeny/Dziedziny (eng. Domain Model)</strong> nie zawiera tego bagażu, to czysta implementacja wartości (<strong>wartość biznesowa</strong>) jaką ma dawać aplikacja. Stworzona w sposób niezależny i łatwa do przetestowania.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><a href="http://godev.gemustudio.com/images/2017/07/blogging-photo-9871.jpg"><img class="size-medium wp-image-1599 alignright" src="http://godev.gemustudio.com/images/2017/07/blogging-photo-9871-300x200.jpg" alt="DDD" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/07/blogging-photo-9871-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/07/blogging-photo-9871-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/07/blogging-photo-9871.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>W celu jej implementacji programista musi rozumieć co jest najważniejszą wartością w oprogramowaniu jakie ma wykonać. Dlatego musi kontaktować się z osobą posiadającą <strong>największą wiedzę</strong> na temat funkcjonalności tworzonej aplikacji. Osoba taka określana jest jako<strong> Ekspert Domenowy  (eng. Domain Expert)</strong>,może to być np. klient.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Często pojawia się problem z wymianą informacji (niejednokrotnie się z nim zetknąłem). Dotyczy problemów językowych występujących w komunikacji pomiędzy programistą, a ekspertem domenowym. Osoby te zazwyczaj wywodzą się z innych środowisk i pojęcia jakimi operują nie są zrozumiałem lub znaczą coś zupełnie innego dla strony przeciwnej.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Rozwiązaniem problemu jest stosowanie tak zwanego <a href="http://godev.gemustudio.com/2017/07/17/domain-driven-design-jezyk-wszechobecny/"><strong>języka wszechobecnego (eng. Ubiquitous Language).</strong></a> Zawierającego wspólnie wypracowane pojęcia dzięki, którym zarówno ekspert domenowy zrozumie programistę jak i odwrotnie.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Jest to technika trudna, wymagająca w implementacji odpowiedniego projektowania i nakładająca na programistę dodatkowy narzut pracy związany z <strong>klepaniem kodu</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Do budowy aplikacji opartej o <strong>Domain-Driven Design</strong> wykorzystać można wielowarstwową architekturę aplikacji. W ten sposób model domenowy zostanie wyodrębniony do własnej warstwy.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: center;">
      <span style="font-size: 14px;">Nadmieniam, tutaj iż głoszę swój osobisty punkt widzenia i sposób prezentacji wiedzy. A jako że nie jestem nieomylny, to mogą i zapewne będą zdarzać się błędy&#8230;</span>
    </p>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>