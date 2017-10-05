---
title: "Integración del SDK de iOS de Azure Mobile Engagement | Microsoft Docs"
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
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="95288-103">Integración de Engagement en iOS</span><span class="sxs-lookup"><span data-stu-id="95288-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95288-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="95288-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="95288-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="95288-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="95288-106">iOS</span><span class="sxs-lookup"><span data-stu-id="95288-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="95288-107">Android</span><span class="sxs-lookup"><span data-stu-id="95288-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="95288-108">Este procedimiento describe la manera más sencilla de activar las funciones de supervisión y análisis de Engagement en su aplicación iOS.</span><span class="sxs-lookup"><span data-stu-id="95288-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="95288-109">El SDK de Engagement requiere iOS7+ y Xcode 8+: el destino de implementación de la aplicación debe ser como mínimo iOS 7.</span><span class="sxs-lookup"><span data-stu-id="95288-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="95288-110">Si realmente depende de XCode 7, puede usar el [SDK v3.2.4 de Engagement para iOS](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="95288-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="95288-111">Existe un problema conocido en el módulo de cobertura de esta versión anterior cuando se ejecuta en dispositivos iOS 10. Consulte la [integración del módulo de cobertura](mobile-engagement-ios-integrate-engagement-reach.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="95288-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="95288-112">Si decide usar el SDK v3.2.4, simplemente omita la importación de `UserNotifications.framework` en el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="95288-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="95288-113">Los siguientes pasos son suficientes para activar el informe de los registros necesarios para calcular todas las estadísticas en relación con los usuarios, las sesiones, las actividades, los bloqueos y los aspectos técnicos.</span><span class="sxs-lookup"><span data-stu-id="95288-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="95288-114">El informe de los registros necesarios para calcular otras estadísticas, como eventos, errores y trabajos debe realizarse manualmente mediante la API de Engagement (consulte [Cómo usar la API de etiquetado avanzado de Mobile Engagement en su aplicación iOS](mobile-engagement-ios-use-engagement-api.md)) debido a que estas estadísticas dependen de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95288-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="95288-115">Incrustación del SDK de Engagement en su proyecto de iOS</span><span class="sxs-lookup"><span data-stu-id="95288-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="95288-116">Descargue el SDK de iOS [aquí](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="95288-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="95288-117">Agregue el SDK de Engagement al proyecto de iOS: en Xcode, haga clic con el botón derecho en el proyecto, elija **"Agregar archivos a..."** y elija la carpeta `EngagementSDK`.</span><span class="sxs-lookup"><span data-stu-id="95288-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="95288-118">Engagement requiere la contratación de marcos adicionales para trabajar: en el Explorador de proyectos, abra el panel de proyectos y elija el destino correcto.</span><span class="sxs-lookup"><span data-stu-id="95288-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="95288-119">A continuación, abra la pestaña **"Generar fases"** en el menú **"Vincular binario con bibliotecas"** y agregue estos marcos:</span><span class="sxs-lookup"><span data-stu-id="95288-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="95288-120">`UserNotifications.framework`- configure el vínculo como `Optional`</span><span class="sxs-lookup"><span data-stu-id="95288-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="95288-121">`AdSupport.framework`- configure el vínculo como `Optional`</span><span class="sxs-lookup"><span data-stu-id="95288-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="95288-122">El marco de trabajo AdSupport se puede quitar.</span><span class="sxs-lookup"><span data-stu-id="95288-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="95288-123">Engagement necesita este marco para recopilar el IDFA.</span><span class="sxs-lookup"><span data-stu-id="95288-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="95288-124">No obstante, la recopilación de IDFA se puede deshabilitar \<ios-sdk-engagement-idfa\> para cumplir con la nueva directiva de Apple con respecto a este identificador.</span><span class="sxs-lookup"><span data-stu-id="95288-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="95288-125">Inicializar el SDK de Engagement</span><span class="sxs-lookup"><span data-stu-id="95288-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="95288-126">Debe modificar el delegado de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="95288-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="95288-127">En la parte superior del archivo de implementación, importe el agente de Engagement.</span><span class="sxs-lookup"><span data-stu-id="95288-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="95288-128">Inicialice Engagement dentro del método '**applicationDidFinishLaunching:**' o '**application:didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="95288-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="95288-129">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="95288-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="95288-130">Método recomendado: sobrecargar las clases `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="95288-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="95288-131">Si desea que se generen todos los registros que requiere Engagement para calcular los usuarios, las sesiones, las actividades, los bloqueos y las estadísticas técnicas, simplemente puede hacer que todas las subclases `UIViewController` se hereden de las clases `EngagementViewController` (misma regla para `UITableViewController` -\> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="95288-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="95288-132">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="95288-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="95288-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="95288-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="95288-134">Método alternativo: llamar a `startActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="95288-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="95288-135">Si no puede o no desea sobrecargar las clases `UIViewController`, en su lugar, puede iniciar sus actividades mediante una llamada directa a los métodos de `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="95288-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95288-136">El SDK de iOS llama automáticamente al método `endActivity()` cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95288-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="95288-137">Por lo tanto, es *MUY* recomendable llamar al método `startActivity` cada vez que cambie la actividad del usuario y *NUNCA* llamar al método `endActivity`, ya que fuerza la finalización de la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="95288-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="95288-138">Informes de ubicación</span><span class="sxs-lookup"><span data-stu-id="95288-138">Location reporting</span></span>
<span data-ttu-id="95288-139">Las condiciones de servicio de Apple no permiten a las aplicaciones utilizar el seguimiento de ubicación con fines de estadísticas únicamente.</span><span class="sxs-lookup"><span data-stu-id="95288-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="95288-140">Por lo tanto, se recomienda habilitar los informes de ubicación solo si la aplicación también utiliza el seguimiento de ubicación por otro motivo.</span><span class="sxs-lookup"><span data-stu-id="95288-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="95288-141">A partir de iOS 8, debe proporcionar una descripción del modo en que su aplicación utiliza los servicios de ubicación estableciendo una cadena para la clave [NSLocationWhenInUseUsageDescription] o [NSLocationAlwaysUsageDescription] en el archivo Info.plist de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95288-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="95288-142">Si desea registrar la ubicación en segundo plano con Engagement, agregue la clave NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="95288-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="95288-143">En los demás casos, agregue la clave NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="95288-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="95288-144">Tenga en cuenta que necesita tanto NSLocationAlwaysAndWhenInUseUsageDescription como NSLocationWhenInUseUsageDescription para notificar la ubicación de fondo en iOS 11.</span><span class="sxs-lookup"><span data-stu-id="95288-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="95288-145">Informes de ubicaciones de áreas diferidas</span><span class="sxs-lookup"><span data-stu-id="95288-145">Lazy area location reporting</span></span>
<span data-ttu-id="95288-146">Los informes de ubicación de área diferida permiten notificar el país, la región y la localidad asociados con los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="95288-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="95288-147">Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI).</span><span class="sxs-lookup"><span data-stu-id="95288-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="95288-148">El área del dispositivo se notifica como máximo una vez por sesión.</span><span class="sxs-lookup"><span data-stu-id="95288-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="95288-149">El GPS no se utiliza nunca y, por tanto, este tipo de informe de ubicación tiene muy poco impacto (por no decir ninguno) en la batería.</span><span class="sxs-lookup"><span data-stu-id="95288-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="95288-150">Las áreas notificadas se utilizan para elaborar estadísticas geográficas acerca de los usuarios, las sesiones, los eventos y los errores.</span><span class="sxs-lookup"><span data-stu-id="95288-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="95288-151">También se pueden usar como criterios en campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="95288-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="95288-152">La última área conocida registrada para un dispositivo se puede recuperar gracias a la [API del dispositivo].</span><span class="sxs-lookup"><span data-stu-id="95288-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="95288-153">Para habilitar los informes de ubicación de área diferida, agregue la siguiente línea después de inicializar el agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="95288-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="95288-154">Informes de ubicación en tiempo real</span><span class="sxs-lookup"><span data-stu-id="95288-154">Real time location reporting</span></span>
<span data-ttu-id="95288-155">Los informes de ubicación en tiempo real permiten notificar la latitud y la longitud asociadas con los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="95288-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="95288-156">De forma predeterminada, este tipo de informes de ubicación solo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI), y los informes solo están activos cuando la aplicación se ejecuta en primer plano (por ejemplo, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="95288-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="95288-157">Las ubicaciones en tiempo real *NO* se usan para calcular las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="95288-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="95288-158">Su único objetivo es permitir el uso de criterios de geovallas en tiempo real \<Reach-Audience-geofencing\> en las campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="95288-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="95288-159">Para habilitar los informes de ubicación en tiempo real, agregue la siguiente línea después de inicializar el agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="95288-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="95288-160">Informes basados en GPS</span><span class="sxs-lookup"><span data-stu-id="95288-160">GPS based reporting</span></span>
<span data-ttu-id="95288-161">De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red.</span><span class="sxs-lookup"><span data-stu-id="95288-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="95288-162">Para habilitar el uso de ubicaciones basadas en GPS (que son mucho más precisas), agregue:</span><span class="sxs-lookup"><span data-stu-id="95288-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="95288-163">Informes en segundo plano</span><span class="sxs-lookup"><span data-stu-id="95288-163">Background reporting</span></span>
<span data-ttu-id="95288-164">De forma predeterminada, los informes de ubicación en tiempo real solo están activos cuando la aplicación se ejecuta en primer plano (es decir, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="95288-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="95288-165">Para habilitar los informes también en segundo plano, agregue:</span><span class="sxs-lookup"><span data-stu-id="95288-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="95288-166">Cuando la aplicación se ejecuta en segundo plano, solo se notifican las ubicaciones de red, incluso si ha habilitado el GPS.</span><span class="sxs-lookup"><span data-stu-id="95288-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="95288-167">La implementación de esta función efectuará una llamada a [startMonitoringSignificantLocationChanges] cuando la aplicación pase a un segundo plano.</span><span class="sxs-lookup"><span data-stu-id="95288-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="95288-168">Tenga en cuenta que la aplicación se reiniciará automáticamente en segundo plano si se produce un nuevo evento de ubicación.</span><span class="sxs-lookup"><span data-stu-id="95288-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="95288-169">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="95288-169">Advanced reporting</span></span>
<span data-ttu-id="95288-170">De manera opcional, si desea notificar eventos, errores y trabajos específicos de la aplicación, deberá usar la API de Engagement a través de los métodos de la clase `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="95288-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="95288-171">Un objeto de esta clase se puede recuperar mediante una llamada al método estático `[EngagementAgent shared]` .</span><span class="sxs-lookup"><span data-stu-id="95288-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="95288-172">La API de Engagement permite usar todas las capacidades avanzadas de Engagement, que se detallan en Cómo usar la API de Engagement en iOS (así como en la documentación técnica de la clase `EngagementAgent` ).</span><span class="sxs-lookup"><span data-stu-id="95288-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="95288-173">Deshabilitación de la recopilación de IDFA</span><span class="sxs-lookup"><span data-stu-id="95288-173">Disable IDFA collection</span></span>
<span data-ttu-id="95288-174">De forma predeterminada, Engagement utilizará [IDFA] para identificar a un usuario de forma exclusiva.</span><span class="sxs-lookup"><span data-stu-id="95288-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="95288-175">Pero si no está utilizando publicidad en otra parte de la aplicación, es posible que el proceso de revisión de la tienda de aplicaciones le rechace.</span><span class="sxs-lookup"><span data-stu-id="95288-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="95288-176">La colección de IDFA se puede deshabilitar mediante la adición de la macro de preprocesador `ENGAGEMENT_DISABLE_IDFA` en el archivo pch (o en la `Build Settings` de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="95288-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="95288-177">Así se asegurará de que no haya ninguna referencia a `ASIdentifierManager`, `advertisingIdentifier` ni a `isAdvertisingTrackingEnabled` en la compilación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95288-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="95288-178">Integración en el archivo **prefix.pch** :</span><span class="sxs-lookup"><span data-stu-id="95288-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="95288-179">Puede verificar que la colección IDFA está correctamente deshabilitada en la aplicación comprobando los registros de prueba de Engagement.</span><span class="sxs-lookup"><span data-stu-id="95288-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="95288-180">Consulte la documentación de las pruebas de integración \<ios-sdk-engagement-test-idfa\> para más información.</span><span class="sxs-lookup"><span data-stu-id="95288-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="95288-181">Deshabilitación de los informes de registro</span><span class="sxs-lookup"><span data-stu-id="95288-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="95288-182">Mediante una llamada al método</span><span class="sxs-lookup"><span data-stu-id="95288-182">Using a method call</span></span>
<span data-ttu-id="95288-183">Si desea que Engagement deje de enviar registros, puede efectuar una llamada:</span><span class="sxs-lookup"><span data-stu-id="95288-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="95288-184">Esta llamada es persistente: usa `NSUserDefaults` para almacenar la información.</span><span class="sxs-lookup"><span data-stu-id="95288-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="95288-185">Puede habilitar de nuevo los informes de registro mediante la llamada a la misma función con `YES`.</span><span class="sxs-lookup"><span data-stu-id="95288-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="95288-186">Integración en la agrupación de configuraciones</span><span class="sxs-lookup"><span data-stu-id="95288-186">Integration in your settings bundle</span></span>
<span data-ttu-id="95288-187">En lugar de llamar a esta función, también puede integrar esta configuración directamente en el archivo `Settings.bundle` existente.</span><span class="sxs-lookup"><span data-stu-id="95288-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="95288-188">La cadena `engagement_agent_enabled` debe utilizarse como un identificador de preferencia y debe estar asociada a un modificador para alternar (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="95288-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="95288-189">El siguiente ejemplo de `Settings.bundle` muestra el proceso de implementación:</span><span class="sxs-lookup"><span data-stu-id="95288-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

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
<span data-ttu-id="95288-190">[API del dispositivo]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="95288-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="95288-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="95288-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="95288-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="95288-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="95288-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="95288-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="95288-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="95288-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
