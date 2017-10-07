---
title: aaaGet Started with Azure Mobile Engagement para Xamarin.iOS
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción para las aplicaciones de Xamarin.iOS y análisis."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Introducción a Azure Mobile Engagement para aplicaciones Xamarin.iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción a los usuarios de las notificaciones toosegmented en una aplicación de Xamarin.iOS.
En este tutorial, puede crear una aplicación Xamarin.iOS vacía que recopile datos básicos y reciba notificaciones push mediante el Sistema de notificaciones push de Apple (APNS).

> [!NOTE]
> servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible. Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requiere siguiente de hello:

* [Xamarin Studio](http://xamarin.com/studio). También puede utilizar Visual Studio con Xamarin, pero en este tutorial se usa Xamarin Studio. Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx)para obtener instrucciones. 
* [SDK de Mobile Engagement Xamarin](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "integración básica de" hello mínimo establecido toocollect requiere datos y enviar una notificación de inserción.

Se creará una aplicación básica con la integración de hello toodemonstrate de Xamarin:

### <a name="create-a-new-xamarinios-project"></a>Creación de un nuevo proyecto de Xamarin.iOS
1. Inicie Xamarin Studio. Vaya demasiado**archivo** -> **New** -> **solución** 
   
    ![][1]
2. Seleccione **ver solo la aplicación**, asegúrese de que el idioma Hola seleccionado es **C#** y, a continuación, haga clic en **siguiente**.
   
    ![][2]
3. Rellene hello **nombre de la aplicación** hello y **identificador de la organización** y, a continuación, haga clic en **siguiente**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Asegúrese de que ese Hola finalmente use toodeploy que su aplicación iOS está usando un identificador de aplicación que coincida con exactamente con hello aquí tiene el identificador de paquete de perfil de publicación. 
   > 
   > 
4. Hola de actualización **nombre del proyecto**, **nombre de la solución** y **ubicación** si es necesario y haga clic en **crear**.
   
    ![][4]

Xamarin Studio creará la aplicación de demostración de hello en el que se integrará Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar el backend de interacción de tooMobile de aplicación
1. Haga clic en hello **paquetes** carpeta de windows de la solución de Hola y seleccione **agregar paquetes...**
   
    ![][5]
2. Busque hello **Xamarin SDK de Microsoft Azure Mobile Engagement** y agregar soluciones tooyour.  
   
    ![][6]
3. Abra **AppDelegate.cs** y agregue Hola siguiente instrucción using:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. Hola **FinishedLaunching** método, agregue Hola después de la conexión de hello tooinitialize con Mobile Engagement back-end. Asegúrese de que tooadd su **ConnectionString**. Este código también usa un ficticia **NotificationIcon** que se agrega de forma Hola SDK de Mobile Engagement que puede que desee tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Habilitar supervisión en tiempo real
En orden toostart enviando los datos y asegurarse de que los usuarios de hello están activos, debe enviar al menos una pantalla toohello Mobile Engagement back-end.

1. Abra **ViewController.cs** y agregue Hola siguiente instrucción using:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Reemplace la clase hello desde el que `ViewController` hereda de `UIViewController` demasiado`EngagementViewController`. 

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación
Mobile Engagement le permite toointeract con los usuarios y alcance con notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hello las secciones siguientes configure su aplicación tooreceive ellos.

### <a name="modify-your-application-delegate"></a>Modifique su delegado de la aplicación
1. Hola abierto **AppDelegate.cs** y agregue Hola siguiente instrucción using:
   
        using System; 
2. Ahora dentro de hello `FinishedLaunching` método hello después tooregister para los mensajes de inserción después de agregar`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Por último - actualizar o agregar Hola siguientes métodos:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. En su **Info.plist** de archivos de solución de hello, confirme que hello **identificador de paquete** coincide con hello **Id. de aplicación** tiene en su perfil de aprovisionamiento en hello Dev de Apple Centro. 
   
    ![][7]
5. En Hola mismo **Info.plist** de archivos, asegúrese de que ha activado hello **habilitar modos en segundo plano** y **notificaciones remoto**. 
   
     ![][8]
6. Ejecutar la aplicación hello en dispositivo Hola que se ha asociado con este perfil de publicación. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
