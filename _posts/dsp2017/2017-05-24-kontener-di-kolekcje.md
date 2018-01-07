---
title: 'Kontener DI &#8211; kolekcje'
date: 2017-05-24T12:51:58+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/05/24/kontener-di-kolekcje/
image: /assets/images/2017/05/blogging-photo-7501.jpg
categories:
  - 'C#'
  - Programowanie
tags:
  - Autofac
  - 'C#'
  - Dependency Injection
  - DI
  - IEnumerable
  - Kolekcje
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <p style="text-align: justify;">
      W zmaganiach z kontenerem <strong>AutoFac</strong>, natrafiłem na możliwość wstrzykiwania całych kolekcji implementujących ten sam interfejs.<a href="http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-5.jpg"><img class="wp-image-1165 alignright" src="http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-5-200x300.jpg" alt="" width="107" height="161" srcset="http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-5-200x300.jpg 200w, http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-5.jpg 600w" sizes="(max-width: 107px) 100vw, 107px" /></a>
    </p>
    
    <p>
      Dzięki takiemu podejściu udało mi się znacznie uprościć kod algorytmu. Niniejszym dzielę się swoimi spostrzeżeniami oraz przykładową poglądową implementacją rozwiązania jakie zastosowałem.
    </p>
    <!--break-->
    <p>
      &nbsp;
    </p>
    
    <h2 style="text-align: justify;">
      Interfejs
    </h2>
    
    <p style="text-align: justify;">
      Bardzo prosty interfejs <strong>IOnlyForTest</strong> zawierający szkielet metody <strong>Calc</strong> przyjmującej dwa parametry <strong>a</strong> i <strong>b</strong>, następnie zwracający wynik operacji.
    </p>
    
    <pre class="lang:c# decode:true" title="Interfejs wykorzystywany w kolekcji.">using System;

namespace Test
{
    public interface IOnlyForTest
    {
        int Calc(int a, Int b);
    }
}</pre>
    
    <p style="text-align: justify;">
      Klasa implementująca <strong>IOnlyForTest</strong> zostanie automatycznie wstrzyknięta jako jeden z elementów kolekcji.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="text-align: justify;">
      Rejestrowanie klas w module kontenera AutoFac
    </h2>
    
    <p style="text-align: justify;">
      Moduł rejestrowania klas implementujących interfejs <strong>IOnlyForTest</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Rejestrowanie klas obiektów implementujących interfejs IOnlyForTest.">namespace Test
{
    public class TestModule : Module
    {
        protected override void Load(ContainerBuilder builder)
        {
            builder.RegisterType&lt;AddOnlyForTest&gt;().AsImplementedInterfaces();
            builder.RegisterType&lt;SubdOnlyForTest&gt;().AsImplementedInterfaces();
        }
    }
}</pre>
    
    <p style="text-align: justify;">
      Można by tutaj powiedzieć, iż własnie budowane są kolejne elementy kolekcji jaka zostanie wstrzyknięta do docelowego obiektu.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="text-align: justify;">
      Przykładowe klasy implementujące interfejs
    </h2>
    
    <p>
      Pierwsza z klas zwraca wynik dodawania liczby <strong>a</strong> i <strong>b</strong>;
    </p>
    
    <pre class="lang:c# decode:true " title="Implementacja interfejsu IOnlyForTest, wynikiem jest dodawanie dwóch liczb a i b.">using System;

namespace Test
{
    public class AddOnlyForTest : IOnlyForTest
    {
        public int Calc(int a, Int b)
        {
            return a + b;
        }
    }
}</pre>
    
    <p style="text-align: justify;">
      Druga funkcjonuje analogicznie z tym, iż zwraca różnicę.
    </p>
    
    <pre class="lang:c# decode:true " title="Implementacja interfejsu IOnlyForTest, wynikiem jest odejmowanie dwóch liczb a i b.">using System;

namespace Test
{
    public class SubOnlyForTest : IOnlyForTest
    {
        public int Calc(int a, Int b)
        {
            return a - b;
        }
    }
}</pre>
    
    <p style="text-align: justify;">
      Obie są rejestrowane przez moduł kontenera <strong>AutoFac</strong>.
    </p>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-9452.jpg"><img class="aligncenter size-medium wp-image-1175" src="http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-9452-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-9452-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-9452-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/blogging-photo-9452.jpg 900w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="text-align: justify;">
      Użycie wstrzykiwania kolekcji
    </h2>
    
    <p style="text-align: justify;">
      Na koniec pozostaje implementacja klasy <strong>TestEnumerable</strong>. To właśnie w niej zostanie wstrzyknięta kolekcja zawierająca listę zarejestrowanych klas implementujących <strong>IOnlyForTest</strong>.
    </p>
    
    <pre class="lang:c# decode:true" title="Użycie DI + enumeracji do wyliczeń.">using System;
using System.Collections.Generic;


namespace Test
{
    public class TestEnumerable
    {
        private readonly IEnumerable&lt;IOnlyForTest&gt; _testEnumerableList;

        public TestEnumerable(IEnumerable&lt;IOnlyForTest&gt; testEnumerableList)                
        {
            _testEnumerableList = testEnumerableList;

            RunTest(DateTime.MinValue, DateTime.MaxValue);
        }

        public void RunTest(DateTime from, DateTime to)
        {
            var a = 1;
            var b = 1;
            var result = 0;

            foreach (var testEnumerable in _testEnumerableList)
            {
                result += testEnumerable.Calc(a, b);
            }           
        }
    }
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <h2 style="text-align: justify;">
      Koniec
    </h2>
    
    <p style="text-align: justify;">
      Niniejszy kod nie przedstawia żadnej logicznej implementacji, jest to tylko przykład testowy. Głównym jego założeniem jest przedstawienie sposobu łączenia klas implementujących ten sam interfejs w kolekcję. I następnie użycie ich w pętli.
    </p>
    
    <p>
      Mam nadzieję, iż ten wirtualny przykład znajdzie zadowolonego odbiorcę.
    </p>
    
    <!-- AddThis Advanced Settings generic via filter on the_content -->
    
    <!-- AddThis Share Buttons generic via filter on the_content -->
  </div>
</div>