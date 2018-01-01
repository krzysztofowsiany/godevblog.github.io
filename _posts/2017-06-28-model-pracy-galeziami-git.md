---
id: 1530
title: Model pracy z gałęziami w GIT
date: 2017-06-28T10:17:19+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1530
permalink: /2017/06/28/model-pracy-galeziami-git/
dslc_post_template:
  - default
image: /assets/images/2017/06/blogging-photo-2016.jpg
categories:
  - Bez kategorii
  - GIT
tags:
  - Gałęzie
  - GIT
  - Model
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <div id="attachment_1541" style="width: 236px" class="wp-caption alignright">
      <a href="http://godev.gemustudio.com/assets/images/2017/06/git-model@2x.png"><img class="wp-image-1541 size-medium" title="Model pracy z GITem od Vincenta Driessena" src="http://godev.gemustudio.com/assets/images/2017/06/git-model@2x-226x300.png" alt="Model pracy z GITem od Vincenta Driessena" width="226" height="300" srcset="http://godev.gemustudio.com/assets/images/2017/06/git-model@2x-226x300.png 226w, http://godev.gemustudio.com/assets/images/2017/06/git-model@2x-768x1018.png 768w, http://godev.gemustudio.com/assets/images/2017/06/git-model@2x-773x1024.png 773w, http://godev.gemustudio.com/assets/images/2017/06/git-model@2x.png 1150w" sizes="(max-width: 226px) 100vw, 226px" /></a>
      
      <p class="wp-caption-text">
        Model pracy z GITem od Vincenta Driessena
      </p>
    </div>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">Ostatnimi czasy natknąłem się w internetach na model pracy z repozytorium GIT wykreowany przez <a href="http://nvie.com"><strong>Vincenta Driessena</strong></a>. Jego podejście sugeruje by trzymać się dwóch głównych gałęzi o nazwach </span><b>master</b><span style="font-weight: 400;"> i jej podgałęzi rozwojowej </span><b>develop</b><span style="font-weight: 400;">.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">Gałąź master odzwierciedla docelowy kod programu jaki znajduje się na produkcji z niej wyciągane są podgałęzie w przypadku wymagania poprawek jest to warstwa gałęzi </span><b>hotfix branches</b><span style="font-weight: 400;">.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">Z gałęzi </span><b>develop </b><span style="font-weight: 400;">rozwijane są dwie warstwy gałęzi:</span></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-size: 20px;"><b>feature branches</b><span style="font-weight: 400;"> &#8211; zawiera podgałęzie nowych funkcjonalności</span></span>
      </li>
      <li style="font-weight: 400;">
        <span style="font-size: 20px;"><b>release branches</b><span style="font-weight: 400;"> &#8211; zawiera podgałęzie konkretnych wydań</span></span>
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">Z warstwy </span><b>feature branches</b><span style="font-weight: 400;"> poprzez <strong>develop</strong> trafiają implementację funkcjonalności do warstwy </span><b>release branches</b><span style="font-weight: 400;">.</span></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="text-align: justify;">
      <b>Praca z hotfixami</b>
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400;"><a href="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-7235.jpg"><img class="size-medium wp-image-1547 alignleft" src="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-7235-300x200.jpg" alt="MODEL PRACY Z GAŁĘZIAMI W GIT" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-7235-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-7235-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-7235.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a><span style="font-size: 20px;">Poprawki nanosimy w gałęzi master poprzez ich implementację w warstwie <strong>hotfix branches</strong>. Stosujemy tutaj konwencję nazewnictwa </span></span><span style="font-size: 20px;"><b>hotfix-*.</b></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>*</b><span style="font-weight: 400;"> &#8211; oznacza wersję do jakiej odnoszą się poprawki,przykładowo jeżeli poprawki nanoszone są na wersji </span><b>2.0</b><span style="font-weight: 400;"> to wówczas hotfix można oznaczyć jako wersję </span><b>2.0.1</b><span style="font-weight: 400;">.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">Po naniesieniu poprawek hotfix należy zmerdżować do gałęzi </span><b>develop </b><span style="font-weight: 400;">oraz </span><b>master</b><span style="font-weight: 400;">. Tak by obie zawierały naniesione poprawki.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Jeżeli w trakcie powstania hotfixa istnieje gałąź w warstwie release branches, to wówczas nie merdżujemy do develop tylko do bieżącej gałęzi releasowej. Ostatecznie po zamknięciu gałęzi release i tak trafi do gałęzi develop.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Przykład:</span><br /> <span style="font-weight: 400; font-size: 20px;"> Do zaimplementowania jest bug znajdujący się w wersji 2.0.</span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="color: #66aaff; font-size: 20px;"><span style="font-weight: 400;">tworzymy odgałęzienie</span><b> hotfix-2.0.1</b></span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout -b hotfix-2.0.1 master</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="color: #66aaff; font-size: 20px;"><span style="font-weight: 400;">poprawiamy błąd/błędy, z</span>mieniamy wersję aplikacji na 2.0.1</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git commit -am “Zmiana wersji na 2.0.1”</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">nanosimy poprawki:</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><i><span style="font-weight: 400;">. poprawki</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">. commit</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">.</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">.</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">. ostatnie poprawki</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">. ostatni commit</span></i></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">łączymy poprawki z gałęzią master</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout master</b></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git merge &#8211;no-ff hotfix-2.0.1</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">tagowanie wersji</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git tag -a 1.2.1</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">łączymy poprawki z gałęzią develop, jeżeli istnieje gałąź nowego wydania to wówczas łączymy do niego.</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout develop</b></span><br /> <span style="font-size: 20px;"> <b>git merge &#8211;no-ff hotfix-2.0.1</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">usuwanie gałęzi poprawki</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git branch -d hotfix-2.0.1</b></span><br /> <span style="font-weight: 400;"> </span>
    </p>
    
    <h2 style="text-align: justify;">
      <b>Praca z Featureami</b>
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400;"><a href="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-2016.jpg"><img class="size-medium wp-image-1549 alignleft" src="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-2016-300x200.jpg" alt="GIT" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-2016-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-2016-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-2016.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a><span style="font-size: 20px;">Nowe funkcjonalności wdrażane w aplikacji powinny znajdować się w swoich indywidualnych pod gałęziach. Daje to niejako piaskownice do pracy nad nimi, i gwarancję, że nie popsujemy funkcjonowania systemu w trakcie prac.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Nazewnictwo gałęzi dotyczących funkcjonalności nie jest tak rygorystycznie określone. Należałoby przyjąć własną konwencję.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">Gałęzie z warstwy </span><b>feature branches</b><span style="font-weight: 400;"> wywodzą się od gałęzi </span><b>develop</b><span style="font-weight: 400;">.</span></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Przykład:</span><br /> <span style="font-weight: 400; font-size: 20px;"> Praca nad nową funkcją w systemie:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="color: #66aaff; font-size: 20px;"><span style="font-weight: 400;">tworzymy odgałęzienie</span><b> features/new_ultra_super_feature</b></span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout -b features/new_ultra_super_feature develop</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">pracujemy nad funkcjami:</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><i><span style="font-weight: 400;">nowa funkcja 1 </span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">nowa funkcja 2</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">nowa funkcja 3</span></i></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">łączymy funkcjonalności z gałęzią develop</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout develop</b></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git merge &#8211;no-ff features/new_ultra_super_feature</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">usuwanie gałęzi funkcjonalności</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git branch -d features/new_ultra_super_feature</b></span><br /> <span style="font-size: 20px;"> <b> </b></span>
    </p>
    
    <h2>
      <b>Praca z releasami</b>
    </h2>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400;"><a href="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-8056.jpg"><img class="size-medium wp-image-1551 alignleft" src="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-8056-300x200.jpg" alt="Model pracy z repozytorium GITa." width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-8056-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-8056-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/06/blogging-photo-8056.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a><span style="font-size: 20px;">Releasy to nic innego jak przygotowanie zestawu funkcjonalności do grupowego wydania na produkcję. W warstwie <strong>release branches</strong> stosujemy nazewnictwo  </span></span><span style="font-size: 20px;"><b>release-*.</b></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">* &#8211; oznacza wersję, będzie to kolejny numerek w konwencji jaka została przyjęta, np. 0.1, 0.2, 1.0, itp.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Gałęzie z warstwy<strong> release branches</strong> wywodzą się od gałęzi <strong>develop</strong> i poprzez właśnie tą gałąź implementowane są nowe funkcje.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Jeżeli przygotowania nowego wydania dobiegły końca, należy domerdżować nowy <strong>release</strong> do gałęzi master oraz <strong>develop</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><span style="font-weight: 400;">W nowym wydaniu będą znajdować się także hotfixy dlatego, należy połączyć także z gałęzią </span><b>develop </b><span style="font-weight: 400;">(hotfixy znajdą się w gałęzi </span><b>develop</b><span style="font-weight: 400;">).</span></span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-weight: 400; font-size: 20px;">Przykład:</span><br /> <span style="font-weight: 400; font-size: 20px;"> Przygotowujemy nowe wydanie oznaczone wersją 3.0:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="color: #66aaff; font-size: 20px;"><span style="font-weight: 400;">tworzymy odgałęzienie</span><b> release-3.0</b></span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout -b release-3.0 develop</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">zmieniamy wersję aplikacji na 3.0</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git commit -am “Zmiana wersji na 3.0”</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">pracujemy nad funkcjami:</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><i><span style="font-weight: 400;">nowa funkcja 1 -> develop -> release-3.0</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">nowa funkcja 2 -> develop -> release-3.0</span></i></span><br /> <span style="font-size: 20px;"> <i><span style="font-weight: 400;">nowa funkcja 3 -> develop -> release-3.0</span></i></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">łączymy ewentualne hotfixy (np. dla wersji 2.9)</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git merge &#8211;no-ff hotfix-2.9.1</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">łączymy wydanie gałęzią master</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout master</b></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git merge &#8211;no-ff release-3.0</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">tagowanie wersji</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git tag -a 3.0</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">łączymy poprawki z gałęzią develop</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git checkout develop</b></span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git merge &#8211;no-ff release-3.0</b></span>
    </p>
    
    <ul style="text-align: justify;">
      <li style="font-weight: 400;">
        <span style="font-weight: 400; color: #66aaff; font-size: 20px;">usuwanie gałęzi wydania</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 20px;"><b>git branch -d release-3.0</b></span><br /> <span style="font-weight: 400;"> </span>
    </p>
    
    <h2>
      <span style="font-weight: 400;">Linki</span>
    </h2>
    
    <p style="text-align: justify;">
      <a href="http://nvie.com/files/Git-branching-model.pdf"><span style="font-weight: 400;">http://nvie.com/files/Git-branching-model.pdf</span></a><br /> <span style="font-weight: 400;">http://nvie.com/posts/a-successful-git-branching-model/</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>