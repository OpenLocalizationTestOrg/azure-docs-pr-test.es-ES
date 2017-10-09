---
title: "aaaWindows Universal integración con el SDK de aplicaciones de interacción"
description: "¿Cómo tooIntegrate Azure Mobile Engagement con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Integración del SDK de Windows Universal Apps Engagement
> [!div class="op_single_selector"]
> * [Windows universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Este procedimiento describe las funciones de la aplicación Universal de Windows de supervisión y análisis hello más sencilla forma tooactivate Engagement.

Hola pasos es que toocompute necesita un suficiente informe de hello tooactivate de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals. Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md) desde Estas estadísticas son dependientes de la aplicación.

## <a name="supported-versions"></a>Versiones compatibles
Hola Mobile Engagement SDK para aplicaciones universales de Windows solo se puede integrar en tiempo de ejecución de Windows y aplicaciones de plataforma Universal de Windows de destino:

* Windows 8
* Windows 8.1
* Windows Phone 8,1
* Windows 10 (familias de escritorio y portátiles)

> [!NOTE]
> Si se dirige a Windows Phone Silverlight, consulte toohello [procedimiento de integración de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Instalar SDK de aplicaciones universales de Mobile Engagement Hola
### <a name="all-platforms"></a>Todas las plataformas
Hola Mobile Engagement SDK para Windows aplicación Universal está disponible como un paquete de Nuget llamado *MicrosoftAzure.MobileEngagement*. Puede instalarlo desde Hola Administrador de paquetes de Nuget de Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x y Windows Phone 8.1
NuGet implementa automáticamente los recursos SDK de Hola Hola `Resources` carpeta Hola raíz de su proyecto de aplicación.

### <a name="windows-10-universal-windows-platform-applications"></a>Aplicaciones de la Plataforma universal de Windows de Windows 10
NuGet no implementar automáticamente los recursos SDK de hello en la aplicación de UWP todavía. Deberá toodo manualmente hasta que la implementación de recursos vuelve a producirse en NuGet:

1. Abra el Explorador de archivos.
2. Navegue toohello ubicación siguiente (**x.x.x** es la versión de hello de interacción que se va a instalar): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*
3. Hola de arrastrar y colocar **recursos** carpeta desde la raíz del toohello explorer Hola del archivo del proyecto en Visual Studio.
4. En Visual Studio, seleccione el proyecto y activar hello **mostrar todos los archivos** icono encima de hello **el Explorador de soluciones**.
5. Algunos archivos no se incluyen en el proyecto de Hola. tooimport ellos a la vez haga clic en hello **recursos** carpeta, **excluir del proyecto** otro derecho haga clic en hello **recursos** carpeta, **Include en el proyecto** toore-incluir toda la carpeta Hola. Todos los archivos de hello **recursos** carpeta ahora se incluyen en el proyecto.

## <a name="add-hello-capabilities"></a>Agregar capacidades de Hola
Hola Engagement SDK tiene algunas capacidades de hello SDK de Windows en orden toowork correctamente.

Abra su `Package.appxmanifest` de archivos y asegúrese de que se declaran ese Hola siguiendo las capacidades:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Inicializar Hola Engagement SDK
### <a name="engagement-configuration"></a>Configuración de Engagement
configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto.

Editar este archivo toospecify:

* La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.

Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.

### <a name="engagement-initialization"></a>Inicialización de Engagement
Al crear un nuevo proyecto, se genera un archivo `App.xaml.cs` . Esta clase hereda de `Application` y contiene muchos métodos importantes. También será usado tooinitialize Hola Engagement SDK.

Modificar Hola `App.xaml.cs`:

* Agregar tooyour `using` instrucciones:
  
      using Microsoft.Azure.Engagement;
* Definir una método tooshare Hola interacción la inicialización una vez para todas las llamadas:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Llame a `InitEngagement` en hello `OnLaunched` método:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Cuando la aplicación se inicia utilizando un esquema personalizado, a continuación, Hola otra línea de comandos de aplicación o hello `OnActivated` se llama al método. También debe tooinitiate Hola Engagement SDK cuando se activa la aplicación. por lo tanto, invalidar toodo `OnActivated` método:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Se desaconseja encarecidamente tooadd Hola interacción inicialización en otro lugar de la aplicación.
> 
> 

## <a name="basic-reporting"></a>Informes básicos
### <a name="recommended-method-overload-your-page-classes"></a>Método recomendado: sobrecargar las clases `Page`
Informe de hello order tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, basta con hacer que todos los su `Page` subclases heredan de hello `EngagementPage` clases.

Este es un ejemplo de cómo toodo esto en una página de la aplicación. Puede hacer lo mismo para todas las páginas de la aplicación de Hola.

#### <a name="c-source-file"></a>Archivo de código fuente C#
Modifique el archivo `.xaml.cs` de página:

* Agregar tooyour `using` instrucciones:
  
      using Microsoft.Azure.Engagement;
* Reemplace `Page` por `EngagementPage`:

**Sin Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Con Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Si la página invalida hello `OnNavigatedTo` método, ser seguro toocall `base.OnNavigatedTo(e)`. En caso contrario, no se incluirán actividad hello (hello `EngagementPage` llamadas `StartActivity` dentro de su `OnNavigatedTo` método).
> 
> 

#### <a name="xaml-file"></a>Archivo XAML
Modifique el archivo `.xaml` de página:

* Agregue las declaraciones de espacios de nombres tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Reemplace `Page` por `engagement:EngagementPage`:

**Sin Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Con Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Invalidar el comportamiento predeterminado de Hola
De forma predeterminada, nombre de la clase de página de Hola Hola se notifica como nombre de la actividad de hello, con ningún extra. Si la clase hello usa el sufijo "Página" Hola, interacción, también se quitará.

Si desea comportamiento predeterminado de toooverride Hola para nombre de hello, basta con agregar este código tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Si desea tooreport algunos datos adicionales con la actividad, puede agregar este código tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Estos métodos se invocan desde dentro de hello `OnNavigatedTo` método de la página.

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: llamar a `StartActivity()` manualmente
Si no puede o no desea que toooverload su `Page` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent` métodos directamente.

Se recomienda toocall `StartActivity` dentro de su `OnNavigatedTo` al método de la página.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Asegúrese de finalizar la sesión correctamente.
> 
> Hola SDK Universal de Windows llama automáticamente a hello `EndActivity` método cuando se cierra la aplicación hello. Por lo tanto, es **alta** recomienda hello toocall `StartActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado**nunca** llamada hello `EndActivity` método, este método envía tooEngagement servidor que usuario actual tiene deje Hola aplicación, esta acción afecta a todos los registros de aplicación.
> 
> 

## <a name="advanced-reporting"></a>Informes avanzados
Si lo desea, puede que desee eventos específicos de aplicación tooreport, errores y los trabajos y toodo por lo tanto, use otros métodos que se encuentran en Hola Hola `EngagementAgent` clase. Hola interacción API permite toouse todas las capacidades avanzadas de contratación.

Para obtener más información, consulte [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md).

## <a name="advanced-configuration"></a>Configuración avanzada
### <a name="disable-automatic-crash-reporting"></a>Deshabilitar los informes automáticos de bloqueo
Puede deshabilitar Hola automática de informes de errores característica de contratación. A continuación, cuando se produce una excepción no controlada, Engagement no hará nada.

> [!WARNING]
> Si tiene previsto toodisable esta característica, tenga en cuenta que cuando se producirá un bloqueo no controlado en la aplicación, interacción no enviará bloqueo hello **AND** no se cerrará la sesión de Hola y trabajos.
> 
> 

bloqueo automático toodisable reporting, simplemente personalizar la configuración según la forma de Hola se declaró:

#### <a name="from-engagementconfigurationxml-file"></a>Desde el archivo `EngagementConfiguration.xml`
Establecer un informe de bloqueo demasiado`false` entre `<reportCrash>` y `</reportCrash>` etiquetas.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Desde el objeto `EngagementConfiguration` en tiempo de ejecución
Establecer toofalse de bloqueo de informe mediante el objeto EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Modo de ráfaga
De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real. Si la aplicación informa de los registros con mucha frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (Esto se denomina hello "modo de ráfaga").

toodo por lo tanto, llame al método hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hola argumento es un valor en **milisegundos**. En cualquier momento, si desea que el registro en tiempo real de tooreactivate hello, simplemente llamar a Hola método sin parámetros o con el valor de hello 0.

Hello el modo de ráfaga incremente ligeramente batería Hola vida pero tiene un impacto en hello Monitor de contratación: duración de las sesiones y los trabajos de todos los será redondeado toohello ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible). Es recomendable toouse ya no es un umbral de ráfaga de 30000 (30 s). Tendrá que toobe tenga en cuenta que los registros guardados son elementos too300 limitado. Si el envío es demasiado largo, puede perder algunos registros.

> [!WARNING]
> umbral de ráfaga de Hello no se puede configurar tooa período anterior a 1s. Si intentas toodo por lo tanto, Hola SDK se muestran un seguimiento con error de Hola y configurará automáticamente y restablece valor predeterminado de toohello, es decir, 0. Esto desencadenará Hola SDK tooreport Hola registros en tiempo real.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

