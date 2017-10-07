---
title: "información general del SDK de Mobile Engagement iOS aaaAzure | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>SDK de iOS para Azure Mobile Engagement
Iniciar todos los detalles de Hola de aquí tooget acerca de cómo toointegrate Azure Mobile Engagement en una aplicación de iOS. Si desea que toogive que un bloque try en primer lugar, asegúrese de que no nuestro [tutorial de 15 minutos](mobile-engagement-ios-get-started.md).

Haga clic en hello toosee [contenido de SDK](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Procedimientos de integración
1. Empiece aquí: [cómo toointegrate Mobile Engagement en la aplicación de iOS](mobile-engagement-ios-integrate-engagement.md)
2. Para las notificaciones: [cómo toointegrate alcance (notificaciones) en la aplicación de iOS](mobile-engagement-ios-integrate-engagement-reach.md)
3. Implementación del plan de etiqueta: [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación iOS](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Notas de la versión
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Se han corregido las notificaciones borradas en el fondo.
* Se han corregido las advertencias de XCode 9 sobre las API a las que no se llamaba en cola principal.
* Se ha corregido una fuga de memoria en los sondeos de cobertura.
* Se ha eliminado el soporte técnico para iOS 6.X. A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 7.

Para la versión anterior, consulte hello [completar notas de la versión](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Procedimientos de actualización
Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Puede tener a toofollow varios procedimientos si ejecutado varias versiones de hello SDK vea Hola completa [procedimientos de actualización de](mobile-engagement-ios-upgrade-procedure.md).

Para cada nueva versión de hello SDK debe reemplazar primero (quitar y volver a importar en xcode) Hola carpetas EngagementSDK y EngagementReach.

### <a name="from-300-too400"></a>Desde 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 es obligatorio a partir de la versión 4.0.0 de hello SDK.

> [!NOTE]
> Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Hay un problema conocido en el módulo de reach Hola de esta versión anterior mientras se ejecuta en dispositivos iOS 10: las notificaciones del sistema no están activadas. toofix esto tendrá tooimplement hello en desuso API `application:didReceiveRemoteNotification:` en la aplicación el delegado como sigue:
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **No se recomienda esta solución** ya que este comportamiento puede cambiar en la próxima actualización de la versión de iOS (por menor que sea) porque esta API de iOS está en desuso. Debería pasar tooXCode 8 tan pronto como sea posible.
>
>

#### <a name="usernotifications-framework"></a>Marco de UserNotifications
Necesita tooadd hello `UserNotifications` framework en fases de compilación.

en el Explorador de proyectos hello, abra el panel de proyecto y seleccione destino correcto Hola. A continuación, abra hello **"Fases de compilación"** ficha y Hola **"Binario con bibliotecas de vínculos"** menú, agregue framework `UserNotifications.framework` -establecer Hola vínculo como`Optional`

#### <a name="application-push-capability"></a>Funcionalidad de inserción de la aplicación
XCode 8 puede restablecer la aplicación capacidad de inserción, compruébela en hello `capability` ficha de su destino seleccionado.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Agregar código de registro de hello nueva iOS notificación 10
Hola anteriores código fragmento tooregister aplicación hello toonotifications todavía funciona, pero está usando en desuso API mientras se ejecuta en iOS 10.

Hola de importación `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>

En el método de delegado de aplicación `application:didFinishLaunchingWithOptions` reemplace:

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

por:

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolución de conflictos de delegado de UNUserNotificationCenter

*Si ni la aplicación ni una de las bibliotecas de terceros implementa `UNUserNotificationCenterDelegate`, puede pasar por alto esta parte.*

Un `UNUserNotificationCenter` delegado es utilizado por el ciclo de vida de hello SDK toomonitor Hola de notificaciones de interacción en dispositivos que ejecutan en iOS 10 o superior. Hola SDK tiene su propia implementación de hello `UNUserNotificationCenterDelegate` de protocolo, pero puede haber solo un `UNUserNotificationCenter` delegar por aplicación. Cualquier otro delegado agrega toohello `UNUserNotificationCenter` objeto entrarán en conflicto con hello interacción uno. Si Hola SDK detecta a delegado su o cualquier otro de terceros no usará su propio toogive de implementación, una posibilidad tooresolve Hola conflictos. Tendrá tooadd Hola interacción lógica tooyour posee conflictos de hello tooresolve de delegado en orden.

Hay dos tooachieve formas esto.

Propuesta 1, enviando el delegado llama toohello SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

O propuesta 2, heredando de hello `AEUserNotificationHandler` (clase)

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Puede determinar si una notificación pueden proceder de contratación o no pasando su `userInfo` diccionario toohello agente `isEngagementPushPayload:` método de la clase.

Asegúrese de que ese hello `UNUserNotificationCenter` delegado del objeto se establece el delegado tooyour dentro de cualquier hello `application:willFinishLaunchingWithOptions:` o hello `application:didFinishLaunchingWithOptions:` método de delegado de la aplicación.
Por ejemplo, si implementa Hola anteriormente propuesta 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
