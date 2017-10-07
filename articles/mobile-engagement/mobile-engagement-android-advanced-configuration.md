---
title: "configuración de aaaAdvanced de Azure Mobile Engagement SDK de Android"
description: "Describe Hola incluidos Hola manifiesto Android con Azure Mobile Engagement Android SDK de opciones de configuración avanzada"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="160cd-103">Configuración avanzada para el SDK de Android para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="160cd-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="160cd-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="160cd-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="160cd-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="160cd-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="160cd-106">iOS</span><span class="sxs-lookup"><span data-stu-id="160cd-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="160cd-107">Android</span><span class="sxs-lookup"><span data-stu-id="160cd-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="160cd-108">Este procedimiento describe cómo tooconfigure distintas opciones de configuración para las aplicaciones de Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="160cd-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="160cd-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="160cd-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="160cd-110">Requisitos de permiso</span><span class="sxs-lookup"><span data-stu-id="160cd-110">Permission Requirements</span></span>
<span data-ttu-id="160cd-111">Algunas opciones requieren permisos específicos, todos ellos se enumeran aquí para referencia y en línea en la característica específica de Hola.</span><span class="sxs-lookup"><span data-stu-id="160cd-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="160cd-112">Agregar estos toohello permisos AndroidManifest.xml del proyecto inmediatamente antes o después de hello `<application>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="160cd-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="160cd-113">código de Hello permiso debe toolook como Hola siguiente, donde se cumplimentan permiso adecuado de Hola de tabla de Hola que sigue.</span><span class="sxs-lookup"><span data-stu-id="160cd-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="160cd-114">Permiso</span><span class="sxs-lookup"><span data-stu-id="160cd-114">Permission</span></span> | <span data-ttu-id="160cd-115">Cuándo se usa</span><span class="sxs-lookup"><span data-stu-id="160cd-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="160cd-116">INTERNET</span><span class="sxs-lookup"><span data-stu-id="160cd-116">INTERNET</span></span> |<span data-ttu-id="160cd-117">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="160cd-117">Required.</span></span> <span data-ttu-id="160cd-118">Para informes básicos</span><span class="sxs-lookup"><span data-stu-id="160cd-118">For basic reporting</span></span> |
| <span data-ttu-id="160cd-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="160cd-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="160cd-120">Obligatorio.</span><span class="sxs-lookup"><span data-stu-id="160cd-120">Required.</span></span> <span data-ttu-id="160cd-121">Para informes básicos</span><span class="sxs-lookup"><span data-stu-id="160cd-121">For basic reporting</span></span> |
| <span data-ttu-id="160cd-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="160cd-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="160cd-123">Necesario.</span><span class="sxs-lookup"><span data-stu-id="160cd-123">Required.</span></span> <span data-ttu-id="160cd-124">tooshow el centro de notificaciones de hello tras el reinicio del dispositivo</span><span class="sxs-lookup"><span data-stu-id="160cd-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="160cd-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="160cd-125">WAKE_LOCK</span></span> |<span data-ttu-id="160cd-126">Se recomienda su uso.</span><span class="sxs-lookup"><span data-stu-id="160cd-126">Recommended.</span></span> <span data-ttu-id="160cd-127">Habilita la recopilación de datos cuando se usa la conexión WiFi o cuando la pantalla está apagada</span><span class="sxs-lookup"><span data-stu-id="160cd-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="160cd-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="160cd-128">VIBRATE</span></span> |<span data-ttu-id="160cd-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="160cd-129">Optional.</span></span> <span data-ttu-id="160cd-130">Habilita la vibración cuando se reciben las notificaciones</span><span class="sxs-lookup"><span data-stu-id="160cd-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="160cd-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="160cd-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="160cd-132">Opcional.</span><span class="sxs-lookup"><span data-stu-id="160cd-132">Optional.</span></span> <span data-ttu-id="160cd-133">Habilita la notificación de panorama general de Android</span><span class="sxs-lookup"><span data-stu-id="160cd-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="160cd-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="160cd-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="160cd-135">Opcional.</span><span class="sxs-lookup"><span data-stu-id="160cd-135">Optional.</span></span> <span data-ttu-id="160cd-136">Habilita la notificación de panorama general de Android</span><span class="sxs-lookup"><span data-stu-id="160cd-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="160cd-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="160cd-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="160cd-138">Opcional.</span><span class="sxs-lookup"><span data-stu-id="160cd-138">Optional.</span></span> <span data-ttu-id="160cd-139">Habilita los informes de ubicación en tiempo real</span><span class="sxs-lookup"><span data-stu-id="160cd-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="160cd-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="160cd-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="160cd-141">Opcional.</span><span class="sxs-lookup"><span data-stu-id="160cd-141">Optional.</span></span> <span data-ttu-id="160cd-142">Habilita los informes de ubicación basados en GPS</span><span class="sxs-lookup"><span data-stu-id="160cd-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="160cd-143">A partir de Android M, [algunos permisos se administran en tiempo de ejecución](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="160cd-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="160cd-144">Si ya usas ``ACCESS_FINE_LOCATION``, es necesario tooalso usar ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="160cd-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="160cd-145">Opciones de configuración del manifiesto de Android</span><span class="sxs-lookup"><span data-stu-id="160cd-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="160cd-146">Informe de bloqueos</span><span class="sxs-lookup"><span data-stu-id="160cd-146">Crash report</span></span>
<span data-ttu-id="160cd-147">informes de bloqueo de toodisable, agregue este código entre hello `<application>` y `</application>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="160cd-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="160cd-148">Umbral de ráfaga</span><span class="sxs-lookup"><span data-stu-id="160cd-148">Burst threshold</span></span>
<span data-ttu-id="160cd-149">De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="160cd-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="160cd-150">Si los registros de informe de aplicaciones varían con frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (denominada "irrumpir modo").</span><span class="sxs-lookup"><span data-stu-id="160cd-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="160cd-151">toodo por lo tanto, agregue este código entre hello `<application>` y `</application>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="160cd-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="160cd-152">El modo de ráfaga ligeramente aumenta la duración de la batería de hello pero tiene un impacto en el Monitor de interacción de hello: duración de las sesiones y los trabajos de todos los son toohello redondeado ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible).</span><span class="sxs-lookup"><span data-stu-id="160cd-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="160cd-153">El umbral de ráfaga no debe ser superior a 30 000 (30 segundos).</span><span class="sxs-lookup"><span data-stu-id="160cd-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="160cd-154">Tiempo de espera de sesión</span><span class="sxs-lookup"><span data-stu-id="160cd-154">Session timeout</span></span>
 <span data-ttu-id="160cd-155">Para terminar una actividad, al presionar hello **inicio** o **volver** clave, por teléfono de hello establecer inactivo o saltar a otra aplicación.</span><span class="sxs-lookup"><span data-stu-id="160cd-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="160cd-156">De forma predeterminada, una sesión se finaliza diez segundos después del final de Hola de su última actividad.</span><span class="sxs-lookup"><span data-stu-id="160cd-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="160cd-157">Esto evita una división de sesión cada vez que lo utiliza Hola cierre y devuelva toohello aplicación rápidamente, lo que puede ocurrir cuando el usuario de hello recoge una imagen, comprueba una notificación, etcetera. Puede que desee toomodify este parámetro.</span><span class="sxs-lookup"><span data-stu-id="160cd-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="160cd-158">toodo por lo tanto, agregue este código entre hello `<application>` y `</application>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="160cd-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="160cd-159">Deshabilitación de los informes de registro</span><span class="sxs-lookup"><span data-stu-id="160cd-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="160cd-160">Mediante una llamada al método</span><span class="sxs-lookup"><span data-stu-id="160cd-160">Using a method call</span></span>
<span data-ttu-id="160cd-161">Si desea enviar registros de toostop de interacción, puede llamar:</span><span class="sxs-lookup"><span data-stu-id="160cd-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="160cd-162">Esta llamada es persistente: usa un archivo de preferencias compartido.</span><span class="sxs-lookup"><span data-stu-id="160cd-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="160cd-163">Si la interacción está activa cuando se llama a esta función, puede tardar un minuto para hello toostop de servicio.</span><span class="sxs-lookup"><span data-stu-id="160cd-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="160cd-164">Sin embargo no inicie la próxima vez que inicia la aplicación hello servicio hello en hello todos los.</span><span class="sxs-lookup"><span data-stu-id="160cd-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="160cd-165">Puede habilitar el registro de reporting nuevo mediante una llamada a Hola la misma función con `true`.</span><span class="sxs-lookup"><span data-stu-id="160cd-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="160cd-166">Integración en su propia `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="160cd-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="160cd-167">En lugar de llamar a esta función, también puede integrar este valor directamente en su `PreferenceActivity` existente.</span><span class="sxs-lookup"><span data-stu-id="160cd-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="160cd-168">Puede configurar toouse de contratación sus preferencias de archivo (con el modo deseado de hello) de hello `AndroidManifest.xml` de archivos con `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="160cd-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="160cd-169">Hola `engagement:agent:settings:name` clave es toodefine usado Hola nombre de archivo de preferencias compartidas hello.</span><span class="sxs-lookup"><span data-stu-id="160cd-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="160cd-170">Hola `engagement:agent:settings:mode` clave es el modo de Hola de toodefine utilizado del archivo de preferencias compartidas Hola.</span><span class="sxs-lookup"><span data-stu-id="160cd-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="160cd-171">Use Hola mismo modo que en su `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="160cd-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="160cd-172">modo de saludo se debe pasar como un número: Si usas una combinación de marcas de constantes en el código, compruebe el valor total de Hola.</span><span class="sxs-lookup"><span data-stu-id="160cd-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="160cd-173">Interacción siempre utiliza hello `engagement:key` booleano clave en el archivo de preferencias de Hola para administrar esta configuración.</span><span class="sxs-lookup"><span data-stu-id="160cd-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="160cd-174">Hola siguiendo el ejemplo de `AndroidManifest.xml` muestra Hola valores predeterminados:</span><span class="sxs-lookup"><span data-stu-id="160cd-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="160cd-175">A continuación, puede agregar un `CheckBoxPreference` en el diseño de preferencias como Hola sigue uno:</span><span class="sxs-lookup"><span data-stu-id="160cd-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
