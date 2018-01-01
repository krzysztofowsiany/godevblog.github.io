---
id: 479
title: 'C#rek &#8211; hipopotam cz.3.'
date: 2017-03-21T23:50:51+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=479
permalink: /2017/03/21/crek-hipopotam-cz-3/
image: /assets/images/2017/03/żaba.png
categories:
  - Bez kategorii
  - Daj Się Poznać 2017
tags:
  - 'C#rek'
  - dajsiepoznac2017
  - DSP2017
  - Visual Studio 2015
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      C#rek trochę już obyty z <strong>GU</strong>J<strong>I</strong>, rozmyślając o zielonych migdałach, czasem też o programowaniu. Po wielu chwilach doszedł do wniosku, iż programowanie jest to ciężki kawałek chleba, ale warto poświęcić jedną, czy dwie kąpiele błotne na rzecz nauki. Szkoda tylko, że jest tak osamotniony w swych poczynaniach, w okolicy żadnego ogra o podobnych pomyślunkach.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Pułapki &#8211; Breakpoint
    </h2>
    
    <p>
      Hipek ma mały problem z ro<a href="http://godev.gemustudio.com/assets/images/2017/03/menu_breakpoints.png"><img class="alignleft wp-image-487 size-full" src="http://godev.gemustudio.com/assets/images/2017/03/menu_breakpoints.png" alt="" width="613" height="124" srcset="http://godev.gemustudio.com/assets/images/2017/03/menu_breakpoints.png 613w, http://godev.gemustudio.com/assets/images/2017/03/menu_breakpoints-300x61.png 300w" sizes="(max-width: 613px) 100vw, 613px" /></a>balami i czasem te wredne istoty gryzą niemiłosiernie. Jest jednak na to rozwiązanie można pozastawiać pułapki. C#rek wie co to pułapki, nie raz łapał żaby.
    </p>
    
    <p style="text-align: justify;">
      Jednak na spaślaku trzeba to robić dobrze, wykorzystać można do tego kilka magicznych sztuczek.
    </p>
    
    <p style="text-align: justify;">
      Obieramy miejsce w kodziku, gdzie tą pułapke chcemy zastawić i zaklęciem <strong>F9</strong>, lub poprzez machnięcie lewym pośladkiem gryzonia (LPM), w menu <strong>Debug</strong>. W miejscu gdzie pułapka ma być postawiona celujemy w <strong>Toogle Breakpoint</strong>.
    </p>
    
    <p style="text-align: justify;">
      Od razu tutaj można rzec, iż innym przydatnym zaklęciem <strong>Crtl+Shift+F9</strong> zdej<a href="http://godev.gemustudio.com/assets/images/2017/03/żaba.png"><img class="alignright wp-image-557 size-medium" src="http://godev.gemustudio.com/assets/images/2017/03/żaba-300x200.png" alt="C#rek" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/żaba-300x200.png 300w, http://godev.gemustudio.com/assets/images/2017/03/żaba-768x512.png 768w, http://godev.gemustudio.com/assets/images/2017/03/żaba.png 1000w" sizes="(max-width: 300px) 100vw, 300px" /></a>mujemy wszystkie pułapki <strong>Delete All Breakpoints.</strong>
    </p>
    
    <p>
      Podkreślić tutaj trzeba bardzo ważną sprawę, można polować na robala w tym celu użyć trzeba kilku ciekawych zaklęć:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>F10</strong> &#8211; dzięki temu zaklęciu można śledzić robala krok po kroku idąc główną ścieżką,
      </li>
      <li style="text-align: justify;">
        <strong>F11</strong> &#8211; podobnie jak wyżej tutaj możemy deptać po piętach robalom, jednak w tym przypadku możemy wchodzić w zakamarki (metody),
      </li>
      <li style="text-align: justify;">
        <strong>F5</strong> &#8211; pozwala uruchomić śledzenie, ale także zrobić szybkiego susa do kolejnej pułapki.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Lista pułapek &#8211; Breakpoints
    </h2>
    
    <h4 style="text-align: center;">
      <a href="http://godev.gemustudio.com/assets/images/2017/03/breakpoints.png"><img class="alignright wp-image-486 size-full" src="http://godev.gemustudio.com/assets/images/2017/03/breakpoints.png" alt="" width="577" height="215" srcset="http://godev.gemustudio.com/assets/images/2017/03/breakpoints.png 577w, http://godev.gemustudio.com/assets/images/2017/03/breakpoints-300x112.png 300w" sizes="(max-width: 577px) 100vw, 577px" /></a>
    </h4>
    
    <p style="text-align: justify;">
      C#rek ma małą pamięć, dlatego przyda się tutaj lista pułapek, można ją przywołać zaklęciem <strong>Crtl+D B.</strong>
    </p>
    
    <p>
      Pokaże się ładna lista, gdzie można różne cuda robić, <strong>wyłączać, włączać, kasować, wyszukiwać, dodawać</strong> pułapki i wszystko na widoku.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Taki robalomonitoring, gdzie, kiedy, co, itd. Warto korzystać.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Podglądy &#8211; Autos, Immediate Window, Locals
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h03_26.png"><img class="alignright wp-image-564 size-full" src="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h03_26.png" alt="" width="266" height="313" srcset="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h03_26.png 266w, http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h03_26-255x300.png 255w" sizes="(max-width: 266px) 100vw, 266px" /></a>Podczas śledzenia przyd<a href="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h26_50.png"><img class="alignleft wp-image-565 size-full" src="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h26_50.png" alt="" width="357" height="304" srcset="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h26_50.png 357w, http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h26_50-300x255.png 300w" sizes="(max-width: 357px) 100vw, 357px" /></a>ać się może nieco informacji do nawigacji, tak by po omacku nie szukać robali.
    </p>
    
    <p style="text-align: justify;">
      Trza tu wymienić następujące zaklęcia:
    </p>
    
    <p>
      <strong>Crtl+D, I</strong> &#8211; Immediate Window &#8211; konsola z możliwością wykonywania poleceń, np. podgląd, wystarczy wpisać nazwę zmiennej i potwierdzić enterem,
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>Crtl+D, A</strong> &#8211; Autos &#8211; wgląd do zmiennych w całej aplikacji,
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>Crtl+D, L</strong> &#8211; Locals &#8211; to lokalne podglądy informacji, można je porozwijać, by dowiedzieć się więcej (bieżący zakres),
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>Crtl+D, W</strong> &#8211; Watch &#8211; wybierać można własne informacje do podglądu, dostępne są po wduszeniu prawego przycisku gryzonia na zmienną i wybraniu &#8222;Add Watch&#8221;,
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h27_22.png"><img class="wp-image-566 size-full alignleft" src="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h27_22.png" alt="" width="415" height="300" srcset="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h27_22.png 415w, http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h27_22-300x217.png 300w" sizes="(max-width: 415px) 100vw, 415px" /></a>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: left;">
      <strong>Crtl+Alt+W, 2, </strong><strong>Crtl+Alt+W, 3,  </strong><strong>Crtl+Alt+W, 4, </strong><strong>Crtl+Alt+W, 5</strong> &#8211; otwarcie okiennicy pozostałych okien <strong>Watch</strong>, jakby komu było mało jednej.
    </p>
    
    <p style="text-align: left;">
      <a href="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h37_59.png"><img class="wp-image-568 size-full alignright" src="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h37_59.png" alt="" width="563" height="113" srcset="http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h37_59.png 563w, http://godev.gemustudio.com/assets/images/2017/03/2017-03-21_23h37_59-300x60.png 300w" sizes="(max-width: 563px) 100vw, 563px" /></a>
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
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="background-color: #ffffaa;">Po tej obszernej wiedzy, warto by poćwiczyć nowe zaklęcia/umiejętności.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Koniec o hipopotamie
    </h2>
    
    <p style="text-align: justify;">
      To ostatni wpis hipopotamowy, mam nadzieję, że forma i treść oraz wartość intelektualna, jaką chciałem przedstawić rozbawi i nauczy.
    </p>
    
    <p style="text-align: justify;">
      Proszę o komentowanie, czy jest to dobra forma, czy też nie?
    </p>
    
    <div>
    </div>
    
    <h2>
    </h2>
    
    <h2>
    </h2>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
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
        <strong>Twitter: </strong><a href="https://twitter.com/gemu_gocom">twitter.com/gemu_gocom</a>, jak by
      </div>
    </div>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>