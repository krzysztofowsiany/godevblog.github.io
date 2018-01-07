---
id: 1613
title: 'Garbage Collector &#8211; Sprawdzanie kiedy sąsiad wyrzuca śmieci.'
date: 2017-11-20T20:03:06+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=1613
permalink: /garbage-collector-sprawdzanie-sasiad-wyrzuca-smieci/
dslc_post_template:
  - default
image: /assets/images/2017/11/blogging-photo-2016.jpg
categories:  
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
short: Garbage Collector ma zaimplementowaną pewną funkcjonalność. Daje nam ona kontrolę nad procesem niszczenia obiektów. Jako że do zarządzania pamięcią wykorzystywany jest specjalny agent i nie musimy się martwić o niszczenie obiektów. Tym samym nie wiemy, kiedy to nastąpi.

---
**Garbage Collector** ma zaimplementowaną pewną funkcjonalność. Daje nam ona kontrolę nad procesem niszczenia obiektów. Jako że do zarządzania pamięcią wykorzystywany jest specjalny agent i nie musimy się martwić o niszczenie obiektów. Tym samym nie wiemy, kiedy to nastąpi.



Użycie finalizatorów spowoduje możliwość uchwycenia procesu niszczenia obiektu w metodzie.

## Działanie

[![Dispose][image1]][image1]{:.post-left-image}

**Garbage Collector** skanując obiekty przeznaczone do niszczenia, inaczej traktuje obiekty zawierające finalizator. Umieszcza je na specjalnej kolejce obiektów nieosiągalnych (ang. **freachable quaque**).
    
Zawartość kolejki jest przetwarzana, i proces niszczenia obiektu jest delegowany do metody: **protected override void Finalize()**.
    
Zwalnianie pamięci w ten sposób jest czasochłonne, dlatego należy go używać z rozwagą i w zasadzie powinno się stosować tylko do specyficznych sytuacji:
* otwartych połączeń sieciowych,
* połączeń do bazy danych,
* otwartych plików,
* użytych bibliotek spoza .NET półświatka,
* obiektów COM (Component Object Model).

Finalizatory można używać jedynie w klasach i tylko jedno wystąpienie na klasę.
    
**Finalizujemy jedynie obszary niezarządzanego kodu.**{: .highlight-1}

    
## Jak użyć?
       
Szkielet metody **Finalize**.
        
```csharp 
protected override void Finalize()  
{  
    try  
    {  
        // niszczymy obiekty!
    }  
    finally  
    {  
        base.Finalize();  
    }  
}
```
    
Możemy oczywiście użyć składni podobnej do jęcyka C++, czyli destruktora. Jednak będzie on przez kompilator zamieniony na metodę **Finalize**.
      
```csharp 
class NazwaKlasy
{
    ~NazwaKlasy()  // destruktor taki jak w C++:)
    {
        // i czyścimy pamięć
    }
}
```

## Wykorzystanie interfejsu IDisposable

Do poprawnego użycia finalizatorów wykorzystamy interfejs **IDisposable**.

Poniżej znajduje się szkielet implementacji użycia **IDisposable**.
    
```csharp 
public class NazwaKlasy: IDisposable {  
   bool disposed = false; 
   //przydatna flaga, 
   //określająca czy Dispose zostało już wykonane
   
   public void Dispose() 
   //metoda pochodzi z interfejsu IDisposable, 
   //możemy ją wołać samodzielnie z kodu.
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
}
```
   
Metoda Dispose może zostać wywołana z obiektu. Jest ona także wymagana, by wykorzystać dyrektywę języka **using**.
    
```csharp 
using (var nazwaObiektu = new NazwaKlasy()) {
    nazwaObiektu.Metoda();
    nazwaObiektu.Metoda2();
}
```

W takiej składni metoda **Dispose** z interfejsu **IDisposable** zostanie wywołana przez dyrektywę using. 
    
W przypadku braku implementacji interfejsu **IDisposable** przez klasę, będziemy mieli błąd kompilacji.
    
 **C.D.N.**

[image1]: /assets/images/2017/11/blogging-photo-8399.jpg 