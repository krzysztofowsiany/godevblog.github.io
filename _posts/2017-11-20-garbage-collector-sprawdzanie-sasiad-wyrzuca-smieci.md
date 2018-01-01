---
id: 1613
title: 'Garbage Collector &#8211; Sprawdzanie kiedy sąsiad wyrzuca śmieci.'
date: 2017-11-20T20:03:06+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1613
permalink: /2017/11/20/garbage-collector-sprawdzanie-sasiad-wyrzuca-smieci/
dslc_post_template:
  - default
image: /images/2017/11/blogging-photo-2016.jpg
categories:
  - Bez kategorii
  - 'C#'
  - Programowanie
tags:
  - 'C#'
  - destructor
  - Dispose
  - Finalize
  - Garbage Collector
  - GC
  - IDisposable
  - using
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong>Garbage Collector</strong> ma zaimplementowaną pewną funkcjonalność. Daje nam ona kontrolę nad procesem niszczenia obiektów. Jako że do zarządzania pamięcią wykorzystywany jest specjalny agent i nie musimy się martwić o niszczenie obiektów. Tym samym nie wiemy, kiedy to nastąpi.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Użycie finalizatorów spowoduje możliwość uchwycenia procesu niszczenia obiektu w metodzie.</span>
    </p>
    
    <h1>
      Działanie
    </h1>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;"><strong><a href="http://godev.gemustudio.com/images/2017/11/blogging-photo-8399.jpg"><img class="size-medium wp-image-1944 alignright" src="http://godev.gemustudio.com/images/2017/11/blogging-photo-8399-300x200.jpg" alt="Dispose" width="300" height="200" srcset="http://godev.gemustudio.com/images/2017/11/blogging-photo-8399-300x200.jpg 300w, http://godev.gemustudio.com/images/2017/11/blogging-photo-8399-768x512.jpg 768w, http://godev.gemustudio.com/images/2017/11/blogging-photo-8399.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>Garbage Collector</strong> skanując obiekty przeznaczone do niszczenia, inaczej traktuje obiekty zawierające finalizator. Umieszcza je na specjalnej kolejce obiektów nieosiągalnych (ang. <strong>freachable quaque</strong>).</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Zawartość kolejki jest przetwarzana, i proces niszczenia obiektu jest delegowany do metody: <strong>protected override void Finalize()</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Zwalnianie pamięci w ten sposób jest czasochłonne, dlatego należy go używać z rozwagą i w zasadzie powinno się stosować tylko do specyficznych sytuacji:</span>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <span style="font-size: 16px;">otwartych połączeń sieciowych,</span>
      </li>
      <li>
        <span style="font-size: 16px;">połączeń do bazy danych,</span>
      </li>
      <li>
        <span style="font-size: 16px;">otwartych plików,</span>
      </li>
      <li>
        <span style="font-size: 16px;">użytych bibliotek spoza .NET półświatka,</span>
      </li>
      <li>
        <span style="font-size: 16px;">obiektów COM (Component Object Model).</span>
      </li>
    </ul>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Finalizatory można używać jedynie w klasach i tylko jedno wystąpienie na klasę.</span>
    </p>
    
    <h2 style="background: lightblue; text-align: center; padding: 10px;">
      Finalizujemy jedynie obszary niezarządzanego kodu.
    </h2>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Jak użyć?
    </h1>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Szkielet metody <strong>Finalize</strong>.</span>
    </p>
    
    <pre class="lang:c# decode:true" title="Przykład metody finalize">protected override void Finalize()  
{  
    try  
    {  
        // niszczymy obiekty!
    }  
    finally  
    {  
        base.Finalize();  
    }  
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Możemy oczywiście użyć składni podobnej do jęcyka C++, czyli destruktora. Jednak będzie on przez kompilator zamieniony na metodę <strong>Finalize</strong>.</span>
    </p>
    
    <pre class="lang:c# decode:true" title="Finalizator w formie destruktora">class NazwaKlasy
{
    ~NazwaKlasy()  // destruktor taki jak w C++:)
    {
        // i czyścimy pamięć
    }
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Wykorzystanie interfejsu IDisposable
    </h1>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Do poprawnego użycia finalizatorów wykorzystamy interfejs <strong>IDisposable</strong>.</span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Poniżej znajduje się szkielet implementacji użycia <strong>IDisposable</strong>.</span>
    </p>
    
    <pre class="lang:c# decode:true" title="Szkielet użycia IDisposable">public class NazwaKlasy: IDisposable {  
   bool disposed = false; //przydatna flaga, określająca czy Dispose zostało już wykonane
   
   public void Dispose() //metoda pochodzi z interfejsu IDisposable, możemy ją wołać samodzielnie z kodu.
   { 
      Dispose(true);
      GC.SuppressFinalize(this);           
   }
   
   protected virtual void Dispose(bool disposing)
   {
      if (disposed)
         return; 
      
      if (disposing) {
         // niszczymy obiekty
      }
      
      // Niszczymy niezarządzane obiekty
      
      disposed = true;
   }

   ~NazwaKlasy() //finalizator
   {
      Dispose(false);
   }
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">Metoda Dispose może zostać wywołana z obiektu. Jest ona także wymagana, by wykorzystać dyrektywę języka <strong>using</strong>.</span>
    </p>
    
    <pre class="lang:c# decode:true" title="Użycie dyrektywy using.">using (var nazwaObiektu = new NazwaKlasy()) {
    nazwaObiektu.Metoda();
    nazwaObiektu.Metoda2();
}</pre>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">W takiej składni metoda <strong>Dispose</strong> z interfejsu <strong>IDisposable</strong> zostanie wywołana przez dyrektywę using. </span>
    </p>
    
    <p style="text-align: justify;">
      <span style="font-size: 16px;">W przypadku braku implementacji interfejsu <strong>IDisposable</strong> przez klasę, będziemy mieli błąd kompilacji.</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <strong>C.D.N.</strong>
    </p>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>