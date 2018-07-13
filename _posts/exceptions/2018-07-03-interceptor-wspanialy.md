---

title: Interceptor Wspaniały
date: 2018-07-07
author: Krzysztof Owsiany
layout: post
permalink: interceptor-wspanialy
published: false
comments: true
image: /assets/images/2018/07/exceptions/interceptor/post.jpg
categories:
  - Prelekcje
tags:
  - Interceptor
  - Clean Code
  - Exceptions
  - wyjątki

short: 


---
Interceptor catche them all and keep clean code!

Pewnego pięknego dnia, gdy już ostatnia linijka kodu została napisana. A wygrzany Visual zakończył bezwstydnie konsumować RAM i CPU. Poszedł ostatni commit do repozytorium, a wraz z nim Catcher.

Pełnił on ważną funkcję w kodzie, jak jakiś roztargniony developer spowoduje błąd w programie. Catcher miał za zadanie wychwycić tą wyjątkową, ale nader częstą sytuację. Jak już pochwycił to co się zdążyć nie powinno to jego zadaniem było poinformowanie o tym, zapisanie w rejestrze na przyszłość. Czasem czynił to w sposób niezrozumiały, ale takie życie nie zawsze wie dokładnie dlaczego ten stan się wydarzył.

Do tej pory jego życie przebiegało dość beztrosko, robił swoje nie zawsze i nie wszędzie, przez co często ów program potrafił się wysypać, a nawet w ekstremalnych sytuacjach walnąć z grubej rury popularnym blue screen-em. 

- Te Zdzichu patrz znowu nam się apka wysypała!
- Heniu zobacz logi co się stało.
- W logach nic nima, pewnie znowu nie było Catchera!
- trzeba coś z tym zrobić, bezwzględnie!

tu by wstawić koda
i pokonteplować

Heniu i Zdzichu zasięgnęli języka u Wuja googla i znaleźli sposób na catch-ema-all. Po prostu trzeba wykorzystać unchalledexceptions, już żaden nie ucieknie. Każdy będzie chwycony za ogon i zalogowany. 

Catcher zorianetował się, że jest coraz mniej wykorzystywany. Stanął przed groźbą wymarcia. Po co używać skoro już wszystko jest łapane z marszu. 

- Co to teraz będzie? 
- Przegapiłem sytuację.
- Co ja teraz będę catchował:(.

Kod z dnia na dzień stawał się coraz bardziej czytelny. Unchalled łapał wszystkie dziwne sytuacje. Catcher odchodził w zapomnienie. Rozpił się roztył i nie było z nim kolorowo. Zaczął bezmyślnie trącać Throwa, a wiadomo, że to psikusna bestia. Pozostawiona w nieodpowiednim miejscu o nieodpowiedniej porze może zburzyć krew wielu developerom. 

Zdołowany, zhańbiony podczas jednej z libacji zabawiał się w kontrolowanie zachowania aplikacji. Był już tak podchmielony, że zaczął widzieć zjawy. Ukazał mu się bóg Pattern. 
Wszechwiedzący, wszechobecny, do niego odwołują się developerzy jak nie chcą wynajdować koła na nowo. To on stoi na straży prawidłowego implementowania kodu.

- O cholera dzisiaj to nieźle te trunki kopią, jakieś wzorce widzę!
- Milcz głupcze - rzekł pattern.
- Czy nie wiesz do czego zostałeś stworzony!?
- Do łapania wyjątków, tym się powinieneś zajmować, a nie zabawą z przepływem w aplikacji!

Catcher zrozumiał, że to nie zwidy i sam Pattern do niego przybył. A co jak się okaże, że nie jest zgodny i zostanie całkowicie wyeliminowany...

- O wszechobecny Pattern-ie, nie deletuj mnie z tego języka.
- Nie po tom się fatygował. Pełnisz ważną funkcję, ale się źle sprawujesz.
- Co mam uczynić, by cię zadowolić.
- Musisz wrócić do łapania, to twój cel.
- Ale jak Unchalled bierze wszystko. Co mam zrobić??
- Większą wartość musisz dać. Myśl bardziej abstrakcyjnie. W innym aspekcie.

To powiedziawszy Pattern zniknął. Został sam Catcher z myślami. 
- Hmm. Myśl abstrakcyjnie, co ten stary Pattern miał na myśli!?

Oczywiście Catcher nie zrozumiałe całej przekazanej przez Patterna ideii, ale o tym miał się dopiero przekonać.

Myślał intensywnie, łapał całą transmisję internetową, by odnaleźć coś co pomoże. Trwało to bardzo długo.
Zaintrygowało go jedno stwierdzenie, delegacja.
- Brzmi ciekawie, to jak bym komuś zlecił pracę, a ja tylko czerpał zyski. I kod będzie czytelniejszy. Developer pomyśli, że za tym nie stoję ja.

Jak pomyślał tak zrobił. Szybko przeistoczył się i teraz już nikt go jawnie nie widział. Jedynie kontakt odbywał się przez pośrednika. 

Developerzy pochwycili koncept, spróbowali, ale jednak to nie było to dalej marudzili.
- Zobacz Zdzichu jaka dziwna składnia. 
- Tak, nie wygląda to za piknie.
- Niby nie ma Catchera, ale metoda w metodzie, jakieś triki iście z JavaScript-a.
- Powiem Ci, że nie jestem przekonany. Może będzie trzeba zrezygnować z tego podejścia...

Catcher przechwycił tą transmisję. I już nie mógł spokojnie robić swojej roboty.
- Znowu to samo, znowu źle. Co ja mam zrobić by ich zadowolić. Stary piernik źle doradził. Wpuścił mnie w maliny. 

Wyklinając Patterna, rozmyślając cały czas błąkało mu się po drodze to co usłyszał. "Większą wartość musisz dać. Myśl bardziej abstrakcyjnie. W innym aspekcie"...
- "Myśl abstrakcyjnie". Przecież myślę abstrakcyjnie. - Powtarzał.
- Abstrakcyjnie, aspekcie, aspekcie, aspekcie...
- Jakim aspekcie - co miał na myśli?????

I nagle olśniło Catchera. Uświadomił sobie, że chodzi o aspekty.  Tak jest coś takiego jak Aspect Oriented Programming. Polega ono na tym, że dokładamy do naszego kodziku dodatkową funkcjonalność działającą w innym obszarze niepowiązanych ze sobą funkcji. Realizując zagadnienie, a korzystając z aspektów realizujemy niezwiązane/odseparowane na poziomie funkcji działania. 

- Czyli co, że niby ja miałbym być jakimś aspektem. - Zburzył się Catcher...

Gdy się jednak już uspokoił zorientował się, że to dla niego oznacza mniej roboty. Jest w jednym miejscu i ogarnia wszystkie miejsca, bo jest dodatkowym aspektem dołożonym do bazowego kodu. Nie zaciemnia, wydzielił się do innej odpowiedzialności. Kod jest bardziej przejrzysty, co jest aspektem to jest, a co kodem biznesowym to jest nim.
Dodatkowy aspekt jest mniej widzialny. Nikt się nie zorientuje, że to ten sam Catcher.
- Hmm, mogą mnie poznać. Muszę sobie wymyślić jakąś ksywę...
Jak powiedział tak uczynił. Korzystając z dobrodziejstwa wyrazów bliskoznacznych. 
Co jest w zbliżonym znaczeniu do łapania. Przechwycenie. To teraz będę przechwycał wyjątkowe sytuacje i tak nazwę się Interceptor.
Nikt się nie dowie, że pod nową nazwą ukrywa się stary, dobrze znany Catcher.
Ale kto by się przejmował, ważne że robi robotę. i czyni kod czytelniejszym.

Ale czy na pewno...


[post]: /assets/images/2018/07/exceptions/interceptor/post.jpg
[post-big]: /assets/images/2018/07/exceptions/interceptor/post-big.jpg