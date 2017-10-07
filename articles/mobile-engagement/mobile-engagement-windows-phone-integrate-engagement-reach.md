---
title: "aaaWindows Phone Silverlight alcanzar integración con el SDK"
description: "¿Cómo tooIntegrate Azure Mobile Engagement alcanzar con aplicaciones de Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Integración del SDK de cobertura de Windows Phone Silverlight
Debe seguir el procedimiento de integración de hello descrito en hello [integración del SDK de interacción de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir esta guía.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Incrustar Hola interacción Reach SDK en el proyecto de Windows Phone Silverlight
No tiene nada tooadd. `EngagementReach` y los recursos de ya están en el proyecto.

> [!TIP]
> Puede personalizar imágenes ubicado en hello `Resources` carpeta del proyecto, especialmente icono de marca de hello (ese icono de interacción de toohello predeterminado).
> 
> 

## <a name="add-hello-capabilities"></a>Agregar capacidades de Hola
Hola interacción Reach SDK tiene algunas capacidades adicionales.

Abra su `WMAppManifest.xml` de archivos y asegúrese de que se declaran ese Hola siguiendo las capacidades:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Hello uno se utiliza por primera vez mostrar hello MPNS servicio tooallow Hola de notificación del sistema. Hello segunda es tooembed usa una tarea de explorador en hello SDK.

Editar hello `WMAppManifest.xml` de archivos y agregar dentro de hello `<Capabilities />` etiqueta:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Habilitar Hola servicio de notificaciones Push de Microsoft
Hola de orden toouse **servicio de notificaciones Push de Microsoft** (denominadas MPNS) su `WMAppManifest.xml` archivo debe tener un `<App />` etiquetar con un `Publisher` atributo establece toohello nombre del proyecto.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inicializar Hola interacción Reach SDK
### <a name="engagement-configuration"></a>Configuración de Engagement
configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto.

Editar este archivo de configuración de alcance toospecify:

* *Opcional*, indicar si se activa la inserción nativa de hello (MPNS) o no entre `<enableNativePush>` y `</enableNativePush>` etiquetas, (`true` de forma predeterminada).
* *Opcional*, indicar Hola nombre de canal de inserción de hello entre `<channelName>` y `</channelName>` etiquetas, proporcionar Hola misma que la aplicación puede usar o déjela en blanco actualmente.

Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Puede especificar nombre de Hola de canal de inserción de hello MPNS de la aplicación. De forma predeterminada, interacción crea un nombre basado en hello appId. No tenga necesidad de toospecify Hola nombre usted mismo, excepto si tiene intención de canal de inserción de hello toouse fuera de contratación.
> 
> 

### <a name="engagement-initialization"></a>Inicialización de Engagement
Modificar Hola `App.xaml.cs`:

* Agregar tooyour `using` instrucciones:
  
      using Microsoft.Azure.Engagement;
* Inserte `EngagementReach.Instance.Init` justo después de `EngagementAgent.Instance.Init` en `Application_Launching`:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Insertar `EngagementReach.Instance.OnActivated` en hello `Application_Activated` método:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Hola `EngagementReach.Instance.Init` se ejecuta en un subproceso dedicado. No tiene toodo usted mismo.
> 
> 

## <a name="app-store-submission-considerations"></a>Consideraciones de envío de la tienda de aplicaciones
Microsoft impone algunas reglas al usar notificaciones de inserción de hello:

De hello Microsoft [las directivas de aplicación] documentación, sección 2.9:

1) Debe solicitar notificaciones de inserción de hello usuario tooaccept tooreceive. A continuación, en la configuración, agregue un notificaciones de inserción de manera toodisable Hola.

objeto de Hello EngagementReach proporciona dos métodos toomanage Hola/opt: desactivación, `EnableNativePush()` y `DisableNativePush()`. Por ejemplo, podría crear una opción en la configuración de hello con un toodisable de alternancia o habilitar MPNS.

También puede decidir toodeactivate MPNS a través de la configuración de la interacción de hello\<windows phone sdk alcance configuración\>.

> 2.9.1) aplicación hello en primer lugar debe describir Hola notificaciones toobe proporcionado y **obtener permiso de express del usuario de hello (OPC-in)**, y **debe proporcionar un mecanismo a través de qué Hola usuario puede optar por recibir notificaciones de inserción**. Todas las notificaciones que se proporciona mediante Hola servicio de notificaciones Push de Microsoft deben ser coherentes con hello descripción proporcionada toohello usuario y debe cumplir con todas las aplicables [las directivas de aplicación] [ Content Policies]y [requisitos adicionales para los tipos de aplicación específica].
> 
> 

2) No debería usar demasiadas notificaciones push. Engagement controlará las notificaciones por usted.

> 2.9.2) aplicación hello y su uso del programa Hola a servicio de notificaciones Push de Microsoft deben no excesivamente usar ancho de banda de hello servicio de notificaciones Push de Microsoft o la capacidad de red, o en caso contrario, sobrecargar innecesariamente un Windows Phone u otros dispositivos de Microsoft o el servicio con excesivo push notificaciones, según lo determinado por Microsoft en el criterio razonable y no debe dañar ni interferir con las redes de Microsoft o servidores o los servidores de terceros o redes conectadas toohello servicio de notificaciones de inserción de Microsoft.
> 
> 

3) No confíe en la información de MPNS toosend criticals. Interacción usa MPNS, por lo que esta regla también se aplica de las campañas de hello creadas dentro de hello interacción front-end.

> 2.9.3) Hola servicio de notificaciones Push de Microsoft no puede ser toosend usado notificaciones que son de misión crítica o de otra manera podría afectar a cuestiones de vida o muerte, incluyendo pero sin las notificaciones críticas relacionadas tooa médicas limitador o condición. MICROSOFT expresamente rechaza cualquier garantía que Hola uso de hello MICROSOFT PUSH notificación servicio o entrega de MICROSOFT PUSH notificación servicio las notificaciones le puede sin interrupción, libre de errores, o en caso contrario garantiza tooOCCUR base en tiempo real de ON A.
> 
> 

**No podemos garantizar que la aplicación pasará el proceso de validación de hello si no respeta estas recomendaciones.**

## <a name="handle-data-push-optional"></a>Control de la inserción de datos (opcional)
Si desea que su inserciones de datos de aplicación toobe tooreceive capaz de alcance, deberá tooimplement dos eventos de hello EngagementReach clase:

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

Puede ver esa devolución de llamada de Hola de cada método devuelve un valor booleano. Interacción envía un back-end de tooits de comentarios después de enviar la inserción de datos de Hola. Si la devolución de llamada de hello devuelve false, Hola `exit` comentarios se estarán. De lo contrario, será `action`. Si no se establece ninguna devolución de llamada para los eventos de hello, Hola `drop` comentarios se devolverá tooEngagement.

> [!WARNING]
> Interacción no es capaz de tooreceive opiniones de múltiplos para una inserción de datos. Si tiene previsto tooset varios controladores en un evento, tenga en cuenta que los comentarios de Hola corresponderá toohello penúltima enviado. En este caso, se recomienda tooalways devuelve Hola mismo tooavoid valor tener comentarios confuso en hello front-end.
> 
> 

## <a name="customize-ui-optional"></a>Personalizar la interfaz de usuario (opcional)
### <a name="first-step"></a>Primer paso
Le permitimos alcance de hello toocustomize interfaz de usuario.

toodo por lo tanto, tiene una subclase de hello toocreate `EngagementReachHandler` clase.

**Código de ejemplo:**

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

A continuación, establezca el contenido de Hola de hello `EngagementReach.Instance.Handler` campo con su objeto personalizado en su `App.xaml.cs` clase dentro de hello `Application_Launching` método.

**Código de ejemplo:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> De forma predeterminada, Engagement usa su propia implementación de `EngagementReachHandler`. No tienes toocreate el suyo propio, y si lo hace, no tiene toooverride cada método. comportamiento predeterminado de Hello es objeto de base de tooselect Hola interacción.
> 
> 

### <a name="layouts"></a>Diseños
De forma predeterminada, alcance usará recursos Hola incrustada de las notificaciones de hello DLL toodisplay hello y páginas.

Sin embargo, puede decidir los toouse su propios recursos tooreflect su marca en estos componentes.

Puede invalidar `EngagementReachHandler` métodos en su toouse de interacción de subclase tootell los diseños:

**Código de ejemplo:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Hola `CreateNotification` método puede devolver null. no se mostrarán notificaciones de Hola y campaña de cobertura de Hola se van a quitar.
> 
> 

toosimplify su implementación de diseño, también proporcionamos nuestro propio xaml que puede servir como base para el código. Se encuentran en el archivo del SDK de interacción de hello (/ src/alcance /).

> [!WARNING]
> orígenes de Hola que ofrecemos son Hola exacto que mismo que utilizamos. Por lo que si desea toomodify ellos directamente, no olvide el espacio de nombres de toochange Hola y Hola nombre.
> 
> 

### <a name="notification-position"></a>Posición de notificación
De forma predeterminada, se muestra una notificación en la aplicación en hello parte inferior izquierda de la aplicación hello. Puede cambiar este comportamiento mediante la invalidación hello `GetNotificationPosition` método de hello `EngagementReachHandler` objeto.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Actualmente, puede elegir entre hello `BOTTOM` (valor predeterminado) y `TOP` posiciones.

### <a name="launch-message"></a>Iniciar el mensaje
Cuando un usuario hace clic en una notificación del sistema (una notificación del sistema), inicia interacción Hola aplicación, carga Hola contenido de hello envíen mensajes y mostrar página Hola Hola correspondiente de la campaña.

Hay un retraso entre el inicio de Hola de pantalla de hello y aplicación Hola de página hello (según la velocidad de saludo de la red).

usuario de toohello tooindicate que algo se está cargando, debe proporcionar una información visual, como una barra de progreso o un indicador de progreso. Engagement no puede controlar esto por sí solo, pero le ofrece algunos controladores para ello.

tooimplement Hola de devolución de llamada, realice:

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Puede establecer la devolución de llamada de hello en su `Application_Launching` método de su `App.xaml.cs` archivo, preferentemente antes de hello `EngagementReach.Instance.Init()` llamar.

> [!TIP]
> Hola subprocesos de interfaz de usuario llama a cada controlador. No es necesario tooworry cuando se utiliza un cuadro de mensajes o algo relacionado con la interfaz de usuario.
> 
> 

[las directivas de aplicación]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisitos adicionales para los tipos de aplicación específica]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

