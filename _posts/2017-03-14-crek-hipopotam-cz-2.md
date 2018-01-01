---
id: 376
title: 'C#rek &#8211; hipopotam cz.2.'
date: 2017-03-14T23:54:02+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=376
permalink: /2017/03/14/crek-hipopotam-cz-2/
image: /images/2017/03/crek_head.png
categories:
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
      <img class="alignleft wp-image-382" src="http://godev.gemustudio.com/images/2017/03/crek-215x300.png" alt="C#rek" width="148" height="207" />Przechadzając się po zielonym, zalesionym bagnie C#rek rozmyślał o robocie, jaką może wykonać przy pomocy tego co się dowiedział. Napotkał też na pewien problem. Ludzie się go boją, uciekają gdy tylko zobaczą wielkiego, strasznego i brzydkiego zielonego stwora. Więc jak u licha zarobi na życie, skoro ludzie się boją i mówią w nieco innym języku. Zaiste to jest problem…
    </p>
    
    <h3 style="text-align: center; padding: 10px;">
      Ale jak już C#rek zostanie starym Ogrem, to ludzie będą sami przychodzić. Wtedy się ich będzie straszyć! Nawet widły i ogień nie pomogą!
    </h3>
    
    <h4 style="text-align: center;">
    </h4>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Ukryte możliwości &#8211; Package Manager Console
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/03/Package-Manager-Console-1.png"><img class="alignright wp-image-389" src="http://godev.gemustudio.com/images/2017/03/Package-Manager-Console-1-300x139.png" alt="" width="315" height="146" srcset="http://godev.gemustudio.com/images/2017/03/Package-Manager-Console-1-300x139.png 300w, http://godev.gemustudio.com/images/2017/03/Package-Manager-Console-1.png 410w" sizes="(max-width: 315px) 100vw, 315px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Hipopotam ma wiele ukrytych zdolności, na pierwszy rzut oka nie widać trzeba odpowiednio połaskotać, by się pojawiły. Połaskotać trzeba w specjalnym miejscu. Niestety nie ma tutaj żadnej sztuczki i trzeba się osobiście pofatygować do:
    </p>
    
    <p style="text-align: justify;">
      <strong>View -> Other Windows -> Package Manager Console.</strong>
    </p>
    
    <p style="text-align: justify;">
      I tam ukaże się dobrodziejstwo, jak się dobrze połaskota to można niezłe cuda znaleźć.
    </p>
    
    <p style="text-align: justify;">
      Ale trzeba wiedzieć jak:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>get-help NuGet</strong> &#8211; podstawowe łaskotanie pozwoli zobaczyć pełne możliwości,
      </li>
      <li style="text-align: justify;">
        <strong>Find-Package</strong> &#8211; tak wykryjemy jakie ukryte zdolności ma ta ociężała bestia,
      </li>
      <li style="text-align: justify;">
        <strong>Get-Package</strong> &#8211; to niezły ruch, bo pokaże wszystko co zwierzak potrafi,
      </li>
      <li style="text-align: justify;">
        <strong>Package-Install</strong> &#8211; jeśli chcemy, by ciągle np. przynosił badyl z bagienka to jest odpowiednie łaskotanie,
      </li>
      <li style="text-align: justify;">
        <strong>Uninstall-Package</strong> &#8211; jak się nie podoba sztuczka, to trzeba oduczyć,
      </li>
      <li style="text-align: justify;">
        <strong>Update-Package</strong> &#8211; warto czasem sprawdzić, czy hipek nie rozwinął już jakiejś znanej zdolności.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Gorzej jak bestia popuści na wyjściu <strong><a href="http://nlog-project.org/">NLoga</a></strong> lub <strong><a href="https://logging.apache.org/log4net/">log4neta</a></strong>.
    </h3>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Obowiązki hipopotama &#8211; Task List
    </h2>
    
    <p style="text-align: justify;">
      Ta mądra bestia potrafi zapamiętać co jest do zrobienia i w odpowiedni sposób przedstawić tą wiedzę.<a href="http://godev.gemustudio.com/images/2017/03/Task-List.png"><img class="alignleft wp-image-399 size-medium" src="http://godev.gemustudio.com/images/2017/03/Task-List-300x205.png" alt="" width="300" height="205" srcset="http://godev.gemustudio.com/images/2017/03/Task-List-300x205.png 300w, http://godev.gemustudio.com/images/2017/03/Task-List.png 377w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p style="text-align: justify;">
      A, że ogry mają dobrą pamięć, bo krótką to warto skorzystać z tego zaklęcia: <strong>Crtl+W, T</strong>.
    </p>
    
    <p style="text-align: justify;">
      W trakcie pracy wystarczy wpisać magiczne słowo <strong>//TODO: tekscik,</strong> a hipopotam zapamięta tą informację.
    </p>
    
    <p>
      Niżej fragment ogro-kodu autorstwa C#reka.
    </p>
    
    <h4 style="text-align: center;">
      Wszelkie prawa zastrzeżone pod groźbą usmażenia i zjedzenia!
    </h4>
    
    <p>
      &nbsp;
    </p>
    
    <pre class="c#">using DietaOgra;

namespace DietaOgra.Dziczyzna
{
    public class Czlowiek : Zwierze
    {
        public Czlowiek(bool widziec)
        {
             if(widziec)
             {
                   Gonic();            
                   Zlapac();
                   //TODO: sprawdzić czy nie narobił w gacie.
                   Zjesc(); 
            }
        }
    }
}
</pre>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      WST (Wyższa Szkoła Tresury) &#8211; Options
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/03/Skróty.png"><img class="alignright wp-image-390 size-medium" src="http://godev.gemustudio.com/images/2017/03/Skróty-300x206.png" alt="" width="300" height="206" srcset="http://godev.gemustudio.com/images/2017/03/Skróty-300x206.png 300w, http://godev.gemustudio.com/images/2017/03/Skróty-768x526.png 768w, http://godev.gemustudio.com/images/2017/03/Skróty.png 814w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Żeby tego było mało, można przełączyć bestie w tryb serwisowy i wówczas to już można robić co się zechce. Pozamieniać nogi z uszami. Pozmieniać komendy do sztuczek, jakich nauczył się hipopotam przez swoje długie życie.
    </p>
    
    <p style="text-align: justify;">
      W tym celu trzeba z menusa zapodać: <strong>Tools -> Options -> Environment -> Keyboard</strong>
    </p>
    
    <p style="text-align: justify;">
      I wówczas całe dobrodziejstwo jest już dostępne, jak na widoczku obok.
    </p>
    
    <p style="text-align: justify;">
      C#rek nie ogarnia tego ogromu możliwości i korzysta z defaultowych ustawień, ale może kiedyś, jak już wszystkie Księżniczki pocałują swoich Żabo-Księciów&#8230;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Krojenie &#8211; Split Code Windows
    </h2>
    
    <p>
      <a href="http://godev.gemustudio.com/images/2017/03/2017-03-14_18h16_17.png"><img class="alignleft wp-image-402 size-medium" src="http://godev.gemustudio.com/images/2017/03/2017-03-14_18h16_17-287x300.png" alt="" width="287" height="300" srcset="http://godev.gemustudio.com/images/2017/03/2017-03-14_18h16_17-287x300.png 287w, http://godev.gemustudio.com/images/2017/03/2017-03-14_18h16_17.png 338w" sizes="(max-width: 287px) 100vw, 287px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Jakby kto chciał i miał naprawdę dużego, wyrośniętego hipopotama, takiego co na 4K wchodzi. To wówczas można sobie pokroić bestię na kawałeczki.
    </p>
    
    <p style="text-align: justify;">
      I z każdego korzystać jak się chce i gdzie się chce.
    </p>
    
    <p>
      Kompozycji jest wiele, można na lewo, można na prawo, na środek, na górę i dół. Trzeba tylko tym gryzoniem dobrze operować przy układaniu.
    </p>
    
    <p>
      Kawałki można na siebie w stertę układać i potem takie zakładki się pokazują. Można wyciągać kawałem na szczyt i na niego patrzeć.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Jak się tak poukłada to już o tym było w <a href="http://godev.gemustudio.com/2017/03/06/crek-hipopotam/">poprzednim tekście</a>. Można zapisać i potem podmieniać wedle widzimisię.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="background: #BBBBBB; padding: 2px;">
      Na koniec
    </h2>
    
    <p style="text-align: justify;">
      Najlepiej w boju także praktykować.<img class=" alignright" src="http://www.advancedcomputers.co.nz/wp-content/themes/ac/img/tv-screen-repair.jpg" width="278" height="185" />
    </p>
    
    <p style="text-align: justify;">
      Więcej na temat hipopotama można znaleźć <a href="https://www.visualstudio.com/pl/vs/">tu</a>.
    </p>
    
    <p style="text-align: justify;">
      Dziękuję za uwagę i proszę o nie rzucanie kamieniami.:D za jęzor i formę wypowiedzi.
    </p>
    
    <p style="text-align: justify;">
      C. D. N.
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
      <a href="http://devstyle.pl/daj-sie-poznac/" target="_blank" rel="noopener noreferrer"><img class="wp-image-104 size-full alignright" title="Daj Się Poznać 2017" src="http://godev.gemustudio.com/images/2017/02/dsp2017-3.png" alt="" width="68" height="154" /></a>
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
        <strong>Twitter: </strong><a href="https://twitter.com/gemu_gocom">twitter.com/gemu_gocom</a>
      </div>
    </div>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>