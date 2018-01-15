---
title: PictOgr - mój CQRS -4-
date: 2017-04-20
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-moj-cqrs-4
image: /assets/images/2017/04/pictogr-moj-cqrs-4/travis-ci.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - CQRS
  - dajsiepoznac2017
  - DSP2017
  - GitHub
  - PictOgr
  - Travis-CI
short: Zapowiadałem na ten wpis, iż będzie on dotyczył wykorzystania ES oraz walidatorów, jednak powstał mały bałagan w projekcie czego skutkiem było wyodrębnienie CQRS do osobnego repozytorium.
---
Zapowiadałem na ten wpis, iż będzie on dotyczył wykorzystania **ES** oraz walidatorów, jednak powstał mały bałagan w projekcie czego skutkiem było wyodrębnienie **CQRS** do osobnego repozytorium.

**[github.com/krzysztofowsiany/cqrs]**{:.h-4}

[![CQRS][travis-logo]][travis-logo-big]{:.post-left-image}

Biblioteka powiązana jest z napisanym już wcześniej modułami do implementacji testów.

Takie podejście pozwoliło mi na wykorzystanie po raz pierwszy mechanizmu pod modułów w **GIT**, EXP rośnie.:)

Mechanizm ten pozwala na dołączanie do repozytorium innych repozytoriów jako pod moduły i korzystanie z nich.

## Pod moduły - GIT
Do konfiguracji pod modułów służy plik o nazwie **.gitmodules**.

Plik .gitmodules.
{% highlight yml %}
[submodule "CQRS"]
        path = CQRS
        url = https://github.com/krzysztofowsiany/cqrs
{% endhighlight %}
    
Należy określić, nazwę podmodułu, ścieżkę gdzie będzie znajdowało się dołączone repozytorium oraz jego adres.

Po dodaniu pliku .gitmodules wydając polecenie **git submodule update** aktualizujemy dodane podmoduły.

## Travis
[![CQRS - GitHub.][travis-ci]][travis-ci-big]{:.post-right-image}
Dodatkowo zaadaptowałem projekt tak by można było wykorzystać narzędzie o nazwie **[Travis-CI]**.

Jest to darmowy serwer (dla oprogramowania **Open Source)** ciągłej integracji pozwalający na kontrolowanie poprawności działania aplikacji poprzez przygotowanie środowiska, instalację zależności, budowaniu, testowaniu, i raportowaniu tego procederu.
 
Travis wymaga konfiguracji zapisanej w pliku o nazwie **.travis.yml**.
    
Konfiguracja Travis-CI dla biblioteki CQRS.
{% highlight yml %}
language: csharp
solution: CQRS.sln
install:
  - nuget restore CQRS.sln
  - nuget install xunit.runners -Version 1.9.2 -OutputDirectory testrunner
script:
  - xbuild /p:Configuration=Debug
  - mono ./testrunner/xunit.runners.1.9.2/tools/xunit.console.clr4.exe ./CQRS.Tests/bin/Debug/CQRS.Tests.dll
{% endhighlight %}

Plik ten daje duże możliwości, i przykład jaki wykorzystałem jest bardzo prosty, polegający na określeniu plików projektu, instalacji wymaganych zależności, następnie uruchomienie samego skryptu budowania **xbuild** oraz wykonania testów.

Więcej o konfiguracji Travisa przy pomocy yamla pod adresem: **[docs.travis-ci.com/user/customizing-the-build]**.

Co ciekawe całe środowisko uruchomieniowe działa na Linuxie dlatego wykorzystywana jest tutaj platforma **[mono]**.

W celu wykorzystania musiałem nieco zmienić projekt CQRS-a, pozbyć się runnera dla VS, oraz obniżyć wersję xUnita do 1.9.2, w takiej konfiguracji udało mi się dokonać pierwszego builda.:D
    
**[travis-ci.org/krzysztofowsiany/cqrs]**:<img src="https://travis-ci.org/krzysztofowsiany/cqrs.svg?branch=master">

[![CQRS - GitHub.][mycqrs-travis]][mycqrs-travis-big]{:.post-center-image}

## Koniec
Co prawda krótki post, jednak ostatni święta  i z nimi związane długie wyjazdy/powroty do rodziny. Dlatego wpis taki króciasty,

Jednak mam nadzieję, że interesujący.
    
**Linki:**
* [docs.travis-ci.com/user/customizing-the-build],
* [travis-ci.org],
* [www.mono-project.com/docs/about-mono/supported-platforms/linux],
* [github.com/krzysztofowsiany/cqrs],
* [travis-ci.org/krzysztofowsiany/cqrs].

**Dziękuję za wytrwałość i zachęcam do komentowania.**
    
{% include_relative dsp.md %}

[mono]: http://www.mono-project.com/docs/about-mono/supported-platforms/linux/

[github.com/krzysztofowsiany/cqrs]: https://github.com/krzysztofowsiany/cqrs

[docs.travis-ci.com/user/customizing-the-build]: https://docs.travis-ci.com/user/customizing-the-build
[travis-ci.org]: https://travis-ci.org
[Travis-CI]: https://travis-ci.org
[www.mono-project.com/docs/about-mono/supported-platforms/linux]: http://www.mono-project.com/docs/about-mono/supported-platforms/linux
[travis-ci.org/krzysztofowsiany/cqrs]: https://travis-ci.org/krzysztofowsiany/cqrs

[travis-ci]: /assets/images/2017/04/pictogr-moj-cqrs-4/travis-ci.png
[travis-ci-big]: /assets/images/2017/04/pictogr-moj-cqrs-4/travis-ci-big.png

[travis-logo]: /assets/images/2017/04/pictogr-moj-cqrs-4/travis-logo.png
[travis-logo-big]: /assets/images/2017/04/pictogr-moj-cqrs-4/travis-logo-big.png

[mycqrs-travis]: /assets/images/2017/04/pictogr-moj-cqrs-4/mycqrs-travis.png
[mycqrs-travis-big]: /assets/images/2017/04/pictogr-moj-cqrs-4/mycqrs-travis-big.png