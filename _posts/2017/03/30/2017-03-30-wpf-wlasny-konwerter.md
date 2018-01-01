---
id: 641
title: 'WPF &#8211; własny konwerter.'
date: 2017-03-30T00:21:46+00:00
author: gocom
layout: post
guid: http://godev.gemustudio.com/?p=641
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
    
    <p style="text-align: justify;">
      <a href="http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016.jpg"><img class="alignleft wp-image-652 size-medium" src="http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-300x200.jpg" alt="WPF - własny konwerter." width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/03/20160629-IMG_412501343_czerwca-29-2016-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>Budując aplikacje na bazie WPFu, mamy do dyspozycji wiele ciekawych możliwości ominięcia pisania tak zwanego kodu &#8222;<strong>code-behind</strong>&#8222;. W celu wiązania danych z widokiem wykorzystujemy <strong>Bindowanie </strong>(łączenie właściwości kontrolek z przypisanym do widoku kontekstem danych <strong>DataContext</strong>).
    </p>
    
    <p style="text-align: justify;">
      Niemniej jednak zdarza się, iż wyświetlanie danych w takiej postaci jest nie wystarczające np. chcemy przy pomocy zmiennej <strong>bool</strong> ustawić widoczność kontrolki która przyjmuje właściwości typu <strong>Visibility</strong> (<strong>Collapsed</strong>, <strong>Hidden</strong>, <strong>Visible</strong>). W takiej sytuacji z pomocą przychodzi nam <strong>konwerter</strong>, dzięki któremu możemy dokonać transformacji: <strong>bool -> Visibility</strong>.
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
    
    <p style="text-align: justify;">
      Konwerter posiada dwie składowe metody jakie implementuje z interfejsu <strong>IValueConverter</strong>:<a href="http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016.jpg"><img class="size-medium wp-image-648 alignright" src="http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/03/20160806-IMG_562900040_sierpnia-06-2016-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <ul style="text-align: justify;">
      <li>
        <strong>Convert</strong> &#8211; jest używana w przypadku konwersji z typu źródłowego na docelowy, może przyjmować parametry. Właśnie w tej metodzie dokonujemy transformacji <strong>bool</strong> na <strong>VIsibility</strong>. Wartość zwracana jest w miejscu użycia w kontrolce.
      </li>
    </ul>
    
    <ul>
      <li style="text-align: justify;">
        <strong>ConvertBack</strong> &#8211; alternatywna operacja, jeżeli chcemy wykonać wsteczną konwersję z typu <strong>VIsibility</strong> na <strong>bool</strong>, działa bardzo podobnie jedynie jest inna transformacja danych.
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
    
    <p style="text-align: justify;">
      W celu użycia konwertera należy go załadować do zasobów okna (linie 1 &#8211; 5).
    </p>
    
    <p style="text-align: justify;">
      Kolejna pozycja to użycie konwertera (linia 6), poprzez bindowanie.
    </p>
    
    <p style="text-align: justify;">
      Parametry użycia:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>Path</strong> &#8211; określa źródło danych w <strong>DataContext</strong>, na te wartości typu <strong>bool</strong> będzie reagował konwerter <strong>BoolToVisibilityConverter</strong>,
      </li>
      <li style="text-align: justify;">
        <strong>Mode</strong> &#8211; typ wiązania, <strong>TwoWay</strong>, oznacza wiązanie w dwie strony, cczyli zapis i odczyt właściwości,
      </li>
      <li style="text-align: justify;">
        <strong>Converter</strong> &#8211; definicja konwertera, należy określić iż pochodzi ze statycznych zasobów, jego nazwę,
      </li>
      <li style="text-align: justify;">
        <strong>ConverterParameter </strong>&#8211; w razie potrzeby można przekazać parametry do konwertera.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    
    <h4 style="text-align: center;">
      Tak przygotowany konwerter można wielokrotnie wykorzystywać w aplikacjach.
    </h4>
    
    <p>
      &nbsp;
    </p>
    
    <div>
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