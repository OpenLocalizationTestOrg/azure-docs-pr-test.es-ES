---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
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
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="94651-103">¿Cómo tooIntegrate interacción en Android</span><span class="sxs-lookup"><span data-stu-id="94651-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94651-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="94651-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="94651-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="94651-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="94651-106">iOS</span><span class="sxs-lookup"><span data-stu-id="94651-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="94651-107">Android</span><span class="sxs-lookup"><span data-stu-id="94651-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="94651-108">Este procedimiento describe las funciones de la aplicación Android de supervisión y análisis hello más sencilla forma tooactivate Engagement.</span><span class="sxs-lookup"><span data-stu-id="94651-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94651-109">El nivel mínimo de la API del SDK de Android debe ser 10 o superior (Android 2.3.3 o superior).</span><span class="sxs-lookup"><span data-stu-id="94651-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="94651-110">Hola pasos es que toocompute necesita un suficiente informe de hello tooactivates de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals.</span><span class="sxs-lookup"><span data-stu-id="94651-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="94651-111">Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en sus Android](mobile-engagement-android-use-engagement-api.md) desde estos las estadísticas son dependientes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94651-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="94651-112">No inserte Hola Engagement SDK y el servicio en su proyecto de Android</span><span class="sxs-lookup"><span data-stu-id="94651-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="94651-113">Descarga Hola SDK de Android de [aquí](https://aka.ms/vq9mfn) obtener `mobile-engagement-VERSION.jar` y colóquelos en hello `libs` carpeta del proyecto de Android (crear carpeta de bibliotecas de hello si aún no existe).</span><span class="sxs-lookup"><span data-stu-id="94651-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94651-114">Si compila el paquete de aplicación con ProGuard, deberá tookeep algunas clases.</span><span class="sxs-lookup"><span data-stu-id="94651-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="94651-115">Puede usar Hola siguiente fragmento de código de configuración:</span><span class="sxs-lookup"><span data-stu-id="94651-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="94651-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="94651-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="94651-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="94651-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="94651-118">Especifique la cadena de conexión de interacción por Hola que realiza la llamada siguiente método en la actividad del iniciador hello:</span><span class="sxs-lookup"><span data-stu-id="94651-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="94651-119">cadena de conexión de Hello para la aplicación se muestra en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="94651-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="94651-120">Si no se especifica, agregue los siguientes permisos Android de hello (antes de hello `<application>` etiqueta):</span><span class="sxs-lookup"><span data-stu-id="94651-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="94651-121">Agregar pasos de la sección de hello (entre hello `<application>` y `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="94651-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="94651-122">Cambio `<Your application name>` por su nombre de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94651-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="94651-123">Hola `android:label` atributo permite toochoose Hola nombre de servicio de contratación de hello tal y como aparecerá toohello los usuarios finales en la pantalla de bienvenida "Ejecutar servicios" de su teléfono.</span><span class="sxs-lookup"><span data-stu-id="94651-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="94651-124">Es recomendable tooset este atributo demasiado`"<Your application name>Service"` (p. ej. `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="94651-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="94651-125">Hola especificando `android:process` atributo garantiza que ese servicio de contratación de Hola se ejecutará en su propio proceso (ejecutando interacción Hola mismo proceso cuando la aplicación hará que el subproceso de interfaz de usuario/main potencialmente responde a una menor).</span><span class="sxs-lookup"><span data-stu-id="94651-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="94651-126">Cualquier código que se coloque en `Application.onCreate()` y otras devoluciones de llamada de la aplicación se ejecutará para los procesos de todas las de su aplicación, incluido el servicio de contratación de Hola.</span><span class="sxs-lookup"><span data-stu-id="94651-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="94651-127">Puede tener efectos secundarios no deseados (por ejemplo, las asignaciones de memoria innecesario y subprocesos de proceso Hola Engagement, receptores de difusión duplicados o servicios).</span><span class="sxs-lookup"><span data-stu-id="94651-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="94651-128">Si invalida `Application.onCreate()`, resulta hello tooadd recomendado siguiente fragmento de código al principio de Hola de su `Application.onCreate()` función:</span><span class="sxs-lookup"><span data-stu-id="94651-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="94651-129">Puede hacer lo mismo para Hola `Application.onTerminate()`, `Application.onLowMemory()` y `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="94651-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="94651-130">También puede extender `EngagementApplication` en lugar de extender `Application`: Hola de devolución de llamada `Application.onCreate()` Hola comprobación del proceso y llamadas `Application.onApplicationProcessCreate()` solo si proceso actual de hello es no Hola uno Hola interacción servicio de hospedaje, hello mismas reglas se aplican para Hola otras devoluciones de llamada.</span><span class="sxs-lookup"><span data-stu-id="94651-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="94651-131">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="94651-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="94651-132">Método recomendado: sobrecargar las clases `Activity`</span><span class="sxs-lookup"><span data-stu-id="94651-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="94651-133">En informe de hello pedido tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, tiene todos los toomake su `*Activity` subclases heredan de hello correspondiente `Engagement*Activity` clases (por ejemplo, si se extiende la actividad heredada `ListActivity`, asegúrese de extiende `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="94651-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="94651-134">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="94651-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="94651-135">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="94651-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="94651-136">Cuando se usa `EngagementListActivity` o `EngagementExpandableListActivity`, asegúrese de que todas las llamadas demasiado`requestWindowFeature(...);` se realiza antes de la llamada de hello demasiado`super.onCreate(...);`, en caso contrario, se producirá un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="94651-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="94651-137">Puede encontrar estas clases en hello `src` carpeta y puede copiarlos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="94651-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="94651-138">clases de Hello también están en hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="94651-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="94651-139">Método alternativo: llamar a `startActivity()` y `endActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="94651-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="94651-140">Si no puede o no desea que toooverload su `Activity` clases, en su lugar, puede iniciar y finalizar las actividades mediante una llamada a `EngagementAgent`de métodos directamente.</span><span class="sxs-lookup"><span data-stu-id="94651-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94651-141">Hola SDK de Android nunca llama hello `endActivity()` método, incluso cuando se cierra la aplicación hello (en Android, las aplicaciones no son realmente nunca cerradas).</span><span class="sxs-lookup"><span data-stu-id="94651-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="94651-142">Por lo tanto, es *alta* recomienda hello toocall `startActivity()` método Hola `onResume` devolución de llamada de *todos los* sus actividades y hello `endActivity()` método Hola `onPause()` devolución de llamada de *todos los* sus actividades.</span><span class="sxs-lookup"><span data-stu-id="94651-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="94651-143">Se trata de toobe de manera única de hello seguro de que no se perderá las sesiones.</span><span class="sxs-lookup"><span data-stu-id="94651-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="94651-144">Si una sesión se ha filtrado, Hola servicio interacción nunca se desconectará de backend de interacción de hello (ya que servicio Hola permanece conectado mientras está pendiente una sesión).</span><span class="sxs-lookup"><span data-stu-id="94651-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="94651-145">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="94651-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="94651-146">Este toohello muy similar en el ejemplo se `EngagementActivity` clase y sus variantes, cuyo código fuente se proporciona en hello `src` carpeta.</span><span class="sxs-lookup"><span data-stu-id="94651-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="94651-147">Prueba</span><span class="sxs-lookup"><span data-stu-id="94651-147">Test</span></span>
<span data-ttu-id="94651-148">Ahora compruebe la integración mediante la ejecución su aplicación móvil en un dispositivo o emulador y comprobar que registra una sesión en la pestaña Monitor de Hola.</span><span class="sxs-lookup"><span data-stu-id="94651-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="94651-149">las secciones siguientes se Hola son opcionales.</span><span class="sxs-lookup"><span data-stu-id="94651-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="94651-150">Informes de ubicación</span><span class="sxs-lookup"><span data-stu-id="94651-150">Location reporting</span></span>
<span data-ttu-id="94651-151">Si desea toobe ubicaciones notificado, necesita tooadd unas pocas líneas de configuración (entre hello `<application>` y `</application>` etiquetas).</span><span class="sxs-lookup"><span data-stu-id="94651-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="94651-152">Informes de ubicaciones de áreas diferidas</span><span class="sxs-lookup"><span data-stu-id="94651-152">Lazy area location reporting</span></span>
<span data-ttu-id="94651-153">Informes de ubicación de área lenta permiten país de hello tooreport, región y localidad asociado toodevices.</span><span class="sxs-lookup"><span data-stu-id="94651-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="94651-154">Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI).</span><span class="sxs-lookup"><span data-stu-id="94651-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="94651-155">área de dispositivo de Hola se notifica como máximo una vez por sesión.</span><span class="sxs-lookup"><span data-stu-id="94651-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="94651-156">Hello GPS nunca se utiliza, y, por tanto, este tipo de informe de ubicación tiene muy pocas (no toosay ningún) impacto en la batería de Hola.</span><span class="sxs-lookup"><span data-stu-id="94651-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="94651-157">Áreas notificadas son toocompute usado geográfica estadísticas acerca de los usuarios, sesiones, eventos y errores.</span><span class="sxs-lookup"><span data-stu-id="94651-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="94651-158">También se pueden usar como criterios en campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="94651-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="94651-159">ubicación de área lenta tooenable reporting, puede hacerlo mediante la configuración de Hola se mencionó anteriormente en este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="94651-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="94651-160">También necesita hello tooadd después permiso si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="94651-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="94651-161">O bien, puede seguir usando ``ACCESS_FINE_LOCATION`` si ya lo usa en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94651-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="94651-162">Informes de ubicación en tiempo real</span><span class="sxs-lookup"><span data-stu-id="94651-162">Real time location reporting</span></span>
<span data-ttu-id="94651-163">Informes de ubicación en tiempo real permiten asociada de latitud y tooreport hello toodevices.</span><span class="sxs-lookup"><span data-stu-id="94651-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="94651-164">De forma predeterminada, este tipo de informes de ubicación sólo usa ubicaciones de red (basadas en el identificador de la celda o Wi-Fi) y reporting Hola solo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="94651-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="94651-165">Ubicaciones de tiempo real son *no* utiliza las estadísticas de toocompute.</span><span class="sxs-lookup"><span data-stu-id="94651-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="94651-166">Su único propósito es el uso de Hola de tooallow de barrera geográfica en tiempo real \<perímetro de audiencia de Reach\> criterio de campañas.</span><span class="sxs-lookup"><span data-stu-id="94651-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="94651-167">ubicación en tiempo real de tooenable reporting, puede hacerlo mediante la configuración de Hola se mencionó anteriormente en este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="94651-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="94651-168">También necesita hello tooadd después permiso si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="94651-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="94651-169">O bien, puede seguir usando ``ACCESS_FINE_LOCATION`` si ya lo usa en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="94651-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="94651-170">Informes basados en GPS</span><span class="sxs-lookup"><span data-stu-id="94651-170">GPS based reporting</span></span>
<span data-ttu-id="94651-171">De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red.</span><span class="sxs-lookup"><span data-stu-id="94651-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="94651-172">uso de hello tooenable de GPS basadas ubicaciones (que son mucho más precisas), use el objeto de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="94651-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="94651-173">También necesita hello tooadd después permiso si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="94651-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="94651-174">Informes en segundo plano</span><span class="sxs-lookup"><span data-stu-id="94651-174">Background reporting</span></span>
<span data-ttu-id="94651-175">De forma predeterminada, el informes de ubicación en tiempo real sólo está activa cuando la aplicación hello se ejecuta en primer plano (es decir, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="94651-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="94651-176">tooenable Hola reporting también en segundo plano, use el objeto de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="94651-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="94651-177">Cuando la aplicación hello se ejecuta en segundo plano, se notifican únicas ubicaciones a basados en red, incluso si ha habilitado Hola GPS.</span><span class="sxs-lookup"><span data-stu-id="94651-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="94651-178">informes de ubicación de fondo de Hola se detendrá si el usuario de hello su dispositivo reinicia, puede agregar este toomake reiniciará automáticamente al arrancar el sistema:</span><span class="sxs-lookup"><span data-stu-id="94651-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="94651-179">También necesita hello tooadd después permiso si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="94651-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="94651-180">Permisos de Android M</span><span class="sxs-lookup"><span data-stu-id="94651-180">Android M permissions</span></span>
<span data-ttu-id="94651-181">A partir de Android M, algunos permisos se administran en tiempo de ejecución y se necesita la aprobación del usuario.</span><span class="sxs-lookup"><span data-stu-id="94651-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="94651-182">permisos de Hello en tiempo de ejecución se desactivará de forma predeterminada para las nuevas instalaciones de aplicación si el destino es el nivel de API de Android 23.</span><span class="sxs-lookup"><span data-stu-id="94651-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="94651-183">De lo contrario, se activan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="94651-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="94651-184">usuario de Hello puede habilitar o deshabilitar los permisos desde el menú de configuración del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="94651-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="94651-185">Al desactivar los permisos en el menú de sistema elimina procesos en segundo plano de la aplicación hello, esto es un comportamiento del sistema y no tiene ningún efecto en la capacidad de inserción de tooreceive en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="94651-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="94651-186">En el contexto de Hola de Mobile Engagement, permisos de Hola que necesiten la aprobación en tiempo de ejecución son:</span><span class="sxs-lookup"><span data-stu-id="94651-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="94651-187">`WRITE_EXTERNAL_STORAGE` (solo cuando el destino es la API de Android nivel 23)</span><span class="sxs-lookup"><span data-stu-id="94651-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="94651-188">almacenamiento externo de Hola se usa solo para la característica de panorama general de alcance.</span><span class="sxs-lookup"><span data-stu-id="94651-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="94651-189">Si encuentra pidiendo a los usuarios este toobe permiso potencialmente perjudiciales, se puede quitar si se usa solo para Mobile Engagement, pero al costo de Hola de deshabilitar la característica de imagen grande.</span><span class="sxs-lookup"><span data-stu-id="94651-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="94651-190">Para las características de la ubicación de hello, debe solicitar toouser permisos mediante un cuadro de diálogo estándar del sistema.</span><span class="sxs-lookup"><span data-stu-id="94651-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="94651-191">Si se aprueba el usuario hello, necesita tootell ``EngagementAgent`` tootake que cambian en cuenta en tiempo real (cambio de hello en caso contrario será procesado Hola siguiente Hola usuario inicia Hola aplicación en tiempo de).</span><span class="sxs-lookup"><span data-stu-id="94651-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="94651-192">Este es un toouse de ejemplo de código en una actividad de los permisos de aplicación toorequest y el resultado de hello hacia delante, si es positivo demasiado``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="94651-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="94651-193">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="94651-193">Advanced reporting</span></span>
<span data-ttu-id="94651-194">Opcionalmente, si desea eventos específicos de aplicación tooreport, errores y trabajos, debe toouse Hola API de interacción a través de métodos de Hola de hello `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="94651-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="94651-195">Un objeto de esta clase puede ser recuperó por llamada hello `EngagementAgent.getInstance()` método estático.</span><span class="sxs-lookup"><span data-stu-id="94651-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="94651-196">permite todas las capacidades avanzadas de contratación toouse Hello API de contratación y se detalla cómo Hola tooUse la API de interacción en Android (así como en la documentación técnica de Hola de hello `EngagementAgent` clase).</span><span class="sxs-lookup"><span data-stu-id="94651-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="94651-197">Configuración avanzada (en AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="94651-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="94651-198">Reactivar bloqueos</span><span class="sxs-lookup"><span data-stu-id="94651-198">Wake locks</span></span>
<span data-ttu-id="94651-199">Si desea toobe seguro de que se envían las estadísticas en tiempo real cuando el uso de Wi-Fi o cuando la pantalla de bienvenida está desactivada, agregar Hola después permiso opcional:</span><span class="sxs-lookup"><span data-stu-id="94651-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="94651-200">Informe de bloqueos</span><span class="sxs-lookup"><span data-stu-id="94651-200">Crash report</span></span>
<span data-ttu-id="94651-201">Si desea que los informes de bloqueo toodisable, agregue esta (entre hello `<application>` y `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="94651-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="94651-202">Umbral de ráfaga</span><span class="sxs-lookup"><span data-stu-id="94651-202">Burst threshold</span></span>
<span data-ttu-id="94651-203">De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="94651-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="94651-204">Si la aplicación informa de los registros con mucha frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (Esto se denomina hello "modo de ráfaga").</span><span class="sxs-lookup"><span data-stu-id="94651-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="94651-205">toodo, por lo tanto, agregue esta (entre hello `<application>` y `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="94651-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="94651-206">Hello el modo de ráfaga incremente ligeramente batería Hola vida pero tiene un impacto en hello Monitor de contratación: duración de las sesiones y los trabajos de todos los será redondeado toohello ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible).</span><span class="sxs-lookup"><span data-stu-id="94651-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="94651-207">Es recomendable toouse ya no es un umbral de ráfaga de 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="94651-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="94651-208">Tiempo de espera de sesión</span><span class="sxs-lookup"><span data-stu-id="94651-208">Session timeout</span></span>
<span data-ttu-id="94651-209">De forma predeterminada, una sesión es 10s finaliza después del final de Hola de su última actividad (que normalmente se produce al presionar Hola inicio o hacer copia de clave, por teléfono de hello establecer inactivo o saltar a otra aplicación).</span><span class="sxs-lookup"><span data-stu-id="94651-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="94651-210">Se trata de tooavoid una división de sesión cada vez que lo utiliza Hola salir y devolver rápidamente la aplicación de toohello (que puede ocurrir cuando recoge una imagen, comprobar una notificación, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="94651-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="94651-211">Puede que desee toomodify este parámetro.</span><span class="sxs-lookup"><span data-stu-id="94651-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="94651-212">toodo, por lo tanto, agregue esta (entre hello `<application>` y `</application>` etiquetas):</span><span class="sxs-lookup"><span data-stu-id="94651-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="94651-213">Deshabilitación de los informes de registro</span><span class="sxs-lookup"><span data-stu-id="94651-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="94651-214">Mediante una llamada al método</span><span class="sxs-lookup"><span data-stu-id="94651-214">Using a method call</span></span>
<span data-ttu-id="94651-215">Si desea enviar registros de toostop de interacción, puede llamar:</span><span class="sxs-lookup"><span data-stu-id="94651-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="94651-216">Esta llamada es persistente: usa un archivo de preferencias compartido.</span><span class="sxs-lookup"><span data-stu-id="94651-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="94651-217">Si la interacción está activa cuando se llama a esta función, puede tardar 1 minuto para hello toostop de servicio.</span><span class="sxs-lookup"><span data-stu-id="94651-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="94651-218">Sin embargo no inicie la próxima vez que inicia la aplicación hello servicio hello en hello todos los.</span><span class="sxs-lookup"><span data-stu-id="94651-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="94651-219">Puede habilitar el registro de reporting nuevo mediante una llamada a Hola la misma función con `true`.</span><span class="sxs-lookup"><span data-stu-id="94651-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="94651-220">Integración en su propia `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="94651-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="94651-221">En lugar de llamar a esta función, también puede integrar este valor directamente en su `PreferenceActivity` existente.</span><span class="sxs-lookup"><span data-stu-id="94651-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="94651-222">Puede configurar toouse de contratación sus preferencias de archivo (con el modo deseado de hello) de hello `AndroidManifest.xml` de archivos con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="94651-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="94651-223">Hola `engagement:agent:settings:name` clave es toodefine usado Hola nombre de archivo de preferencias compartidas hello.</span><span class="sxs-lookup"><span data-stu-id="94651-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="94651-224">Hola `engagement:agent:settings:mode` clave es modo de hello toodefine utilizado del archivo de preferencias compartidas hello, debe usar hello mismo modo que en su `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="94651-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="94651-225">modo de saludo se debe pasar como un número: Si usas una combinación de marcas de constantes en el código, compruebe el valor total de Hola.</span><span class="sxs-lookup"><span data-stu-id="94651-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="94651-226">Interacción siempre usar hello `engagement:key` booleano clave en el archivo de preferencias de Hola para administrar esta configuración.</span><span class="sxs-lookup"><span data-stu-id="94651-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="94651-227">Hola siguiendo el ejemplo de `AndroidManifest.xml` muestra Hola valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="94651-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="94651-228">A continuación, puede agregar un `CheckBoxPreference` en el diseño de preferencias como Hola sigue uno:</span><span class="sxs-lookup"><span data-stu-id="94651-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
