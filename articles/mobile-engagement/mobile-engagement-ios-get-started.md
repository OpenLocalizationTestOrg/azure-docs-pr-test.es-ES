---
title: aaaGet Started with Azure Mobile Engagement para iOS en Objective C | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement a las notificaciones de inserción y de análisis para aplicaciones de iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Introducción a Azure Mobile Engagement para aplicaciones iOS en Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción tooan iOS aplicación de notificaciones toosegmented a los usuarios.
En este tutorial, puede crear una aplicación iOS vacía que recopile datos básicos y reciba notificaciones push mediante el sistema de notificaciones push de Apple (APN).

Este tutorial requiere siguiente de hello:

* XCode 8, que se puede instalar desde la tienda de aplicaciones para Mac
* Hola [Mobile Engagement SDK para iOS]

Completar este tutorial es un requisito previo para todos los tutoriales de Mobile Engagement para aplicaciones iOS.

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción. Encontrará documentación de integración completa de Hola Hola [integración de SDK de Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)

Se creará una aplicación básica con la integración de XCode toodemonstrate Hola.

### <a name="create-a-new-ios-project"></a>Creación de un nuevo proyecto iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Conectar el back-end de aplicación toohello Mobile Engagement
1. Descargar hello [Mobile Engagement SDK para iOS].
2. Extraer Hola. tar.gz carpeta de tooa de archivo en el equipo.
3. Haga clic en proyecto de hello y, a continuación, seleccione **agrega archivos a**.

    ![][1]
4. Desplazarse por las carpetas de toohello en la que extrajo Hola SDK, seleccione hello `EngagementSDK` carpeta, haga clic en **opciones** Hola esquina inferior izquierda y asegúrese de que esa casilla hello **copiar elementos si es necesario** hello y casilla de verificación para el destino se comprueban a continuación, presione **Aceptar**.

    ![][2]
5. Hola abierto **fases de compilación** ficha y en hello **binario con las bibliotecas de vínculos** menú, agregue marcos de hello tal y como se muestra a continuación:

    ![][3]
6. Volver atrás toohello portal de Azure en la aplicación **información de conexión** página y copiar la cadena de conexión Hola.

    ![][4]
7. Agregar Hola después de la línea de código en su **AppDelegate.m** archivo.

        #import "EngagementAgent.h"
8. Ahora pega cadena de conexión de Hola Hola `didFinishLaunchingWithOptions` delegar.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`es una instrucción opcional que permite los registros SDK que tooidentify problemas.

## <a id="monitor"></a>Habilitación de la supervisión en tiempo real
En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).

1. Abra hello **ViewController.h** archivo e importar **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Ahora reemplace superclase Hola de hello **ViewController** interfaz por `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación
Mobile Engagement le permite toointeract con los usuarios y alcance con notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hello las secciones siguientes configure su aplicación tooreceive ellos.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Habilitar la tooreceive aplicación silenciosa de las notificaciones de inserción
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Agregar proyecto de hello alcance de la biblioteca tooyour
1. Haga clic con el botón derecho en el proyecto.
2. Seleccione **Agregar archivo a**.
3. Desplazarse por las carpetas de toohello en la que extrajo Hola SDK.
4. Seleccione hello `EngagementReach` carpeta.
5. Haga clic en **Agregar**.

### <a name="modify-your-application-delegate"></a>Modifique su delegado de la aplicación
1. En **AppDeletegate.m** de archivos, importe el módulo de llegar a la interacción de Hola.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. Hola interior `application:didFinishLaunchingWithOptions` método, cree un módulo de Reach y páselo tooyour línea de inicialización de contratación existente:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Habilitar la tooreceive de la aplicación notificaciones de inserción de APNS
1. Agregar Hola después línea toohello `application:didFinishLaunchingWithOptions` método:

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. Agregar hello `application:didRegisterForRemoteNotificationsWithDeviceToken` método tal como se indica a continuación:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Agregar hello `didFailToRegisterForRemoteNotificationsWithError` método tal como se indica a continuación:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Agregar hello `didReceiveRemoteNotification:fetchCompletionHandler` método tal como se indica a continuación:

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement SDK para iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
