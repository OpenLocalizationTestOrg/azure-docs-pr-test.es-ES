---
title: "Integración del SDK de Android para Azure Mobile Engagement"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="d7d14-103">Integración de Engagement en Android</span><span class="sxs-lookup"><span data-stu-id="d7d14-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7d14-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d7d14-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="d7d14-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d7d14-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="d7d14-106">iOS</span><span class="sxs-lookup"><span data-stu-id="d7d14-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="d7d14-107">Android</span><span class="sxs-lookup"><span data-stu-id="d7d14-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="d7d14-108">Este procedimiento describe la manera más fácil de activar las funciones de Análisis y Supervisión de Engagement en su aplicación de Android.</span><span class="sxs-lookup"><span data-stu-id="d7d14-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7d14-109">El nivel mínimo de la API del SDK de Android debe ser 10 o superior (Android 2.3.3 o superior).</span><span class="sxs-lookup"><span data-stu-id="d7d14-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="d7d14-110">Los siguientes pasos son suficientes para activar el informe de registros necesarios para calcular todas las estadísticas relativas a Usuarios, Sesiones, Actividades, Bloqueos y Aspectos técnicos.</span><span class="sxs-lookup"><span data-stu-id="d7d14-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="d7d14-111">El informe de los registros necesarios para calcular otras estadísticas, como eventos, errores y trabajos debe realizarse manualmente mediante la API de Engagement (vea [Cómo usar la API de etiquetado avanzado de Mobile Engagement en su dispositivo Android](mobile-engagement-android-use-engagement-api.md) ) debido a que estas estadísticas dependen de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7d14-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="d7d14-112">Inserción del SDK y el servicio Engagement en el proyecto de Android</span><span class="sxs-lookup"><span data-stu-id="d7d14-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="d7d14-113">Descargue el SDK de Android [aquí](https://aka.ms/vq9mfn). Obtenga `mobile-engagement-VERSION.jar` y colóquelos en la carpeta `libs` del proyecto Android (cree la carpeta libs si aún no existe).</span><span class="sxs-lookup"><span data-stu-id="d7d14-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7d14-114">Si compila su paquete de aplicación con ProGuard, deberá mantener algunas clases.</span><span class="sxs-lookup"><span data-stu-id="d7d14-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="d7d14-115">Puede usar el siguiente snippet de configuración:</span><span class="sxs-lookup"><span data-stu-id="d7d14-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="d7d14-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="d7d14-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="d7d14-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="d7d14-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="d7d14-118">Especifique la cadena de conexión de Engagement mediante la llamada al siguiente método en la actividad del iniciador:</span><span class="sxs-lookup"><span data-stu-id="d7d14-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d7d14-119">La cadena de conexión de la aplicación se muestra en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d14-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="d7d14-120">Si no está, agregue los siguientes permisos de Android (delante de la etiqueta `<application>`):</span><span class="sxs-lookup"><span data-stu-id="d7d14-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="d7d14-121">Agregue la siguiente sección (entre las etiquetas `<application>` y `</application>`):</span><span class="sxs-lookup"><span data-stu-id="d7d14-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="d7d14-122">Cambie `<Your application name>` por el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7d14-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="d7d14-123">La clave `android:label` le permite elegir el nombre del servicio Engagement que aparecerá para los usuarios finales en la pantalla "Running services" (Servicios en ejecución) de su teléfono.</span><span class="sxs-lookup"><span data-stu-id="d7d14-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="d7d14-124">Se recomienda establecer este atributo en `"<Your application name>Service"` (por ejemplo, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="d7d14-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="d7d14-125">La especificación del atributo `android:process` garantiza que el servicio Engagement se ejecutará en su propio proceso (al ejecutarse Engagement en el mismo proceso que su aplicación, el subproceso principal y de interfaz de usuario podría tener menos capacidad de respuesta).</span><span class="sxs-lookup"><span data-stu-id="d7d14-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="d7d14-126">Cualquier código que coloque en `Application.onCreate()` y otras devoluciones de llamada de aplicaciones se ejecutará para todos los procesos de la aplicación, incluido el servicio Engagement.</span><span class="sxs-lookup"><span data-stu-id="d7d14-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="d7d14-127">Esto puede tener efectos secundarios no deseados (como asignaciones innecesarias de memoria y subprocesos en el proceso de Engagement o receptores o servicios de difusión duplicados).</span><span class="sxs-lookup"><span data-stu-id="d7d14-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="d7d14-128">Si anula `Application.onCreate()`, se recomienda que agregue el siguiente snippet de código al comienzo de su función `Application.onCreate()`:</span><span class="sxs-lookup"><span data-stu-id="d7d14-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="d7d14-129">Puede hacer lo mismo para `Application.onTerminate()`, `Application.onLowMemory()` y `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="d7d14-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="d7d14-130">También puede ampliar `EngagementApplication` en lugar de `Application`: la devolución de llamada `Application.onCreate()` solo realiza el proceso y llama a `Application.onApplicationProcessCreate()` si el proceso actual no es el que hospeda el servicio Engagement; las mismas reglas se aplican para las demás devoluciones de llamada.</span><span class="sxs-lookup"><span data-stu-id="d7d14-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="d7d14-131">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="d7d14-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="d7d14-132">Método recomendado: sobrecargar las clases `Activity`</span><span class="sxs-lookup"><span data-stu-id="d7d14-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="d7d14-133">Para activar el informe de todos los registros que necesita Engagement para calcular las estadísticas de Usuarios, Sesiones, Actividades, Bloqueos y Aspectos técnicos, tiene que hacer que todas las subclases `*Activity` hereden de las clases `Engagement*Activity` correspondientes (por ejemplo, si su actividad heredada amplía `ListActivity`, haga que amplíe `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="d7d14-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="d7d14-134">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d7d14-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="d7d14-135">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="d7d14-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="d7d14-136">Al usar `EngagementListActivity` o `EngagementExpandableListActivity`, asegúrese de que cualquier llamada a `requestWindowFeature(...);` se realice antes que la llamada a `super.onCreate(...);`, de lo contrario se producirá un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="d7d14-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="d7d14-137">Puede encontrar estas clases en la carpeta `src` y puede copiarlas en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="d7d14-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="d7d14-138">Las clases también están en **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="d7d14-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="d7d14-139">Método alternativo: llamar a `startActivity()` y `endActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="d7d14-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="d7d14-140">Si no puede o no quiere sobrecargar sus clases `Activity`, puede iniciar y finalizar sus actividades llamando a los métodos `EngagementAgent` directamente.</span><span class="sxs-lookup"><span data-stu-id="d7d14-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7d14-141">El SDK de Android nunca llama al método `endActivity()`, incluso cuando la aplicación está cerrada (en Android, las aplicaciones nunca se cierran realmente).</span><span class="sxs-lookup"><span data-stu-id="d7d14-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="d7d14-142">Por tanto, es *MUY* recomendable llamar al método `startActivity()` en la devolución de llamada `onResume` de *TODAS* las actividades y al método `endActivity()` en la devolución de llamada `onPause()` de *TODAS* las actividades.</span><span class="sxs-lookup"><span data-stu-id="d7d14-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="d7d14-143">Esta es la única manera de asegurarse de que las sesiones no se pierdan.</span><span class="sxs-lookup"><span data-stu-id="d7d14-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="d7d14-144">Si una sesión se pierde, el servicio Engagement nunca se desconectará del back-end de Engagement (dado que el servicio permanece conectado mientras una sesión esté pendiente).</span><span class="sxs-lookup"><span data-stu-id="d7d14-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="d7d14-145">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d7d14-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="d7d14-146">Este ejemplo es muy parecido a la clase `EngagementActivity` y sus variantes, cuyo código fuente se proporciona en la carpeta `src`.</span><span class="sxs-lookup"><span data-stu-id="d7d14-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="d7d14-147">Prueba</span><span class="sxs-lookup"><span data-stu-id="d7d14-147">Test</span></span>
<span data-ttu-id="d7d14-148">Ahora, para comprobar la integración, ejecute la aplicación móvil en un dispositivo o emulador y compruebe que registra una sesión en la pestaña Monitor.</span><span class="sxs-lookup"><span data-stu-id="d7d14-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="d7d14-149">Las siguientes secciones son opcionales.</span><span class="sxs-lookup"><span data-stu-id="d7d14-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="d7d14-150">Informes de ubicación</span><span class="sxs-lookup"><span data-stu-id="d7d14-150">Location reporting</span></span>
<span data-ttu-id="d7d14-151">Si desea que se notifiquen las ubicaciones, deberá agregar algunas líneas de configuración (entre las etiquetas `<application>` y `</application>`).</span><span class="sxs-lookup"><span data-stu-id="d7d14-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="d7d14-152">Informes de ubicaciones de áreas diferidas</span><span class="sxs-lookup"><span data-stu-id="d7d14-152">Lazy area location reporting</span></span>
<span data-ttu-id="d7d14-153">Los informes de ubicación de área diferida permiten notificar el país, la región y la localidad asociados con los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7d14-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="d7d14-154">Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI).</span><span class="sxs-lookup"><span data-stu-id="d7d14-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="d7d14-155">El área del dispositivo se notifica como máximo una vez por sesión.</span><span class="sxs-lookup"><span data-stu-id="d7d14-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="d7d14-156">El GPS no se utiliza nunca y, por tanto, este tipo de informe de ubicación tiene muy poco impacto (por no decir ninguno) en la batería.</span><span class="sxs-lookup"><span data-stu-id="d7d14-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="d7d14-157">Las áreas notificadas se utilizan para elaborar estadísticas geográficas acerca de los usuarios, las sesiones, los eventos y los errores.</span><span class="sxs-lookup"><span data-stu-id="d7d14-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="d7d14-158">También se pueden usar como criterios en campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="d7d14-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="d7d14-159">Para habilitar los informes diferidos de ubicación, puede hacerlo mediante la configuración anteriormente mencionada en este procedimiento: </span><span class="sxs-lookup"><span data-stu-id="d7d14-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d7d14-160">Puede que también deba agregar el siguiente permiso si no existe:</span><span class="sxs-lookup"><span data-stu-id="d7d14-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="d7d14-161">O bien, puede seguir usando ``ACCESS_FINE_LOCATION`` si ya lo usa en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7d14-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="d7d14-162">Informes de ubicación en tiempo real</span><span class="sxs-lookup"><span data-stu-id="d7d14-162">Real time location reporting</span></span>
<span data-ttu-id="d7d14-163">Los informes de ubicación en tiempo real permiten notificar la latitud y la longitud asociadas con los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d7d14-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="d7d14-164">De forma predeterminada, este tipo de informes de ubicación solo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI), y los informes solo están activos cuando la aplicación se ejecuta en primer plano (por ejemplo, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="d7d14-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="d7d14-165">Las ubicaciones en tiempo real *NO* se usan para calcular las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="d7d14-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="d7d14-166">Su única finalidad es permitir el uso de criterios de geovallado en tiempo real \<Reach-Audience-geofencing\> en las campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="d7d14-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="d7d14-167">Para habilitar los informes de ubicación en tiempo real, puede hacerlo mediante la configuración anteriormente mencionada en este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="d7d14-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d7d14-168">Puede que también deba agregar el siguiente permiso si no existe:</span><span class="sxs-lookup"><span data-stu-id="d7d14-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="d7d14-169">O bien, puede seguir usando ``ACCESS_FINE_LOCATION`` si ya lo usa en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7d14-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="d7d14-170">Informes basados en GPS</span><span class="sxs-lookup"><span data-stu-id="d7d14-170">GPS based reporting</span></span>
<span data-ttu-id="d7d14-171">De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red.</span><span class="sxs-lookup"><span data-stu-id="d7d14-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="d7d14-172">Para habilitar el uso de ubicaciones basadas en GPS (que son mucho más precisas), use el objeto de configuración:</span><span class="sxs-lookup"><span data-stu-id="d7d14-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d7d14-173">Puede que también deba agregar el siguiente permiso si no existe:</span><span class="sxs-lookup"><span data-stu-id="d7d14-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="d7d14-174">Informes en segundo plano</span><span class="sxs-lookup"><span data-stu-id="d7d14-174">Background reporting</span></span>
<span data-ttu-id="d7d14-175">De forma predeterminada, los informes de ubicación en tiempo real solo están activos cuando la aplicación se ejecuta en primer plano (es decir, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="d7d14-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="d7d14-176">Para habilitar los informes también en segundo plano, use el objeto de configuración:</span><span class="sxs-lookup"><span data-stu-id="d7d14-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="d7d14-177">Cuando la aplicación se ejecuta en segundo plano, solo se notifican las ubicaciones de red, incluso si ha habilitado el GPS.</span><span class="sxs-lookup"><span data-stu-id="d7d14-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="d7d14-178">El informe de ubicación en segundo plano se detendrá si el usuario reinicia su dispositivo; puede agregar esto para hacer que se reinicie automáticamente en el momento de inicio:</span><span class="sxs-lookup"><span data-stu-id="d7d14-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="d7d14-179">Puede que también deba agregar el siguiente permiso si no existe:</span><span class="sxs-lookup"><span data-stu-id="d7d14-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="d7d14-180">Permisos de Android M</span><span class="sxs-lookup"><span data-stu-id="d7d14-180">Android M permissions</span></span>
<span data-ttu-id="d7d14-181">A partir de Android M, algunos permisos se administran en tiempo de ejecución y se necesita la aprobación del usuario.</span><span class="sxs-lookup"><span data-stu-id="d7d14-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="d7d14-182">Los permisos en tiempo de ejecución se desactivan de manera predeterminada para las nuevas instalaciones de aplicaciones con destino la API de Android nivel 23.</span><span class="sxs-lookup"><span data-stu-id="d7d14-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="d7d14-183">De lo contrario, se activan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d7d14-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="d7d14-184">El usuario puede habilitar o deshabilitar esos permisos en el menú de configuración del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d7d14-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="d7d14-185">Desactivar los permisos en el menú del sistema termina los procesos en segundo plano de la aplicación; se trata de un comportamiento del sistema y no afecta a la capacidad para recibir inserciones en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="d7d14-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="d7d14-186">En el contexto de Mobile Engagement, los permisos que requieren aprobación en tiempo de ejecución son:</span><span class="sxs-lookup"><span data-stu-id="d7d14-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="d7d14-187">`WRITE_EXTERNAL_STORAGE` (solo cuando el destino es la API de Android nivel 23)</span><span class="sxs-lookup"><span data-stu-id="d7d14-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="d7d14-188">El almacenamiento externo se usa únicamente para la característica de imágenes grandes de alcance.</span><span class="sxs-lookup"><span data-stu-id="d7d14-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="d7d14-189">Si observa que pedir este permiso a los usuarios resulta molesto, puede quitarlo si solo lo usa para Mobile Engagement pero a costa de deshabilitar la característica de grandes imágenes.</span><span class="sxs-lookup"><span data-stu-id="d7d14-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="d7d14-190">Para las características de ubicación, debe solicitar permisos al usuario mediante un cuadro de diálogo estándar del sistema.</span><span class="sxs-lookup"><span data-stu-id="d7d14-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="d7d14-191">Si el usuario lo aprueba, debe indicar a ``EngagementAgent`` que tenga en cuenta ese cambio en tiempo real (de lo contrario,el cambio se procesará la próxima vez que el usuario inicie la aplicación).</span><span class="sxs-lookup"><span data-stu-id="d7d14-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="d7d14-192">Este es un ejemplo de código para usar en una actividad de la aplicación para solicitar permisos y reenviar el resultado si es positivo a ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="d7d14-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="d7d14-193">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="d7d14-193">Advanced reporting</span></span>
<span data-ttu-id="d7d14-194">De manera opcional, si desea notificar eventos, errores y trabajos específicos de la aplicación, deberá usar la API de Engagement a través de los métodos de la clase `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="d7d14-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="d7d14-195">Un objeto de esta clase se puede recuperar mediante la llamada al método estático `EngagementAgent.getInstance()` .</span><span class="sxs-lookup"><span data-stu-id="d7d14-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="d7d14-196">La API de Engagement permite usar todas las capacidades avanzadas de Engagement, que se detallan en Cómo usar la API de Engagement en Android (así como en la documentación técnica de la clase `EngagementAgent` ).</span><span class="sxs-lookup"><span data-stu-id="d7d14-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="d7d14-197">Configuración avanzada (en AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="d7d14-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="d7d14-198">Reactivar bloqueos</span><span class="sxs-lookup"><span data-stu-id="d7d14-198">Wake locks</span></span>
<span data-ttu-id="d7d14-199">Si desea asegurarse de que las estadísticas se envían en tiempo real cuando se utilice Wifi o cuando la pantalla esté apagada, agregue el siguiente permiso opcional:</span><span class="sxs-lookup"><span data-stu-id="d7d14-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="d7d14-200">Informe de bloqueos</span><span class="sxs-lookup"><span data-stu-id="d7d14-200">Crash report</span></span>
<span data-ttu-id="d7d14-201">Si desea deshabilitar los informes de bloqueo, agregue esto (entre las etiquetas `<application>` y `</application>`):</span><span class="sxs-lookup"><span data-stu-id="d7d14-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="d7d14-202">Umbral de ráfaga</span><span class="sxs-lookup"><span data-stu-id="d7d14-202">Burst threshold</span></span>
<span data-ttu-id="d7d14-203">De forma predeterminada, el servicio de Engagement informa los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="d7d14-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="d7d14-204">Si su aplicación notifica registros con mucha frecuencia, es mejor almacenar en búfer los registros y notificarlos todos a la vez de manera periódica (esto se conoce como "modo de ráfaga").</span><span class="sxs-lookup"><span data-stu-id="d7d14-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="d7d14-205">Para ello, agregue esto (entre las etiquetas `<application>` y `</application>`):</span><span class="sxs-lookup"><span data-stu-id="d7d14-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="d7d14-206">El modo de ráfaga aumenta ligeramente la duración de la batería, pero afecta al monitor de Engagement: la duración de todas las sesiones y trabajos se redondeará al umbral de ráfaga (por lo tanto, es posible que las sesiones y los trabajos más cortos que el umbral de ráfaga no sean visibles).</span><span class="sxs-lookup"><span data-stu-id="d7d14-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="d7d14-207">Se recomienda usar un umbral de ráfaga inferior a 30.000 (30 segundos).</span><span class="sxs-lookup"><span data-stu-id="d7d14-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="d7d14-208">Tiempo de espera de sesión</span><span class="sxs-lookup"><span data-stu-id="d7d14-208">Session timeout</span></span>
<span data-ttu-id="d7d14-209">De forma predeterminada, una sesión finaliza a los 10 seg. del final de su última actividad (que normalmente se produce al presionar Inicio o la tecla de retroceso, poniendo el teléfono inactivo o yendo a otra aplicación).</span><span class="sxs-lookup"><span data-stu-id="d7d14-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="d7d14-210">Esto se hace para evitar que una sesión se divida cada vez que el usuario sale de la aplicación y vuelve a ella muy rápidamente (lo que puede suceder cuando se selecciona una imagen, se comprueba una notificación, etc.).</span><span class="sxs-lookup"><span data-stu-id="d7d14-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="d7d14-211">Puede que desee modificar este parámetro.</span><span class="sxs-lookup"><span data-stu-id="d7d14-211">You may want to modify this parameter.</span></span> <span data-ttu-id="d7d14-212">Para ello, agregue esto (entre las etiquetas `<application>` y `</application>`):</span><span class="sxs-lookup"><span data-stu-id="d7d14-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="d7d14-213">Deshabilitación de los informes de registro</span><span class="sxs-lookup"><span data-stu-id="d7d14-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="d7d14-214">Mediante una llamada al método</span><span class="sxs-lookup"><span data-stu-id="d7d14-214">Using a method call</span></span>
<span data-ttu-id="d7d14-215">Si desea que Engagement deje de enviar registros, puede efectuar una llamada:</span><span class="sxs-lookup"><span data-stu-id="d7d14-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="d7d14-216">Esta llamada es persistente: usa un archivo de preferencias compartido.</span><span class="sxs-lookup"><span data-stu-id="d7d14-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="d7d14-217">Si Engagement está activo cuando llama a esta función, puede que el servicio tarde 1 minuto en detenerse.</span><span class="sxs-lookup"><span data-stu-id="d7d14-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="d7d14-218">Sin embargo, no se iniciará el servicio la próxima vez que inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d7d14-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="d7d14-219">Puede habilitar de nuevo los informes de registro mediante la llamada a la misma función con `true`.</span><span class="sxs-lookup"><span data-stu-id="d7d14-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="d7d14-220">Integración en su propia `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="d7d14-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="d7d14-221">En lugar de llamar a esta función, también puede integrar este valor directamente en su `PreferenceActivity` existente.</span><span class="sxs-lookup"><span data-stu-id="d7d14-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="d7d14-222">Puede configurar Engagement para usar su archivo de preferencias (con el modo deseado) en el archivo `AndroidManifest.xml` con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="d7d14-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="d7d14-223">La clave `engagement:agent:settings:name` se usa para definir el nombre del archivo de preferencias compartido.</span><span class="sxs-lookup"><span data-stu-id="d7d14-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="d7d14-224">La clave `engagement:agent:settings:mode` se usa para definir el modo del archivo de preferencias compartido; debe usar el mismo modo que en su `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="d7d14-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="d7d14-225">El modo se debe pasar como un número: si usa una combinación de indicadores constantes en su código, compruebe el valor total.</span><span class="sxs-lookup"><span data-stu-id="d7d14-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="d7d14-226">Engagement siempre usa la clave booleana `engagement:key` dentro del archivo de preferencias para administrar este valor.</span><span class="sxs-lookup"><span data-stu-id="d7d14-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="d7d14-227">En el siguiente ejemplo de `AndroidManifest.xml` se muestran los valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="d7d14-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="d7d14-228">Luego, puede agregar un `CheckBoxPreference` a su diseño de preferencias como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="d7d14-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
