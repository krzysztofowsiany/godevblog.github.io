---
title: 'PictOgr &#8211; widok konfiguracji + model domeny'
date: 2017-05-10T00:56:26+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/05/10/pictogr-widok-konfiguracji-model-domeny/
image: /assets/images/2017/05/IMG_0950-1.jpg
categories:
  - Daj Się Poznać 2017
tags:
  - dajsiepoznac2017
  - DDD
  - DSP2017
  - PictOgr
  - WPF
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h2 style="background: #ffff9c; padding: 5pt; text-align: left;">
      Widok konfiguracji
    </h2>
    

      Ważnym elementem PictOgr-a jest konfiguracja, w niej właśnie będzie definiowana struktura katalogów dla zdjęć. Nazwy powinny składać się z wielu <a href="http://godev.gemustudio.com/assets/images/2017/05/pictogr-config.png"><img class="alignright wp-image-1035 size-medium" src="http://godev.gemustudio.com/assets/images/2017/05/pictogr-config-300x263.png" alt="widok konfiguracji" width="300" height="263" srcset="http://godev.gemustudio.com/assets/images/2017/05/pictogr-config-300x263.png 300w, http://godev.gemustudio.com/assets/images/2017/05/pictogr-config.png 684w" sizes="(max-width: 300px) 100vw, 300px" /></a>modułów. W tym celu konfiguracja powinna dać możliwość składania wzorca lokalizacji pliku z dostępnych modułów nazwy jakie można wyciągnąć z pliku:
    </p>
    
    <ul>
      <li style="text-align: justify;">
        <strong>EXIF</strong> &#8211; Exchangeable Image FIle Format &#8211; bogactwo możliwości definicji nazw,
      </li>
      <li style="text-align: justify;">
        czasy utworzenia
      </li>
      <li style="text-align: justify;">
        nazwa pliku
      </li>
      <li style="text-align: justify;">
        podstawowe znaki jak: -, _, / i inne jakie dojdą w trakcie.
      </li>
    </ul>
    
    <p>
      &nbsp;
    </p>
    

      Widok dość prosty, zawiera zakładkę &#8222;Formats&#8221;, w której to będzie posortowana według kolejności dodawania lista modułów nazw z lewej strony natomiast z prawej pogrupowane moduły nazw z jakich będzie można zdefiniować nazwę i lokalizację pliku.
    </p>
    

      Zdefiniowany w<a href="http://godev.gemustudio.com/assets/images/2017/05/pictogr-config2.png"><img class="wp-image-1036 size-full alignleft" src="http://godev.gemustudio.com/assets/images/2017/05/pictogr-config2.png" alt="" width="248" height="209" /></a>zorzec nazwy będzie wyświetlany na dole wraz z przykładową przetworzoną ścieżką do pliku.
    </p>
    

      Widok nie zawiera możliwości zapisu/odczytu zdefiniowanego wzorca nazwy, to będzie rozbudowane w kolejnych etapach budowy aplikacji.
    </p>
    

      Dodatkowo aplikacja będzie posiadała dziennik zadań, w którym to będzie można określić kiedy i o której godzinie ma zostać wykonana procedura porządkowania plików. Widok konfiguracji nie został przygotowany dlatego na tą chwilę będzie pominięty.
    </p>
    
    <p>
      &nbsp;
    </p>
    

      Podstawowa konfiguracja jaką będzie można ustawić to start aplikacji z systemem -> <strong>Tray</strong> oraz integracja z menu podręcznym tak by była możliwość uruchomienia porządkowania np. bezpośrednio na katalogu.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1 style="background: #ffff9c; padding: 5pt; text-align: left;">
      Rozbudowa modelu domeny
    </h1>
    

      Każdy moduł będzie posiadał swój typ, do tego wykorzystany został typ wyliczeniowy , obecnie zawiera dwie pozycje dla EXIFa i bazowych modułów nazw.
    </p>
    
    <pre class="lang:c# decode:true" title="Enumeracja listy typów modułów nazw.">namespace PictOgr.Core.Domain
{
	public enum ModuleType
	{
		Base = 0,
		EXIF = 1
	}
}</pre>
    

      Typ modułu wykorzystywany jest przez model nazwy: <strong>NameModule</strong>.
    </p>
    

      Model składa się także z identyfikatora w formacie GUID, oraz nazwy.
    </p>
    

      I to właśnie nazwa będzie odzwierciedlać moduł i następnie zostanie zastąpiona rzeczywistymi danymi pobranymi z pliku.
    </p>
    
    <pre class="lang:c# decode:true " title="Model nazwy modułu.">using System;

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
</pre>
    

      Jest to model domenowy dlatego jego ustawienie możliwe jest jedynie w konstruktorze z wykorzystaniem metod zawierających walidację.
    </p>
    

      Tak utworzony obiekt nie będzie zmieniany w trakcie działania aplikacji.
    </p>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_9780.jpg"><img class="aligncenter size-medium wp-image-1046" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_9780-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_9780-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9780-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_9780-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <pre class="lang:c# decode:true " title="DTO modułu nazwy.">using System;
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
</pre>
    

      Klasa odpowiedzialna za przekazywanie danych z modelu domeny do aplikacji wygląda bardzo prosto i zawiera w zasadzie te same pola jakie znajdują się w domenie. W tym przypadku mogą ulegać modyfikacji.
    </p>
    

      Moduły nazwy są wykorzystywane przez następny model domeny o nazwie <strong>CompositionName</strong>, zawiera on w sobie listę modułów nazw i identyfikator.
    </p>
    
    <pre class="lang:c# decode:true" title="Model skomponowanego wzorca nazwy.">using System;
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
</pre>
    
    <p>
      &nbsp;
    </p>
    

      Także w tym przypadku model domeny ma swojego odpowiednika w warstwie infrastruktury o nazwie <strong>CompositionNameDto</strong>.
    </p>
    
    <pre class="lang:c# decode:true " title="DTO kompozycji nazwy.">using System;
using System.Collections.Generic;

namespace PictOgr.Infrastructure.DTO
{
	public class CompositionNameDto
	{
		public List&lt;NameModuleDto&gt; NameModuoles { get; set; }
		public Guid CompositionId { get; set; }
	}
}
</pre>
    

      DTO dla kompozycji nazwy jest bardzo proste i zawiera jedynie listę nazw modułów, oraz identyfikator kompozycji.
    </p>
    

      <a href="http://godev.gemustudio.com/assets/images/2017/05/IMG_0043.jpg"><img class="size-medium wp-image-1049 alignright" src="http://godev.gemustudio.com/assets/images/2017/05/IMG_0043-300x200.jpg" alt="" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/05/IMG_0043-300x200.jpg 300w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0043-768x512.jpg 768w, http://godev.gemustudio.com/assets/images/2017/05/IMG_0043-1024x683.jpg 1024w" sizes="(max-width: 300px) 100vw, 300px" /></a>
    </p>
    

      Czy to dobra czy nie dobra implementacja problemu, to już zostanę rozliczony przez historię:D. Jednak walczę nadal i pozostał tylko jeden post wymagany do ukończenia <strong>DSP2017</strong>. Tak że widzę światełko w tunelu oraz perspektywy na dalsze blogowanie i rozwijanie PictOgra.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center;">
      <strong>Dziękuję za wytrwałość i zachęcam do komentowania.</strong>
    </h3>
    
    <p>
      &nbsp;
    </p>
    
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