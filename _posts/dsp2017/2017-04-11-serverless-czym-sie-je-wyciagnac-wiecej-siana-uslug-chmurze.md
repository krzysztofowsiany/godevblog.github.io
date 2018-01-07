---
id: 734
title: 'Serverless &#8211; z czym się je i jak wyciągnąć więcej siana z usług w chmurze.'
date: 2017-04-11T11:51:14+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/04/11/serverless-czym-sie-je-wyciagnac-wiecej-siana-uslug-chmurze/
image: /assets/images/2017/04/Server.jpg
categories:
  - Bez kategorii
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - Serverlees
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      Był czas na <strong>monolity</strong>, przyszedł czas na <strong>mikroserwisy</strong> pora jeszcze bardziej zminimalizować, zejść do poziomu wykonywania pojedynczych funkcji, czyli<strong> serverless</strong>.
    </p>
    
    <p style="text-align: justify;">
      Osobiście jeszcze nie zetknąłem się praktycznie z tą usługą, nie mniej jednak widziałem dwie prezentacje na konferencji <strong><a href="http://2016.4developers.org.pl/pl/">4D w Warszawie</a>,</strong> tym samym temat mnie nieco zainteresował.
    </p>
    
    <p style="text-align: justify;">
      Niemniej jest ona bardzo interesująca. Na pewno w wielu przypadkach, gdzie dotychczas wymagane było stawienie kupy softu w celu wystawienia prostych usług będzie znacznie uproszczone i <strong>na pewno tańsze</strong>.
    </p>
    
    <h1 style="background: gold; padding: 5px;">
      Monolityczny sytem
    </h1>
    
    <p style="text-align: justify;">
      Może kilka przykładów. Na pierwszym obrazku przedstawiam prosty schemat serwera monolitycznego.
    </p>
    
    <p style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/04/monolit.png"><img class="aligncenter wp-image-776 size-large" src="http://godev.gemustudio.com/assets/images/2017/04/monolit-1024x328.png" alt="System Monolityczny." width="855" height="274" srcset="http://godev.gemustudio.com/assets/images/2017/04/monolit-1024x328.png 1024w, http://godev.gemustudio.com/assets/images/2017/04/monolit-300x96.png 300w, http://godev.gemustudio.com/assets/images/2017/04/monolit-768x246.png 768w, http://godev.gemustudio.com/assets/images/2017/04/monolit.png 1160w" sizes="(max-width: 855px) 100vw, 855px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Jest to podejście gdzie na jednym serwerze instaluje się wszelkie oprogramowanie jakie jest niezbędne do udostępnienia usługi np. Apache, MySQL, Postfix.
    </p>
    
    <p style="text-align: justify;">
      Oczywiście można uruchomić w takim podejściu wiele aplikacji, jednak wszystko znajduje się na jednym serwerze. Jest to marnotrawstwo zasobów i niesie ze sobą duże koszty utrzymania (serwer + obsługa).
    </p>
    
    <h1 style="background: gold; padding: 5px;">
      Microservices
    </h1>
    
    <p style="text-align: justify;">
      Nowszym podejściem jest wykorzystanie mikro-usług. Polega to na tym, iż rozbijamy na małe fragmenty budowaną aplikację i poszczególne moduły uruchamiamy <strong>1></strong> serwerach. Można znacznie prościej skalować system dzięki możliwości rozproszenia bardziej zasobożernych usług na osobne serwery.
    </p>
    
    <p style="text-align: justify;">
      Wykorzystuje się w tej sytuacji tak zwane kontenery (np. <a href="https://www.docker.com/"><strong>Docker</strong></a>). To rozwiązanie powoduje zamknięcie mikro-serwisu w kontenerze, który jest tak naprawdę systemem operacyjnym specjalnie przygotowanym do obsługi danej usługi.
    </p>
    
    <p style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/04/microservice.png"><img class="aligncenter wp-image-775 size-large" src="http://godev.gemustudio.com/assets/images/2017/04/microservice-1024x722.png" alt="Mikroserwisy" width="855" height="603" srcset="http://godev.gemustudio.com/assets/images/2017/04/microservice-1024x722.png 1024w, http://godev.gemustudio.com/assets/images/2017/04/microservice-300x212.png 300w, http://godev.gemustudio.com/assets/images/2017/04/microservice-768x542.png 768w, http://godev.gemustudio.com/assets/images/2017/04/microservice.png 1174w" sizes="(max-width: 855px) 100vw, 855px" /></a>
    </p>
    
    <p style="text-align: justify;">
      Działa to niezależnie podobnie jak maszyna wirtualna, jednak to rozwiązanie jest zoptymalizowane pod kątem użycia zasobów. Dlatego też wspólne części systemów wykorzystanych przez kontener współdzielą swoje zasoby a jedynie różnice wynikające z potrzeb mikro-serwisu są odosobnione.
    </p>
    
    <p style="text-align: justify;">
      Wykorzystanie kontenera to także kamień milowy w dostarczaniu oprogramowania do środowiska produkcyjnego, które w tym przypadku będzie identyczne jak to, na którym aplikacja jest testowana.
    </p>
    
    <p style="text-align: justify;">
      Tak naprawdę nie dostarczamy samej aplikacji a cały ekosystem zbudowany i uruchamiany na serwerze/chmurze.
    </p>
    
    <p style="text-align: justify;">
      Zbudowanie systemu w oparciu o architekturę mikro-usług jest trudniejszym podejściem (coś za coś) aniżeli system monolityczny.
    </p>
    
    <p style="text-align: justify;">
      Wymaga zaplanowania jak podzielić mikro-usługi, przygotować odpowiednią konfigurację w procesie dostarczania. Jednak ten narzut jaki jest wymagany na początku tworzenia projektu przynosi efekty podczas jego utrzymania.
    </p>
    
    <h1 style="background: gold; padding: 5px;">
      Serverless
    </h1>
    
    <p style="text-align: justify;">
      Nowy trend idzie dalej, i polega na odseparowaniu na poziomie funkcji. Dzięki temu podejściu korzystając z dostępnego rozwiązania (chmury) z usługą mamy możliwość wykonania pojedyńczej funkcji. Używamy zasobów chmury jedynie wtedy kiedy jej faktycznie potrzebujemy, nie mamy uruchomionego tak zwanego serwera. Gdyż do dystpozycji mamy usługę udostępnioną przez wybranego dostawcę.
    </p>
    
    <p style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/04/serverlees.png"><img class="aligncenter wp-image-777 size-large" src="http://godev.gemustudio.com/assets/images/2017/04/serverlees-1024x512.png" alt="Serverless" width="855" height="428" srcset="http://godev.gemustudio.com/assets/images/2017/04/serverlees-1024x512.png 1024w, http://godev.gemustudio.com/assets/images/2017/04/serverlees-300x150.png 300w, http://godev.gemustudio.com/assets/images/2017/04/serverlees-768x384.png 768w, http://godev.gemustudio.com/assets/images/2017/04/serverlees.png 1088w" sizes="(max-width: 855px) 100vw, 855px" /></a>
    </p>
    
    <p>
      Nie interesują nas w tym przypadku aspekty techniczne związane z utrzymaniem środowiska do uruchomienia funkcji. Po prostu odpowiednio zaprogramowana i skonfigurowana <strong>funkcja</strong> jest nam udostępniona w formie jakiej potrzebujemy (np. JSON, XML).
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="background: gold; padding: 5px;">
      $$$
    </h1>
    
    <p>
      Stosunek oszczędności między monolitem a serverlessem są znaczące. Odchodzi utrzymanie kosztownego serwera. W pewnych sytuacjach tak naprawdę serwerless może być darmowy w ramach wykorzystanej usługi rozliczenie uzależnione jest od ilości wykonanych funkcji oraz zasobów jakie do tej funkcji zostaną przypisane (<a href="https://aws.amazon.com/lambda/">AWS Lambda</a>).
    </p>
    
    <p>
      Można oszacować koszt jaki należy ponieść do obsługi aplikacji na stronie: <strong><a href="http://serverlesscalc.com/">serverlesscalc.com</a></strong>.
    </p>
    
    <p>
      Obecnie wiele stron wykorzystuje zasoby z doskoku, na żądanie. Duża część zasobów jest marnotrawiona, dzięki wykorzystanie <strong>serverless</strong>, dostawca ma możliwość lepszego balansowania użycia serwera, tym samym wyciśnie więcej soków z infrastruktury co przełoży się intratnie na zyski.
    </p>
    
    <p>
      Być może, pojawia się porównania, które dogłębnie ukażą różnicę. Niestety nie znalazłem na chwilę obecną żadnych wykresów. I tym samym jeżeli ktoś posiada takowa wiedzę to zapraszam do smarowania (obsmarowania) w komentarzach.
    </p>
    
    <p>
      Przydatne linki:
    </p>
    
    <p>
      <a href="https://serverless.com/">https://serverless.com</a>
    </p>
    
    <p>
      <a href="https://azure.microsoft.com/en-us/services/functions/">https://azure.microsoft.com/en-us/services/functions/</a>
    </p>
    
    <p>
      <a href="https://aws.amazon.com/lambda/serverless-architectures-learn-more/">https://aws.amazon.com/lambda/serverless-architectures-learn-more/</a>
    </p>
    
    <p>
      <a href="https://aws.amazon.com/serverless/">https://aws.amazon.com/serverless/</a>
    </p>
    
    <div>
      <div style="text-align: center;">
      </div>
      
      <div style="text-align: center;">
      </div>
      
      <div style="text-align: center;">
        <strong>Jest to post przygotowany na potrzeby konkursu &#8222;Daj Się Poznać 2017&#8221; organizowanym przez <a href="http://devstyle.pl">Macieja Aniserowicza</a>.</strong>
      </div>
      
      <div style="text-align: center;">
         <a href="http://devstyle.pl/daj-sie-poznac/" target="_blank" rel="noopener noreferrer"><img class="wp-image-104 size-full alignright" title="Daj Się Poznać 2017" src="http://godev.gemustudio.com/assets/images/2017/02/dsp2017-3.png" alt="" width="68" height="154" /></a>
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
    </div>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>