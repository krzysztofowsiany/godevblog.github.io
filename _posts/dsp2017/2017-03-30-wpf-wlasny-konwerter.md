---
title: WPF - własny konwerter.
date: 2017-03-30
author: Krzysztof Owsiany
layout: post
published: true
permalink: /wpf-wlasny-konwerter
image: /assets/images/2017/03/wpf-wlasny-konwerter/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DSP2017
  - WPF
short: Budując aplikacje na bazie WPFu, mamy do dyspozycji wiele ciekawych możliwości ominięcia pisania tak zwanego kodu &#8222;code-behind&#8222;. W celu wiązania danych z widokiem wykorzystujemy Bindowanie (łączenie właściwości kontrolek z przypisanym do widoku kontekstem danych DataContext).
---
## Czym jest konwerter
[![WPF - własny konwerter.][post]][post-big]{:.post-left-image}
Budując aplikacje na bazie WPFu, mamy do dyspozycji wiele ciekawych możliwości ominięcia pisania tak zwanego kodu &#8222;**code-behind**&#8222;. W celu wiązania danych z widokiem wykorzystujemy **Bindowanie** (łączenie właściwości kontrolek z przypisanym do widoku kontekstem danych **DataContext**).

Niemniej jednak zdarza się, iż wyświetlanie danych w takiej postaci jest nie wystarczające np. chcemy przy pomocy zmiennej **bool** ustawić widoczność kontrolki która przyjmuje właściwości typu **Visibility** (**Collapsed**, **Hidden**, **Visible**). W takiej sytuacji z pomocą przychodzi nam **konwerter**, dzięki któremu możemy dokonać transformacji: **bool -> Visibility**.

## Implementacja

{% highlight csharp linenos %}
using System;
using System.Globalization;
using System.Windows;
using System.Windows.Data;

namespace GUITests.Converters
{
  [ValueConversion(typeof(bool), typeof(Visibility))]
  public class BoolToVisiblityConverter : IValueConverter
  {
		public object Convert(
            object value,
            Type targetType, 
            object parameter,
            CultureInfo culture)
		{
			var isVisible = (bool)value;

			return isVisible ? Visibility.Visible : Visibility.Hidden;
		}

		public object ConvertBack(
            object value,
            Type targetType, 
            object parameter, 
            CultureInfo culture)
		{
			var isVisible = (Visibility)value;

			return isVisible == Visibility.Visible;
		}
	}
}
{% endhighlight %}

Konwerter posiada dwie składowe metody jakie implementuje z interfejsu **IValueConverter**:
[![WPF - własny konwerter.][image1]][image1-big]{:.post-right-image}
* **Convert** - jest używana w przypadku konwersji z typu źródłowego na docelowy, może przyjmować parametry. Właśnie w tej metodzie dokonujemy transformacji **bool** na **Visibility**. Wartość zwracana jest w miejscu użycia w kontrolce.
* **ConvertBack** - alternatywna operacja, jeżeli chcemy wykonać wsteczną konwersję z typu **Visibility** na **bool**, działa bardzo podobnie jedynie jest inna transformacja danych.

## Użycie
Deklaracja i użycie konwertera.
{% highlight xml linenos %}
<Window.Resources>
  <ResourceDictionary>
    <local:BoolToVisibilityConverter x:Key="boolToVisibilityConverter" />
  </ResourceDictionary>
</Window.Resources>

<Button Visibility="{Binding Path=Visible, Mode=TwoWay, 
  Converter={StaticResource boolToVisibilityConverter}, 
  ConverterParameter=params}"/>
{% endhighlight %}

W celu użycia konwertera należy go załadować do zasobów okna (linie 1 - 5).

Kolejna pozycja to użycie konwertera (linia 7 - 9), poprzez bindowanie.

Parametry użycia:
* **Path** - określa źródło danych w **DataContext**, na te wartości typu **bool** będzie reagował konwerter **BoolToVisibilityConverter**,
* **Mode** - typ wiązania, **TwoWay**, oznacza wiązanie w dwie strony, cczyli zapis i odczyt właściwości,
* **Converter** - definicja konwertera, należy określić iż pochodzi ze statycznych zasobów, jego nazwę,
* **ConverterParameter** - w razie potrzeby można przekazać parametry do konwertera.
    
**Tak przygotowany konwerter można wielokrotnie wykorzystywać w aplikacjach.**{:.color_1}

{% include_relative dsp.md %}

[post]: assets/images/2017/03/wpf-wlasny-konwerter/post.jpg
[post-big]: assets/images/2017/03/wpf-wlasny-konwerter/post-big.jpg

[image1]: assets/images/2017/03/wpf-wlasny-konwerter/image1.jpg
[image1-big]: assets/images/2017/03/wpf-wlasny-konwerter/image1-big.jpg