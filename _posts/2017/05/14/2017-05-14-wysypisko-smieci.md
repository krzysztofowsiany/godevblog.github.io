---
id: 1060
title: 'Garbage Collector &#8211; Wysypisko śmieci.'
date: 2017-05-14T22:58:28+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1060
permalink: /2017/05/14/wysypisko-smieci/
dslc_post_template:
  - default
image: /assets/images/2017/05/IMG_9281.jpg
categories:
  - Bez kategorii
  - Daj Się Poznać 2017
tags:
  - 'C#'
  - dajsiepoznac2017
  - DSP2017
  - Garbage Collection
  - GC
  - 'Mark&amp;Sweep'
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_0108.jpg"><img class="alignright wp-image-1089 size-medium" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_0108-200x300.jpg" alt="Garbage Collector" width="200" height="300" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_0108-200x300.jpg 200w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0108-683x1024.jpg 683w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0108.jpg 720w" sizes="(max-width: 200px) 100vw, 200px" /></a>Nasz wspaniały język C#, znosi z nas prawie pełną odpowiedzialność za sprzątanie po sobie.
    </p>
    
    <p style="text-align: justify;">
      Można by rzec, iż mamy zatrudnioną sprzątaczkę i nawet nie wiemy, kiedy magicznie bałagan znika. Oczywiści mowa tutaj o <strong>Garbage Collector</strong>.
    </p>
    
    <p style="text-align: justify;">
      Jeszcze dzisiaj pamiętam trudność, i obowiązek kontrolowania wycieków pamięci, gdy pisałem oprogramowanie z wykorzystaniem języka C++.
    </p>
    
    <p style="text-align: justify;">
      Z drugiej strony człowiek był bardziej odpowiedzialny za to co się działo w kodzie.
    </p>
    
    <p style="text-align: justify;">
      Teraz w dobie ogromnych pamięci RAM, <strong>GC</strong>, często można  zapomnieć o wyciekach pamięci.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="text-align: justify;">
      Działanie
    </h1>
    
    <p style="text-align: justify;">
      Alokowanie pamięci odbywa się niejako w dwóch miejscach:
    </p>
    
    <ul style="text-align: justify;">
      <li>
        na <strong>stosie (Stack)</strong> &#8211; zarządzaniem zajmuje się CLR (Common Language Runtime), i zawiera referencje do faktycznie utworzonych obiektów na stercie,
      </li>
      <li>
        na <strong>sterta (Heap)</strong> &#8211;  zarządzaniem zajmuje się GC.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      Śmietnik działa  bardzo sprytnie, w pierwszej fazie (<strong>Mark</strong>) znakuje obiekty jakie są używane -> istnieją powiązane z obiektem referencje (<span style="color: #ff0000;"><strong>Stack -> Heap</strong></span>),  po czym  zaznacza je.
    </p>
    
    <p style="text-align: justify;">
      Tak oznaczone obiekty nie zostaną usunięte w fazie drugiej (<strong>Sweep</strong>).
    </p>
    
    <h2 style="text-align: center; background-color: lightblue; padding: 10px;">
      Tym sposobem dochodzimy do nazwy stosowanego w GC algorytmu -> <strong>Mark & Sweep</strong>.
    </h2>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Aplikacje składają  się z wielu obiektów, i proces czyszczenia może trwać dość długo, zależnie od ilości obiektów. Dlatego nie jest on często uruchamiany.
    </p>
    
    <p style="text-align: justify;">
      Automatyczne wyzwoleni <strong>GC</strong> następuje w sytuacji gdy zostanie przekroczony pewien zakres pamięci.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Generacje
    </h1>
    
    <p style="text-align: justify;">
      <strong>GC</strong> kategoryzuje obiekty według ich wieku powstania, tym samym przydzielane są do odpowiednich pokoleń oznaczanych odpowiednio <strong>0, 1, 2</strong>.
    </p>
    
    <p style="text-align: justify;">
      Zmiana pokolenia następuje podczas uruchomienia <strong>GC</strong>, awans w pokoleniu następuje gdy obiekt nie nadaje się do zniszczenia.<a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_0307.jpg"><img class="aligncenter wp-image-1090 size-medium" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_0307-300x200.jpg" alt="Garbage Collector" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_0307-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0307-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0307-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Jeżeli obiekt jest potrzebny i są do niego powiązane referencje ze stosu na stertę to wówczas jest on ważny i podbijana jest jego ranka od 0 do 2.
    </p>
    
    <p>
      Do generacji przydzielany jest budżet, dla 0 przyjmuje się wielkość <strong>256 KB</strong>, w przypadku przekroczenia podczas  alokowanie nowego obiektu następuje uruchomienie czyszczenia na generacji 0, w tym czasie istnieje duża szansa, iż część obiektów nadaje się do zniszczenia lub awansu na wyższe pokolenie.
    </p>
    
    <p>
      Po przeczyszczeniu następuje ponowna próba alokacji jeżeli się nie powiedzie to automatycznie obiekt awansuje do wyższej generacji.
    </p>
    
    <p>
      Generacja zerowa jest miejscem gdzie obiekty są najczęściej tworzone i niszczone, dlatego też jej wielkość <strong>256 KB</strong>, jest obszarem, który powinien z łatwością zmieścić się w pamięci  <strong>L2 &#8211; cache procesora</strong>.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>C.D.N.</strong>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <div style="text-align: justify;">
        <strong>Jest to post przygotowany na potrzeby konkursu &#8222;Daj Się Poznać 2017&#8221; organizowanym przez <a href="http://devstyle.pl">Macieja Aniserowicza</a>.</strong>
      </div>
      
      <div style="text-align: justify;">
        <a href="http://devstyle.pl/daj-sie-poznac/" target="_blank" rel="noopener noreferrer"><img class="wp-image-104 size-full alignright" title="Daj Się Poznać 2017" src="http://godev.gemustudio.com/assets/images/2017/02/dsp2017-3.png" alt="" width="68" height="154" /></a>
      </div>
      
      <div style="font-size: 10pt; padding: 10px;">
        <div style="text-align: justify;">
          <strong>Projekt: </strong><a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/">PictOgr</a>.
        </div>
        
        <div style="text-align: justify;">
          <strong>GitHub: </strong><a href="https://github.com/krzysztofowsiany/pictogr">github.com/krzysztofowsiany/pictogr</a>
        </div>
        
        <div style="text-align: justify;">
          <strong>Blog: </strong><a href="http://godev.gemustudio.com">godev.gemustudio.com</a>
        </div>
        
        <div style="text-align: justify;">
          <strong>Snapchat</strong>: <a href="https://www.snapchat.com/add/gocom7" target="_blank" rel="noopener noreferrer">gocom7</a>
        </div>
        
        <div style="text-align: justify;">
          <strong>RSS: </strong><a href="http://godev.gemustudio.com/category/daj-sie-poznac-2017/feed">godev.gemustudio.com/category/daj-sie-poznac-2017/feed</a>
        </div>
        
        <div style="text-align: justify;">
          <strong>Facebook:</strong><a href="https://www.facebook.com/PictOgr-1729700930654225/">www.facebook.com/PictOgr-1729700930654225/</a>
        </div>
        
        <div style="text-align: justify;">
          <strong>Twitter: </strong><a href="https://twitter.com/gemu_gocom">twitter.com/gemu_gocom</a>
        </div>
      </div>
    </div>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>