---
title: "aaaWindows Universal avanzada Reporting con interacción de MobileApps"
description: "¿Cómo tooIntegrate Azure Mobile Engagement con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Informes avanzados con hello SDK de interacción de aplicaciones Universal de Windows
> [!div class="op_single_selector"]
> * [Windows universal](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Este tema describe los escenarios de informes adicionales en la aplicación universal de Windows. Estos escenarios incluyen opciones que puede elegir tooapply toohello aplicación creado en hello [Introducción](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Antes de iniciar este tutorial, debe completar primero hello [Introducción](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, que es deliberadamente sencilla y directa. Este tutorial explica las opciones adicionales que puede elegir.

## <a name="specifying-engagement-configuration-at-runtime"></a>Especificación de la configuración de Engagement en tiempo de ejecución
configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto, que es donde se especifica en hello [Introducción](mobile-engagement-windows-store-dotnet-get-started.md) tema.

Pero también puede especificar en tiempo de ejecución: se puede llamar a Hola siguiente método antes de la inicialización de agente de interacción de hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Método recomendado: sobrecargar las clases `Page`
tooactivate Hola reporting de todos los registros de hello requeridos interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, poner todos los su `Page` subclases heredan de hello `EngagementPage` clases.

Este es un ejemplo para una página de la aplicación. Puede hacer lo mismo para todas las páginas de la aplicación de Hola.

### <a name="c-source-file"></a>Archivo de código fuente C#
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
> Si la página invalida hello `OnNavigatedTo` método, ser seguro toocall `base.OnNavigatedTo(e)`. De lo contrario, actividad hello no se notificará (hello `EngagementPage` llamadas `StartActivity` dentro de su `OnNavigatedTo` método).
> 
> 

### <a name="xaml-file"></a>Archivo XAML
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

### <a name="override-hello-default-behaviour"></a>Invalidar el comportamiento predeterminado de Hola
De forma predeterminada, nombre de la clase de página de Hola Hola se notifica como nombre de la actividad de hello, con ningún extra. Si la clase hello usa el sufijo "Página" Hola, interacción quita.

comportamiento de toooverride Hola predeterminado para el nombre de hello, agregue este código:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport información adicional con la actividad, agregue este código:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Estos métodos se invocan desde dentro de hello `OnNavigatedTo` método de la página.

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: llamar a `StartActivity()` manualmente
Si no puede o no desea que toooverload su `Page` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent` métodos directamente.

Se recomienda llamar a `StartActivity` dentro del método `OnNavigatedTo` de su página.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Asegúrese de finalizar la sesión correctamente.
> 
> Hola SDK Universal de Windows llama automáticamente a hello `EndActivity` método cuando se cierra la aplicación hello. Por lo tanto, es **alta** recomienda hello toocall `StartActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado**nunca** llamada hello `EndActivity` método. Este método notifica a servidor de interacción de Hola que el usuario actual Hola ha dejado la aplicación hello, lo que afectará a todos los registros de aplicación.
> 
> 

## <a name="advanced-reporting"></a>Informes avanzados
Si lo desea, puede que desee eventos específicos de la aplicación de tooreport, errores y los trabajos y toodo por lo tanto, use otros métodos que se encuentran en Hola Hola `EngagementAgent` clase. Hola interacción API permite el uso de las capacidades avanzadas de todas las interacciones.

Para obtener más información, consulte [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md).

