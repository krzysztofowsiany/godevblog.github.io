---
title: VPS - noc grozy!
date: 2017-06-09
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

      Początkiem roku podjąłem męską decyzję, migruje do **Dockera** przed końcem 2017 roku. Wczoraj ok **22:00** wykonuję sobie deploja na serwer (**Laravel**), a tu trach problem. **Memmory_limit** w php. Ano to się zwiększy w końcu sobie administruję sam!. **Vim -> /memory_limit -> e -> 256M -> ESC -> :wq**. Brak efektu! **WTF**! Aaa restart **indianina** pomoże&#8230; <span style="font-size: 24px;">**<span style="color: #ff0000;">TRAHHHH padł serwer WWW!</span>**</span>
    </p>
    

      Aaaaaaaaaa i co teraz tyle stron projektów. **OhFuck() ->BLOG!**
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
    

      **Oh fuck spałem! -** a problem się nie naprawił.
    </p>
    

      Po paru godzinach <a href="http://devblaze.gemustudio.com/">kolega</a> zasugerował backup and reinstall apache.
    </p>
    

      Tak po tym działa, jeszcze przywracanie konfiguracji.
    </p>
    
    <h2 style="background-color: lightyellow; text-align: center; padding: 10px;">
      **Ewidentnie pora pozbyć się tego potwora, i w końcu popływać z wielorybem.**
    </h2>
