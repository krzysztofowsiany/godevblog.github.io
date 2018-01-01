---
id: 1911
title: 'Domain-Driven Development &#8211; &#8222;nadejszła wiekopomna chłiła&#8221;'
date: 2017-11-13T23:40:24+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1911
permalink: /2017/11/13/domain-driven-development-nadejszla-wiekopomna-chliala/
dslc_post_template:
  - default
image: /assets/images/2017/11/blogging-photo-3271.jpg
categories:
  - Bez kategorii
  - Domain-Driven Design
tags:
  - Code Review
  - DDD
  - Domain Expert
  - Domain Model
  - Domain-Driven Design
  - GIT
  - GitHub
  - MVVM
  - Visual Studio Code
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Długo tutaj mnie nie było, wiele się działo, zmiana pracy, konferencje, wyjazdy. Blog-abstynencja.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><a href="http://godev.gemustudio.com/assets/images/2017/11/blogging-photo-9818.jpg"><img class="size-medium wp-image-1916 alignright" src="http://godev.gemustudio.com/assets/images/2017/11/blogging-photo-9818-200x300.jpg" alt="Domain Expert" width="200" height="300" srcset="http://godev.gemustudio.com/assets/images/2017/11/blogging-photo-9818-200x300.jpg 200w, http://godev.gemustudio.com/assets/images/2017/11/blogging-photo-9818.jpg 600w" sizes="(max-width: 200px) 100vw, 200px" /></a>Liznąwszy nieco wiedzy na temat <a href="http://godev.gemustudio.com/2017/07/13/domain-driven-design-wstep/" target="_blank" rel="noreferrer noopener"><strong>Domain-Driven Development</strong></a>, </span><strong><span style="color: #ff0000;"><em><span style="font-size: 16px;">pora wrzucić jakiegoś kota do wora</span>.</em></span></strong>
    </p>
    
    <h2>
      O projekcie
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Chwilami rozmyślałem na temat projektu, jaki chciałbym zmaltretować. Wyszło przy tym kilka ciekawych pomysłów. Jednak do realizacji podejmę się projektu prostego, rozwiązującego mój mały problemik.</span>
    </p>
    
    <p>
      <span style="font-size: 16px;">Nie lubię np. tracić czasu na takie działanie jak:</span>
    </p>
    
    <ul>
      <li>
        <span style="font-size: 16px;">odpalanie gita w konkretnej lokalizacji,</span>
      </li>
      <li>
        <span style="font-size: 16px;">otwieranie folderu projektu,</span>
      </li>
      <li>
        <span style="font-size: 16px;">otwieranie konkretnych plików, np. z dokumentacją,</span>
      </li>
      <li>
        <span style="font-size: 16px;">wchodzenie na konkretne strony internetowe,</span>
      </li>
      <li>
        <span style="font-size: 16px;">otwieranie terminala w oknie (także z uprawnieniami admina).</span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Dodatkowo fajnie by było jak bym jednym kliknięciem miał od razu uruchomione wszystko co potrzebuję do pracy.</span><br /> <span style="font-size: 16px;"> Przykładowo:</span>
    </p>
    
    <ol>
      <li>
        <span style="font-size: 16px;">Otwarty edytor <strong>Visual Studio Code</strong> z projektem.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Otwarta konsola <strong>GIT</strong> dla tego projektu.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Folder projektu.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Przeglądarki (Firefox, Chrome, Edge, Opera do testowania frontendu).</span>
      </li>
    </ol>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Apka siedziałaby sobie cicho w Tray-u, aż ją wyciągnę za oszywę do roboty.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Chciałbym oczywiście mieć możliwość definiowania w prosty sposób profili uruchomienia oraz samych wyzwalaczy.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Fajno by też było jak by konfiguracja była archiwizowana (najlepiej gdzieś hen daleko). Tak by nie stracić w razie awarii systemu.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Cele dla stworzenia <strong>MVP</strong> aplikacji:</span>
    </p>
    
    <ol>
      <li>
        <span style="font-size: 16px;">Jak najszybciej dodać wyzwalacz.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Wiele typów wyzwalaczy.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Jak najszybciej wywołać wyzwalacz.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Łatwy dostęp do: wyzwalaczy, konfiguracji i profili.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Prostota i szybkość tutaj jest najważniejsza.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Automatyczne kopie bezpieczeństwa.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Przywracanie z kopii.</span>
      </li>
      <li>
        <span style="font-size: 16px;">Kopie w chmurze: dropbox, google drive, onedrive.</span>
      </li>
    </ol>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Pomyślałem, że w ramach projektu <a href="http://godev.gemustudio.com/2017/07/13/domain-driven-design-wstep/" target="_blank" rel="noreferrer noopener"><strong>DDD</strong></a>, stworzę sobie właśnie taki sofcik.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Tym samym stałem się Ekspertem Domenowym (ang. <strong>Domain Expert</strong>)…</span>
    </p>
    
    <h2>
      Technologia
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Co do technologii, jako że apka ma działać na Windozie, to skorzystam z języka <strong>C# + WPF</strong>. Oprócz tego zapewne znajdzie się wiele przydatnych bibliotek do logowania, konteneryzacji, <strong>MVVM</strong>.</span><br /> <span style="font-size: 16px;"> Aplikacja zbudowana zostanie z wykorzystaniem <a href="http://godev.gemustudio.com/2017/04/05/architektura-cebuli/" target="_blank" rel="noreferrer noopener"><strong>Onion Architecturę</strong></a>, tak by wyodrębnić <a href="http://godev.gemustudio.com/2017/07/24/domain-driven-design-izolacja-przy-pomocy-warstw/" target="_blank" rel="noreferrer noopener"><strong>warstwę biznesową</strong></a>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Jako młody adept szkolenia przeprowadzonego przez <a href="http://devstyle.pl" target="_blank" rel="noreferrer noopener"><strong>Macieja Aniserowicza</strong></a> dotyczącego <strong>Testowania Automatycznego</strong>. Nie omieszkam ich tutaj zastosować 😀</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Kod wrzuci się na <a href="https://github.com/krzysztofowsiany" target="_blank" rel="noreferrer noopener"><strong>GitHub-a</strong></a>, może ktoś wykona <strong>Code Review</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Ponownie polecam poniższe książki.</span>
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