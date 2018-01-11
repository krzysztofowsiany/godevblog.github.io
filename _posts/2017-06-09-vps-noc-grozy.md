---
title: VPS - noc grozy!
date: 2017-06-09T13:57:10+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: vps-noc-grozy
image: /assets/images/2017/06/ vps-noc-grozy/blogging-photo-7983.jpg
categories:
tags:
  - Apache
  - Docker
  - Laravel
  - PHP
  - Story from my life
  - Z życia wzięte
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">

      Początkiem roku podjąłem męską decyzję, migruje do <strong>Dockera</strong> przed końcem 2017 roku. Wczoraj ok <strong>22:00</strong> wykonuję sobie deploja na serwer (<strong>Laravel</strong>), a tu trach problem. <strong>Memmory_limit</strong> w php. Ano to się zwiększy w końcu sobie administruję sam!. <strong>Vim -> /memory_limit -> e -> 256M -> ESC -> :wq</strong>. Brak efektu! <strong>WTF</strong>! Aaa restart <strong>indianina</strong> pomoże&#8230; <span style="font-size: 24px;"><strong><span style="color: #ff0000;">TRAHHHH padł serwer WWW!</span></strong></span>
    </p>
    

      Aaaaaaaaaa i co teraz tyle stron projektów. <strong>OhFuck() ->BLOG!</strong>
    </p>
    

      Dwie godziny walki z g____m, nic żadnego konstruktywnego rozwiązania  a tu zegar tyka pora spać strony nie działają&#8230;<a href="http://godev.gemustudio.com/assets/images/2017/04/event.png"><img class="wp-image-819 alignright" src="http://godev.gemustudio.com/assets/images/2017/04/event-300x272.png" alt="Laravel" width="292" height="265" srcset="http://godev.gemustudio.com/assets/images/2017/04/event-300x272.png 300w, http://godev.gemustudio.com/assets/images/2017/04/event-768x697.png 768w, http://godev.gemustudio.com/assets/images/2017/04/event.png 1000w" sizes="(max-width: 292px) 100vw, 292px" /></a>
    </p>
    

      Chwile po tym.
    </p>
    

      <span style="color: #00aa00;">shutdown</span>
    </p>
    

      <span style="color: #00aa00;">*</span>
    </p>
    

      <span style="color: #00aa00;">*</span>
    </p>
    

      <span style="color: #00aa00;">*</span>
    </p>
    

      <span style="color: #00aa00;">start</span>
    </p>
    

      <span style="color: #00aa00;">loading&#8230;</span>
    </p>
    

      <span style="color: #00aa00;">sytem started.</span>
    </p>
    

      <strong>Oh fuck spałem! &#8211;</strong> a problem się nie naprawił.
    </p>
    

      Po paru godzinach <a href="http://devblaze.gemustudio.com/">kolega</a> zasugerował backup and reinstall apache.
    </p>
    

      Tak po tym działa, jeszcze przywracanie konfiguracji.
    </p>
    
    <h2 style="background-color: lightyellow; text-align: center; padding: 10px;">
      <strong>Ewidentnie pora pozbyć się tego potwora, i w końcu popływać z wielorybem.</strong>
    </h2>
