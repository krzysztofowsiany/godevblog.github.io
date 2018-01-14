---
title: Typowanie generyków
date: 2017-05-10
author: Krzysztof Owsiany
layout: post
published: true
permalink: /typowanie-generykow
image: /assets/images/2017/05/typowanie-generykow/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - Generic
short: Typowym zastosowaniem typu generycznego jest wydzielenie typowania na zewnątrz klasy. Działa to na zasadzie wstrzyknięcia pewnego typu do klasy i manipulacja nim. Do klasy generycznej możemy wstrzyknąć dowolny typ, który będzie można używać według  algorytmów zawartych w klasie.
---
[![Typowanie generyków][image1]][image1-big]{:.post-right-image}
Typowym zastosowaniem typu generycznego jest wydzielenie typowania na zewnątrz klasy. Działa to na zasadzie wstrzyknięcia pewnego typu do klasy i manipulacja nim. Do klasy generycznej możemy wstrzyknąć dowolny typ, który będzie można używać według  algorytmów zawartych w klasie.
    
Przykładowa klasa do porównania.
{% highlight csharp linenos %}
public class SampleCompareClass<TCompareType>
{
    public bool IsEqual(TCompareType a, TCompareType b)
    {
        return a.Equals(b);
    }
}
{% endhighlight %}    

Typ generyczny posiada swoją nazwę symboliczną, bardzo często wykorzystuje się  po prostu dużą literę **T**. Jednak nic nie stoi na przeszkodzie by nazwę określić w bardziej logiczny ciąg, np: **TCompareType**. Dobrą praktyką jest pozostawienie przedrostka T, która jak mniemam pochodzi z typów generycznych stosowanych w języku **C++** określanych jako **T**emplate.
    
Użycie typu generycznego.
{% highlight csharp linenos %}
var comparer = new SampleCompareClass<int>();
var a = 1;
var b = 2;

var isEqual = comparer.IsEqual(a, b);
{% endhighlight %}
    
**Nazewnictwo szczególnie przydatne gdy użyjemy więcej typów generycznych.**

## Ograniczenia na typach generycznych
Świat idzie do przodu, języki programowania także ewoluują, i tak doczekaliśmy się rozszerzenia możliwości typów generycznych o ograniczenia. Do tej pory można było przekazać prawie dowolny typ do klasy generycznej, obecnie można to bardzo ograniczyć tym samym gdy **dev** spróbuje przekazać nie odpowiedni typ, kompilator strzeli errorem prosto w &#8230;

Od wujka &#8222;Billa&#8221;, dostajemy słówko kluczowe **where**, i tym samym możemy określić konkretny typ jaki może zostać &#8222;wstrzyknięty&#8221; do klasy generycznej.
    
Klasa generyczna z ograniczeniem i użycie.
{% highlight csharp linenos %}
public class SimpleType {
    public int Value { get; private set; }
    public SimpleType(int @value){
        Value = @value;
    }        
}     
         
public class SampleCompareClass<TCompareType> where TCompareType : SimpleType
{
    public bool IsEqual(TCompareType a, TCompareType b)
    {
        return a.Value.Equals(b.Value);
    }
}
{% endhighlight %}

[![Generics][image2]][image2-big]{:.post-left-image}
Składnia użycia ograniczenia to: **where TGenericTypeName : TypeName**.

Jak można  zauważyć implementacja metody **IsEqual** uległa zmianie, wykorzystuje właściwość **Value**, w tym przypadku jeżeli przekażemy niespójny typ do klasy generycznej, nie będzie on posiadał właściwości **Value**, to walnie błędem.

W przypadku gdy wykorzystamy więcej typów generycznych można wykorzystać więcej ograniczeń oddzielając je przecinkami:

public class SampleClass**TTypeOne**, **TTypeTwo** where **TTypeOne : Credential1**, where TTypeTwo : **Credential2**{ }

Istnieje także możliwość ustawienie wielu ograniczeń dla typu generycznego:
    
public class SampleClass<**TType**> where **TType****: Credential1**, **Credential2 **{ }

## Typy ograniczeń
[![Typy ograniczeń][image3]][image3-big]{:.post-left-image}
Oczywiście nie jest to jedyny sposób ograniczenia jest ich nieco więcej:
* **where TStruct: struct** - ten typ ograniczenia określa, iż można wstrzyknąć do klasy generycznej typy wartości z wyjątkiem **nullable**, np: **int**, **byte**, **long**, jednak nie będą się już klasyfikować typy **int?**, **long?,**
* **where TClass : class** - ** **TClass może zostać zastąpiony przez typy referencyjne: class, interface, array,  delegate,
* **where TNew : new()** - można wykorzystać typy posiadające publiczny konstruktor bezparametrowy, to ograniczenie w przypadku stosowania wielu do typu generycznego powinno znajdować się na końcu,
* **where TBaseClass : BaseClassName** - typ musi bazować na klasie o nazwie **BaseClassName**,
* **where TInterface : InterfaceName** - wstrzykiwany typ musi implementować interfejs o nazwie **InterfaceName**,
* **where TType: U** - typ generyczny **TType** musi być typu generycznego **U**.

**Mam cichą nadzieję, iż jest to przydatna wiedza, ja na pewno nauczyłem się wiele pisząc tego posta, zachęcam do pisania zawsze jest duża szansa, iż napisałem jakąś  bujdę.**
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/05/typowanie-generykow/post.jpg
[post-big]: /assets/images/2017/05/typowanie-generykow/post-big.jpg

[image1]: /assets/images/2017/05/typowanie-generykow/image1.jpg
[image1-big]: /assets/images/2017/05/typowanie-generykow/image1-big.jpg

[image2]: /assets/images/2017/05/typowanie-generykow/image2.jpg
[image2-big]: /assets/images/2017/05/typowanie-generykow/image2-big.jpg

[image3]: /assets/images/2017/05/typowanie-generykow/image3.jpg
[image3-big]: /assets/images/2017/05/typowanie-generykow/image3-big.jpg