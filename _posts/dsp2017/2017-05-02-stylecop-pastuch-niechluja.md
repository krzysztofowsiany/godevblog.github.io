---
id: 895
title: 'StyleCop - pastuch na niechluja!'
date: 2017-05-02T22:44:41+00:00
author: Krzysztof Owsiany
layout: post
published: false
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

      Jest pewien sprytny sposób na niechluja w kodzie. Można zmusić kodera do trzymania się określonej etykiety kodowania przy pomocy narzędzia o nazwie **<a href="https://stylecop.codeplex.com/">StyleCop</a>.**
    </p>
    

      W celu instalacji należy uwarzyć magiczną miksturę w kotle o nazwie **Package Manager Console**, **Install-Package StyleCop.Analyzers.**
    </p>
    

      Po instalacji w okienku **Solution Explorer** znajdziemy w referencjach zainstalowanego **StyleCopa**, zawiera on w sobie listę dyrektyw jakie będzie można skonfigurować wedle własnego uznania.
    </p>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/05/stylecop.png"><img class="aligncenter wp-image-976 size-full" src="http://godev.gemustudio.com/assets/images/2017/05/stylecop.png" alt="StyleCop " width="689" height="269" srcset="http://godev.gemustudio.com/assets/images/2017/05/stylecop.png 689w, http://godev.gemustudio.com/assets/images/2017/05/stylecop-300x117.png 300w" sizes="(max-width: 689px) 100vw, 689px" /></a>
    </p>
    

      **VS** podczas kompilacji wyrzuci listę ostrzeżeń dotyczących niezgodności w stylu kodowania. Obrazuje to poniższy zrzut ekranu.
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/05/StyleCop2.png"><img class="aligncenter wp-image-978 size-full" src="http://godev.gemustudio.com/assets/images/2017/05/StyleCop2.png" alt="StyleCop " width="851" height="546" srcset="http://godev.gemustudio.com/assets/images/2017/05/StyleCop2.png 851w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop2-300x192.png 300w, http://godev.gemustudio.com/assets/images/2017/05/StyleCop2-768x493.png 768w" sizes="(max-width: 851px) 100vw, 851px" /></a>
    </p>
    

      W powyższym przypadku **StyleCop** sugeruje, iż usingi powinny być objęte w obszar przestrzeni nazw. Wskazuje na to odpowiednia dyrektywa **SA1200.**
    </p>
    

      I teraz gdzie ten pastuch, a proste obecnie niespójności w stylu kodowania skutkują jedynie ostrzeżeniami. Można skonfigurować **StyleCop** tak by wywalał błędy:D. Tym samym zmuszał do poprawy.
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
        Zbrodni tej dokonać można  poprzez wskazanie dyrektywy w referencjach analizatora **StyleCop.Analyzers**. Wciśnięcie prawego przycisku myszki, wyborze **Set Rule Set Severity** i zaznaczeniu **Error**. Efekt działania na zrzucie poniżej.
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
      Każdy fragment kodu nie spełniający dyrektywy **SA1200**, będzie powodował błąd, czyli będzie do poprawy, nawet najdrobniejszy szczegół jak za dużo spacji za średnikiem, czy za dużo pustych linii między metodami, jest tego wiele zachęcam do przetestowania!
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <h4 style="text-align: center;">
      Być może jest to chamskie:D, jednak uważam, iż jest to dobry sposób by wymusić na programiście dyscyplinę dbania o styl kodu.
    </h4>
    
{% include_relative dsp.md %}