---
title: VPS - noc grozy!
date: 2017-06-09
author: Krzysztof Owsiany
layout: post
published: true
permalink: /vps-noc-grozy
image: /assets/images/2017/06/vps-noc-grozy/post.jpg
categories:
tags:
  - Apache
  - Docker
  - Laravel
  - PHP
  - Story from my life
  - Z życia wzięte
short: Początkiem roku podjąłem męską decyzję, migruje do Dockera przed końcem 2017 roku. Wczoraj ok 22:00 wykonuję sobie deploja na serwer (Laravel), a tu trach problem. 
---
Początkiem roku podjąłem męską decyzję, migruje do **Dockera** przed końcem 2017 roku. Wczoraj ok **22:00** wykonuję sobie deploja na serwer (**Laravel**), a tu trach problem. **Memmory_limit** w php. Ano to się zwiększy w końcu sobie administruję sam!. **Vim -> /memory_limit -> e -> 256M -> ESC -> :wq**. Brak efektu! **WTF**! Aaa restart **indianina** pomoże&#8230; **TRAHHHH padł serwer WWW!**.

Aaaaaaaaaa i co teraz tyle stron projektów. **OhFuck() ->BLOG!**

Dwie godziny walki z g____m, nic żadnego konstruktywnego rozwiązania  a tu zegar tyka pora spać strony nie działają&#8230;
[![Laravel][image1]][image1-big]{:.post-right-image}
    
Chwile po tym.

**shutdown**

**#**

**#**

**#**

**start**

**loading&#8230;**

**sytem started**

**Oh fuck spałem!** - a problem się nie naprawił.

Po paru godzinach [kolega] zasugerował backup and reinstall apache.
Tak po tym działa, jeszcze przywracanie konfiguracji.

**Ewidentnie pora pozbyć się tego potwora, i w końcu popływać z wielorybem.**{:.h-2}

{% include_relative dsp.md %}

[post]: /assets/images/2017/06/vps-noc-grozy/post.jpg
[post-big]: /assets/images/2017/06/vps-noc-grozy/post-big.jpg

[image1]: /assets/images/2017/06/vps-noc-grozy/image1.png
[image1-big]: /assets/images/2017/06/vps-noc-grozy/image1-big.png

[kolega]: {{site.blaze}}