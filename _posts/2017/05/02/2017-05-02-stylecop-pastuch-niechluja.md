---
id: 895
title: 'StyleCop &#8211; pastuch na niechluja!'
date: 2017-05-02T22:44:41+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=895
permalink: /2017/05/02/stylecop-pastuch-niechluja/
image: /assets/images/2017/05/IMG_9832.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - StyleCop
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      Jest pewien sprytny sposób na niechluja w kodzie. Można zmusić kodera do trzymania się określonej etykiety kodowania przy pomocy narzędzia o nazwie <strong><a href="https://stylecop.codeplex.com/">StyleCop</a>.</strong>
    </p>
    
    <p style="text-align: justify;">
      W celu instalacji należy uwarzyć magiczną miksturę w kotle o nazwie <strong>Package Manager Console</strong>, <strong>Install-Package StyleCop.Analyzers.</strong>
    </p>
    
    <p style="text-align: justify;">
      Po instalacji w okienku <strong>Solution Explorer</strong> znajdziemy w referencjach zainstalowanego <strong>StyleCopa</strong>, zawiera on w sobie listę dyrektyw jakie będzie można skonfigurować wedle własnego uznania.
    </p>
    
    <p style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/05/stylecop.png"><img class="aligncenter wp-image-976 size-full" src="http://godev.gemustudio.com/assets/images/2017/05/stylecop.png" alt="StyleCop " width="689" height="269" srcset="http://godev.gemustudio.com/assets/images/2017/05/stylecop.png 689w, http://godev.gemustudio.com/assets/images/2017/05/stylecop-300x117.png 300w" sizes="(max-width: 689px) 100vw, 689px" /></a>
    </p>
    
    <p style="text-align: justify;">
      <strong>VS</strong> podczas kompilacji wyrzuci listę ostrzeżeń dotyczących niezgodności w stylu kodowania. Obrazuje to poniższy zrzut ekranu.
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/05/StyleCop2.png"><img class="aligncenter wp-image-978 size-full" src="http://godev.gemustudio.com/assets/images/2017/05/StyleCop2.png" alt="StyleCop " width="851" height="546" srcset="http://godev.gemustudio.com/assets/images/2017/05/StyleCop2.png 851w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop2-300x192.png 300w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop2-768x493.png 768w" sizes="(max-width: 851px) 100vw, 851px" /></a>
    </p>
    
    <p style="text-align: justify;">
      W powyższym przypadku <strong>StyleCop</strong> sugeruje, iż usingi powinny być objęte w obszar przestrzeni nazw. Wskazuje na to odpowiednia dyrektywa <strong>SA1200.</strong>
    </p>
    
    <p style="text-align: justify;">
      I teraz gdzie ten pastuch, a proste obecnie niespójności w stylu kodowania skutkują jedynie ostrzeżeniami. Można skonfigurować <strong>StyleCop</strong> tak by wywalał błędy:D. Tym samym zmuszał do poprawy.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <div>
      <div style="text-align: justify;">
        <a href="http://godev.gemustudio.com/assets/images/2017/05/StyleCop3.png"><img class="aligncenter wp-image-982 size-full" src="http://godev.gemustudio.com/assets/images/2017/05/StyleCop3.png" alt="" width="569" height="222" srcset="http://godev.gemustudio.com/assets/images/2017/05/StyleCop3.png 569w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop3-300x117.png 300w" sizes="(max-width: 569px) 100vw, 569px" /></a>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <div style="text-align: justify;">
        Zbrodni tej dokonać można  poprzez wskazanie dyrektywy w referencjach analizatora <strong>StyleCop.Analyzers</strong>. Wciśnięcie prawego przycisku myszki, wyborze <strong>Set Rule Set Severity</strong> i zaznaczeniu <strong>Error</strong>. Efekt działania na zrzucie poniżej.
      </div>
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <div style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/05/StyleCop5.png"><img class="aligncenter wp-image-983 size-full" src="http://godev.gemustudio.com/assets/images/2017/05/StyleCop5.png" alt="" width="968" height="117" srcset="http://godev.gemustudio.com/assets/images/2017/05/StyleCop5.png 968w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop5-300x36.png 300w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop5-768x93.png 768w" sizes="(max-width: 968px) 100vw, 968px" /></a>
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <div style="text-align: justify;">
      Każdy fragment kodu nie spełniający dyrektywy <strong>SA1200</strong>, będzie powodował błąd, czyli będzie do poprawy, nawet najdrobniejszy szczegół jak za dużo spacji za średnikiem, czy za dużo pustych linii między metodami, jest tego wiele zachęcam do przetestowania!
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <h4 style="text-align: center;">
      Być może jest to chamskie:D, jednak uważam, iż jest to dobry sposób by wymusić na programiście dyscyplinę dbania o styl kodu.
    </h4>
    
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