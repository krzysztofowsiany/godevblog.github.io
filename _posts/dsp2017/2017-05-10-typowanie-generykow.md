---
id: 991
title: Typowanie generyków
date: 2017-05-10T00:56:37+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/05/10/typowanie-generykow/
image: /assets/images/2017/05/IMG_1033.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - Generic
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">

      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_9491.jpg"><img class="aligncenter wp-image-1025 size-large" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_9491-1024x683.jpg" alt="Typowanie generyków" width="855" height="570" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_9491-1024x683.jpg 1024w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9491-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9491-768x512.jpg 768w" sizes="(max-width: 855px) 100vw, 855px" /></a>
    </p>
    
    <p>
      Typowym zastosowaniem typu generycznego jest wydzielenie typowania na zewnątrz klasy. Działa to na zasadzie wstrzyknięcia pewnego typu do klasy i manipulacja nim. Do klasy generycznej możemy wstrzyknąć dowolny typ, który będzie można używać według  algorytmów zawartych w klasie.
    </p>
    
    <pre class="lang:c# decode:true" title="Przykładowa klasa do porównania.">public class SampleCompareClass&lt;TCompareType&gt;
{
    public bool IsEqual(TCompareType a, TCompareType b)
    {
        return a.Equals(b);
    }
}</pre>
    

      Typ generyczny posiada swoją nazwę symboliczną, bardzo często wykorzystuje się  po prostu dużą literę **T**. Jednak nic nie stoi na przeszkodzie by nazwę określić w bardziej logiczny ciąg, np: **TCompareType**. Dobrą praktyką jest pozostawienie przedrostka T, która jak mniemam pochodzi z typów generycznych stosowanych w języku **C++** określanych jako **T**emplate.
    </p>
    
    <pre class="lang:c# decode:true" title="Użycie typu generycznego.">var comparer = new SampleCompareClass&lt;int&gt;();
var a = 1;
var b = 2;

var isEqual = comparer.IsEqual(a, b);</pre>
    
    <p style="text-align: center;">
      **Nazewnictwo szczególnie przydatne gdy użyjemy więcej typów generycznych.**
    </p>
    
    <h1 style="text-align: justify;">
      Ograniczenia na typach generycznych
    </h1>
    

      Świat idzie do przodu, języki programowania także ewoluują, i tak doczekaliśmy się rozszerzenia możliwości typów generycznych o ograniczenia. Do tej pory można było przekazać prawie dowolny typ do klasy generycznej, obecnie można to bardzo ograniczyć tym samym gdy **dev** spróbuje przekazać nie odpowiedni typ, kompilator strzeli errorem prosto w &#8230;
    </p>
    

      Od wujka &#8222;Billa&#8221;, dostajemy słówko kluczowe **where**, i tym samym możemy określić konkretny typ jaki może zostać &#8222;wstrzyknięty&#8221; do klasy generycznej.
    </p>
    
    <pre class="lang:c# decode:true" title="Klasa generyczna z ograniczeniem i użycie.">public class SimpleType {
    public int Value { get; private set; }
    public SimpleType(int @value){
        Value = @value;
    }        
}     
         
public class SampleCompareClass&lt;TCompareType&gt; where TCompareType : SimpleType
{
    public bool IsEqual(TCompareType a, TCompareType b)
    {
        return a.Value.Equals(b.Value);
    }
}</pre>
    
    <p>
      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_9632.jpg"><img class="alignleft wp-image-1013 size-medium" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_9632-300x200.jpg" alt="Generics" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_9632-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9632-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9632-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p>
      Składnia użycia ograniczenia to: <span style="color: #3355ff;">**where TGenericTypeName : TypeName**</span>.
    </p>
    

      Jak można  zauważyć implementacja metody **IsEqual** uległa zmianie, wykorzystuje właściwość **Value**, w tym przypadku jeżeli przekażemy niespójny typ do klasy generycznej, nie będzie on posiadał właściwości **Value**, to walnie błędem.
    </p>
    
    <p>
      W przypadku gdy wykorzystamy więcej typów generycznych można wykorzystać więcej ograniczeń oddzielając je przecinkami:
    </p>
    
    <p>
      <span style="color: #0055ff;">public class SampleClass**TTypeOne**, **TTypeTwo** where **TTypeOne : Credential1**, where TTypeTwo : **Credential2**{ }</span>
    </p>
    
    <p>
      Istnieje także możliwość ustawienie wielu ograniczeń dla typu generycznego:
    </p>
    

      <span style="color: #3355ff;">public class SampleClass<**TType**> where **TType****: Credential1**, **Credential2 **{ }</span>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="text-align: justify;">
      Typy ograniczeń
    </h1>
    

      Oczywiście nie jest to jedyny sposób ograniczenia jest ich nieco więcej:<a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_9010.jpg"><img class="size-medium wp-image-1008 alignright" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_9010-300x199.jpg" alt="" width="300" height="199" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_9010-300x199.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9010-768x510.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9010-1024x680.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <ul>
      <li style="text-align: justify;">
        **where TStruct: struct** - ten typ ograniczenia określa, iż można wstrzyknąć do klasy generycznej typy wartości z wyjątkiem **nullable**, np: **int**, **byte**, **long**, jednak nie będą się już klasyfikować typy **int?**, **long?,**
      </li>
      <li style="text-align: justify;">
        **where TClass : class** - ** **TClass może zostać zastąpiony przez typy referencyjne: class, interface, array,  delegate,
      </li>
      <li style="text-align: justify;">
        **where TNew : new()** - można wykorzystać typy posiadające publiczny konstruktor bezparametrowy, to ograniczenie w przypadku stosowania wielu do typu generycznego powinno znajdować się na końcu,
      </li>
      <li style="text-align: justify;">
        **where TBaseClass : BaseClassName** - typ musi bazować na klasie o nazwie **BaseClassName**,
      </li>
      <li style="text-align: justify;">
        **where TInterface : InterfaceName** - wstrzykiwany typ musi implementować interfejs o nazwie **InterfaceName**,
      </li>
      <li style="text-align: justify;">
        **where TType: U** - typ generyczny **TType** musi być typu generycznego **U**.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: center;">
      **Mam cichą nadzieję, iż jest to przydatna wiedza, ja na pewno nauczyłem się wiele pisząc tego posta, zachęcam do pisania zawsze jest duża szansa, iż napisałem jakąś  bujdę.**
    </p>
    
{% include_relative dsp.md %}