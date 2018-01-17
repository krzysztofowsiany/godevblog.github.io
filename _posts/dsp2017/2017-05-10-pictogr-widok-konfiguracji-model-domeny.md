---
title: PictOgr - widok konfiguracji + model domeny
date: 2017-05-10
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-widok-konfiguracji-model-domeny
image: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/post.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DDD
  - DSP2017
  - PictOgr
  - WPF
short: Ważnym elementem PictOgr-a jest konfiguracja, w niej właśnie będzie definiowana struktura katalogów dla zdjęć. Nazwy powinny składać się z wielu modułów.
---
Ważnym elementem PictOgr-a jest konfiguracja, w niej właśnie będzie definiowana struktura katalogów dla zdjęć. Nazwy powinny składać się z wielu modułów. W tym celu konfiguracja powinna dać możliwość składania wzorca lokalizacji pliku z dostępnych modułów nazwy jakie można wyciągnąć z pliku:
* **EXIF** - Exchangeable Image FIle Format - bogactwo możliwości definicji nazw,
* czasy utworzenia,
* nazwa pliku,
* podstawowe znaki jak: -, _, / i inne jakie dojdą w trakcie.
    
[![Widok konfiguracji][pictogr-config]][pictogr-config-big]{:.post-center-image}

Widok dość prosty, zawiera zakładkę &#8222;Formats&#8221;, w której to będzie posortowana według kolejności dodawania lista modułów nazw z lewej strony natomiast z prawej pogrupowane moduły nazw z jakich będzie można zdefiniować nazwę i lokalizację pliku.

Zdefiniowany wzorzec nazwy będzie wyświetlany na dole wraz z przykładową przetworzoną ścieżką do pliku.

Widok nie zawiera możliwości zapisu/odczytu zdefiniowanego wzorca nazwy, to będzie rozbudowane w kolejnych etapach budowy aplikacji.

![Widok konfiguracji][pictogr-config2]{:.post-right-image}

Dodatkowo aplikacja będzie posiadała dziennik zadań, w którym to będzie można określić kiedy i o której godzinie ma zostać wykonana procedura porządkowania plików. Widok konfiguracji nie został przygotowany dlatego na tą chwilę będzie pominięty.

Podstawowa konfiguracja jaką będzie można ustawić to start aplikacji z systemem -> **Tray** oraz integracja z menu podręcznym tak by była możliwość uruchomienia porządkowania np. bezpośrednio na katalogu.

## Rozbudowa modelu domeny
Każdy moduł będzie posiadał swój typ, do tego wykorzystany został typ wyliczeniowy , obecnie zawiera dwie pozycje dla EXIFa i bazowych modułów nazw.
    
Enumeracja listy typów modułów nazw.
{% highlight csharp lineno %}
namespace PictOgr.Core.Domain
{
	public enum ModuleType
	{
		Base = 0,
		EXIF = 1
	}
}
{% endhighlight %}

Typ modułu wykorzystywany jest przez model nazwy: **NameModule**.

Model składa się także z identyfikatora w formacie GUID, oraz nazwy.

I to właśnie nazwa będzie odzwierciedlać moduł i następnie zostanie zastąpiona rzeczywistymi danymi pobranymi z pliku.

Model nazwy modułu.
{% highlight csharp lineno %}
using System;

namespace PictOgr.Core.Domain
{
	public class NameModule
	{
		public ModuleType ModuleType { get; private set; }
		public string Name { get; private set; }
		public Guid NameModuleId { get; private set; }

		public NameModule(string name, Guid nameModuleId, ModuleType moduleType)
		{
			SetModuleType(moduleType);
			SetName(name);
			SetModuleId(nameModuleId);

			ModuleType = moduleType;
			Name = name;
			NameModuleId = nameModuleId;
		}

		private void SetModuleId(Guid nameModuleId)
		{
			NameModuleId = nameModuleId;
		}

		private void SetName(string name)
		{
			if (string.IsNullOrWhiteSpace(name))
			{
				throw new Exception("Name must be set.");
			}

			Name = name;
		}

		private void SetModuleType(ModuleType moduleType)
		{
			ModuleType = moduleType;
		}
	}
}
{% endhighlight %}

Jest to model domenowy dlatego jego ustawienie możliwe jest jedynie w konstruktorze z wykorzystaniem metod zawierających walidację.


Tak utworzony obiekt nie będzie zmieniany w trakcie działania aplikacji.
    
DTO modułu nazwy.
{% highlight csharp lineno %}
using System;
using PictOgr.Core.Domain;

namespace PictOgr.Infrastructure.DTO
{
	public class NameModuleDto
	{
		public ModuleType ModuleType { get; set; }
		public string Name { get; set; }
		public Guid NameModuleId { get; set; }
	}
}
{% endhighlight %}

[![Widok konfiguracji][image1]][image1-big]{:.post-left-image}
Klasa odpowiedzialna za przekazywanie danych z modelu domeny do aplikacji wygląda bardzo prosto i zawiera w zasadzie te same pola jakie znajdują się w domenie. W tym przypadku mogą ulegać modyfikacji.

Moduły nazwy są wykorzystywane przez następny model domeny o nazwie **CompositionName**, zawiera on w sobie listę modułów nazw i identyfikator.
    
Model skomponowanego wzorca nazwy.
{% highlight csharp lineno %}
using System;
using System.Collections.Generic;

namespace PictOgr.Core.Domain
{
	public class CompositionName
	{
		public List&lt;NameModule&gt; NameModuoles { get; }
		public Guid CompositionId { get; private set; }

		public CompositionName(Guid compositionId)
		{
			NameModuoles = new List&lt;NameModule&gt;();
			SetCompositionId(compositionId);
		}

		private void SetCompositionId(Guid compositionId)
		{
			CompositionId = compositionId;
		}
	}
}
{% endhighlight %}

Także w tym przypadku model domeny ma swojego odpowiednika w warstwie infrastruktury o nazwie **CompositionNameDto**.
    
DTO kompozycji nazwy.
{% highlight csharp lineno %}
using System;
using System.Collections.Generic;

namespace PictOgr.Infrastructure.DTO
{
	public class CompositionNameDto
	{
		public List&lt;NameModuleDto&gt; NameModuoles { get; set; }
		public Guid CompositionId { get; set; }
	}
}
{% endhighlight %}

DTO dla kompozycji nazwy jest bardzo proste i zawiera jedynie listę nazw modułów, oraz identyfikator kompozycji.

[![Widok konfiguracji][image2]][image2-big]{:.post-right-image}

Czy to dobra czy nie dobra implementacja problemu, to już zostanę rozliczony przez historię:D. Jednak walczę nadal i pozostał tylko jeden post wymagany do ukończenia **DSP2017**. Tak że widzę światełko w tunelu oraz perspektywy na dalsze blogowanie i rozwijanie PictOgra.
    
**Dziękuję za wytrwałość i zachęcam do komentowania.**

{% include_relative dsp.md %}

[post]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/post.jpg
[post-big]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/post-big.jpg

[pictogr-config]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/pictogr-config.png
[pictogr-config-big]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/pictogr-config-big.png

[pictogr-config2]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/pictogr-config2.png

[image1]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/image1.jpg
[image1-big]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/image1-big.jpg

[image2]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/image2.jpg
[image2-big]: /assets/images/2017/05/pictogr-widok-konfiguracji-model-domeny/image2-big.jpg