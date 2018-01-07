---
id: 490
title: 'PictOgr &#8211; pierwszy kod'
date: 2017-03-21T19:20:56+00:00
author: Krzysztof Owsiany
layout: post
published: false
permalink: /2017/03/21/pictogr-pierwszy-kod/
image: /assets/images/2017/03/kontener.png
categories:
  - Bez kategorii
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - Autofac
  - 'C#'
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
---
<div id="dslc-theme-content">
  <div id="dslc-theme-content-inner">
    <h1>
      Zmiana biblioteki logów
    </h1>
    
    <p style="text-align: justify;">
      Już na samym począteczku problemy, musiałem wymienić bibliotekę logów z <strong><a href="https://logging.apache.org/log4net/">log4net</a></strong> na <strong><a href="http://nlog-project.org/">NLog</a></strong>, okazało się, iż w moim projekcie opartym na.NET 4.5.2 nie można wykorzystać biblioteki log4net i tyle z nauki.
    </p>
    
    <p style="text-align: justify;">
      Oczywiście, żeby było śmieszniej dowiedziałem się o tym po konfiguracji, instalacji w sytuacji wystąpienia problemu z zapisem logów, czyli X czasu poszło się paść.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Autofac &#8211; kontenerek na moje śmieci
    </h1>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      <img class="size-medium alignleft" src="http://docs.autofac.org/en/latest/_assets/images/logo.png" width="185" height="150" />Kolejno przyszedł czas na wdrożenie <strong>DIP</strong> (<strong>Dependency Inversion Principle</strong>) przy wykorzystaniu <strong>Dependency Injection</strong>. Do tego po instalacji pakietu trzeba trochę popracować nad szkieletem wykorzystującym Autofac-a.
    </p>
    
    <p style="text-align: justify;">
      A czym jest taki kontenerek? To bardzo proste, to składowisko obiektów naszej aplikacji. Trzeba go załadować w sposób jaki się chcę. A potem już tylko korzystać.
    </p>
    
    <p style="text-align: justify;">
      Realizuje fragment zasad <strong>SOLID</strong>, a dokładnie ostatnią literkę.
    </p>
    
    <p style="text-align: justify;">
      Zasada<strong> DIP</strong> określa, iż obiekty nie powinny być tworzone na żądanie, a wstrzykiwane z zewnątrz. Dzięki czemu zależność obiektu wykorzystującego inne klasy jest odwrócona. Określamy jakie klasy/interfejsy chcemy otrzymać, a kontener je dostarczy.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Dobra rada dla programisty &#8211; bądź SOLIDny.
    </h3>
    
    <p style="text-align: justify;">
      Poniżej klasa statyczna implementująca ładowanie modułów kontenera.
    </p>
    
    <pre class="lang:c# decode:true" title="Budowanie kontenera">using System.Linq;
using Autofac;
using Autofac.Core;

namespace PictOgr.Core.AutoFac
{
    public static class Container
    {
        public static ContainerBuilder CreateBuilder()
        {
            var builder = new ContainerBuilder();

            LoadModules(builder);

            return builder;
        }

        private static void LoadModules(ContainerBuilder builder)
        {
            var types = AppDomain.CurrentDomain.GetAssemblies()
                .SelectMany(x =&gt; x.GetTypes())
                .Where(t =&gt; t.IsAssignableTo() && t.IsClass && !t.IsAbstract);

            foreach (var type in types)
            {
                builder.RegisterModule((IModule) Activator.CreateInstance(type));
            }
        }
    }
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      <img class="alignright wp-image-544 size-medium" src="http://godev.gemustudio.com/assets/images/2017/03/kontener-300x200.png" alt="PictOgr - pierwszy kod" width="300" height="200" srcset="http://godev.gemustudio.com/assets/images/2017/03/kontener-300x200.png 300w, http://godev.gemustudio.com/assets/images/2017/03/kontener.png 331w" sizes="(max-width: 300px) 100vw, 300px" />
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Kontener można ładować parami, nie trzeba używać jednej łopaty. Można dodawać wiele ładując je automatycznie, za to odpowiedzialny jest zaznaczony fragment kodu.
    </p>
    
    <p>
      Polega to na przeszukaniu wszystkich klas w aplikacji i wyciągnięciu ich typów spełniających wskazane warunki.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Ładowanie moich śmieci
    </h1>
    
    <p style="text-align: justify;">
      Z kolei kod poniżej to modulik, mały jest i w tym przypadku ładuje wszystkie zależności dla NLoga. Po wykonaniu tego kodu w programie można wstrzykiwać loggera.
    </p>
    
    <p style="text-align: justify;">
      Oczywiście można rejestrować w kontenerze dowolne klasy np.<em><strong> builder.RegisterType<SplashScreenView>();</strong></em>
    </p>
    
    <pre class="lang:c# decode:true " title="Moduł kontenera">using Autofac;
using Autofac.Extras.NLog;

namespace PictOgr.Core
{
	public class CoreModule : Module
	{
		protected override void Load(ContainerBuilder builder)
		{
			base.Load(builder);
			
			builder.RegisterModule();
		}
	}
}</pre>
    
    <p>
      Moduły tworzymy zazwyczaj w obszarach powiązanych razem z klasami jakie są ładowane. Unikamy tym samym zwalenia tworzenie wszystkich obiektów w jednym miejscu, czyli porządeczek.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Używanie kontenera
    </h1>
    
    <p style="text-align: justify;">
      Po załadowaniu fajnie byłoby użyć Autofaca, ale wiadomo wszystko ma swój początek i koniec, dlatego należy zainicjować kontener. W moim przypadku będzie to w głównej klasie <strong>App.</strong>
    </p>
    
    <p style="text-align: justify;">
      L.12 tworzy kontener, czyli ładuje wszystkie moduliki z <a href="http://godev.gemustudio.com/2017/03/01/pictogr-pomysl/"><strong>PictOgr-a</strong></a>.
    </p>
    
    <p style="text-align: justify;">
      Linia niżej to wyciągnięcie obiektu z kontenera, w tym przypadku okna powitalnego <strong>SplashScreenView</strong>.
    </p>
    
    <pre class="lang:c# decode:true " title="Rejestrowanie obiektó w kontenerze, przy starcie aplikacji.">using System.Windows;
using Autofac;
using PictOgr.Core.AutoFac;
using PictOgr.SplashScreen.Views;

namespace PictOgr
{
	public partial class App : Application
	{
		private void OnStartup(object sender, StartupEventArgs e)
		{
			var container = Container.CreateBuilder().Build();

			var splashScreenView = container.Resolve();

			splashScreenView.Show();
		}
	}
}</pre>
    
    <p>
      &nbsp;
    </p>
    
    <div style="text-align: center;">
      <img class="alignleft" src="http://emedical24.pl/userdata/gfx/44fe02e595bd5967e384623c8ef7df45.jpg" alt="" width="245" height="114" />
    </div>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Jednak w tym przypadku żądamy od kontenera konkretnego obiektu, nie różni się to za bardzo od klasycznego podejścia, czyli <strong>new Klasa()</strong>, dlatego DI wykonywać będziemy w następujący sposób:
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <pre class="lang:c# decode:true" title="Wstrzykiwanie zależności.">public class StartApplicationCommand : ICommand
	{
		private readonly MainWindowView mainWindowView;

		public StartApplicationCommand(MainWindowView mainWindowView)
		{
			this.mainWindowView = mainWindowView;
		}
        ...
</pre>
    
    <p>
      Dotyczy to klasy <strong>MainWindowView</strong>, nigdzie nie jest ona tutaj tworzona, jest otrzymywana jako atrybut konstruktora, biblioteka Autofac wstrzykuje tą zależność.
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h1>
      Ogromne możliwości
    </h1>
    
    <p style="text-align: justify;">
      Autofac jest bardzo rozbudowaną biblioteką, pozwala w różny sposób tworzyć obiekty, zbudowany jest na bazie wzorca projektowego <strong>Fluent Interface</strong>, który to pozwala na kaskadowe wywoływanie metod z klasy macierzystej. Każda metoda zwraca referencję do klasy, tym samym bazujemy na jednej klasie i wykonujemy na niej operacje.
    </p>
    
    <p style="text-align: justify;">
      Zastosowanie fluenta daje możliwość zapisu kolejnych etapów rejestrowania klasy z wykorzystaniem separacji kropką.
    </p>
    
    <p style="text-align: justify;">
      <strong><span class="pln"> builder</span><span class="pun">.</span><span class="typ">RegisterType</span><span class="pun"><TestClass</span><span class="pun">>().</span><span class="typ">As</span><span class="pun"><</span><span class="typ">ITestClass</span><span class="pun">>();</span></strong>
    </p>
    
    <p style="text-align: justify;">
      W powyższym przykładzie rejestrujemy klase <strong>TestClass</strong> jako interfejs <strong>ITestClass</strong>.<img class="size-medium wp-image-529 alignright" src="http://godev.gemustudio.com/assets/images/2017/03/20151125-IMG-2015-11-25-9999_4-300x200.jpg" alt="" width="300" height="200" />
    </p>
    
    <p style="text-align: justify;">
      Możemy także określić, iż klasa ma mieć tylko jedną instancję (<strong>Wzorzec Singleton</strong>) poprzez dopisanie
    </p>
    
    <p style="text-align: justify;">
      <span class="pln">builder</span><span class="pun">.</span><span class="typ">RegisterType</span><span class="pun"><TestClass</span><span class="pun">>().</span><span class="typ">As</span><span class="pun"><</span><span class="typ">ITestClass</span><span class="pun">>()</span><strong>.SingleInstance();</strong>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Można zarejestrować klasę samodzielnie ją tworząc, taką operację wykonujemy poniższym poleceniem:
    </p>
    
    <p>
      <strong><span class="pln">builder</span><span class="pun">.</span><span class="typ">RegisterInstance</span><span class="pun">(</span><span class="kwd">new</span> TestClass<span class="pun">())</span><span class="pun">.</span><span class="typ">As</span><span class="pun"><</span><span class="typ">ITestClass</span><span class="pun">>();</span></strong>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <p>
      Poniższy kodzik pokazuje, że można wykonać metodę w tworzonym obiekcie zaraz po jej utworzeniu.
    </p>
    
    <p>
      <strong><span class="pln">builder</span><span class="pun">.</span><span class="typ">RegisterType</span><span class="pun"><TestClass</span><span class="pun">>()</span><span class="pun">.</span><span class="typ">As</span><span class="pun"><<span class="typ">ITestClass</span></span><span class="pun">>()</span><span class="pun">.</span><span class="typ">OnActivated</span><span class="pun">(</span><span class="pln">e </span><span class="pun">=></span><span class="pln"> e</span><span class="pun">.</span><span class="typ">Instance</span><span class="pun">.</span><span class="typ">Test</span><span class="pun">());</span></strong>
    </p>
    
    <p>
      &nbsp;
    </p>
    
    <h3 style="text-align: center; background: #FFFF9C; padding: 5pt;">
      Teraz to już pozostaje tylko &#8222;wstrzykiwać&#8221;&#8230; zależności 😉
    </h3>
    
    <p>
      &nbsp;
    </p>
    
    <p style="text-align: justify;">
      Na dzisiaj tyle. Jestem w implementacji testów i CQRSa.
    </p>
    
    <p style="text-align: justify;">
      Liczę na konstruktywne komentarze:).
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