---
id: 264
title: 'PictOgr &#8211; przygotowanie projektu'
date: 2017-03-13T19:54:02+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/03/13/pictogr-przygotowanie-projektu/
image: /assets/images/2017/03/13268041_594339104075545_5456660171174717784_o-e1489413262661.jpg
categories:
  - Daj Się Poznać 2017
  - Fotografia
tags:
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1>
      Repo
    </h1>
    
    <p>
      Najsam przód trzeba by sobie przygotować projekcik, dlatego raz dwa + nazwa i VS wygenerował mi się WPFik. Następnie fajnie byłoby kontrolować wersje kiedy i jak pasuje kod.
    </p>
    
    <p>
      W katalożku <strong><a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/">PictOgr-a</a></strong> odpalam basha i frunę:
    </p>
    
    <ul>
      <li>
        wydaję sobie komende <strong>git init</strong>,
      </li>
      <li>
        dopinam GitHuba <strong>git remote add origin https://github.com/krzysztofowsiany/pictogr</strong>,
      </li>
      <li>
        zaciągam GitHubem wklepując <strong>git fetch</strong>,
      </li>
      <li>
        i cacy.
      </li>
    </ul>
    
    <p>
      <a href="https://github.com/krzysztofowsiany/pictogr"><img class="aligncenter" src="https://www.filepicker.io/api/file/M4Ia0lToSE2a0XkSMKUv" alt="PictOgr - przygotowanie projektu" width="1710" height="440" /></a>
    </p>
    
    <p>
      Moja robota w drzewie git:
    </p>
    
    <p>
      <strong>master->dev</strong>
    </p>
    
    <p>
      <strong>dev</strong>-ka rozwijam sobie na bieżąco rozwijając taski w pod gałązkach, jak mi wpadnie do głowy potrzeba wydania wersji to wrzucam sobie w <strong>master</strong>.
    </p>
    
    <p>
      Po powrocie do przyszłości może się też pojawić gałązka <strong>testing</strong>, tj. <strong>maser->testing->dev</strong>.
    </p>
    
    <p>
      Potem już tylko podpinanie pliczków, ignorowanie i integracja z repo.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Zabawa w bibliotekarza
    </h1>
    
    <p>
      <a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/"><strong><img class=" alignleft" src="http://www.ibrpolska.pl/assets/images/2015/03/Biblio.jpg" width="244" height="180" /></strong></a>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/"><strong>PictOgr</strong></a> potrzebuje wsparcia, trzeba było udać się do biblioteki i godzinami studiować zawartość.
    </p>
    
    <p>
      Ale udało się wyłuskać kilka pozycji obowiązkowych w miejscu o nazwie &#8222;<strong>Package Manager Console</strong>&#8222;.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <h3>
        Dla projektu kilka &#8222;książek&#8221; z biblioteki:
      </h3>
      
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>AutoFac</strong> &#8211; kontenerek na obiekty,
          </div>
        </li>
        
        <li>
          <div style="float: left;">
             (<strong>Install-Package Autofac, <a href="https://autofac.org">https://autofac.org</a></strong>)
          </div>
        </li>
      </ul>
    </div>
    
    <p>
      ,
    </p>
    
    <div>
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>LiteDb</strong> &#8211; bazka dla nieznających S-kuela,
          </div>
        </li>
        
        <li>
          <div style="float: left;">
             (<strong>Install-Package LiteDb, <a href="http://www.litedb.org">http://www.litedb.org</a></strong>),
          </div>
        </li>
      </ul>
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>log4net</strong> &#8211; zapis popełnionych błędów i innych informacji,
          </div>
        </li>
        
        <li>
          <div style="float: left;">
             (<strong>Install-Package log4net, </strong><strong><a href="https://logging.apache.org/log4net">https://logging.apache.org/log4net</a></strong>),
          </div>
        </li>
        
        <li>
        </li>
      </ul>
      
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>photo.exif</strong> &#8211; czytanie nagłówka EXIF z pliczków graficznych
          </div>
        </li>
        
        <li>
          <div style="float: left;">
            , (<strong>Install-Package photo.exif, <a href="https://github.com/fraxedas/photo">https://github.com/fraxedas/photo</a></strong>).
          </div>
        </li>
      </ul>
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <h3>
      </h3>
      
      <h3>
        Do teścików będę potrzebował poniższego zestawu:
      </h3>
      
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>FakeItEasy</strong> &#8211; do udawania obiektów w testach,
          </div>
        </li>
        
        <li>
          <div style="float: left;">
             (<strong>Install-Package FakeItEasy, <a href="https://fakeiteasy.github.io">https://fakeiteasy.github.io</a></strong>),
          </div>
        </li>
      </ul>
      
      <p>
        &nbsp;
      </p>
      
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>xUnit</strong> &#8211; baza do teścików, dodatkowo VS wymaga runnera,
          </div>
        </li>
        
        <li>
          <div style="float: left;">
             (<strong>Install-Package xUnit, <a href="https://xunit.github.io/">https://xunit.github.io</a></strong>),
          </div>
        </li>
      </ul>
      
      <p>
        &nbsp;
      </p>
      
      <ul style="list-style: none;">
        <li>
          <div style="float: none; clear: both;">
            <img class="size-full wp-image-134 alignleft" style="float: left;" src="http://godev.gemustudio.com/assets/images/2017/02/Pokeball.png" width="15" height="15" />
          </div>
          
          <div style="float: left;">
            <strong>Shouldly</strong> &#8211; upiększone asercje w oparciu o Fluent Pattern,
          </div>
        </li>
        
        <li>
          <div style="float: left;">
             (<strong>Install-Package Shouldly, <a href="http://docs.shouldly-lib.net">http://docs.shouldly-lib.net</a></strong>).
          </div>
        </li>
      </ul>
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      To tyle na chwilę obecną, w trakcie rozwoju, zapewne dojdą kolejne biblioteczki.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Testowanie Ogra
    </h1>
    
    <p>
      <img class="display:block; float: left; alignleft" src="http://ocdn.eu/pulscms-transforms/1/oQAktkpTURBXy9mMmI4MTE3NDU1NDkwZTliZGU4ZjdjYWRjY2M1ZTlmMS5qcGeRkwIAzQHk" width="461" height="308" />
    </p>
    
    <p>
      Testować trzeba dużo, a w zasadzie szybciej niż się cokolwiek zrobi. Słaby jestem w tym chciałbym to zmienić.Dlatego przeznaczę cały project na to ;).
    </p>
    
    <p>
      Będzie się zwał <strong>PictOgr.Tests</strong> i całe mięsko tam będzie się znajdować.
    </p>
    
    <p>
      Nie jestem Krzysztof Kolumb (choć Krzysztof) i hameryki nie odkryję na nowo, chcę się tego nauczyć, a to jest dobry pomysł, a i ludzie będą paczeć na mój kod.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <div style="width: 220px; margin: 0 auto; font-size: 18pt;">
      <div style="background: lightgreen; text-align: center; padding: 5px;">
        <strong>Ty! Pacz!</strong>
      </div>
      
      <div style="background: #ff9980; text-align: center; padding: 5px;">
        <strong>Nie ma testów!</strong>
      </div>
      
      <div style="background: lightgreen; text-align: center; padding: 5px;">
        <strong>HA!</strong>
      </div>
      
      <div style="background: #ff9980; text-align: center; padding: 5px;">
        <strong>HA!</strong>
      </div>
      
      <div style="background: lightgreen; text-align: center; padding: 5px;">
        <strong>HA!</strong>
      </div>
      
      <div style="background: #ff9980; text-align: center; padding: 5px;">
        <strong>Co za burak!</strong>
      </div>
      
      <div style="background: lightgreen; text-align: center; padding: 5px;">
        <strong>HA!</strong>
      </div>
      
      <div style="background: #ff9980; text-align: center; padding: 5px;">
        <strong>HA!</strong>
      </div>
      
      <div style="background: lightgreen; text-align: center; padding: 5px;">
        <strong>HA!</strong>
      </div>
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Struktura Ogra
    </h1>
    
    <p>
      <a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/"><img class="wp-image-309 size-full alignright" src="http://godev.gemustudio.com/assets/images/2017/03/projekt.png" width="327" height="262" srcset="http://godev.gemustudio.com/assets/images/2017/03/projekt.png 327w, http://godev.gemustudio.com/assets/images/2017/03/projekt-300x240.png 300w" sizes="(max-width: 327px) 100vw, 327px" /></a>Początkowo słaba ta strukturka tylko 3 projekciki. A toteż mało czasu człowiek ma tylko 24h i projekt mozolnie pcha się do przodu jak ślimak.
    </p>
    
    <h2 style="background: #ecffb3; text-align: center; padding: 10px;">
      Jak to dobrze, że jestem devem i mam 48h na dobę.
    </h2>
    
    <p>
      <strong>PictOgr</strong> &#8211; główny projekt, WPFki podstawowego widoku
    </p>
    
    <p>
      <strong>PictOgr.Core</strong> &#8211; przydatne zestawy funkcji, jak pobieranie mięcha dla kontenera <strong>AutoFac.</strong>
    </p>
    
    <p>
      <strong>PictOgr.Tests</strong> &#8211; testy, testy, moje testy aplikacji nic po za tym.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      I the End
    </h1>
    
    <p>
      Pokusiłem się o implementację:
    </p>
    
    <ul>
      <li>
        <strong>CQRS</strong>
      </li>
      <li>
        <strong>AutoFac</strong>
      </li>
      <li>
        <strong>Testów.</strong>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Jest to kod rozwojowy i jak się rozwinie to wówczas będzie czas na post.
    </p>
    
    <p>
      Ale to w kolejnym skrobaniu tekstu na &#8222;Daj Się Poznać 2017&#8221;.
    </p>
    
{% include_relative dsp.md %}