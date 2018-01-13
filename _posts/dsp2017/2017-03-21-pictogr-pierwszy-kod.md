---
title: PictOgr - pierwszy kod
date: 2017-03-21
author: Krzysztof Owsiany
layout: post
published: true
permalink: /pictogr-pierwszy-kod
image: /assets/images/2017/03/pictogr-pierwszy-kod/post.png
categories:
  - Daj Się Poznać 2017
  - PictOgr
tags:
  - Autofac
  - 'C#'
  - dajsiepoznac2017
  - DSP2017
  - PictOgr
short: Już na samym począteczku problemy, musiałem wymienić bibliotekę logów z log4net na NLog, okazało się, iż w moim projekcie opartym na .NET 4.5.2 nie można wykorzystać biblioteki log4net i tyle z nauki.
---
## Zmiana biblioteki logów
Już na samym począteczku problemy, musiałem wymienić bibliotekę logów z **[log4net]** na **[NLog]**, okazało się, iż w moim projekcie opartym na .NET 4.5.2 nie można wykorzystać biblioteki log4net i tyle z nauki.

Oczywiście, żeby było śmieszniej dowiedziałem się o tym po konfiguracji, instalacji w sytuacji wystąpienia problemu z zapisem logów, czyli X czasu poszło się paść.
    
## Autofac - kontenerek na moje śmieci
![Autofac][autofac-logo]{:.post-left-image}
Kolejno przyszedł czas na wdrożenie **DIP** (**Dependency Inversion Principle**) przy wykorzystaniu **Dependency Injection**. Do tego po instalacji pakietu trzeba trochę popracować nad szkieletem wykorzystującym Autofac-a.
    
A czym jest taki kontenerek? To bardzo proste, to składowisko obiektów naszej aplikacji. Trzeba go załadować w sposób jaki się chcę. A potem już tylko korzystać.
    
Realizuje fragment zasad **SOLID**, a dokładnie ostatnią literkę.
    
Zasada **DIP** określa, iż obiekty nie powinny być tworzone na żądanie, a wstrzykiwane z zewnątrz. Dzięki czemu zależność obiektu wykorzystującego inne klasy jest odwrócona. Określamy jakie klasy/interfejsy chcemy otrzymać, a kontener je dostarczy.
    
**Dobra rada dla programisty - bądź SOLIDny.**{:.h-1}
    
Poniżej klasa statyczna implementująca ładowanie modułów kontenera.
    
{% highlight csharp linenos %}
using System.Linq;
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
                .Where(t => 
                    t.IsAssignableTo() 
                    && t.IsClass 
                    && !t.IsAbstract);

            foreach (var type in types)
            {
                builder.RegisterModule((IModule) Activator.CreateInstance(type));
            }
        }
    }
}
{% endhighlight %}

![PictOgr - pierwszy kod][post]{:.post-left-image} 
Kontener można ładować parami, nie trzeba używać jednej łopaty. Można dodawać wiele ładując je automatycznie, za to odpowiedzialny jest zaznaczony fragment kodu.
    
Polega to na przeszukaniu wszystkich klas w aplikacji i wyciągnięciu ich typów spełniających wskazane warunki.
    
## Ładowanie moich śmieci
Z kolei kod poniżej to modulik, mały jest i w tym przypadku ładuje wszystkie zależności dla NLoga. Po wykonaniu tego kodu w programie można wstrzykiwać loggera.

Oczywiście można rejestrować w kontenerze dowolne klasy np. **builder.RegisterType**<**SplashScreenView**>**();**

{% highlight csharp linenos  %}
using Autofac;
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
}
{% endhighlight %}
    
Moduły tworzymy zazwyczaj w obszarach powiązanych razem z klasami jakie są ładowane. Unikamy tym samym zwalenia tworzenie wszystkich obiektów w jednym miejscu, czyli porządeczek.
    
## Używanie kontenera
Po załadowaniu fajnie byłoby użyć Autofaca, ale wiadomo wszystko ma swój początek i koniec, dlatego należy zainicjować kontener. W moim przypadku będzie to w głównej klasie **App**.
    
L.12 tworzy kontener, czyli ładuje wszystkie moduliki z **[PictOgr-a][pictogr]**.

Linia niżej to wyciągnięcie obiektu z kontenera, w tym przypadku okna powitalnego **SplashScreenView**.
    
Rejestrowanie obiektów w kontenerze, przy starcie aplikacji.
{% highlight csharp linenos  %}
using System.Windows;
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
}
{% endhighlight %}

![Dependency Injection][dependency-injection]

Jednak w tym przypadku żądamy od kontenera konkretnego obiektu, nie różni się to za bardzo od klasycznego podejścia, czyli **new Klasa()**, dlatego DI wykonywać będziemy w następujący sposób:

Wstrzykiwanie zależności.
{% highlight csharp linenos  %}
public class StartApplicationCommand : ICommand
{
		private readonly MainWindowView mainWindowView;

		public StartApplicationCommand(MainWindowView mainWindowView)
		{
			this.mainWindowView = mainWindowView;
		}
        ...
{% endhighlight %}

Dotyczy to klasy **MainWindowView**, nigdzie nie jest ona tutaj tworzona, jest otrzymywana jako atrybut konstruktora, biblioteka Autofac wstrzykuje tą zależność.
    
## Ogromne możliwości
Autofac jest bardzo rozbudowaną biblioteką, pozwala w różny sposób tworzyć obiekty, zbudowany jest na bazie wzorca projektowego **Fluent Interface**, który to pozwala na kaskadowe wywoływanie metod z klasy macierzystej. Każda metoda zwraca referencję do klasy, tym samym bazujemy na jednej klasie i wykonujemy na niej operacje.

Zastosowanie fluenta daje możliwość zapisu kolejnych etapów rejestrowania klasy z wykorzystaniem separacji kropką.
    
**builder**.**RegisterType**{:.color_1}<**TestClass**{:.color_2}>().**As**{:.color_1}<**ITestClass**{:.color_2}>();

W powyższym przykładzie rejestrujemy klase **TestClass** jako interfejs **ITestClass**.

[![PictOgr - pierwszy kod][image1]][image1-big]{:.post-left-image}

Możemy także określić, iż klasa ma mieć tylko jedną instancję (**Wzorzec Singleton**) poprzez dopisanie

**builder**.**RegisterType**{:.color_1}<**TestClass**{:.color_2}>().**As**{:.color_1}<**ITestClass**{:.color_2}>().**SingleInstance**{:.color_1}();
    
Można zarejestrować klasę samodzielnie ją tworząc, taką operację wykonujemy poniższym poleceniem:
    
**builder**.**RegisterInstance**{:.color_1}(new **TestClass**{:.color_2}()).**As**{:.color_1}<**ITestClass**{:.color_2}>();

Poniższy kodzik pokazuje, że można wykonać metodę w tworzonym obiekcie zaraz po jej utworzeniu.
    
**builder**.**RegisterType**{:.color_1}<**TestClass**{:.color_2}>().**As**{:.color_1}<**ITestClass**{:.color_2}>().**OnActivated**{:.color_1}(e => e.**Instance**.**Test**{:.color_1}());
    
**Teraz to już pozostaje tylko &#8222;wstrzykiwać&#8221;&#8230; zależności 😉**{:.h-1}

Na dzisiaj tyle. Jestem w implementacji testów i CQRSa.
    
Liczę na konstruktywne komentarze:).
    
{% include_relative dsp.md %}

[post]: /assets/images/2017/03/pictogr-pierwszy-kod/post.png
[autofac-logo]: /assets/images/2017/03/pictogr-pierwszy-kod/autofac-logo.png
[dependency-injection]: /assets/images/2017/03/pictogr-pierwszy-kod/dependency-injection.png

[image1]: /assets/images/2017/03/pictogr-pierwszy-kod/image1.jpg
[image1-big]: /assets/images/2017/03/pictogr-pierwszy-kod/image1-big.jpg

[pictogr]: {{site.url}}/pictogr-pomysl
[log4net]: https://logging.apache.org/log4net/
[NLog]: http://nlog-project.org/