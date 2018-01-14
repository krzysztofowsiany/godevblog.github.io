---
title: Serverless - z czym się je i jak wyciągnąć więcej siana z usług w chmurze.
date: 2017-04-11
author: Krzysztof Owsiany
layout: post
published: true
permalink: /serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze
image: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - Serverlees
short: Był czas na monolity, przyszedł czas na mikroserwisy pora jeszcze bardziej zminimalizować, zejść do poziomu wykonywania pojedynczych funkcji, czyli serverless. Osobiście jeszcze nie zetknąłem się praktycznie z tą usługą, nie mniej jednak widziałem dwie prezentacje na konferencji 4D w Warszawie, tym samym temat mnie nieco zainteresował.
---
[![Serverless][post]][post-big]{:.post-right-image}
Był czas na **monolity**, przyszedł czas na **mikroserwisy** pora jeszcze bardziej zminimalizować, zejść do poziomu wykonywania pojedynczych funkcji, czyli **serverless**.

Osobiście jeszcze nie zetknąłem się praktycznie z tą usługą, nie mniej jednak widziałem dwie prezentacje na konferencji **[4D w Warszawie]**, tym samym temat mnie nieco zainteresował.

Niemniej jest ona bardzo interesująca. Na pewno w wielu przypadkach, gdzie dotychczas wymagane było stawienie kupy softu w celu wystawienia prostych usług będzie znacznie uproszczone i **na pewno tańsze**.

## Monolityczny sytem
Może kilka przykładów. Na pierwszym obrazku przedstawiam prosty schemat serwera monolitycznego.
[![System Monolityczny][monolit]][monolit-big]{:.post-left-image}
Jest to podejście gdzie na jednym serwerze instaluje się wszelkie oprogramowanie jakie jest niezbędne do udostępnienia usługi np. Apache, MySQL, Postfix.

Oczywiście można uruchomić w takim podejściu wiele aplikacji, jednak wszystko znajduje się na jednym serwerze. Jest to marnotrawstwo zasobów i niesie ze sobą duże koszty utrzymania (serwer + obsługa).

## Microservices
Nowszym podejściem jest wykorzystanie mikro-usług. Polega to na tym, iż rozbijamy na małe fragmenty budowaną aplikację i poszczególne moduły uruchamiamy **1>** serwerach. Można znacznie prościej skalować system dzięki możliwości rozproszenia bardziej zasobożernych usług na osobne serwery.

Wykorzystuje się w tej sytuacji tak zwane kontenery (np. **[Docker]**). To rozwiązanie powoduje zamknięcie mikro-serwisu w kontenerze, który jest tak naprawdę systemem operacyjnym specjalnie przygotowanym do obsługi danej usługi.

[![Mikroserwisy][microservice]][microservice-big]{:.post-right-image}
Działa to niezależnie podobnie jak maszyna wirtualna, jednak to rozwiązanie jest zoptymalizowane pod kątem użycia zasobów. Dlatego też wspólne części systemów wykorzystanych przez kontener współdzielą swoje zasoby a jedynie różnice wynikające z potrzeb mikro-serwisu są odosobnione.

Wykorzystanie kontenera to także kamień milowy w dostarczaniu oprogramowania do środowiska produkcyjnego, które w tym przypadku będzie identyczne jak to, na którym aplikacja jest testowana.

Tak naprawdę nie dostarczamy samej aplikacji a cały ekosystem zbudowany i uruchamiany na serwerze/chmurze.

Zbudowanie systemu w oparciu o architekturę mikro-usług jest trudniejszym podejściem (coś za coś) aniżeli system monolityczny.

Wymaga zaplanowania jak podzielić mikro-usługi, przygotować odpowiednią konfigurację w procesie dostarczania. Jednak ten narzut jaki jest wymagany na początku tworzenia projektu przynosi efekty podczas jego utrzymania.

## Serverless
Nowy trend idzie dalej, i polega na odseparowaniu na poziomie funkcji. Dzięki temu podejściu korzystając z dostępnego rozwiązania (chmury) z usługą mamy możliwość wykonania pojedyńczej funkcji. Używamy zasobów chmury jedynie wtedy kiedy jej faktycznie potrzebujemy, nie mamy uruchomionego tak zwanego serwera. Gdyż do dystpozycji mamy usługę udostępnioną przez wybranego dostawcę.

[![Serverless][serverlees]][serverlees-big]{:.post-left-image}

Nie interesują nas w tym przypadku aspekty techniczne związane z utrzymaniem środowiska do uruchomienia funkcji. Po prostu odpowiednio zaprogramowana i skonfigurowana **funkcja** jest nam udostępniona w formie jakiej potrzebujemy (np. JSON, XML).
    
## $$$
Stosunek oszczędności między monolitem a serverlessem są znaczące. Odchodzi utrzymanie kosztownego serwera. W pewnych sytuacjach tak naprawdę serwerless może być darmowy w ramach wykorzystanej usługi rozliczenie uzależnione jest od ilości wykonanych funkcji oraz zasobów jakie do tej funkcji zostaną przypisane ([AWS Lambda]).

Można oszacować koszt jaki należy ponieść do obsługi aplikacji na stronie: **[serverlesscalc.com]**.

Obecnie wiele stron wykorzystuje zasoby z doskoku, na żądanie. Duża część zasobów jest marnotrawiona, dzięki wykorzystanie **serverless**, dostawca ma możliwość lepszego balansowania użycia serwera, tym samym wyciśnie więcej soków z infrastruktury co przełoży się intratnie na zyski.

Być może, pojawia się porównania, które dogłębnie ukażą różnicę. Niestety nie znalazłem na chwilę obecną żadnych wykresów. I tym samym jeżeli ktoś posiada takowa wiedzę to zapraszam do smarowania (obsmarowania) w komentarzach.

Przydatne linki:
* [serverless.com],
* [azure.microsoft.com/en-us/services/functions],
* [aws.amazon.com/lambda/serverless-architectures-learn-more],
* [aws.amazon.com/serverless].

{% include_relative dsp.md %}

[serverlesscalc.com]: http://serverlesscalc.com
[serverless.com]: https://serverless.com
[azure.microsoft.com/en-us/services/functions]: https://azure.microsoft.com/en-us/services/functions
[aws.amazon.com/lambda/serverless-architectures-learn-more]: https://aws.amazon.com/lambda/serverless-architectures-learn-more
[aws.amazon.com/serverless]: https://aws.amazon.com/serverless

[4D w Warszawie]: http://2016.4developers.org.pl/pl

[Docker]: https://www.docker.com

[AWS Lambda]: https://aws.amazon.com/lambda/

[post]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/post.jpg
[post-big]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/post-big.jpg

[microservice]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/microservice.png
[microservice-big]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/microservice-big.png

[serverlees]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/serverlees.png
[serverlees-big]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/serverlees-big.png

[monolit]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/monolit.png
[monolit-big]: /assets/images/2017/04/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/monolit-big.png