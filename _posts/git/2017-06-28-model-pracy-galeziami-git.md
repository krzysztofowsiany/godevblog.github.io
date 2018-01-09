---
title: Model pracy z gałęziami w GIT
date: 2017-06-28T10:17:19+00:00
author: Krzysztof Owsiany
layout: post
permalink: /model-pracy-galeziami-git/
published: true
image: /assets/images/2017/06/model-pracy-galeziami-git/post.jpg
categories:
  - GIT
tags:
  - Gałęzie
  - GIT
  - Model

short: Ostatnimi czasy natknąłem się w internetach na model pracy z repozytorium GIT wykreowany przez http://nvie.com Vincenta Driessena. Jego podejście sugeruje by trzymać się dwóch głównych gałęzi o nazwach master i jej podgałęzi rozwojowej develop.
---
## Model pracy z GITem od Vincenta Driessena
[![Model pracy z GITem od Vincenta Driessena][image1]][image1-big]{:.post-right-image}
Ostatnimi czasy natknąłem się w internetach na model pracy z repozytorium GIT wykreowany przez **[Vincenta Driessena](http://nvie.com)**. Jego podejście sugeruje by trzymać się dwóch głównych gałęzi o nazwach **master** i jej podgałęzi rozwojowej **develop**.

Gałąź master odzwierciedla docelowy kod programu jaki znajduje się na produkcji z niej wyciągane są podgałęzie w przypadku wymagania poprawek jest to warstwa gałęzi **hotfix branches**.

Z gałęzi **develop** rozwijane są dwie warstwy gałęzi:
* **feature branches** - zawiera podgałęzie nowych funkcjonalności,
* **release branches** - zawiera podgałęzie konkretnych wydań.
 
Z warstwy **feature branches** poprzez **develop** trafiają implementację funkcjonalności do warstwy **release branches**.
    
## Praca z hotfixami
[![MODEL PRACY Z GAŁĘZIAMI W GIT][image2]][image2-big]{:.post-left-image}
Poprawki nanosimy w gałęzi master poprzez ich implementację w warstwie **hotfix branches**. Stosujemy tutaj konwencję nazewnictwa **hotfix-N**.

**N - oznacza wersję do jakiej odnoszą się poprawki, przykładowo jeżeli poprawki nanoszone są na wersji 2.0** to wówczas hotfix można oznaczyć jako wersję **2.0.1**.
    
Po naniesieniu poprawek hotfix należy zmerdżować do gałęzi **develop** oraz **master**. Tak by obie zawierały naniesione poprawki.

Jeżeli w trakcie powstania hotfixa istnieje gałąź w warstwie release branches, to wówczas nie merdżujemy do develop tylko do bieżącej gałęzi releasowej. Ostatecznie po zamknięciu gałęzi release i tak trafi do gałęzi develop.

Przykład:
Do zaimplementowania jest bug znajdujący się w wersji 2.0.    
    
*tworzymy odgałęzienie hotfix-2.0.1*{:.color_3}    

**git checkout -b hotfix-2.0.1 master**{:.color_2}
    
*poprawiamy błąd/błędy, zmieniamy wersję aplikacji na 2.0.1*{:.color_3} 

**git commit -am “Zmiana wersji na 2.0.1”**{:.color_2}
    
*nanosimy poprawki:*{:.color_3}

* *poprawki*{:.color_3}
* *commit... ostatnie poprawki*{:.color_3}
* *ostatni commit*{:.color_3}
    
*łączymy poprawki z gałęzią master*{:.color_3}

**git checkout master**{:.color_2}

**git merge -no-ff hotfix-2.0.1**{:.color_2}

*tagowanie wersji*{:.color_3} 

**git tag -a 1.2.1**{:.color_2}

*Łączymy poprawki z gałęzią develop, jeżeli istnieje gałąź nowego wydania to wówczas łączymy do niego.*{:.color_3} 

**git checkout develop**{:.color_2}
**git merge -no-ff hotfix-2.0.1**{:.color_2}
    
*usuwanie gałęzi poprawki*{:.color_3} 

**git branch -d hotfix-2.0.1**{:.color_2}
    
## Praca z Featureami
[![GIT][post]][post-big]{:.post-right-image}
Nowe funkcjonalności wdrażane w aplikacji powinny znajdować się w swoich indywidualnych pod gałęziach. Daje to niejako piaskownice do pracy nad nimi, i gwarancję, że nie popsujemy funkcjonowania systemu w trakcie prac.

Nazewnictwo gałęzi dotyczących funkcjonalności nie jest tak rygorystycznie określone. Należałoby przyjąć własną konwencję.

Gałęzie z warstwy **feature branches** wywodzą się od gałęzi **develop**.

Przykład:
Praca nad nową funkcją w systemie:  
    
*tworzymy odgałęzienie features/new_ultra_super_feature*{:.color_3} 

**git checkout -b features/new_ultra_super_feature develop**{:.color_2}

*pracujemy nad funkcjami:*{:.color_3} 

*nowa funkcja 1*{:.color_3} 
*nowa funkcja 2*{:.color_3} 
*nowa funkcja 3*{:.color_3} 
    
*łączymy funkcjonalności z gałęzią develop*{:.color_3} 

**git checkout develop**{:.color_2}

**git merge -no-ff features/new_ultra_super_feature**{:.color_2}

*usuwanie gałęzi funkcjonalności*{:.color_3} 

**git branch -d features/new_ultra_super_feature**{:.color_2}
    
## Praca z releasami    
[![Model pracy z repozytorium GITa.][image3]][image3-big]{:.post-left-image}
Releasy to nic innego jak przygotowanie zestawu funkcjonalności do grupowego wydania na produkcję. W warstwie **release branches** stosujemy nazewnictwo  **release-N**.
N - oznacza wersję, będzie to kolejny numerek w konwencji jaka została przyjęta, np. 0.1, 0.2, 1.0, itp.

Gałęzie z warstwy **release branches** wywodzą się od gałęzi **develop** i poprzez właśnie tą gałąź implementowane są nowe funkcje.
    
Jeżeli przygotowania nowego wydania dobiegły końca, należy domerdżować nowy **release** do gałęzi master oraz **develop**.
    
W nowym wydaniu będą znajdować się także hotfixy dlatego, należy połączyć także z gałęzią **develop** (hotfixy znajdą się w gałęzi **develop**).

Przykład:
Przygotowujemy nowe wydanie oznaczone wersją 3.0:
    
*tworzymy odgałęzienie release-3.0*{:.color_3} 

**git checkout -b release-3.0 develop**{:.color_2}
    

*zmieniamy wersję aplikacji na 3.0*{:.color_3} 

**git commit -am “Zmiana wersji na 3.0”**{:.color_2}
    
*pracujemy nad funkcjami:*{:.color_3} 

*nowa funkcja 1 -> develop -> release-3.0*{:.color_3} 

*nowa funkcja 2 -> develop -> release-3.0*{:.color_3} 

*nowa funkcja 3 -> develop -> release-3.0*{:.color_3} 
    
*łączymy ewentualne hotfixy (np. dla wersji 2.9)*{:.color_3}

**git merge -no-ff hotfix-2.9.1**{:.color_2}
    
*łączymy wydanie gałęzią master*{:.color_3} 

**git checkout master**{:.color_2}
    
**git merge -no-ff release-3.0**{:.color_2}
     
*tagowanie wersji*{:.color_3}

**git tag -a 3.0**{:.color_2}

    
*łączymy poprawki z gałęzią develop*{:.color_3}

**git checkout develop**{:.color_2}
    
**git merge -no-ff release-3.0**{:.color_2} 

    
*usuwanie gałęzi wydania*{:.color_3}

**git branch -d release-3.0**{:.color_2}

## Linki
* [http://nvie.com/files/Git-branching-model.pdf](http://nvie.com/files/Git-branching-model.pdf)
* [http://nvie.com/posts/a-successful-git-branching-model](http://nvie.com/posts/a-successful-git-branching-model)


[post]: /assets/images/2017/06/model-pracy-galeziami-git/post.jpg
[post-big]: /assets/images/2017/06/model-pracy-galeziami-git/post-big.jpg

[image1]: /assets/images/2017/06/model-pracy-galeziami-git/image1.png
[image1-big]: /assets/images/2017/06/model-pracy-galeziami-git/image1-big.png

[image2]: /assets/images/2017/06/model-pracy-galeziami-git/image2.jpg
[image2-big]: /assets/images/2017/06/model-pracy-galeziami-git/image2-big.jpg    
  
[image3]: /assets/images/2017/06/model-pracy-galeziami-git/image3.jpg
[image3-big]: /assets/images/2017/06/model-pracy-galeziami-git/image3-big.jpg    
  