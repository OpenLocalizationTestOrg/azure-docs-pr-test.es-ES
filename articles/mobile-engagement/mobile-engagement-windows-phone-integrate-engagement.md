---
title: "aaaWindows integración con el SDK interacción Phone Silverlight"
description: "¿Cómo tooIntegrate Azure Mobile Engagement con aplicaciones de Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Integración del SDK de Windows Phone Silverlight Engagement
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Este procedimiento describe las funciones en la aplicación de Windows Phone Silverlight de supervisión y análisis hello más sencilla forma tooactivate Azure Mobile Engagement.

Hola pasos es que toocompute necesita un suficiente informe de hello tooactivate de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals. Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) a continuación) debido a que estas estadísticas son dependientes de la aplicación.

## <a name="supported-versions"></a>Versiones compatibles
Hola Mobile Engagement SDK para Silverlight para Windows sólo se puede integrar en las aplicaciones con destino:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Si se dirige a Windows Phone 8.1 (no de Silverlight), consulte toohello [procedimiento de integración de Windows Universal](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Instalar el SDK de Silverlight de Mobile Engagement Hola
Hola Mobile Engagement SDK para Silverlight para Windows está disponible como un paquete de Nuget llamado *MicrosoftAzure.MobileEngagement*. Puede instalarlo desde Hola Administrador de paquetes de Nuget de Visual Studio. 

## <a name="add-hello-capabilities"></a>Agregar capacidades de Hola
Hola Engagement SDK tiene algunas capacidades de hello SDK de Windows Phone Silverlight en orden toowork correctamente.

Abra su `WMAppManifest.xml` de archivos y asegúrese de que Hola siguiendo las capacidades se declaran en hello `Capabilities` panel:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Inicializar Hola Engagement SDK
### <a name="engagement-configuration"></a>Configuración de Engagement
configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto.

Editar este archivo toospecify:

* La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.

Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.

### <a name="engagement-initialization"></a>Inicialización de Engagement
Al crear un nuevo proyecto, se genera un archivo `App.xaml.cs` . Esta clase hereda de `Application` y contiene muchos métodos importantes. También será usado tooinitialize Hola Engagement SDK.

Modificar Hola `App.xaml.cs`:

* Agregar tooyour `using` instrucciones:
  
      using Microsoft.Azure.Engagement;
* Insertar `EngagementAgent.Instance.Init` en hello `Application_Launching` método:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Insertar `EngagementAgent.Instance.OnActivated` en hello `Application_Activated` método:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Se desaconseja encarecidamente tooadd Hola interacción inicialización en otro lugar de la aplicación. Sin embargo, tenga en cuenta que hello `EngagementAgent.Instance.Init` método se ejecuta en un subproceso dedicado y no en el subproceso de interfaz de usuario de Hola.
> 
> 

## <a name="basic-reporting"></a>Informes básicos
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Método recomendado: sobrecargar las clases `PhoneApplicationPage`
Informe de hello order tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, basta con hacer que todos los su `PhoneApplicationPage` subclases heredan de hello `EngagementPage` clases.

Este es un ejemplo de cómo toodo esto en una página de la aplicación. Puede hacer lo mismo para todas las páginas de la aplicación de Hola.

#### <a name="c-source-file"></a>Archivo de código fuente C#
Modifique el archivo `.xaml.cs` de página:

* Agregar tooyour `using` instrucciones:
  
      using Microsoft.Azure.Engagement;
* Reemplace `PhoneApplicationPage` por `EngagementPage`:

**Sin Engagement:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Con Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Si la página hereda de hello `OnNavigatedTo` método, puede toolet cuidado Hola `base.OnNavigatedTo(e)` llamar. En caso contrario, no se notificarán actividad hello. De hecho, Hola `EngagementPage` llama a `StartActivity` dentro de hello `OnNavigatedTo` método.
> 
> 

#### <a name="xaml-file"></a>Archivo XAML
Modifique el archivo `.xaml` de página:

* Agregue las declaraciones de espacios de nombres tooyour:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Reemplace `phone:PhoneApplicationPage` por `engagement:EngagementPage`:

**Sin Engagement:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Con Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Invalidar el comportamiento predeterminado de Hola
De forma predeterminada, nombre de la clase de página de Hola Hola se notifica como nombre de la actividad de hello, con ningún extra. Si la clase hello usa el sufijo "Página" Hola, interacción, también se quitará.

Si desea comportamiento predeterminado de toooverride Hola para nombre de hello, basta con agregar este código tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Si desea tooreport cierta información adicional con la actividad, puede agregar este código tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Estos métodos se invocan desde dentro de hello `OnNavigatedTo` método de la página.

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: llamar a `StartActivity()` manualmente
Si no puede o no desea que toooverload su `PhoneApplicationPage` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent` métodos directamente.

Recomendamos que llame a `StartActivity` dentro del método `OnNavigatedTo` de su PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Asegúrese de finalizar la sesión correctamente.
> 
> Hola SDK llama automáticamente a hello `EndActivity` método cuando se cierra la aplicación hello. Por lo tanto, es **alta** recomienda hello toocall `StartActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado**nunca** llamada hello `EndActivity` método. Este método envía un servidor de interacción de toohello mensajes que usuario actual de hello ha abandonado la aplicación hello y esto afecta a todos los registros de aplicación.
> 
> 

## <a name="advanced-reporting"></a>Informes avanzados
Si lo desea, puede que desee eventos específicos de aplicación tooreport, errores y los trabajos y toodo por lo tanto, use otros métodos que se encuentran en Hola Hola `EngagementAgent` clase. Hola interacción API permite toouse todas las capacidades avanzadas de contratación.

Para obtener más información, consulte [cómo toouse Hola avanzada Mobile Engagement etiquetado API en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Configuración avanzada
### <a name="disable-automatic-crash-reporting"></a>Deshabilitar los informes automáticos de bloqueo
Puede deshabilitar Hola automática de informes de errores característica de contratación. A continuación, cuando se produce una excepción no controlada, Engagement no hará nada.

> [!WARNING]
> Si tiene previsto toodisable esta característica, tenga en cuenta que cuando se producirá un bloqueo no controlado en la aplicación, interacción no enviará bloqueo hello **AND** no cerrará sesión hello y trabajos.
> 
> 

bloqueo automático toodisable reporting, simplemente personalizar la configuración según la forma de Hola se declaró:

#### <a name="from-engagementconfigurationxml-file"></a>Desde el archivo `EngagementConfiguration.xml`
Establecer un informe de bloqueo demasiado`false` entre `<reportCrash>` y `</reportCrash>` etiquetas.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Desde el objeto `EngagementConfiguration` en tiempo de ejecución
Establecer toofalse de bloqueo de informe mediante el objeto EngagementConfiguration.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Modo de ráfaga
De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real. Si la aplicación informa de los registros con mucha frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (Esto se denomina hello "modo de ráfaga").

toodo por lo tanto, llame al método hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hola argumento es un valor en **milisegundos**. En cualquier momento, si desea que el registro en tiempo real de tooreactivate hello, simplemente llamar a Hola método sin parámetros o con el valor de hello 0.

Hello el modo de ráfaga incremente ligeramente batería Hola vida pero tiene un impacto en hello Monitor de contratación: duración de las sesiones y los trabajos de todos los será redondeado toohello ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible). Es recomendable toouse ya no es un umbral de ráfaga de 30000 (30 s). Tendrá que toobe tenga en cuenta que los registros guardados son elementos too300 limitado. Si el envío es demasiado largo, puede perder algunos registros.

> [!WARNING]
> Hello umbral de ráfaga no se puede configurar tooa período menor que un segundo. Si intentas toodo por lo tanto, Hola SDK se muestran un seguimiento con error de Hola y configurará automáticamente y restablece toohello valor de manera predeterminada, es decir, cero segundos. Esto desencadenará Hola SDK tooreport Hola registros en tiempo real.
> 
> 

