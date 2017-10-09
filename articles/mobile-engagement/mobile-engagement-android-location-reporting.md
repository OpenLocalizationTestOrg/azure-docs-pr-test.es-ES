---
title: aaaLocation Reporting de Azure Mobile Engagement SDK de Android
description: "Describe cómo ubicación tooconfigure reporting de Azure Mobile Engagement SDK de Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="edad3-103">Informes de ubicación para el SDK de Android para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="edad3-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="edad3-104">Android</span><span class="sxs-lookup"><span data-stu-id="edad3-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="edad3-105">Este tema se describe cómo ubicación toodo reporting para su aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="edad3-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edad3-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="edad3-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="edad3-107">Informes de ubicación</span><span class="sxs-lookup"><span data-stu-id="edad3-107">Location reporting</span></span>
<span data-ttu-id="edad3-108">Si desea toobe ubicaciones notificado, necesita tooadd unas pocas líneas de configuración (entre hello `<application>` y `</application>` etiquetas).</span><span class="sxs-lookup"><span data-stu-id="edad3-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="edad3-109">Informes de ubicaciones de áreas diferidas</span><span class="sxs-lookup"><span data-stu-id="edad3-109">Lazy area location reporting</span></span>
<span data-ttu-id="edad3-110">Informes de ubicación de área lenta permiten informes país hello, región y localidad asociados con los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="edad3-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="edad3-111">Este tipo de informe de ubicación sólo emplea ubicaciones de red (basadas en el identificador del teléfono móvil o en WIFI).</span><span class="sxs-lookup"><span data-stu-id="edad3-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="edad3-112">área de dispositivo de Hola se notifica como máximo una vez por sesión.</span><span class="sxs-lookup"><span data-stu-id="edad3-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="edad3-113">Hola GPS nunca se utiliza y, por tanto, este tipo de informe de ubicación tiene poca repercusión en batería Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="edad3-114">Áreas notificadas son toocompute usado geográfica estadísticas acerca de los usuarios, sesiones, eventos y errores.</span><span class="sxs-lookup"><span data-stu-id="edad3-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="edad3-115">También se pueden usar como criterios en campañas de cobertura.</span><span class="sxs-lookup"><span data-stu-id="edad3-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="edad3-116">Habilitar ubicación de área lenta informes mediante el uso de la configuración de Hola que se mencionó anteriormente en este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="edad3-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="edad3-117">También deberá toospecify un permiso de ubicación.</span><span class="sxs-lookup"><span data-stu-id="edad3-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="edad3-118">Este código usa el permiso ``COARSE`` :</span><span class="sxs-lookup"><span data-stu-id="edad3-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="edad3-119">Si la aplicación lo requiere, puede usar ``ACCESS_FINE_LOCATION`` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="edad3-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="edad3-120">Informes de ubicación en tiempo real</span><span class="sxs-lookup"><span data-stu-id="edad3-120">Real-time location reporting</span></span>
<span data-ttu-id="edad3-121">Informes de ubicación en tiempo real permiten informes Hola de latitud y longitud asociada a dispositivos.</span><span class="sxs-lookup"><span data-stu-id="edad3-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="edad3-122">Este tipo de informe de ubicación solo emplea ubicaciones de red basadas en el identificador del teléfono móvil o WiFi.</span><span class="sxs-lookup"><span data-stu-id="edad3-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="edad3-123">Hola reporting solo está activa cuando la aplicación hello se ejecuta en primer plano (por ejemplo, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="edad3-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="edad3-124">Ubicaciones en tiempo real son *no* utiliza las estadísticas de toocompute.</span><span class="sxs-lookup"><span data-stu-id="edad3-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="edad3-125">Su único propósito es el uso de Hola de tooallow de geovallado en tiempo real \<perímetro de audiencia de Reach\> criterio de campañas.</span><span class="sxs-lookup"><span data-stu-id="edad3-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="edad3-126">ubicación en tiempo real de tooenable informes, agregue una línea de código toowhere establece la cadena de conexión de interacción de hello en actividad del iniciador Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="edad3-127">resultado de Hello es similar a Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="edad3-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="edad3-128">Informes basados en GPS</span><span class="sxs-lookup"><span data-stu-id="edad3-128">GPS based reporting</span></span>
<span data-ttu-id="edad3-129">De forma predeterminada, los informes de ubicación en tiempo real solo emplean ubicaciones de red.</span><span class="sxs-lookup"><span data-stu-id="edad3-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="edad3-130">tooenable Hola de GPS-based ubicaciones, que son mucho más precisa, usar el objeto de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="edad3-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="edad3-131">También necesita hello tooadd después permiso si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="edad3-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="edad3-132">Informes en segundo plano</span><span class="sxs-lookup"><span data-stu-id="edad3-132">Background reporting</span></span>
<span data-ttu-id="edad3-133">De forma predeterminada, el informes de ubicación en tiempo real sólo está activa cuando la aplicación hello se ejecuta en primer plano (por ejemplo, durante una sesión).</span><span class="sxs-lookup"><span data-stu-id="edad3-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="edad3-134">Hola tooenable informes también en segundo plano, use este objeto de configuración:</span><span class="sxs-lookup"><span data-stu-id="edad3-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="edad3-135">Cuando la aplicación hello se ejecuta en segundo plano, ubicaciones basadas en red solo se notifican, incluso si ha habilitado Hola GPS.</span><span class="sxs-lookup"><span data-stu-id="edad3-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="edad3-136">Si el usuario de Hola que su dispositivo reinicie, informes de ubicación de fondo de Hola se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="edad3-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="edad3-137">toomake reiniciará automáticamente al arrancar el sistema, agregue este código.</span><span class="sxs-lookup"><span data-stu-id="edad3-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="edad3-138">También necesita hello tooadd después permiso si no se especifica:</span><span class="sxs-lookup"><span data-stu-id="edad3-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="edad3-139">Permisos de Android M</span><span class="sxs-lookup"><span data-stu-id="edad3-139">Android M permissions</span></span>
<span data-ttu-id="edad3-140">A partir de Android M, algunos permisos se administran en tiempo de ejecución y necesitan la aprobación del usuario.</span><span class="sxs-lookup"><span data-stu-id="edad3-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="edad3-141">Si su objetivo de nivel de API de Android 23, permisos de hello en tiempo de ejecución están desactivados de forma predeterminada para las nuevas instalaciones de aplicación.</span><span class="sxs-lookup"><span data-stu-id="edad3-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="edad3-142">De lo contrario, se activan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="edad3-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="edad3-143">Puede habilitar o deshabilitar los permisos desde el menú de configuración del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="edad3-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="edad3-144">Al desactivar los permisos del menú del sistema Hola elimina procesos en segundo plano Hola de aplicación hello, que es un comportamiento del sistema y no tiene ningún efecto en la capacidad de inserción de tooreceive en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="edad3-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="edad3-145">En el contexto de Hola de ubicación de Mobile Engagement reporting, los permisos de Hola que necesiten la aprobación en tiempo de ejecución son:</span><span class="sxs-lookup"><span data-stu-id="edad3-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="edad3-146">Solicitar permisos de usuario de hello mediante un cuadro de diálogo estándar del sistema.</span><span class="sxs-lookup"><span data-stu-id="edad3-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="edad3-147">Indicar si se aprueba el usuario hello, ``EngagementAgent`` tootake que cambian en cuenta en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="edad3-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="edad3-148">En caso contrario, cambio de hello es procesado Hola siguiente Hola usuario inicia Hola aplicación en tiempo de.</span><span class="sxs-lookup"><span data-stu-id="edad3-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="edad3-149">Este es un toouse de ejemplo de código en una actividad de los permisos de aplicación toorequest y el resultado de hello hacia delante, si es positivo demasiado``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="edad3-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
