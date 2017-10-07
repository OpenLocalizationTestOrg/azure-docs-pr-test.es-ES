---
title: "aaaAzure integración con el SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>¿Cómo tooIntegrate interacción en iOS
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Este procedimiento describe las funciones en la aplicación de iOS de supervisión y análisis hello más sencilla forma tooactivate Engagement.

Hola Engagement SDK requiere iOS7 + y Xcode 8 y versiones posteriores: destino de implementación de saludo de la aplicación debe tener al menos iOS 7.

> [!NOTE]
> Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Hay un problema conocido en el módulo de Reach Hola de esta versión anterior mientras se ejecuta en dispositivos de iOS 10, vea [Hola alcance de la integración de los módulos](mobile-engagement-ios-integrate-engagement-reach.md) para obtener más detalles. Si elige toouse Hola SDK v3.2.4, omitir hello `UserNotifications.framework` importar en el paso siguiente de saludo.
>
>

Hola pasos es que toocompute necesita un suficiente informe de hello tooactivate de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals. Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación iOS](mobile-engagement-ios-use-engagement-api.md) desde estas estadísticas son dependientes de la aplicación.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Incrustar Hola Engagement SDK en el proyecto de iOS
* Descargar el SDK de iOS de Hola de [aquí](http://aka.ms/qk2rnj).
* Proyecto de complemento Hola Engagement SDK tooyour iOS: en Xcode, haga clic en el proyecto y seleccione **"Agregar archivos demasiado..."** y elija hello `EngagementSDK` carpeta.
* Interacción requiere toowork marcos adicionales: en el Explorador de proyectos hello, abra el panel de proyecto y seleccione Hola destino correcto. A continuación, abra hello **"Fases de compilación"** ficha y Hola **"Binario con bibliotecas de vínculos"** menú, agregue estos marcos de trabajo:

  * `UserNotifications.framework`-establecer Hola vínculo como`Optional`
  * `AdSupport.framework`-establecer Hola vínculo como`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> el marco de trabajo de Hello AdSupport puede quitarse. Interacción necesita este Hola de toocollect IDFA de framework. Sin embargo, se puede deshabilitar la recopilación de IDFA \<ios-sdk-contratación-idfa\> toocomply con nueva directiva de Apple Hola con respecto a este identificador.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Inicializar Hola Engagement SDK
Debe toomodify el delegado de la aplicación:

* Hola parte superior de su archivo de implementación, importe el agente de interacción de hello:

      [...]
      #import "EngagementAgent.h"
* Inicializar interacción dentro de método hello '**applicationDidFinishLaunching:**'o'**application: didFinishLaunchingWithOptions:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Informes básicos
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Método recomendado: sobrecargar las clases `UIViewController`
Informe de hello order tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, basta con hacer que todos los su `UIViewController` subclases heredan de hello `EngagementViewController` clases (misma regla para `UITableViewController`  - \> `EngagementTableViewController`).

**Sin Engagement:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Con Engagement:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Método alternativo: llamar a `startActivity()` manualmente
Si no puede o no desea que toooverload su `UIViewController` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent`de métodos directamente.

> [!IMPORTANT]
> SDK de iOS de Hello llama automáticamente a hello `endActivity()` método cuando se cierra la aplicación hello. Por lo tanto, es *alta* recomienda hello toocall `startActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado*nunca* llamada hello `endActivity` método, desde la llamada a este método obliga a Hola toobe de sesión actual ha finalizado.
>
>

## <a name="location-reporting"></a>Informes de ubicación
Condiciones de Apple del servicio no permitir que las aplicaciones seguimiento solo con fines de estadísticas de la ubicación de toouse. Por lo tanto, se recomienda tooenable ubicación informes solo si la aplicación también usa el seguimiento por algún otro motivo de la ubicación de Hola.

A partir de iOS 8, debe proporcionar una descripción de cómo su aplicación usa los servicios de ubicación mediante el establecimiento de una cadena de clave de hello [NSLocationWhenInUseUsageDescription] o [NSLocationAlwaysUsageDescription]en el archivo Info.plist de la aplicación. Si desea que la ubicación tooreport en segundo plano de hello con interacción, Agregar clave de hello NSLocationAlwaysUsageDescription. En todos los demás casos, Agregar clave de hello NSLocationWhenInUseUsageDescription. Tenga en cuenta que debe NSLocationAlwaysAndWhenInUseUsageDescription y NSLocationWhenInUseUsageDescription la ubicación de fondo tooreport en iOS 11.

### <a name="lazy-area-location-reporting"></a>Informes de ubicaciones de áreas diferidas
Informes de ubicación de área lenta permiten país de hello tooreport, región y localidad asociado toodevices. Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI). área de dispositivo de Hola se notifica como máximo una vez por sesión. Hello GPS nunca se utiliza, y, por tanto, este tipo de informe de ubicación tiene muy pocas (no toosay ningún) impacto en la batería de Hola.

Áreas notificadas son toocompute usado geográfica estadísticas acerca de los usuarios, sesiones, eventos y errores. También se pueden usar como criterios en campañas de cobertura. Hola última conocida área notificada para un dispositivo puede ser recuperada gracias toohello [API de dispositivo].

ubicación de área lenta tooenable informes, agregue Hola después de línea después de inicializar el agente de interacción de hello:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Informes de ubicación en tiempo real
Informes de ubicación en tiempo real permiten asociada de latitud y tooreport hello toodevices. De forma predeterminada, este tipo de informes de ubicación sólo usa ubicaciones de red (basadas en el identificador de la celda o Wi-Fi) y reporting Hola solo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión).

Ubicaciones de tiempo real son *no* utiliza las estadísticas de toocompute. Su único propósito es el uso de Hola de tooallow de barrera geográfica en tiempo real \<perímetro de audiencia de Reach\> criterio de campañas.

ubicación en tiempo real de tooenable informes, agregue Hola después de línea después de inicializar el agente de interacción de hello:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>Informes basados en GPS
De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red. uso de Hola de tooenable de GPS basada en ubicaciones (que son mucho más precisas), agregue:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Informes en segundo plano
De forma predeterminada, el informes de ubicación en tiempo real sólo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión). Hola tooenable informes también en segundo plano, agregue:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Cuando la aplicación hello se ejecuta en segundo plano, se notifican únicas ubicaciones a basados en red, incluso si ha habilitado Hola GPS.
>
>

Implementación de esta función llamará [startMonitoringSignificantLocationChanges] cuando la aplicación entra en segundo plano de Hola. Tenga en cuenta que le automáticamente vuelva a iniciar la aplicación en segundo plano de hello si llega un nuevo evento de ubicación.

## <a name="advanced-reporting"></a>Informes avanzados
Opcionalmente, si desea eventos específicos de aplicación tooreport, errores y trabajos, debe toouse Hola API de interacción a través de métodos de Hola de hello `EngagementAgent` clase. Se puede recuperar un objeto de esta clase que realiza la llamada hello `[EngagementAgent shared]` método estático.

permite todas las capacidades avanzadas de contratación toouse Hello API de contratación y se detalla cómo Hola tooUse la API de interacción en iOS (así como en la documentación técnica de Hola de hello `EngagementAgent` clase).

## <a name="disable-idfa-collection"></a>Deshabilitación de la recopilación de IDFA
De forma predeterminada, Engagement usará hello [IDFA] toouniquely identificar a un usuario. Pero si no usas publicidad en otra parte de la aplicación hello, puede ser rechazados por hello proceso de revisión de la tienda de aplicaciones. Recopilación de IDFA se puede deshabilitar mediante la adición de macro de preprocesador hello `ENGAGEMENT_DISABLE_IDFA` en el archivo de encabezado precompilado (o en hello `Build Settings` de la aplicación). Así se asegurará de que no hay ninguna referencia demasiado`ASIdentifierManager`, `advertisingIdentifier` o `isAdvertisingTrackingEnabled` en la compilación de la aplicación hello.

Integración en hello **prefix.pch** archivo:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Puede comprobar que recopilación de IDFA Hola correctamente está deshabilitado en la aplicación mediante la comprobación de los registros de pruebas de interacción de Hola. Vea Hola pruebas de integración de\<ios sdk interacción prueba idfa\> documentación para obtener más información.

## <a name="disable-log-reporting"></a>Deshabilitación de los informes de registro
### <a name="using-a-method-call"></a>Mediante una llamada al método
Si desea enviar registros de toostop de interacción, puede llamar:

    [[EngagementAgent shared] setEnabled:NO];

Esta llamada es persistente: usa `NSUserDefaults` información de hello toostore.

Puede habilitar el registro de reporting nuevo mediante una llamada a Hola la misma función con `YES`.

### <a name="integration-in-your-settings-bundle"></a>Integración en la agrupación de configuraciones
En lugar de llamar a esta función, también puede integrar esta configuración directamente en el archivo `Settings.bundle` existente. Hola cadena `engagement_agent_enabled` debe usarse como un identificador de preferencias de Hola y debe ser modificador para alternar tooa asociado (`PSToggleSwitchSpecifier`).

Hola siguiendo el ejemplo de `Settings.bundle` muestra cómo tooimplement:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[API de dispositivo]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
