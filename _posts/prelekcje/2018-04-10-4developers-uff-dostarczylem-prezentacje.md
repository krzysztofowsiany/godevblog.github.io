---
title: 4Developers - Uff!! Dostarczyłem prezentację.
date: 2018-04-10
author: Krzysztof Owsiany
layout: post
permalink: /4developers-uff-dostarczylem-prezentacje
published: true
comments: true
image: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/post.jpg
image_big: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/post-big.jpg
categories:
  - Prelekcje
  - 4Developers
  - Wstąpienie  
  - Reactive Extensions
tags:
  - Reactive Extensions
  - Prezentacja
  - 4Developers
  - Wstąpienie  
short: Dawno, a nawet bardzo dawno mnie tutaj nie było po wyzwaniu od Mirka, praktycznie jeden post powstał. Czemu tak się stało? To był j ak piorun z jasnego nie ba, po moim zgłoszeniu jako prelegent na konferencje 4Developers 2018 organizowaną w Warszawie. Okazało się, że się dostałem!!!!
---

Dawno, a nawet bardzo dawno mnie tutaj nie było po wyzwaniu od **[Mirka]**, praktycznie jeden post powstał.
Czemu tak się stało?
To był j ak piorun z jasnego nie ba, po moim zgłoszeniu jako prelegent na konferencje 4Developers 2018 organizowaną w Warszawie. Okazało się, że się dostałem!!!!

## Prezentacja
[![4Developers][post]][post-big]{:.post-right-image}
Ruszyłem z przygotowaniami mojej prezentacji: **Reactive Extensions - wzorzec obserwatora, czyli programowanie sterowane zdarzeniami**.

Niespodziewanie, bardzo mi się przydało doświadczenie jakie zdobyłem podczas 30-dniowego wyzwania.

Rozrzuciłem na ścianie wszystkie pojęcia, słowa jakie mi przyszły do głowy dotyczące tematu. I przez pewien czas tak to zostało, czasem dokładałem coś jeszcze. 
Jak już odniosłem, wrażenie, że więcej nic z siebie nie wyduszę to zrobiłem z tych pojęć, grupy (**Bounding Context**). Miałem  dzięki temu pogląd jakie slajdy chcę zbudować.
Kolejnym krokiem było rozdysponowanie czasu na: wstęp, zakończenie, prezentację typowo związaną z tematykę oraz livecoding:
* Wstęp 2x3 minuty,
* Teoria 4x3 minuty,
* Livecoding 8x3 minuty,
* Zakończenie 1x3 minuty.

Łącznie daje to 45 minut.

Kolejnym etapem było zbudowanie mięcha, przykładów. Powstało ich 5. Wszystkie poszły na [github-a].

Na końcu zabrałem się za stworzenie samej prezentacji.

Po wszystkich przygotowaniach, pora na przetestowanie tej implementacji.
Okazało się, że zdołam pokazać nie 5, nie 3 a tylko 1 przykład, i to z lekkim nagięciem czasu.

Skutkiem tego było zmniejszenie czasu poświęconego na slajdy.

Po pierwszych testach mogłem już trenować. I tutaj rozplanowałem  sobie co i kiedy.

Ten plan dowiozłem do końca. Jednak lekko ucierpiało na tym moje gardło:)

Nigdy wcześniej nie byłem tak dobrze przygotowany do prezentacji, ale także skala wydarzenia dla mnie nie była  jeszcze tak duża:)

## Konferencja i before
[![4Developers][image2]][image2-big]{:.post-left-image}
Dzień wyjazdu na konferencje był lekko zwariowany, najpierw trenowanie prezentacji, potem bieg na 10km, super szybkie ogarnięcie się po biegu, i wyjazd do warszawy. 330km:)

Udało się dotrzeć ok. godziny 21. Rejestracja, meldunek i wypad na before. Jako, że wszędzie jeżdżę z moją maskotką IT (Żona;)).

Tym razem było nie inaczej, udało nam się spotkać kilu znajomych z czego jestem bardzo zadowolony.

9 kwietnia, w hotelu tłumy, wyjście na pierwszą prezentację dostarczoną przez **[Arka Benedykta]** -> **100% pokrycia testami, czy to jest w ogóle możliwe?**{:.color_1}.

Szczególnie w pamięci utkwi mi slajd przedstawiający 100% pokrycie testami przedstawiony w postaci bloków na poszczególnych pozycjach piramidy testów. Prawdą jest nawet stwierdzenie, że to pokrycie jest znacznie większe:) Każda z kolejnych pozycji piramidy testów pokrywa luki warstwy niższej. Tworząc tym samym całościowe pokrycie testami w kontekście całej piramidy. Po prostu super!! Nie myślałem nigdy w ten sposób o testach. Metafora lodów, sadełka w kontekście **Legacy Code** też świetna:)

**W planach mieliśmy jeszcze obejrzeć kilka prezentacji, jednak miałem zaplanowany trening własnej i należało go przeprowadzić, tak strzeliła godzina:)**{:.h-1}

Kolejne wystąpienia jakie odwiedziliśmy, to występ Maestro **[Korsan-a]** -> **Disco.js**{:.color_1}. Super interaktywna prezentacja związana z przetwarzaniem  dźwięku w przeglądarkach z wykorzystaniem JS. Oczywiście nie miałem pojęcia, że ta technologia tak mocno się rozwinęła. To co zobaczyłem, dostarczyło mi masę wiedzy w na temat manipulacją dźwiękiem w przeglądarce:). 

Prezentację można spokojnie brać w kontekście inspiracji, by łamać wzorce, reguły. I dostarczać naprawdę świetne prezentacji:). Jak to mówi **Maciej**: **"Tworzenie front-end-u to sztuka, a nie programowanie."**{:.color_1}

Nie mogłem oczywiście pominąć prezentacji o wielorybach jaką przygotowali wspólnie **[Piotr Gankiewicz]** i **[Dariusz Pawlukiewicz]** -> **Distributed .NET Core**{:.color_1}. Oczywiście się nie zawiodłem: **CQRS**, Architektura przedstawionej aplikacji, **Rancher**, **TravisCI**, etc :D. Prezentacja z dużą ilością wiedzy z naciskiem na budowanie oprogramowania na bazie mikro-serwisów i .NET Core. Nie zabrakło oczywiście automatyzacji (CI/DI).
Jedyny minus, to temperatura w sali. Ale się nie dziwię było tyle podniesionych kontenerów w tej serwerowni, że klima nie dawała rady;) Ale to logiczne, że mikro-serwisy podnoszą poziom utylizacji serwera:)  Nawet na podłodze i w kątach się instancje znalazły;) 

**Tutaj pora na mój show ale o tym niżej;)**{:.color_1}

Kolejny na celowniku był **[Rafała Hryniewski]** -> **ORM - the tip of an iceberg**{:.color_1}. Okazało się, że to niezły wyjadacz **SQL-owy**{:.color_1}. Wnioski oczywiście nieco zbliżone do moich. Tak jak czysty **SQL**{:.color_1} nie jest lekiem na całe zło, tak samo jest ze stosowaniem **ORM-ów**{:.color_1}. Jak zwykle sprawdza się stwierdzenie, że wszystko zależy od zastosowania. 

Zainteresował mnie aspekt nowych możliwości jakie daje **SQLServe-a**{:.color_1}, np. maskowanie danych w bazie. Świetnie się nadaje do ukrywania danych. Być może bardzo przydatne w trakcie nadejścia RODO:) Oczywiście Rafał dowiózł świetną prezentację, a co ważniejsze dużo **[SQL-wej]**{:.color_1} wiedzy.

Na koniec prezentacja **[Radka Maziarki]** -> **CQRS w 4 krokach**{:.color_1}. Widziałem tą prezentację już wcześniej, jednak zawsze rozwinie moje pojęcie o CQRS-sie. Znajdzie się taki skład słów, który wzbogaci moją wiedzę na ten temat. Radek pomimo początkowych problemów ze sprzętem, odstawił świetne wystąpienie. No cóż posiada wiedzę i doświadczenie w tym kontekście. Więc się nie dziwię:)


## Moje wystąpienie
[![4Developers][image1]][image1-big]{:.post-right-image}
O dziwo nie denerwowałem się cały dzień. Tak na prawdę to przed samym wystąpieniem, lekko poczułem nerwy. Zapewne to były skutki przygotowania:). Niefortunnie sobie uszkodziłem odbiornik prezentera przy podpinaniu kabelka HDMI. Peszek ale działa. Kolejny problem jaki miałem to pierwszy kontakt ze zdalnym mikrofonem. Ale sobie poradziłem (I'm engineer :).

Wybiła 15:15 jak w westernie, i jazda pofrunąłem. W trakcie wyczuwałem zdenerwowanie, ale to naprawdę kosmos do tego co było dawniej! Nie nauczyłem się na pamięć, wiedziałem jedynie co chcę powiedzieć i mówiłem. Po czym przeszedłem do kodowania. I w formie jaką przygotowałem było to moje ostatnie wystąpienie. Kolejne jakie przygotuję:) Będą inne. Już mam plany na refaktoryzację prezentacji! Po mimo trudności dowiozłem prezentację, pokazałem kulki:) 
Kończąc poprosiłem o krytyczny feedback jako podkreślając na końcu, że mi się przyda bo to moja pierwsza prelekcja na taką skalę i w takich warunkach.
Oczywiście mam dużą nadzieję, żę nie ostatnia:)
Brawa były - nie było źle. Nikt nie buczał. Nawet były osoby, którym się podobało :)
Feadback też dostałem, indywidualnie, niestety nie wiem tak na prawdę od kogo. Ale z góry dziękuję.

## Wnioski
Z czasem jaki upływa od mojej prelekcji, coraz bardziej uświadamiam sobie co się stało. I moje zadowolenie bardzo rośnie!!! Prawda jest taka, że już się nie mogę doczekać kolejnej edycji i zgłoszenia tematów:) Zdecydowanie myślę, też o wystąpieniu w innych miejscach. **[Nawet mam już zabukowane terminy na kilku grupach .NET:)][prelekcje]**

Mówiąc po cichu, planowałem w tym roku wystąpić na jakiejś konferencji. Taki cel jeden z celów na 2018. Kto by pomyślał, że zostanie zrealizowany już w pierwszym kwartale. I to jeszcze w takiej skali:)

Pozostaje, nanieść poprawki i koko-jumbo i do przodu:)

## Podziękowania
Kończąc chciałbym podziękować za to, że mogłem wystąpić w zasadzie należy się to głównie opiekunowi ścieżek .NET na 4Developers **[Maciejowi]**. Za to, że nie wiem Bóg Perun uderzył w niego piorunem i wybrał między innymi mój temat:). A tak naprawdę to za to, że wyciągnął Mnie i wiele innych osób z piwnicy:). **Inspiruje!**{:.color_1} **Motywuje!**{:.color_1} **Stylizuje!**{:.color_1}

Zdecydowanie, podziękowania też należą się mojej Żonie. Za cierpliwość oraz za to, że w chwilach zwątpienie, potrafi mnie opie...... I zmotywować do działania:)

Podziękowania też należą się organizatorom **[4Developers]**, za organizację tak dużej konferencji.


[Mirka]: https://youtu.be/4AA2DqA2YDo?list=PLxnSvy9dttDngDAGdjwDnM2VtpjDd6AXR
[github-a]: https://github.com/godevblog/30DayChallenge
[Arka Benedykta]: www.benedykt.net
[Korsan-a]: https://korsan.pl/

[Piotr Gankiewicz]: http://piotrgankiewicz.com/
[Dariusz Pawlukiewicz]: http://foreverframe.net
[Rafała Hryniewski]: http://hryniewski.net/
[Radka Maziarki]: https://radblog.pl/

[prelekcje]: {{site.url}}/prelekcje
[Maciejowi]: http://devstyle.pl/

[4Developers]: https://4developers.org.pl


[post]: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/post.jpg
[post-big]: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/post-big.jpg

[image1]: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/image1.jpg
[image1-big]: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/image1-big.jpg

[image2]: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/image2.jpg
[image2-big]: /assets/images/2018/04/4developers-uff-dostarczylem-prezentacje/image2-big.jpg