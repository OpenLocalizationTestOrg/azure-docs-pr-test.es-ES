---
title: "Integración del SDK de Android para Azure Mobile Engagement"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="61c90-103">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="61c90-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="61c90-104">4.3.1 (17/07/2017)</span><span class="sxs-lookup"><span data-stu-id="61c90-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="61c90-105">Se ha corregido un bloqueo que rara vez se produce cuando se llama a `EngagementAgentUtils.isInDedicatedEngagementProcess`, que también se usa en la clase `EngagementApplication`.</span><span class="sxs-lookup"><span data-stu-id="61c90-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="61c90-106">4.3.0 (27/06/2017)</span><span class="sxs-lookup"><span data-stu-id="61c90-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="61c90-107">Compatibilidad con Android 8 (las versiones anteriores del SDK no funcionarán en Android 8).</span><span class="sxs-lookup"><span data-stu-id="61c90-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="61c90-108">Desaparece la dependencia de la biblioteca de soporte.</span><span class="sxs-lookup"><span data-stu-id="61c90-108">No more dependency on support library.</span></span>
* <span data-ttu-id="61c90-109">Se quita la clase `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="61c90-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="61c90-110">Debido a los [límites de ejecución en segundo plano](https://developer.android.com/preview/features/background.html) en Android 8, puede que los registros en segundo plano se retrasen hasta que el usuario interactúe con el dispositivo, lo que provocará que las estadísticas sobre la campaña de inserción **entregada** y la **notificación del sistema mostrada** se retrasen si el dispositivo estaba en suspensión (la notificación se mostrará, sonará y vibrará en tiempo real sin problemas).</span><span class="sxs-lookup"><span data-stu-id="61c90-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="61c90-111">Debido a los [límites de ubicación en segundo plano](https://developer.android.com/preview/features/background-location-limits.html), la ubicación en tiempo real en segundo plano no se actualizará con frecuencia en Android 8.</span><span class="sxs-lookup"><span data-stu-id="61c90-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="61c90-112">4.2.4 (30/03/2017)</span><span class="sxs-lookup"><span data-stu-id="61c90-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="61c90-113">Se han corregido los colores del texto de notificación en aplicación de Android 7 para que coincidan con los de las versiones anteriores de Android.</span><span class="sxs-lookup"><span data-stu-id="61c90-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="61c90-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="61c90-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="61c90-115">No se producirán más bloqueos de WiFi.</span><span class="sxs-lookup"><span data-stu-id="61c90-115">No more WIFI lock.</span></span>
* <span data-ttu-id="61c90-116">Se ha corregido un interbloqueo al llamar a getDeviceId antes de init (error de la versión 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="61c90-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="61c90-117">4.2.2 (17/05/2016)</span><span class="sxs-lookup"><span data-stu-id="61c90-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="61c90-118">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="61c90-119">4.2.1 (10/05/2016)</span><span class="sxs-lookup"><span data-stu-id="61c90-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="61c90-120">Seguridad: deshabilite el acceso a archivos locales de la vista web.</span><span class="sxs-lookup"><span data-stu-id="61c90-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="61c90-121">Seguridad: quite la clase `EngagementPreferenceActivity` que extiende la clase `PreferenceActivity` no segura y obsoleta.</span><span class="sxs-lookup"><span data-stu-id="61c90-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="61c90-122">Seguridad: las actividades de cobertura están ahora documentadas para usar `exported="false"`, esta marca puede usarse también en versiones del SDK anteriores.</span><span class="sxs-lookup"><span data-stu-id="61c90-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="61c90-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="61c90-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="61c90-124">El SDK tiene una licencia de MIT.</span><span class="sxs-lookup"><span data-stu-id="61c90-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="61c90-125">Permite especificar un identificador de dispositivo personalizado en el tiempo de inicialización del SDK.</span><span class="sxs-lookup"><span data-stu-id="61c90-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="61c90-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="61c90-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="61c90-127">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="61c90-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="61c90-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="61c90-129">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="61c90-130">4.1.3 (9/12/2015)</span><span class="sxs-lookup"><span data-stu-id="61c90-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="61c90-131">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="61c90-132">4.1.2 (25/11/2015)</span><span class="sxs-lookup"><span data-stu-id="61c90-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="61c90-133">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="61c90-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="61c90-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="61c90-135">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="61c90-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="61c90-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="61c90-137">Controle el nuevo modelo de permiso para Android M.</span><span class="sxs-lookup"><span data-stu-id="61c90-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="61c90-138">Ahora puede configurar las características de ubicación en tiempo de ejecución en lugar de usar `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="61c90-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="61c90-139">Corrija un error de permiso: si usa `ACCESS_FINE_LOCATION`, ya no necesita `ACCESS_COARSE_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="61c90-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="61c90-140">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="61c90-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="61c90-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="61c90-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="61c90-142">Cambios en el protocolo interno para que la inserción y los análisis sean más confiables.</span><span class="sxs-lookup"><span data-stu-id="61c90-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="61c90-143">La inserción nativa (GCM/ADM) ahora también se usa para notificaciones dentro de la aplicación, por lo que debe configurar las credenciales de inserción nativas para cualquier tipo de campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="61c90-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="61c90-144">Corrección de la notificación con imagen grande: se mostraban solo 10 s después de insertarse.</span><span class="sxs-lookup"><span data-stu-id="61c90-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="61c90-145">Corrección de un error en la vista web: al hacer clic en un vínculo, también se ejecutaba la URL de la acción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="61c90-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="61c90-146">Corrección de un bloqueo excepcional relacionado con la administración del almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="61c90-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="61c90-147">Corrección de la administración dinámica de cadenas de configuración.</span><span class="sxs-lookup"><span data-stu-id="61c90-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="61c90-148">Actualización del CLUF.</span><span class="sxs-lookup"><span data-stu-id="61c90-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="61c90-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="61c90-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="61c90-150">Versión inicial de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="61c90-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="61c90-151">La configuración de appID se reemplaza por una configuración de cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="61c90-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="61c90-152">Se ha eliminado la API para enviar y recibir mensajes XMPP arbitrarios de entidades XMPP arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="61c90-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="61c90-153">Se ha eliminado la API para enviar y recibir mensajes entre dispositivos.</span><span class="sxs-lookup"><span data-stu-id="61c90-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="61c90-154">Mejoras de seguridad.</span><span class="sxs-lookup"><span data-stu-id="61c90-154">Security improvements.</span></span>
* <span data-ttu-id="61c90-155">Seguimiento de SmartAd y Google Play eliminados.</span><span class="sxs-lookup"><span data-stu-id="61c90-155">Google Play and SmartAd tracking removed.</span></span>

