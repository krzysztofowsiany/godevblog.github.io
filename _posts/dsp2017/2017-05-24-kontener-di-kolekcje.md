---
title: Kontener DI - kolekcje
date: 2017-05-24
author: Krzysztof Owsiany
layout: post
published: true
permalink: /kontener-di-kolekcje
image: /assets/images/2017/05/kontener-di-kolekcje/post.jpg
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
[![Kolekcje w kontrolerze Dependency Injection - Autofac][post]][post-big]{:.post-right-image}
W zmaganiach z kontenerem **AutoFac**, natrafiłem na możliwość wstrzykiwania całych kolekcji implementujących ten sam interfejs.
    
Dzięki takiemu podejściu udało mi się znacznie uprościć kod algorytmu. Niniejszym dzielę się swoimi spostrzeżeniami oraz przykładową poglądową implementacją rozwiązania jakie zastosowałem.

## Interfejs
Bardzo prosty interfejs **IOnlyForTest** zawierający szkielet metody **Calc** przyjmującej dwa parametry **a** i **b**, następnie zwracający wynik operacji.

Interfejs wykorzystywany w kolekcji.
{% hightlight csharp linenos %}
using System;
namespace Test
{
    public interface IOnlyForTest
    {
        int Calc(int a, Int b);
    }
}
{% endhightlight %}

Klasa implementująca **IOnlyForTest** zostanie automatycznie wstrzyknięta jako jeden z elementów kolekcji.

## Rejestrowanie klas w module kontenera AutoFac
Moduł rejestrowania klas implementujących interfejs **IOnlyForTest**.
    
Rejestrowanie klas obiektów implementujących interfejs IOnlyForTest.
{% highlight csharp linenos%}
namespace Test
{
    public class TestModule : Module
    {
        protected override void Load(ContainerBuilder builder)
        {
            builder.RegisterType&lt;AddOnlyForTest&gt;().AsImplementedInterfaces();
            builder.RegisterType&lt;SubdOnlyForTest&gt;().AsImplementedInterfaces();
        }
    }
}
{% endhighlight %}

Można by tutaj powiedzieć, iż własnie budowane są kolejne elementy kolekcji jaka zostanie wstrzyknięta do docelowego obiektu.
    
## Przykładowe klasy implementujące interfejs
[![Kolekcje w kontrolerze Dependency Injection - Autofac][image1]][image1-big]{:.post-center-image}

Pierwsza z klas zwraca wynik dodawania liczby **a** i **b**;

Implementacja interfejsu IOnlyForTest, wynikiem jest dodawanie dwóch liczb a i b.
{% hightlight charp linenos %}
using System;

namespace Test
{
    public class AddOnlyForTest : IOnlyForTest
    {
        public int Calc(int a, Int b)
        {
            return a + b;
        }
    }
}
{% endhighlight %}

Druga funkcjonuje analogicznie z tym, iż zwraca różnicę.

Implementacja interfejsu IOnlyForTest, wynikiem jest odejmowanie dwóch liczb a i b.
{% hightlight csharp linenos %}
using System;

namespace Test
{
    public class SubOnlyForTest : IOnlyForTest
    {
        public int Calc(int a, Int b)
        {
            return a - b;
        }
    }
}
{% endhighlight %}

Obie są rejestrowane przez moduł kontenera **AutoFac**.
[![Kolekcje w kontrolerze Dependency Injection - Autofac][image2]][image2-big]{:.post-left-image}

# Użycie wstrzykiwania kolekcji
Na koniec pozostaje implementacja klasy **TestEnumerable**. To właśnie w niej zostanie wstrzyknięta kolekcja zawierająca listę zarejestrowanych klas implementujących **IOnlyForTest**.

Użycie DI + enumeracji do wyliczeń.
{% highlight csharp linenos %}
using System;
using System.Collections.Generic;

namespace Test
{
    public class TestEnumerable
    {
        private readonly IEnumerable<IOnlyForTest> _testEnumerableList;

        public TestEnumerable(IEnumerable<IOnlyForTest> testEnumerableList)                
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
}
{% endhighlight %}
    
## Koniec
Niniejszy kod nie przedstawia żadnej logicznej implementacji, jest to tylko przykład testowy. Głównym jego założeniem jest przedstawienie sposobu łączenia klas implementujących ten sam interfejs w kolekcję. I następnie użycie ich w pętli.

Mam nadzieję, iż ten wirtualny przykład znajdzie zadowolonego odbiorcę.
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/05/kontener-di-kolekcje/post.jpg
[post-big]: /assets/images/2017/05/kontener-di-kolekcje/post-big.jpg

[image1]: /assets/images/2017/05/kontener-di-kolekcje/image1.jpg
[image1-big]: /assets/images/2017/05/kontener-di-kolekcje/image1-big.jpg

[image2]: /assets/images/2017/05/kontener-di-kolekcje/image2.jpg
[image2-big]: /assets/images/2017/05/kontener-di-kolekcje/image2-big.jpg