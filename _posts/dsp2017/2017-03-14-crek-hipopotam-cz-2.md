---
title: C#rek - hipopotam cz.2.
date: 2017-03-14T23:54:02+00:00
author: Krzysztof Owsiany
layout: post
published: true
permalink: /crek-hipopotam-cz-2
image: /assets/images/2017/03/crek-hipopotam-cz-2/post.png
categories:
  - Daj Się Poznać 2017
tags:
  - 'C#rek'
  - dajsiepoznac2017
  - DSP2017
  - Visual Studio 
short: Przechadzając się po zielonym, zalesionym bagnie C#rek rozmyślał o robocie, jaką może wykonać przy pomocy tego co się dowiedział. Napotkał też na pewien problem. Ludzie się go boją, uciekają gdy tylko zobaczą wielkiego, strasznego i brzydkiego zielonego stwora.
---
[![C#rek][image1]][image1-big]{:.post-left-image}
Przechadzając się po zielonym, zalesionym bagnie C#rek rozmyślał o robocie, jaką może wykonać przy pomocy tego co się dowiedział. Napotkał też na pewien problem. Ludzie się go boją, uciekają gdy tylko zobaczą wielkiego, strasznego i brzydkiego zielonego stwora. Więc jak u licha zarobi na życie, skoro ludzie się boją i mówią w nieco innym języku. Zaiste to jest problem…
    
Ale jak już **C#rek** zostanie starym **Ogrem**, to ludzie będą sami przychodzić. Wtedy się ich będzie straszyć! Nawet widły i ogień nie pomogą!
    
## Ukryte możliwości - Package Manager Console
[![Package Manager Console][Package-Manager-Console]][Package-Manager-Console-big]{:.post-right-image} 
Hipopotam ma wiele ukrytych zdolności, na pierwszy rzut oka nie widać trzeba odpowiednio połaskotać, by się pojawiły. Połaskotać trzeba w specjalnym miejscu. Niestety nie ma tutaj żadnej sztuczki i trzeba się osobiście pofatygować do:

**View -> Other Windows -> Package Manager Console.**
    
I tam ukaże się dobrodziejstwo, jak się dobrze połaskota to można niezłe cuda znaleźć.

Ale trzeba wiedzieć jak:
* **get-help NuGet** - podstawowe łaskotanie pozwoli zobaczyć pełne możliwości,
* **Find-Package** - tak wykryjemy jakie ukryte zdolności ma ta ociężała bestia,
* **Get-Package** - to niezły ruch, bo pokaże wszystko co zwierzak potrafi,
* **Package-Install** - jeśli chcemy, by ciągle np. przynosił badyl z bagienka to jest odpowiednie łaskotanie,
* **Uninstall-Package** - jak się nie podoba sztuczka, to trzeba oduczyć,
* **Update-Package** - warto czasem sprawdzić, czy hipek nie rozwinął już jakiejś znanej zdolności.

Gorzej jak bestia popuści na wyjściu **[NLoga]** lub **[log4neta]**.
    
## Obowiązki hipopotama - Task List
Ta mądra bestia potrafi zapamiętać co jest do zrobienia i w odpowiedni sposób przedstawić tą wiedzę.
[![Task List][Task-List]][Task-List-big]{:.post-left-image} 
A, że ogry mają dobrą pamięć, bo krótką to warto skorzystać z tego zaklęcia: **Crtl+W, T**.

W trakcie pracy wystarczy wpisać magiczne słowo **//TODO: tekścik,** a hipopotam zapamięta tą informację.

Niżej fragment ogro-kodu autorstwa C#reka.
    
**Wszelkie prawa zastrzeżone pod groźbą usmażenia i zjedzenia!**{:.h-1}

```csharp
using DietaOgra;

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
                   //TODO: 
                   //sprawdzić czy nie narobił w gacie.
                   Zjesc(); 
            }
        }
    }
}
```
    
## WST (Wyższa Szkoła Tresury) - Options
[![Options][Options]][Options-big]{:.post-left-image} 
Żeby tego było mało, można przełączyć bestie w tryb serwisowy i wówczas to już można robić co się zechce. Pozamieniać nogi z uszami. Pozmieniać komendy do sztuczek, jakich nauczył się hipopotam przez swoje długie życie.

W tym celu trzeba z menusa zapodać: **Tools -> Options -> Environment -> Keyboard**.

I wówczas całe dobrodziejstwo jest już dostępne, jak na widoczku obok.

C#rek nie ogarnia tego ogromu możliwości i korzysta z defaultowych ustawień, ale może kiedyś, jak już wszystkie Księżniczki pocałują swoich Żabo-Księciów...
    
## Krojenie - Split Code Windows
[![Split Code Windows][console]][console-big]{:.post-right-image} 
Jakby kto chciał i miał naprawdę dużego, wyrośniętego hipopotama, takiego co na 4K wchodzi. To wówczas można sobie pokroić bestię na kawałeczki.

I z każdego korzystać jak się chce i gdzie się chce.

Kompozycji jest wiele, można na lewo, można na prawo, na środek, na górę i dół. Trzeba tylko tym gryzoniem dobrze operować przy układaniu.

Kawałki można na siebie w stertę układać i potem takie zakładki się pokazują. Można wyciągać kawałem na szczyt i na niego patrzeć.

Jak się tak poukłada to już o tym było w [poprzednim tekście][crek-hipopotam]. Można zapisać i potem podmieniać wedle widzimisię.
    
## Na koniec
Najlepiej w boju także praktykować. 
![Najlepiej w boju także praktykować][image2]{:.post-left-image} 

Więcej na temat hipopotama można znaleźć <a href="https://www.visualstudio.com/pl/vs/">tu</a>.

Dziękuję za uwagę i proszę o nie rzucanie kamieniami.:D za jęzor i formę wypowiedzi.

C. D. N.
    
{% include_relative dsp.md %}

[crek-hipopotam]: {{site.url}}/crek-hipopotam

[NLoga]: http://nlog-project.org/
[log4net]: https://logging.apache.org/log4net

[post]: /assets/images/2017/03/crek-hipopotam-cz-2/post.jpg
[post-big]: /assets/images/2017/03/crek-hipopotam-cz-2/post-big.jpg

[image1]: /assets/images/2017/03/crek-hipopotam-cz-2/image1.png
[image1-big]: /assets/images/2017/03/crek-hipopotam-cz-2/image1-big.png

[image2]: /assets/images/2017/03/crek-hipopotam-cz-2/image2.jpg

[Package-Manager-Console]: /assets/images/2017/03/crek-hipopotam-cz-2/Package-Manager-Console.png
[Package-Manager-Console-big]: /assets/images/2017/03/crek-hipopotam-cz-2/Package-Manager-Console-big.png

[Task-List]: /assets/images/2017/03/crek-hipopotam-cz-2/Task-List.png
[Task-List-big]: /assets/images/2017/03/crek-hipopotam-cz-2/Task-List-big.png

[Options]: /assets/images/2017/03/crek-hipopotam-cz-2/Options.png
[Options-big]: /assets/images/2017/03/crek-hipopotam-cz-2/Options-big.png

[console]: /assets/images/2017/03/crek-hipopotam-cz-2/console.png
[console-big]: /assets/images/2017/03/crek-hipopotam-cz-2/console-big.png

