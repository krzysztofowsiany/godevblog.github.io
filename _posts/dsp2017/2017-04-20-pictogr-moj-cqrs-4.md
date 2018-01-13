---
id: 828
title: 'PictOgr - mój CQRS -4-'
date: 2017-04-20T21:44:59+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/04/20/pictogr-moj-cqrs-4/
image: /assets/images/2017/04/travis_ci-512.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - GitHub
  - PictOgr
  - Travis-CI
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Command Query Responsibility Segregation - 4 -
    </h1>
    

      Zapowiadałem na ten wpis, iż będzie on dotyczył wykorzystania **ES** oraz walidatorów, jednak powstał mały bałagan w projekcie czego skutkiem było wyodrębnienie **CQRS** do osobnego repozytorium.<img class="alignright" src="https://cdn.travis-ci.org/assets/images/logos/TravisCI-Mascot-1-20feeadb48fc2492ba741d89cb5a5c8a.png" alt="CQRS" width="226" height="224" />
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      <a href="https://github.com/krzysztofowsiany/cqrs">https://github.com/krzysztofowsiany/cqrs</a>
    </h3>
    
    <p>
      &nbsp;
    </p>
    

      Biblioteka powiązana jest z napisanym już wcześniej modułami do implementacji testów.
    </p>
    

      Takie podejście pozwoliło mi na wykorzystanie po raz pierwszy mechanizmu pod modułów w **GIT,**** EXP rośnie.:)**
    </p>
    

      Mechanizm ten pozwala na dołączanie do repozytorium innych repozytoriów jako pod moduły i korzystanie z nich.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Pod moduły - GIT
    </h1>
    
    <p>
      Do konfiguracji pod modułów służy plik o nazwie **.gitmodules**.
    </p>
    
    <pre class="lang:c# decode:true" title="Plik .gitmodules.">[submodule "CQRS"]
        path = CQRS
        url = https://github.com/krzysztofowsiany/cqrs

</pre>
    

      Należy określić, nazwę podmodułu, ścieżkę gdzie będzie znajdowało się dołączone repozytorium oraz jego adres.
    </p>
    

      Po dodaniu pliku .gitmodules wydając polecenie **git submodule update** aktualizujemy dodane podmoduły.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Travis
    </h1>
    
    <p>
      Dodatkowo zaadaptowałem projekt tak by można było wykorzystać narzędzie o nazwie **<a href="https://travis-ci.org/">Travis-CI.</a>**
    </p>
    
    <p>
      Jest to darmowy serwer (dla oprogramowania **Open Source)** ciągłej integracji pozwalający na kontrolowanie poprawności działania aplikacji poprzez przygotowanie środowiska, instalację zależności, budowaniu, testowaniu, i raportowaniu tego procederu.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Travis wymaga konfiguracji zapisanej w pliku o nazwie **.travis.yml**.
    </p>
    
    <pre class="lang:yaml decode:true " title="Konfiguracja Travis-CI dla biblioteki CQRS.">language: csharp
solution: CQRS.sln
install:
  - nuget restore CQRS.sln
  - nuget install xunit.runners -Version 1.9.2 -OutputDirectory testrunner
script:
  - xbuild /p:Configuration=Debug
  - mono ./testrunner/xunit.runners.1.9.2/tools/xunit.console.clr4.exe ./CQRS.Tests/bin/Debug/CQRS.Tests.dll</pre>
    
    <p>
      Plik ten daje duże możliwości, i przykład jaki wykorzystałem jest bardzo prosty, polegający na określeniu plików projektu, instalacji wymaganych zależności, następnie uruchomienie samego skryptu budowania **xbuild** oraz wykonania testów.
    </p>
    

      Więcej o konfiguracji Travisa przy pomocy yamla pod adresem: **https://docs.travis-ci.com/user/customizing-the-build**.
    </p>
    
    <p>
      Co ciekawe całe środowisko uruchomieniowe działa na Linuxie dlatego wykorzystywana jest tutaj platforma **<a href="http://www.mono-project.com/docs/about-mono/supported-platforms/linux/">mono</a>**.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      W celu wykorzystania musiałem nieco zmienić projekt CQRS-a, pozbyć się runnera dla VS, oraz obniżyć wersję xUnita do 1.9.2, w takiej konfiguracji udało mi się dokonać pierwszego builda.:D
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: center;">
      **<a href="https://travis-ci.org/krzysztofowsiany/cqrs"><img class="aligncenter" src="https://travis-ci.org/krzysztofowsiany/cqrs.svg?branch=master" /></a>**
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/04/mycqrs.png"><img class="aligncenter wp-image-835 size-full" src="http://godev.gemustudio.com/assets/images/2017/04/mycqrs.png" alt="CQRS - GitHub" width="687" height="577" srcset="http://godev.gemustudio.com/assets/images/2017/04/mycqrs.png 687w, http://godev.gemustudio.com/assets/images/2017/04/mycqrs-300x252.png 300w" sizes="(max-width: 687px) 100vw, 687px" /></a>
    </p>
    
    <h1 style="text-align: justify;">
    </h1>
    
    <h1 style="text-align: justify;">
      Koniec
    </h1>
    

      Co prawda krótki post, jednak ostatni święta  i z nimi związane długie wyjazdy/powroty do rodziny. Dlatego wpis taki króciasty,
    </p>
    

      Jednak mam nadzieję, że interesujący.
    </p>
    
    <h3 style="text-align: justify;">
      **Linki:**
    </h3>
    
    <ul>
      <li style="text-align: justify;">
        <a href="https://docs.travis-ci.com/user/customizing-the-build">https://docs.travis-ci.com/user/customizing-the-build</a>
      </li>
      <li style="text-align: justify;">
        <a href="https://travis-ci.org/">https://travis-ci.org/</a>
      </li>
      <li style="text-align: justify;">
        <a href="http://www.mono-project.com/docs/about-mono/supported-platforms/linux/">http://www.mono-project.com/docs/about-mono/supported-platforms/linux/</a>
      </li>
      <li style="text-align: justify;">
        <a href="https://github.com/krzysztofowsiany/cqrs">https://github.com/krzysztofowsiany/cqrs</a>
      </li>
      <li style="text-align: justify;">
        <a href="https://travis-ci.org/krzysztofowsiany/cqrs">https://travis-ci.org/krzysztofowsiany/cqrs</a>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      **Dziękuję za wytrwałość i zachęcam do komentowania.**
    </h3>
    
 {% include_relative dsp.md %}