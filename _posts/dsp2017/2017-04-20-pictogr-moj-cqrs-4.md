---
id: 828
title: 'PictOgr &#8211; mój CQRS -4-'
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
      Command Query Responsibility Segregation &#8211; 4 &#8211;
    </h1>
    
    <p style="text-align: justify;">
      Zapowiadałem na ten wpis, iż będzie on dotyczył wykorzystania <strong>ES</strong> oraz walidatorów, jednak powstał mały bałagan w projekcie czego skutkiem było wyodrębnienie <strong>CQRS</strong> do osobnego repozytorium.<img class="alignright" src="https://cdn.travis-ci.org/assets/images/logos/TravisCI-Mascot-1-20feeadb48fc2492ba741d89cb5a5c8a.png" alt="CQRS" width="226" height="224" />
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
    
    <p style="text-align: justify;">
      Biblioteka powiązana jest z napisanym już wcześniej modułami do implementacji testów.
    </p>
    
    <p style="text-align: justify;">
      Takie podejście pozwoliło mi na wykorzystanie po raz pierwszy mechanizmu pod modułów w <strong>GIT,</strong><strong> EXP rośnie.:)</strong>
    </p>
    
    <p style="text-align: justify;">
      Mechanizm ten pozwala na dołączanie do repozytorium innych repozytoriów jako pod moduły i korzystanie z nich.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Pod moduły &#8211; GIT
    </h1>
    
    <p>
      Do konfiguracji pod modułów służy plik o nazwie <strong>.gitmodules</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Plik .gitmodules.">[submodule "CQRS"]
        path = CQRS
        url = https://github.com/krzysztofowsiany/cqrs

</pre>
    
    <p style="text-align: justify;">
      Należy określić, nazwę podmodułu, ścieżkę gdzie będzie znajdowało się dołączone repozytorium oraz jego adres.
    </p>
    
    <p style="text-align: justify;">
      Po dodaniu pliku .gitmodules wydając polecenie <strong>git submodule update</strong> aktualizujemy dodane podmoduły.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Travis
    </h1>
    
    <p>
      Dodatkowo zaadaptowałem projekt tak by można było wykorzystać narzędzie o nazwie <strong><a href="https://travis-ci.org/">Travis-CI.</a></strong>
    </p>
    
    <p>
      Jest to darmowy serwer (dla oprogramowania <strong>Open Source)</strong> ciągłej integracji pozwalający na kontrolowanie poprawności działania aplikacji poprzez przygotowanie środowiska, instalację zależności, budowaniu, testowaniu, i raportowaniu tego procederu.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Travis wymaga konfiguracji zapisanej w pliku o nazwie <strong>.travis.yml</strong>.
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
      Plik ten daje duże możliwości, i przykład jaki wykorzystałem jest bardzo prosty, polegający na określeniu plików projektu, instalacji wymaganych zależności, następnie uruchomienie samego skryptu budowania <strong>xbuild</strong> oraz wykonania testów.
    </p>
    
    <p style="text-align: justify;">
      Więcej o konfiguracji Travisa przy pomocy yamla pod adresem: <strong>https://docs.travis-ci.com/user/customizing-the-build</strong>.
    </p>
    
    <p>
      Co ciekawe całe środowisko uruchomieniowe działa na Linuxie dlatego wykorzystywana jest tutaj platforma <strong><a href="http://www.mono-project.com/docs/about-mono/supported-platforms/linux/">mono</a></strong>.
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
      <strong><a href="https://travis-ci.org/krzysztofowsiany/cqrs"><img class="aligncenter" src="https://travis-ci.org/krzysztofowsiany/cqrs.svg?branch=master" /></a></strong>
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/04/mycqrs.png"><img class="aligncenter wp-image-835 size-full" src="http://godev.gemustudio.com/assets/images/2017/04/mycqrs.png" alt="CQRS - GitHub" width="687" height="577" srcset="http://godev.gemustudio.com/assets/images/2017/04/mycqrs.png 687w, http://godev.gemustudio.com/assets/images/2017/04/mycqrs-300x252.png 300w" sizes="(max-width: 687px) 100vw, 687px" /></a>
    </p>
    
    <h1 style="text-align: justify;">
    </h1>
    
    <h1 style="text-align: justify;">
      Koniec
    </h1>
    
    <p style="text-align: justify;">
      Co prawda krótki post, jednak ostatni święta  i z nimi związane długie wyjazdy/powroty do rodziny. Dlatego wpis taki króciasty,
    </p>
    
    <p style="text-align: justify;">
      Jednak mam nadzieję, że interesujący.
    </p>
    
    <h3 style="text-align: justify;">
      <strong>Linki:</strong>
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
      <strong>Dziękuję za wytrwałość i zachęcam do komentowania.</strong>
    </h3>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <div style="text-align: center;">
        <strong>Jest to post przygotowany na potrzeby konkursu &#8222;Daj Się Poznać 2017&#8221; organizowanym przez <a href="http://devstyle.pl">Macieja Aniserowicza</a>.</strong>
      </div>
      
      <div style="text-align: center;">
         <a href="http://devstyle.pl/daj-sie-poznac/" target="_blank" rel="noopener noreferrer"><img class="wp-image-104 size-full alignright" title="Daj Się Poznać 2017" src="http://godev.gemustudio.com/assets/images/2017/02/dsp2017-3.png" alt="" width="68" height="154" /></a>
      </div>
      
      <div style="font-size: 10pt; padding: 10px;">
        <div>
          <strong>Projekt: </strong><a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/">PictOgr</a>.
        </div>
        
        <div>
          <strong>GitHub: </strong><a href="https://github.com/krzysztofowsiany/pictogr">github.com/krzysztofowsiany/pictogr</a>
        </div>
        
        <div>
          <strong>Blog: </strong><a href="http://godev.gemustudio.com">godev.gemustudio.com</a>
        </div>
        
        <div>
          <strong>Snapchat</strong>: <a href="https://www.snapchat.com/add/gocom7" target="_blank" rel="noopener noreferrer">gocom7</a>
        </div>
        
        <div>
          <strong>RSS: </strong><a href="http://godev.gemustudio.com/category/daj-sie-poznac-2017/feed">godev.gemustudio.com/category/daj-sie-poznac-2017/feed</a>
        </div>
        
        <div>
          <strong>Facebook:</strong><a href="https://www.facebook.com/PictOgr-1729700930654225/">www.facebook.com/PictOgr-1729700930654225/</a>
        </div>
        
        <div>
          <strong>Twitter: </strong><a href="https://twitter.com/gemu_gocom">twitter.com/gemu_gocom</a>
        </div>
      </div>
    </div>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>