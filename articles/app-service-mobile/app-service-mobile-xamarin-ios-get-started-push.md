---
title: "aplicación Xamarin.iOS tooyour de notificaciones de inserción de aaaAdd con el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo toosend de servicio de aplicaciones de Azure toouse push notificaciones tooyour Xamarin.iOS aplicación"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Agregar tooyour de notificaciones de inserción Xamarin.iOS App
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Información general
En este tutorial, agregará toohello de notificaciones de inserción [inicio rápido de Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) del proyecto para que se envía una notificación de inserción toohello dispositivo cada vez que se inserta un registro.

Si no usa Hola descarga el proyecto de servidor de inicio rápido, se necesita Hola paquete de extensión de notificación de inserción. Vea [trabajar con el servidor back-end de .NET Hola SDK para aplicaciones móviles de Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) para obtener más información.

## <a name="prerequisites"></a>Requisitos previos
* Hola completa [inicio rápido de Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) tutorial.
* Un dispositivo iOS físico. Notificaciones de inserción no son compatibles con el simulador de iOS de Hola.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Registrar la aplicación hello las notificaciones de inserción en el portal para desarrolladores de Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Configurar las notificaciones de inserción de toosend de aplicación móvil
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Actualizar notificaciones de inserción de hello servidor proyecto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Configuración del proyecto de Xamarin.iOS
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Agregar aplicación de tooyour de notificaciones de inserción
1. En **QSTodoService**, agregar Hola después de propiedad para que **AppDelegate** puede adquirir el cliente móvil hello:
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Agregue Hola siguiente `using` arriba toohello de instrucción de hello **AppDelegate.cs** archivo.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. En **AppDelegate**, invalidar hello **FinishedLaunching** eventos:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. En Hola el mismo archivo, invalide hello **RegisteredForRemoteNotifications** eventos. En este código está registrando para una notificación de plantilla simple que se enviarán a través de todas las plataformas admitidas por el servidor de Hola.
   
    Para más información sobre las plantillas con centros de notificaciones, vea [Plantillas](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. A continuación, invalidar hello **DidReceivedRemoteNotification** eventos:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

La aplicación ya está actualizado toosupport notificaciones de inserción.

## <a name="test"></a>Prueba de las notificaciones push en su aplicación
1. Hola presione **ejecutar** toobuild proyecto de Hola e Iniciar aplicación hello en un dispositivo compatible con iOS, a continuación, haga clic en **Aceptar** tooaccept notificaciones de inserción.
   
   > [!NOTE]
   > Debe aceptar de forma explícita las notificaciones push desde su aplicación. Esta solicitud sólo produce a Hola primera vez que Hola se ejecuta la aplicación.
   > 
   > 
2. En la aplicación hello, escriba una tarea y, a continuación, haga clic en hello signo más (**+**) icono.
3. Compruebe que se recibe una notificación, y haga clic en **Aceptar** toodismiss Hola notificación.
4. Repita el paso 2 y cierre inmediatamente Hola aplicación, a continuación, compruebe que aparece una notificación.

Ha completado correctamente este tutorial.

<!-- Images. -->

<!-- URLs. -->



