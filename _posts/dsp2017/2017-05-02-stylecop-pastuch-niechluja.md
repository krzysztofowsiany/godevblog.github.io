---
title: StyleCop - pastuch na niechluja!
date: 2017-05-02
author: Krzysztof Owsiany
layout: post
published: true
permalink: /stylecop-pastuch-niechluja
image: /assets/images/2017/05/stylecop-pastuch-niechluja/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - StyleCop
short: Jest pewien sprytny sposób na niechluja w kodzie. Można zmusić kodera do trzymania się określonej etykiety kodowania przy pomocy narzędzia o nazwie StyleCop. W celu instalacji należy uwarzyć magiczną miksturę w kotle o nazwie Package Manager Console, Install-Package StyleCop.Analyzers.
---
[![StyleCop][post]][post-big]{:.post-left-image}
Jest pewien sprytny sposób na niechluja w kodzie. Można zmusić kodera do trzymania się określonej etykiety kodowania przy pomocy narzędzia o nazwie **[StyleCop]**.

W celu instalacji należy uwarzyć magiczną miksturę w kotle o nazwie **Package Manager Console**, **Install-Package StyleCop.Analyzers.**

Po instalacji w okienku **Solution Explorer** znajdziemy w referencjach zainstalowanego **StyleCopa**, zawiera on w sobie listę dyrektyw jakie będzie można skonfigurować wedle własnego uznania.

[![StyleCop][image1]][image1-big]{:.post-right-image}
**VS** podczas kompilacji wyrzuci listę ostrzeżeń dotyczących niezgodności w stylu kodowania. Obrazuje to poniższy zrzut ekranu.

[![StyleCop][image2]][image2-big]{:.post-left-image}    
W powyższym przypadku **StyleCop** sugeruje, iż usingi powinny być objęte w obszar przestrzeni nazw. Wskazuje na to odpowiednia dyrektywa **SA1200.**

I teraz gdzie ten pastuch, a proste obecnie niespójności w stylu kodowania skutkują jedynie ostrzeżeniami. Można skonfigurować **StyleCop** tak by wywalał błędy:D. Tym samym zmuszał do poprawy.

[![StyleCop][image3]][image3-big]{:.post-right-image}
Zbrodni tej dokonać można  poprzez wskazanie dyrektywy w referencjach analizatora **StyleCop.Analyzers**. Wciśnięcie prawego przycisku myszki, wyborze **Set Rule Set Severity** i zaznaczeniu **Error**. Efekt działania na zrzucie poniżej.

[![StyleCop][image4]][image4-big]{:.post-left-image}
Każdy fragment kodu nie spełniający dyrektywy **SA1200**, będzie powodował błąd, czyli będzie do poprawy, nawet najdrobniejszy szczegół jak za dużo spacji za średnikiem, czy za dużo pustych linii między metodami, jest tego wiele zachęcam do przetestowania!
    
**Być może jest to chamskie:D, jednak uważam, iż jest to dobry sposób by wymusić na programiście dyscyplinę dbania o styl kodu.**{:.h-1}
    
{% include_relative dsp.md %}

[StyleCop]: https://stylecop.codeplex.com/

[post]: /assets/images/2017/05/stylecop-pastuch-niechluja/post.jpg
[post-big]: /assets/images/2017/05/stylecop-pastuch-niechluja/post-big.jpg

[image1]: /assets/images/2017/05/stylecop-pastuch-niechluja/image1.png
[image1-big]: /assets/images/2017/05/stylecop-pastuch-niechluja/image1-big.png

[image2]: /assets/images/2017/05/stylecop-pastuch-niechluja/image2.png
[image2-big]: /assets/images/2017/05/stylecop-pastuch-niechluja/image2-big.png

[image3]: /assets/images/2017/05/stylecop-pastuch-niechluja/image3.png
[image3-big]: /assets/images/2017/05/stylecop-pastuch-niechluja/image3-big.png

[image4]: /assets/images/2017/05/stylecop-pastuch-niechluja/image4.png
[image4-big]: /assets/images/2017/05/stylecop-pastuch-niechluja/image4-big.png