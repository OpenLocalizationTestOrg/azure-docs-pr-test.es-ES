---
title: aaaGet Started with Azure Mobile Engagement para iOS en Swift | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para aplicaciones iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Introducción a Azure Mobile Engagement para aplicaciones iOS en Swift
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción tooan iOS aplicación de notificaciones toosegmented a los usuarios.
En este tutorial, puede crear una aplicación iOS vacía que recopile datos básicos y reciba notificaciones push mediante el sistema de notificaciones push de Apple (APN).

Este tutorial requiere siguiente de hello:

* XCode 8, que se puede instalar desde la tienda de aplicaciones para Mac
* Hola [Mobile Engagement SDK para iOS]
* Certificado de notificaciones push (.p12), que puede obtener en el centro de desarrolladores de Apple.

> [!NOTE]
> En este tutorial se usa Swift, versión 3.0. 
> 
> 

Completar este tutorial es un requisito previo para todos los tutoriales de Mobile Engagement para aplicaciones iOS.

> [!NOTE]
> toocomplete este tutorial, debe tener una cuenta activa de Azure. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement
Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción. Encontrará documentación de integración completa de Hola Hola [integración de SDK de Mobile Engagement iOS](mobile-engagement-ios-sdk-overview.md)

Se creará una aplicación básica con la integración de hello toodemonstrate XCode:

### <a name="create-a-new-ios-project"></a>Creación de un nuevo proyecto iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar el backend de interacción de tooMobile de aplicación
1. Descargar hello [Mobile Engagement SDK para iOS]
2. Extraer Hola. tar.gz carpeta de tooa de archivo en el equipo
3. Haga clic en proyecto de Hola y seleccione "Agregar archivos demasiado..."
   
    ![][1]
4. Desplazarse por las carpetas de toohello en la que extrajo Hola SDK y seleccione Hola `EngagementSDK` carpeta, a continuación, haga clic en Aceptar.
   
    ![][2]
5. Abra hello `Build Phases` ficha y Hola `Link Binary With Libraries` menú Agregar marcos Hola tal y como se muestra a continuación:
   
    ![][3]
6. Para crear un protocolo de puente del encabezado toobe toouse capaz de hello del objetivo C API del SDK, seleccione Archivo > Nuevo > Archivo > iOS > origen > archivo de encabezado.
   
    ![][4]
7. Editar archivo encabezado tooyour tooexpose Mobile Engagement Objective-C código Swift código de puente de hello, agregue Hola siguientes importaciones:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. En la configuración de compilación, asegúrese de que el encabezado de protocolo de puente Objective-C de compilación en el compilador de Swift: generación de código de hello tiene un encabezado de toothis de ruta de acceso. Este es un ejemplo de ruta de acceso: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (dependiendo de la ruta de acceso de hello)**
   
   ![][6]
9. Volver atrás toohello portal de Azure en la aplicación *información de conexión* página y copiar Hola cadena de conexión
   
   ![][5]
10. Ahora pega cadena de conexión de Hola Hola `didFinishLaunchingWithOptions` delegar
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Habilitar supervisión en tiempo real
En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).

1. Abra hello **ViewController.swift** archivo y reemplace la clase base hello de **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitación de las notificaciones de inserción y mensajería en la aplicación
Mobile Engagement le permite toointeract y alcance con los usuarios con las notificaciones de inserción y mensajería en la aplicación en el contexto de Hola de campañas. Este módulo se denomina alcance en el portal de interacción móvil Hola.
Hello las secciones siguientes se configurará la aplicación tooreceive ellos.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Habilitar la tooreceive aplicación silenciosa de las notificaciones de inserción
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Agregar proyecto de hello alcance de la biblioteca tooyour
1. Haga clic con el botón derecho del mouse en el proyecto.
2. Seleccionar `Add file too...`
3. Desplazarse por las carpetas de toohello en la que extrajo Hola SDK
4. Seleccione hello `EngagementReach` carpeta
5. Haga clic en Agregar
6. Editar hello tooexpose Mobile Engagement Objective-C alcanzar encabezados de archivo de encabezado de protocolo de puente y agregue Hola siguientes importaciones:
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a>Modifique su delegado de la aplicación
1. Hola interior `didFinishLaunchingWithOptions` : crear un módulo de reach y pasar tooyour línea de inicialización de contratación existente:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Habilitar la tooreceive de la aplicación notificaciones de inserción de APNS
1. Agregar Hola después línea toohello `didFinishLaunchingWithOptions` método:
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. Agregar hello `didRegisterForRemoteNotificationsWithDeviceToken` método tal como se indica a continuación:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Agregar hello `didReceiveRemoteNotification:fetchCompletionHandler:` método tal como se indica a continuación:
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement SDK para iOS]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
