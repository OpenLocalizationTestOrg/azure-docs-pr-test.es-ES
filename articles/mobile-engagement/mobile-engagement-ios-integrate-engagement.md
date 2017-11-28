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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="40471-103">¿Cómo tooIntegrate interacción en iOS</span><span class="sxs-lookup"><span data-stu-id="40471-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40471-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="40471-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="40471-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="40471-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="40471-106">iOS</span><span class="sxs-lookup"><span data-stu-id="40471-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="40471-107">Android</span><span class="sxs-lookup"><span data-stu-id="40471-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="40471-108">Este procedimiento describe las funciones en la aplicación de iOS de supervisión y análisis hello más sencilla forma tooactivate Engagement.</span><span class="sxs-lookup"><span data-stu-id="40471-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="40471-109">Hola Engagement SDK requiere iOS7 + y Xcode 8 y versiones posteriores: destino de implementación de saludo de la aplicación debe tener al menos iOS 7.</span><span class="sxs-lookup"><span data-stu-id="40471-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="40471-110">Si realmente dependen XCode 7, a continuación, puede usar hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="40471-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="40471-111">Hay un problema conocido en el módulo de Reach Hola de esta versión anterior mientras se ejecuta en dispositivos de iOS 10, vea [Hola alcance de la integración de los módulos](mobile-engagement-ios-integrate-engagement-reach.md) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="40471-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="40471-112">Si elige toouse Hola SDK v3.2.4, omitir hello `UserNotifications.framework` importar en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="40471-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="40471-113">Hola pasos es que toocompute necesita un suficiente informe de hello tooactivate de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals.</span><span class="sxs-lookup"><span data-stu-id="40471-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="40471-114">Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación iOS](mobile-engagement-ios-use-engagement-api.md) desde estas estadísticas son dependientes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40471-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="40471-115">Incrustar Hola Engagement SDK en el proyecto de iOS</span><span class="sxs-lookup"><span data-stu-id="40471-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="40471-116">Descargar el SDK de iOS de Hola de [aquí](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="40471-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="40471-117">Proyecto de complemento Hola Engagement SDK tooyour iOS: en Xcode, haga clic en el proyecto y seleccione **"Agregar archivos demasiado..."** y elija hello `EngagementSDK` carpeta.</span><span class="sxs-lookup"><span data-stu-id="40471-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="40471-118">Interacción requiere toowork marcos adicionales: en el Explorador de proyectos hello, abra el panel de proyecto y seleccione Hola destino correcto.</span><span class="sxs-lookup"><span data-stu-id="40471-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="40471-119">A continuación, abra hello **"Fases de compilación"** ficha y Hola **"Binario con bibliotecas de vínculos"** menú, agregue estos marcos de trabajo:</span><span class="sxs-lookup"><span data-stu-id="40471-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="40471-120">`UserNotifications.framework`-establecer Hola vínculo como`Optional`</span><span class="sxs-lookup"><span data-stu-id="40471-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="40471-121">`AdSupport.framework`-establecer Hola vínculo como`Optional`</span><span class="sxs-lookup"><span data-stu-id="40471-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="40471-122">el marco de trabajo de Hello AdSupport puede quitarse.</span><span class="sxs-lookup"><span data-stu-id="40471-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="40471-123">Interacción necesita este Hola de toocollect IDFA de framework.</span><span class="sxs-lookup"><span data-stu-id="40471-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="40471-124">Sin embargo, se puede deshabilitar la recopilación de IDFA \<ios-sdk-contratación-idfa\> toocomply con nueva directiva de Apple Hola con respecto a este identificador.</span><span class="sxs-lookup"><span data-stu-id="40471-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="40471-125">Inicializar Hola Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="40471-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="40471-126">Debe toomodify el delegado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="40471-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="40471-127">Hola parte superior de su archivo de implementación, importe el agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="40471-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="40471-128">Inicializar interacción dentro de método hello '**applicationDidFinishLaunching:**'o'**application: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="40471-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="40471-129">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="40471-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="40471-130">Método recomendado: sobrecargar las clases `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="40471-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="40471-131">Informe de hello order tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, basta con hacer que todos los su `UIViewController` subclases heredan de hello `EngagementViewController` clases (misma regla para `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="40471-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="40471-132">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="40471-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="40471-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="40471-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="40471-134">Método alternativo: llamar a `startActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="40471-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="40471-135">Si no puede o no desea que toooverload su `UIViewController` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent`de métodos directamente.</span><span class="sxs-lookup"><span data-stu-id="40471-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40471-136">SDK de iOS de Hello llama automáticamente a hello `endActivity()` método cuando se cierra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="40471-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="40471-137">Por lo tanto, es *alta* recomienda hello toocall `startActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado*nunca* llamada hello `endActivity` método, desde la llamada a este método obliga a Hola toobe de sesión actual ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="40471-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="40471-138">Informes de ubicación</span><span class="sxs-lookup"><span data-stu-id="40471-138">Location reporting</span></span>
<span data-ttu-id="40471-139">Condiciones de Apple del servicio no permitir que las aplicaciones seguimiento solo con fines de estadísticas de la ubicación de toouse.</span><span class="sxs-lookup"><span data-stu-id="40471-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="40471-140">Por lo tanto, se recomienda tooenable ubicación informes solo si la aplicación también usa el seguimiento por algún otro motivo de la ubicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="40471-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="40471-141">A partir de iOS 8, debe proporcionar una descripción de cómo su aplicación usa los servicios de ubicación mediante el establecimiento de una cadena de clave de hello [NSLocationWhenInUseUsageDescription] o [NSLocationAlwaysUsageDescription]en el archivo Info.plist de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40471-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="40471-142">Si desea que la ubicación tooreport en segundo plano de hello con interacción, Agregar clave de hello NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="40471-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="40471-143">En todos los demás casos, Agregar clave de hello NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="40471-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="40471-144">Tenga en cuenta que debe NSLocationAlwaysAndWhenInUseUsageDescription y NSLocationWhenInUseUsageDescription la ubicación de fondo tooreport en iOS 11.</span><span class="sxs-lookup"><span data-stu-id="40471-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="40471-145">Informes de ubicaciones de áreas diferidas</span><span class="sxs-lookup"><span data-stu-id="40471-145">Lazy area location reporting</span></span>
<span data-ttu-id="40471-146">Informes de ubicación de área lenta permiten país de hello tooreport, región y localidad asociado toodevices.</span><span class="sxs-lookup"><span data-stu-id="40471-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="40471-147">Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI).</span><span class="sxs-lookup"><span data-stu-id="40471-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="40471-148">área de dispositivo de Hola se notifica como máximo una vez por sesión.</span><span class="sxs-lookup"><span data-stu-id="40471-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="40471-149">Hello GPS nunca se utiliza, y, por tanto, este tipo de informe de ubicación tiene muy pocas (no toosay ningún) impacto en la batería de Hola.</span><span class="sxs-lookup"><span data-stu-id="40471-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="40471-150">Áreas notificadas son toocompute usado geográfica estadísticas acerca de los usuarios, sesiones, eventos y errores.</span><span class="sxs-lookup"><span data-stu-id="40471-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="40471-151">También se pueden usar como criterios en campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="40471-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="40471-152">Hola última conocida área notificada para un dispositivo puede ser recuperada gracias toohello [API de dispositivo].</span><span class="sxs-lookup"><span data-stu-id="40471-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="40471-153">ubicación de área lenta tooenable informes, agregue Hola después de línea después de inicializar el agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="40471-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="40471-154">Informes de ubicación en tiempo real</span><span class="sxs-lookup"><span data-stu-id="40471-154">Real time location reporting</span></span>
<span data-ttu-id="40471-155">Informes de ubicación en tiempo real permiten asociada de latitud y tooreport hello toodevices.</span><span class="sxs-lookup"><span data-stu-id="40471-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="40471-156">De forma predeterminada, este tipo de informes de ubicación sólo usa ubicaciones de red (basadas en el identificador de la celda o Wi-Fi) y reporting Hola solo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="40471-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="40471-157">Ubicaciones de tiempo real son *no* utiliza las estadísticas de toocompute.</span><span class="sxs-lookup"><span data-stu-id="40471-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="40471-158">Su único propósito es el uso de Hola de tooallow de barrera geográfica en tiempo real \<perímetro de audiencia de Reach\> criterio de campañas.</span><span class="sxs-lookup"><span data-stu-id="40471-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="40471-159">ubicación en tiempo real de tooenable informes, agregue Hola después de línea después de inicializar el agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="40471-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="40471-160">Informes basados en GPS</span><span class="sxs-lookup"><span data-stu-id="40471-160">GPS based reporting</span></span>
<span data-ttu-id="40471-161">De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red.</span><span class="sxs-lookup"><span data-stu-id="40471-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="40471-162">uso de Hola de tooenable de GPS basada en ubicaciones (que son mucho más precisas), agregue:</span><span class="sxs-lookup"><span data-stu-id="40471-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="40471-163">Informes en segundo plano</span><span class="sxs-lookup"><span data-stu-id="40471-163">Background reporting</span></span>
<span data-ttu-id="40471-164">De forma predeterminada, el informes de ubicación en tiempo real sólo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="40471-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="40471-165">Hola tooenable informes también en segundo plano, agregue:</span><span class="sxs-lookup"><span data-stu-id="40471-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="40471-166">Cuando la aplicación hello se ejecuta en segundo plano, se notifican únicas ubicaciones a basados en red, incluso si ha habilitado Hola GPS.</span><span class="sxs-lookup"><span data-stu-id="40471-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="40471-167">Implementación de esta función llamará [startMonitoringSignificantLocationChanges] cuando la aplicación entra en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="40471-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="40471-168">Tenga en cuenta que le automáticamente vuelva a iniciar la aplicación en segundo plano de hello si llega un nuevo evento de ubicación.</span><span class="sxs-lookup"><span data-stu-id="40471-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="40471-169">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="40471-169">Advanced reporting</span></span>
<span data-ttu-id="40471-170">Opcionalmente, si desea eventos específicos de aplicación tooreport, errores y trabajos, debe toouse Hola API de interacción a través de métodos de Hola de hello `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="40471-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="40471-171">Se puede recuperar un objeto de esta clase que realiza la llamada hello `[EngagementAgent shared]` método estático.</span><span class="sxs-lookup"><span data-stu-id="40471-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="40471-172">permite todas las capacidades avanzadas de contratación toouse Hello API de contratación y se detalla cómo Hola tooUse la API de interacción en iOS (así como en la documentación técnica de Hola de hello `EngagementAgent` clase).</span><span class="sxs-lookup"><span data-stu-id="40471-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="40471-173">Deshabilitación de la recopilación de IDFA</span><span class="sxs-lookup"><span data-stu-id="40471-173">Disable IDFA collection</span></span>
<span data-ttu-id="40471-174">De forma predeterminada, Engagement usará hello [IDFA] toouniquely identificar a un usuario.</span><span class="sxs-lookup"><span data-stu-id="40471-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="40471-175">Pero si no usas publicidad en otra parte de la aplicación hello, puede ser rechazados por hello proceso de revisión de la tienda de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="40471-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="40471-176">Recopilación de IDFA se puede deshabilitar mediante la adición de macro de preprocesador hello `ENGAGEMENT_DISABLE_IDFA` en el archivo de encabezado precompilado (o en hello `Build Settings` de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="40471-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="40471-177">Así se asegurará de que no hay ninguna referencia demasiado`ASIdentifierManager`, `advertisingIdentifier` o `isAdvertisingTrackingEnabled` en la compilación de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="40471-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="40471-178">Integración en hello **prefix.pch** archivo:</span><span class="sxs-lookup"><span data-stu-id="40471-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="40471-179">Puede comprobar que recopilación de IDFA Hola correctamente está deshabilitado en la aplicación mediante la comprobación de los registros de pruebas de interacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="40471-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="40471-180">Vea Hola pruebas de integración de\<ios sdk interacción prueba idfa\> documentación para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="40471-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="40471-181">Deshabilitación de los informes de registro</span><span class="sxs-lookup"><span data-stu-id="40471-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="40471-182">Mediante una llamada al método</span><span class="sxs-lookup"><span data-stu-id="40471-182">Using a method call</span></span>
<span data-ttu-id="40471-183">Si desea enviar registros de toostop de interacción, puede llamar:</span><span class="sxs-lookup"><span data-stu-id="40471-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="40471-184">Esta llamada es persistente: usa `NSUserDefaults` información de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="40471-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="40471-185">Puede habilitar el registro de reporting nuevo mediante una llamada a Hola la misma función con `YES`.</span><span class="sxs-lookup"><span data-stu-id="40471-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="40471-186">Integración en la agrupación de configuraciones</span><span class="sxs-lookup"><span data-stu-id="40471-186">Integration in your settings bundle</span></span>
<span data-ttu-id="40471-187">En lugar de llamar a esta función, también puede integrar esta configuración directamente en el archivo `Settings.bundle` existente.</span><span class="sxs-lookup"><span data-stu-id="40471-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="40471-188">Hola cadena `engagement_agent_enabled` debe usarse como un identificador de preferencias de Hola y debe ser modificador para alternar tooa asociado (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="40471-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="40471-189">Hola siguiendo el ejemplo de `Settings.bundle` muestra cómo tooimplement:</span><span class="sxs-lookup"><span data-stu-id="40471-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
