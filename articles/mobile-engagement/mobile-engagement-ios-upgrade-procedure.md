---
title: "aaaAzure el procedimiento de actualización de SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procedimientos de actualización
Si ya ha integrado una versión anterior de interacción en la aplicación, tener hello tooconsider siguientes puntos al actualizar Hola SDK.

Para cada nueva versión de hello SDK debe reemplazar primero (quitar y volver a importar en xcode) Hola carpetas EngagementSDK y EngagementReach.

## <a name="from-300-too400"></a>Desde 3.0.0 too4.0.0
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

### <a name="usernotifications-framework"></a>Marco de UserNotifications
Necesita tooadd hello `UserNotifications` framework en fases de compilación.

en el Explorador de proyectos hello, abra el panel de proyecto y seleccione destino correcto Hola. A continuación, abra hello **"Fases de compilación"** ficha y Hola **"Binario con bibliotecas de vínculos"** menú, agregue framework `UserNotifications.framework` -establecer Hola vínculo como`Optional`

### <a name="application-push-capability"></a>Funcionalidad de inserción de la aplicación
XCode 8 puede restablecer la aplicación capacidad de inserción, compruébela en hello `capability` ficha de su destino seleccionado.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Agregar código de registro de hello nueva iOS notificación 10
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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Resolución de conflictos de delegado de UNUserNotificationCenter

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

## <a name="from-200-too300"></a>Desde 2.0.0 too3.0.0
Soporte de iOS 4.X eliminado. A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 6.

Si está utilizando el alcance de la aplicación, debe agregar `remote-notification` toohello valor `UIBackgroundModes` matriz en el archivo Info.plist en las notificaciones de orden tooreceive remoto.

Hola método `application:didReceiveRemoteNotification:` necesita toobe reemplazado por `application:didReceiveRemoteNotification:fetchCompletionHandler:` en el delegado de la aplicación.

"AEPushDelegate.h" está en desuso interfaz y necesita tooremove todas las referencias. Esto incluye la eliminación `[[EngagementAgent shared] setPushDelegate:self]` y Hola delegar métodos desde el delegado de la aplicación:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>De 1.16.0 too2.0.0
Hello siguiente describe cómo toomigrate una integración con el SDK de hello Capptain servicio ofrecido por Capptain SAS en una aplicación con la tecnología de Azure Mobile Engagement.
Si va a migrar desde una versión anterior, por favor, consulte hello Capptain sitio web toomigrate too1.16 en primer lugar, aplique Hola siguiendo el procedimiento.

> [!IMPORTANT]
> Capptain e interacción móvil no se Hola los mismos servicios y procedimiento Hola indicado a continuación sólo resalta cómo toomigrate Hola aplicación cliente. Migrar Hola SDK en la aplicación hello no migrará los datos de hello Capptain toohello Mobile Engagement servidores
> 
> 

### <a name="agent"></a>Agente
Hola método `registerApp:` se ha reemplazado por el nuevo método de hello `init:`. El delegado de la aplicación deben actualizarse como corresponda y usar una cadena de conexión:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

Seguimiento de SmartAd se ha quitado del SDK sólo tiene tooremove todas las instancias de `AETrackModule` (clase)

### <a name="class-name-changes"></a>Cambios del nombre de la clase
Como parte de la reconfiguración de marca de hello, hay par clase/de nombres de archivo que necesitan toobe cambiado.

Todas las clases precedidas de "CP" cambian su nombre introduciendo el prefijo "AE".

Ejemplo:

* `CPModule.h`se cambia el nombre demasiado`AEModule.h`.

Todas las clases con el prefijo "Capptain" cambian su nombre para introducir el prefijo "Engagement".

Ejemplos:

* Hola clase `CapptainAgent` se cambia el nombre demasiado`EngagementAgent`.
* Hola clase `CapptainTableViewController` se cambia el nombre demasiado`EngagementTableViewController`.
* Hola clase `CapptainUtils` se cambia el nombre demasiado`EngagementUtils`.
* Hola clase `CapptainViewController` se cambia el nombre demasiado`EngagementViewController`.

