---
id: 641
title: 'WPF - własny konwerter.'
date: 2017-03-30T00:21:46+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/03/30/wpf-wlasny-konwerter/
image: /assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - WPF
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1>
      Czym jest konwerter
    </h1>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016.jpg"><img class="alignleft wp-image-652 size-medium" src="http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-300x200.jpg" alt="WPF - własny konwerter." width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>Budując aplikacje na bazie WPFu, mamy do dyspozycji wiele ciekawych możliwości ominięcia pisania tak zwanego kodu &#8222;**code-behind**&#8222;. W celu wiązania danych z widokiem wykorzystujemy **Bindowanie **(łączenie właściwości kontrolek z przypisanym do widoku kontekstem danych **DataContext**).
    </p>
    

      Niemniej jednak zdarza się, iż wyświetlanie danych w takiej postaci jest nie wystarczające np. chcemy przy pomocy zmiennej **bool** ustawić widoczność kontrolki która przyjmuje właściwości typu **Visibility** (**Collapsed**, **Hidden**, **Visible**). W takiej sytuacji z pomocą przychodzi nam **konwerter**, dzięki któremu możemy dokonać transformacji: **bool -> Visibility**.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Implementacja
    </h1>
    
    <pre class="lang:c# decode:true " title="" konwerter="">using System;
using System.Globalization;
using System.Windows;
using System.Windows.Data;

namespace GUITests.Converters
{
	[ValueConversion(typeof(bool), typeof(Visibility))]
	public class BoolToVisiblityConverter : IValueConverter
	{
		public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
		{
			var isVisible = (bool)value;

			return isVisible ? Visibility.Visible : Visibility.Hidden;
		}

		public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
		{
			var isVisible = (Visibility)value;

			return isVisible == Visibility.Visible;
		}
	}
}</pre>
    

      Konwerter posiada dwie składowe metody jakie implementuje z interfejsu **IValueConverter**:<a href="http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016.jpg"><img class="size-medium wp-image-648 alignright" src="http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        **Convert** - jest używana w przypadku konwersji z typu źródłowego na docelowy, może przyjmować parametry. Właśnie w tej metodzie dokonujemy transformacji **bool** na **VIsibility**. Wartość zwracana jest w miejscu użycia w kontrolce.
      </li>
    </ul>
    
    <ul>
      <li style="text-align: justify;">
        **ConvertBack** - alternatywna operacja, jeżeli chcemy wykonać wsteczną konwersję z typu **VIsibility** na **bool**, działa bardzo podobnie jedynie jest inna transformacja danych.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Użycie
    </h1>
    
    <pre class="lang:c# decode:true " title="Deklaracja i użycie konwertera.">&lt;Window.Resources&gt;

       &lt;ResourceDictionary&gt;

                 &lt;local:BoolToVisibilityConverter x:Key="boolToVisibilityConverter" /&gt;

       &lt;/ResourceDictionary&gt;
&lt;/Window.Resources&gt;

&lt;Button Visibility="{Binding Path=Visible, Mode=TwoWay, Converter={StaticResource boolToVisibilityConverter}, ConverterParameter=params}"/&gt;</pre>
    

      W celu użycia konwertera należy go załadować do zasobów okna (linie 1 - 5).
    </p>
    

      Kolejna pozycja to użycie konwertera (linia 6), poprzez bindowanie.
    </p>
    

      Parametry użycia:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        **Path** - określa źródło danych w **DataContext**, na te wartości typu **bool** będzie reagował konwerter **BoolToVisibilityConverter**,
      </li>
      <li style="text-align: justify;">
        **Mode** - typ wiązania, **TwoWay**, oznacza wiązanie w dwie strony, cczyli zapis i odczyt właściwości,
      </li>
      <li style="text-align: justify;">
        **Converter** - definicja konwertera, należy określić iż pochodzi ze statycznych zasobów, jego nazwę,
      </li>
      <li style="text-align: justify;">
        **ConverterParameter **- w razie potrzeby można przekazać parametry do konwertera.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <h4 style="text-align: center;">
      Tak przygotowany konwerter można wielokrotnie wykorzystywać w aplikacjach.
    </h4>
{% include_relative dsp.md %}