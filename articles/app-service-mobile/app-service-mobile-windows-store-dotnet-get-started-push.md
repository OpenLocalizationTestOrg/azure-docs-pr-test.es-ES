---
title: "aplicación de plataforma Universal de Windows (UWP) de aaaAdd inserción notificaciones tooyour | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse aplicaciones de Mobile de servicio de aplicación de Azure y los centros de notificaciones de Azure toosend push notificaciones tooyour plataforma Universal de Windows (UWP) aplicaciones."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a>Agregar aplicación de Windows de tooyour de notificaciones de inserción
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de Windows](app-service-mobile-windows-store-dotnet-get-started.md) del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción. Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.

## <a name="configure-hub"></a>Configurar un Centro de notificaciones
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Registro de la aplicación para notificaciones push
Se necesita toosubmit su toohello aplicación tienda Windows, después de configura su toointegrate de project server con servicios de notificación de Windows (WNS) toosend inserción.

1. En Visual Studio Solution Explorer, el proyecto de aplicación UWP de Hola de menú contextual, haga clic en **almacén** > **asociar aplicación con hello almacén...** .

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. En el Asistente de hello, haga clic en **siguiente**, inicie sesión con su cuenta de Microsoft, escriba un nombre para la aplicación en **reservar un nuevo nombre de aplicación**, a continuación, haga clic en **reserva**.
3. Después de registro de una aplicación Hola es Hola se creó correctamente, seleccione Nuevo nombre de aplicación, haga clic en **siguiente**y, a continuación, haga clic en **asociar**. Esto agrega manifiesto de aplicación Hola necesario tienda Windows registro información toohello.  
4. Navegue toohello [centro de desarrollo de Windows](https://dev.windows.com/en-us/overview), iniciar sesión con tu cuenta de Microsoft, haga clic en nuevo registro de aplicación hello en **mis aplicaciones**, a continuación, expanda **servicios**  >  **Notificaciones de inserción**.
5. Hola **notificaciones de inserción** página, haga clic en **sitio de los servicios de Live** en **servicios móviles de Microsoft Azure**.
6. En la página de registro de hello, tome nota del valor de hello en **secretos de aplicación** hello y **SID del paquete**, que a continuación utilizará tooconfigure su aplicación móvil de back-end.

    ![Asociar aplicación con la Tienda Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > secreto de cliente de Hola y el SID del paquete son credenciales de seguridad importantes. No los comparta con nadie ni los distribuya con su aplicación. Hola **Id. de aplicación** se utiliza con la autenticación de Microsoft Account de hello tooconfigure secreto.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Configurar notificaciones de inserción de hello back-end toosend
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Actualizar notificaciones de inserción de hello server toosend
Utilice Hola procedimiento siguiente que corresponda al tipo de proyecto de back-end&mdash;cualquier [back-end de .NET](#dotnet) o [Node.js back-end](#nodejs).

### <a name="dotnet"></a>Proyecto de back-end de .NET
1. En Visual Studio, haga clic en proyecto de servidor de Hola y haga clic en **administrar paquetes de NuGet**, busque Microsoft.Azure.NotificationHubs, a continuación, haga clic en **instalar**. Esto instala la biblioteca de cliente de hello centros de notificaciones.
2. Expanda **controladores**, abra TodoItemController.cs y agregue Hola siguientes instrucciones using:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. Hola **PostTodoItem** método, agregar Hola siguiente código después de la llamada de hello demasiado**InsertAsync**:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Este código indica una notificación de inserción de toosend de concentrador de notificación de Hola después de un nuevo elemento de inserción.
4. Volver a publicar el proyecto de servidor de Hola.

### <a name="nodejs"></a>Proyecto de back-end de Node.js
1. Si ya no lo ha hecho, [Descargar proyecto de inicio rápido de hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) o persona use hello [editor en línea en el portal de Azure hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Reemplace el código existente en archivo de hello todoitem.js de Hola por hello siguiente:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    Este modo envía una notificación de WNS que contiene hello item.text Cuando se inserta un nuevo elemento de lista de tareas.
3. Al editar el archivo hello en el equipo local, volver a publicar el proyecto de servidor de Hola.

## <a id="update-app"></a>Agregar aplicación de tooyour de notificaciones de inserción
Después, debe registrarse la aplicación para recibir notificaciones push en el inicio. Si ya se ha habilitado la autenticación, asegúrese de que ese Hola usuario inicia sesión antes de intentar tooregister para las notificaciones de inserción.

1. Abra hello **App.xaml.cs** archivo de proyecto y agregue el siguiente de hello `using` instrucciones:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. En Hola el mismo archivo, agregue la siguiente hello **InitNotificationsAsync** toohello de definición de método **aplicación** clase:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Este código recupera hello URI del canal para la aplicación hello de WNS y, a continuación, registra ese URI del canal con la aplicación de servicio de aplicaciones móviles.
3. En parte superior de Hola de hello **OnLaunched** controlador de eventos de **App.xaml.cs**, agregar hello **async** definición de método de modificador toohello y agregue el siguiente de hello llamada toohello nueva  **InitNotificationsAsync** método, como en el siguiente ejemplo de Hola:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Esto garantiza que hello que channeluri de corta duración se registra cada vez que se inicia la aplicación hello.
4. Recompile el proyecto de aplicación para UWP. La aplicación ya está listo tooreceive recibir notificaciones del sistema.

## <a id="test"></a>Prueba de las notificaciones de inserción en su aplicación
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Pasos siguientes
Más información sobre las notificaciones de inserción:

* [Cómo toouse Hola administra a cliente para aplicaciones móviles de Azure](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Plantillas de proporcionan inserciones de flexibilidad toosend multiplataforma e inserciones localizados. Obtenga información acerca de cómo tooregister plantillas.
* [Diagnosticar problemas de notificaciones push](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  : existen varias razones para que las notificaciones se pierdan o no lleguen a los dispositivos. Este tema muestra cómo hacer que tooanalyze y averiguar la raíz de Hola de errores de notificación de inserción.

Considere la posibilidad de continuar en tooone de hello tutoriales:

* [Agregar aplicación de autenticación tooyour](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.
* [Habilitación de la sincronización sin conexión para su aplicación](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Obtenga información acerca de cómo tooadd sin conexión son compatibles con la aplicación con un aplicación móvil de back-end. Sincronización sin conexión permite a los usuarios finales toointeract con una aplicación móvil&mdash;ver, agregar o modificar datos&mdash;incluso cuando no hay ninguna conexión de red.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
