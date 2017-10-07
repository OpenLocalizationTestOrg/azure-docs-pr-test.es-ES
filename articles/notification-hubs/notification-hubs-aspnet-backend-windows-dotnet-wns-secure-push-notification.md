---
title: "aaaAzure notificación concentradores seguros Push"
description: "Obtenga información acerca de cómo toosend segura las notificaciones de inserción en Azure. Ejemplos de código escritos en C# mediante Hola .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Inserción segura de los Centros de notificaciones de Azure
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Información general
Compatibilidad con notificaciones de inserción de Microsoft Azure le permite tooaccess una infraestructura de inserción fácil de usar, varias plataformas y escala horizontal, que simplifica considerablemente la implementación de Hola de notificaciones de inserción para las aplicaciones de consumidor y empresa para dispositivos móviles plataformas.

A veces debido a restricciones de seguridad o tooregulatory, una aplicación podría querer tooinclude algo en la notificación de Hola que no se transmiten a través de la infraestructura de notificaciones de inserción estándar Hola. Este tutorial describe cómo tooachieve Hola misma experiencia mediante el envío de información confidencial a través de una conexión segura autenticada entre el dispositivo de cliente de Hola y Hola backend de la aplicación.

En un nivel alto, flujo de hello es como sigue:

1. Hola aplicación back-end:
   * Almacena la carga segura en la base de datos back-end.
   * Envía el Id. de Hola de este dispositivo de toohello de notificación (se envía ninguna información segura).
2. aplicación Hello en dispositivo hello, al recibir la notificación de hello:
   * dispositivo de Hello contacta con hello back-end que lo solicita Hola carga de seguridad.
   * aplicación Hello puede mostrar carga hello como una notificación en el dispositivo de Hola.

Es importante toonote que Hola anterior flujo (y en este tutorial), se da por supuesto ese dispositivo Hola almacena un token de autenticación en el almacenamiento local, después de hello usuario inicia sesión en. Esto garantiza una experiencia completamente sin problemas, como dispositivo de hello puede recuperar la carga de seguridad de la notificación de hello con este token. Si la aplicación no almacena tokens de autenticación en el dispositivo de hello, o si pueden haber expirado estos tokens, hello del dispositivo, tras recibir la notificación de Hola debe mostrar una notificación genérica preguntar aplicación Hola de hello usuario toolaunch. aplicación Hello, a continuación, autentica el usuario de Hola y muestra la carga de notificaciones de Hola.

Este tutorial de inserción seguros se muestra cómo toosend una notificación de inserción de forma segura. tutorial de Hola se basa en hello [informar a los usuarios](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, por lo que debe completar los pasos de hello en ese tutorial primero.

> [!NOTE]
> En este tutorial se supone que ha creado y configurado el centro de notificaciones tal como se describe en [Introducción a los Centros de notificaciones (Tienda Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Asimismo, tenga en cuenta que Windows Phone 8.1 requiere credenciales de Windows (no de Windows Phone) y que las tareas en segundo plano no funcionan en Windows Phone 8.0 o Silverlight 8.1. Para las aplicaciones de la tienda Windows, puede recibir notificaciones a través de una tarea en segundo plano únicamente si la aplicación hello está habilitada la pantalla de bloqueo (haga clic en la casilla de verificación de Hola Hola Appmanifest).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Modificar Hola proyecto de Windows Phone
1. Hola **NotifyUserWindowsPhone** proyecto de equipo y agregar Hola después de la tarea en segundo plano código tooApp.xaml.cs tooregister Hola inserción. Agregar Hola después de la línea de código al final de Hola de hello `OnLaunched()` método:
   
        RegisterBackgroundTask();
2. Todavía en App.xaml.cs, agregue Hola siguiente código inmediatamente después de hello `OnLaunched()` método:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Agregue los siguiente hello `using` instrucciones en parte superior de hello del archivo de hello App.xaml.cs:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. De hello **archivo** menú en Visual Studio, haga clic en **guardar todo**.

## <a name="create-hello-push-background-component"></a>Crear hello Push componente en segundo plano
Hola siguiente paso es el componente de segundo plano de inserción de toocreate Hola.

1. En el Explorador de soluciones, haga clic en el nodo de nivel superior de Hola de solución de Hola (**SecurePush de solución** en este caso), a continuación, haga clic en **agregar**, a continuación, haga clic en **nuevo proyecto**.
2. Expanda **Aplicaciones de la Tienda**, haga clic en **Aplicaciones de Windows Phone** y, después, en **Componente de Windows Runtime (Windows Phone)**. Proyecto de hello Name **PushBackgroundComponent**y, a continuación, haga clic en **Aceptar** proyecto de hello toocreate.
   
    ![][12]
3. En el Explorador de soluciones, haga clic en hello **PushBackgroundComponent (Windows Phone 8.1)** proyecto, a continuación, haga clic en **agregar**, a continuación, haga clic en **clase**. Hola nueva clase el nombre **PushBackgroundTask.cs**. Haga clic en **agregar** clase de hello toogenerate.
4. Reemplace todo contenido de Hola de hello **PushBackgroundComponent** definición de espacio de nombres con hello siguiente código, sustituyendo el marcador de posición de hello `{back-end endpoint}` con punto de conexión de back-end de hello obtenido durante la implementación de su back-end:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. En el Explorador de soluciones, haga clic en hello **PushBackgroundComponent (Windows Phone 8.1)** del proyecto y, a continuación, haga clic en **administrar paquetes de NuGet**.
6. En el lado izquierdo de hello, haga clic en **Online**.
7. Hola **búsqueda** , escriba **cliente Http**.
8. En la lista de resultados de hello, haga clic en **Microsoft HTTP Client Libraries**y, a continuación, haga clic en **instalar**. Completar la instalación de Hola.
9. Nuevo en hello NuGet **búsqueda** , escriba **Json.net**. Instalar hello **Json.NET** paquete y, a continuación, ventana de administrador de paquetes de NuGet de hello cerrar.
10. Agregue los siguiente hello `using` las instrucciones en la parte superior de Hola de hello **PushBackgroundTask.cs** archivo:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. En el Explorador de soluciones, en hello **NotifyUserWindowsPhone (Windows Phone 8.1)** proyecto de equipo y haga clic en **referencias**, a continuación, haga clic en **Agregar referencia...** . Cuadro de diálogo Administrador de referencias de hello, casilla Hola junto demasiado**PushBackgroundComponent**y, a continuación, haga clic en **Aceptar**.
12. En el Explorador de soluciones, haga doble clic en **Package.appxmanifest** en hello **NotifyUserWindowsPhone (Windows Phone 8.1)** proyecto. En **notificaciones**, establezca **capaz de recibir** demasiado**Sí**.
    
    ![][3]
13. Todavía en **Package.appxmanifest**, haga clic en hello **declaraciones** menú cerca de la parte superior de Hola. Hola **declaraciones disponibles** de lista desplegable, haga clic en **tareas en segundo plano**y, a continuación, haga clic en **agregar**.
14. En **Package.appxmanifest**, en **Propiedades**, active **Notificación de inserción**.
15. En **Package.appxmanifest**, en **configuración de la aplicación**, tipo **PushBackgroundComponent.PushBackgroundTask** en hello **punto de entrada** campo.
    
    ![][13]
16. De hello **archivo** menú, haga clic en **guardar todo**.

## <a name="run-hello-application"></a>Ejecutar aplicación Hola
toorun Hola aplicación, Hola siguientes:

1. En Visual Studio, ejecute hello **AppBackend** aplicación de API Web. Se mostrará una página web ASP.NET.
2. En Visual Studio, ejecute hello **NotifyUserWindowsPhone (Windows Phone 8.1)** aplicación de Windows Phone. emulador de Windows Phone Hola se ejecuta y carga la aplicación hello automáticamente.
3. Hola **NotifyUserWindowsPhone** aplicación interfaz de usuario, escriba un nombre de usuario y una contraseña. Pueden ser cualquier cadena, pero deben ser Hola el mismo valor.
4. Hola **NotifyUserWindowsPhone** aplicación interfaz de usuario, haga clic en **iniciar sesión y registrar**. A continuación, haga clic en **Enviar inserción**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
