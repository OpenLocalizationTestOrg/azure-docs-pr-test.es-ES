---
title: "aaaWindows integración de SDK de alcanzar de aplicaciones Universal"
description: "¿Cómo tooIntegrate Azure Mobile Engagement alcanzar con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Integración del SDK de Cobertura de Windows Universal Apps
Debe seguir el procedimiento de integración de hello descrito en hello [integración del SDK de interacción Universal de Windows](mobile-engagement-windows-store-integrate-engagement.md) antes de seguir esta guía.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Incrustar Hola interacción Reach SDK en el proyecto Universal de Windows
No tiene nada tooadd. `EngagementReach` y los recursos de ya están en el proyecto.

> [!TIP]
> Puede personalizar imágenes ubicado en hello `Resources` carpeta del proyecto, especialmente icono de marca de hello (ese icono de interacción de toohello predeterminado). En las aplicaciones universales también puede mover hello `Resources` carpeta en su tooshare de proyecto compartido su contenido entre aplicaciones, sino tendrá hello tookeep `Resources\EngagementConfiguration.xml` de archivos en su ubicación predeterminada tal cual depende de la plataforma.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Habilitar el servicio de notificación de Windows hello
### <a name="windows-8x-and-windows-phone-81-only"></a>Solo Windows 8.x y Windows Phone 8.1
Hola de orden toouse **servicio de notificación de Windows** (denominadas WNS) en su `Package.appxmanifest` de archivos en `Application UI` haga clic en `All Image Assets` en cuadro de hello bot izquierdo. En hello derecha del cuadro de hello en `Notifications`, cambiar `toast capable` de `(not set)` demasiado`(Yes)`.

### <a name="all-platforms"></a>Todas las plataformas
Debe toosynchronize su aplicación tooyour cuenta y toohello interacción plataforma de Microsoft. Para ello necesita toocreate una cuenta o inicio de sesión [centro de desarrollo de windows](https://dev.windows.com). Una vez que cree una nueva aplicación y busque Hola SID y una clave secreta. En el servidor front-end de la interacción de hello, ir en la configuración de aplicación en `native push` y pegue las credenciales. Luego, haga clic con el botón secundario del mouse en el proyecto, seleccione `store` y `Associate App with hello Store...`. Aplicación de hello tooselect debe lo crear antes de toosynchronize.

## <a name="initialize-hello-engagement-reach-sdk"></a>Inicializar Hola interacción Reach SDK
Modificar Hola `App.xaml.cs`:

* Inserte `EngagementReach.Instance.Init` justo después de `EngagementAgent.Instance.Init` en su método `InitEngagement`:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Hola `EngagementReach.Instance.Init` se ejecuta en un subproceso dedicado. No tiene toodo usted mismo.

> [!NOTE]
> Si está utilizando las notificaciones de inserción en otra parte de la aplicación, entonces tiene demasiado[compartir su canal de inserción](#push-channel-sharing) con interacción alcanzar.
> 
> 

## <a name="integration"></a>Integración
Interacción proporciona banners de la aplicación de dos maneras tooadd Hola alcance y vistas intersticiales para sondeos en la aplicación y anuncios: Hola superposición de integración y la integración de hello web vistas manuales. No debería combinar ambos enfoque en hello sintonía.

elección de Hello entre integración dos Hola podía resumirse así:

* Puede elegir la integración de superposición de hello si las páginas ya hereda de hello agente `EngagementPage`, es simplemente una cuestión de sustitución de `EngagementPage` por `EngagementPageOverlay` y `xmlns:engagement="using:Microsoft.Azure.Engagement"` por `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` en las páginas.
* Puede elegir integración manual de hello web vistas si desea tooprecisely lugar Hola llegar a la interfaz de usuario dentro de las páginas o si no desea tooadd otro páginas de nivel tooyour de herencia. 

### <a name="overlay-integration"></a>Integración de superposición
superposición de interacción de Hello agrega dinámicamente elementos de interfaz de usuario de hello usan campañas toodisplay en la página. Si la superposición de hello no se ajusta a su diseño debe considerar vistas de hello web integración manual en su lugar.

En el cambio de los archivos .xaml `EngagementPage` referencia demasiado`EngagementPageOverlay`

* Agregue las declaraciones de espacios de nombres tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Reemplace `engagement:EngagementPage` por `engagement:EngagementPageOverlay`:

**Con EngagementPage:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**Con EngagementPageOverlay:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Después, en el archivo. cs, etiquete la página en `EngagementPageOverlay` en lugar de `EngagementPage` e importe `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Reemplace `EngagementPage` por `EngagementPageOverlay`:

**Con EngagementPage:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**Con EngagementPageOverlay:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Agrega Hello superposición de interacción una `Grid` elemento encima de la página está formada por su diseño y Hola dos `WebView` elementos uno para hello banner y Hola otro uno para la vista intersticiales Hola.

Se pueden personalizar elementos de la superposición de hello directamente en hello `EngagementPageOverlay.cs` archivo.

### <a name="web-views-manual-integration"></a>Integración manual de vistas web
Alcance buscan las páginas para hello dos `WebView` elementos responsables de mostrar pancarta hello y vista intersticiales Hola. Hola solo lo tienes toodo es tooadd esos dos `WebView` elementos en alguna parte de las páginas, este es un ejemplo:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


En este Hola ejemplo `WebView` elementos es toofit ajustado su contenedor que automáticamente volver a tamaños de ellos en el caso de cambio de tamaño de ventana o la rotación de pantalla.

> [!WARNING]
> Es importante tookeep Hola misma nomenclatura `engagement_notification_content` y `engagement_announcement_content` para hello `WebView` elementos. Reach los identifica por su nombre. 
> 
> 

## <a name="handle-datapush-optional"></a>Controlar la inserción de datos (opcional)
Si desea que su inserciones de datos de aplicación toobe tooreceive capaz de alcance, deberá tooimplement dos eventos de hello EngagementReach clase:

En App.xaml.cs en el constructor de hello App() agregar:

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

A continuación, establezca el contenido de Hola de hello `EngagementReach.Instance.Handler` campo con su objeto personalizado en su `App.xaml.cs` clase dentro de hello `App()` método.

**Código de ejemplo:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> De forma predeterminada, Engagement usa su propia implementación de `EngagementReachHandler`.
> No tienes toocreate el suyo propio, y si lo hace, no tiene toooverride cada método. comportamiento predeterminado de Hello es objeto de base de tooselect Hola interacción.
> 
> 

### <a name="web-view"></a>Vista web
De forma predeterminada, alcance usará recursos Hola incrustada de las notificaciones de hello DLL toodisplay hello y páginas.

tooprovide una completa de posibilidades de personalización solo se utiliza vista web. Si desea toocustomize diseños, invalidar directamente los archivos de recursos de hello `EngagementAnnouncement.html` y `EngagementNotification.html`. Todo el código, se precisa `<body></body>` toorun correctamente. No obstante, puede agregar una etiqueta exterior `engagement_webview_area`.

Sin embargo, puede decidir toouse sus propios recursos.

Puede invalidar `EngagementReachHandler` métodos en su toouse de interacción de subclase tootell los diseños, pero toman mecanismo de interacción de atención tooembedded hello:

**Código de ejemplo:**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


De forma predeterminada, AnnouncementHTML es `ms-appx-web:///Resources/EngagementAnnouncement.html`. Que representa el archivo html hello que diseñar Hola contenido de un mensaje de inserción (anuncio de texto, anoucement Web y anuncio de sondeo). AnnouncementName es `engagement_announcement_content`. Es nombre Hola Hola webview del diseño de en la página xaml.

NotfificationHTML es `ms-appx-web:///Resources/EngagementNotification.html`. Que representa el archivo html hello que diseñar Hola notificación de un mensaje de inserción. NotfificationName es `engagement_notification_content`. Es nombre Hola Hola webview del diseño de en la página xaml.

### <a name="customization"></a>Personalización
Puede personalizar la vista web de notificación y anuncio como desee si quiere conservar el objeto de Engagement. Tenga cuidado de que se describe webview objeto tres veces: hello primera vez en el archivo xaml, en segundo lugar de tiempo en el archivo .cs en método de "setwebview()" hello y en tercer lugar hora en el archivo html de hello.

* En el xaml se describe el componente de webview de diseño gráfico actual Hola.
* En el archivo .cs puede definir "setwebview()" en el que establecer dimensión Hola de hello dos webview (notificación, anuncio). Es muy eficaz cuando está cambiando el tamaño de aplicación hello.
* En el archivo html de interacción de Hola se describir Hola webview contenido, diseño y Hola posiciones de elementos entre sí.

### <a name="launch-message"></a>Iniciar el mensaje
Cuando un usuario hace clic en una notificación del sistema (una notificación del sistema), interacción inicia la aplicación hello, carga Hola contenido de hello envíen mensajes y mostrar página Hola campaña correspondiente Hola.

Hay un retraso entre el inicio de Hola de pantalla de hello y aplicación Hola de página hello (según la velocidad de saludo de la red).

usuario de toohello tooindicate que algo se está cargando, debe proporcionar una información visual, como una barra de progreso o un indicador de progreso. Engagement no puede controlar esto por sí solo, pero le ofrece algunos controladores para ello.

Agregar tooimplement Hola devolución de llamada, en App.xaml.cs "App() pública {}":

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

Puede establecer la devolución de llamada de hello en el método "App() pública {}" de la `App.xaml.cs` archivo, preferentemente antes de hello `EngagementReach.Instance.Init()` llamar.

> [!TIP]
> Hola subprocesos de interfaz de usuario llama a cada controlador. No es necesario tooworry cuando se utiliza un cuadro de mensajes o algo relacionado con la interfaz de usuario.
> 
> 

## <a id="push-channel-sharing"></a> Uso compartido de canal de inserción
Si está utilizando las notificaciones de inserción para otro fin en la aplicación tendrá canal de inserción de hello toouse característica de hello SDK de interacción de uso compartido. Se trata de inserción tooavoid perdido.

* Puede proporcionar su propia inicialización de llegar a la interacción de inserción de canales toohello. Hola SDK lo utilizará en lugar de solicitar una nueva.

Actualizar inicialización de llegar a la interacción de hello con el canal de inserción en hello `InitEngagement` método de hello `App.xaml.cs` archivo:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* O bien, si su intención es tooconsume Hola push canal después de la inicialización de alcance de hello, a continuación, puede establecer una devolución de llamada en el canal de contratación alcanzar tooget Hola inserción una vez que se crea mediante Hola SDK.

Establezca la devolución de llamada en cualquier lugar **después** Hola inicialización alcance:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Sugerencia de esquema personalizado
Se incluye el uso de esquemas personalizados. Puede enviar un tipo diferente de URI de contratación front-end toobe utilizado en la aplicación de interacción. Los esquemas predeterminados, como `http, ftp, ...`, los administra Windows. Una ventana pedirá información si no hay ninguna aplicación predeterminada instalada en el dispositivo. También puede crear su propio esquema personalizado para su aplicación.

tooset de manera sencilla de Hello una combinación personalizada en su aplicación es tooopen su `Package.appxmanifest` vaya en `Declarations` panel. Seleccione `Protocol` Hola declaraciones disponibles desplácese cuadro y agréguelo. Editar hello `Name` nombre de campo con el nuevo protocolo deseado.

Ahora toouse este protocolo, edite su `App.xaml.cs` con hello `OnActivated` método y no olvide tooinitialize interacción aquí también:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

