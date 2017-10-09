---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
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
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a><span data-ttu-id="d8901-103">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="d8901-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="d8901-104">4.3.1 (17/07/2017)</span><span class="sxs-lookup"><span data-stu-id="d8901-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="d8901-105">Se ha corregido un bloqueo que rara vez puede suceder cuando se llama a `EngagementAgentUtils.isInDedicatedEngagementProcess`, que también usan hello `EngagementApplication` clase.</span><span class="sxs-lookup"><span data-stu-id="d8901-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="d8901-106">4.3.0 (27/06/2017)</span><span class="sxs-lookup"><span data-stu-id="d8901-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="d8901-107">Android admiten 8 (versiones anteriores de hello SDK no funcionarán en Android 8).</span><span class="sxs-lookup"><span data-stu-id="d8901-107">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="d8901-108">Desaparece la dependencia de la biblioteca de soporte.</span><span class="sxs-lookup"><span data-stu-id="d8901-108">No more dependency on support library.</span></span>
* <span data-ttu-id="d8901-109">Se quita la clase `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="d8901-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="d8901-110">Vencimiento demasiado[límites de la ejecución de fondo](https://developer.android.com/preview/features/background.html) en 8 Android, registros en segundo plano se retrasa hasta que el usuario de hello interactúa con el dispositivo de hello, esto tendrá un impacto en la campaña de inserción **entregados** y **Notificación del sistema mostrada** estadísticas que se retrasa si se encontraba inactivo el dispositivo hello (Hola notificación seguirán mostrándose, se anillo y Vibrar en tiempo real sin problemas).</span><span class="sxs-lookup"><span data-stu-id="d8901-110">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="d8901-111">Vencimiento demasiado[límites de ubicación de fondo](https://developer.android.com/preview/features/background-location-limits.html), ubicación de tiempo real de hello en segundo plano no se actualizará con frecuencia en 8 Android.</span><span class="sxs-lookup"><span data-stu-id="d8901-111">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="d8901-112">4.2.4 (30/03/2017)</span><span class="sxs-lookup"><span data-stu-id="d8901-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="d8901-113">Corregir la notificación en la aplicación Hola colores de texto en 7 Android toobe igual que en versiones anteriores de Android.</span><span class="sxs-lookup"><span data-stu-id="d8901-113">Fix in-app notification text colors on Android 7 toobe hello same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="d8901-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="d8901-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="d8901-115">No se producirán más bloqueos de WiFi.</span><span class="sxs-lookup"><span data-stu-id="d8901-115">No more WIFI lock.</span></span>
* <span data-ttu-id="d8901-116">Se ha corregido un interbloqueo al llamar a getDeviceId antes de init (error de la versión 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="d8901-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="d8901-117">4.2.2 (17/05/2016)</span><span class="sxs-lookup"><span data-stu-id="d8901-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="d8901-118">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="d8901-119">4.2.1 (10/05/2016)</span><span class="sxs-lookup"><span data-stu-id="d8901-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="d8901-120">Seguridad: deshabilite el acceso a archivos locales de la vista web.</span><span class="sxs-lookup"><span data-stu-id="d8901-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="d8901-121">Seguridad: quite la clase `EngagementPreferenceActivity` que extiende la clase `PreferenceActivity` no segura y obsoleta.</span><span class="sxs-lookup"><span data-stu-id="d8901-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="d8901-122">Seguridad: alcance actividades ahora están documentados toouse `exported="false"`, esta marca también puede usarse en versiones anteriores del SDK.</span><span class="sxs-lookup"><span data-stu-id="d8901-122">Security: reach activities are now documented toouse `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="d8901-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="d8901-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="d8901-124">Hola SDK ahora con licencia bajo MIT.</span><span class="sxs-lookup"><span data-stu-id="d8901-124">hello SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="d8901-125">Permite especificar un identificador de dispositivo personalizado en el tiempo de inicialización del SDK.</span><span class="sxs-lookup"><span data-stu-id="d8901-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="d8901-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="d8901-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="d8901-127">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="d8901-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="d8901-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="d8901-129">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="d8901-130">4.1.3 (9/12/2015)</span><span class="sxs-lookup"><span data-stu-id="d8901-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="d8901-131">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="d8901-132">4.1.2 (25/11/2015)</span><span class="sxs-lookup"><span data-stu-id="d8901-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="d8901-133">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="d8901-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="d8901-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="d8901-135">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="d8901-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="d8901-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="d8901-137">Controle el nuevo modelo de permiso para Android M.</span><span class="sxs-lookup"><span data-stu-id="d8901-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="d8901-138">Ahora puede configurar las características de ubicación en tiempo de ejecución en lugar de usar `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d8901-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="d8901-139">Corrija un error de permiso: si usa `ACCESS_FINE_LOCATION`, ya no necesita `ACCESS_COARSE_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="d8901-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="d8901-140">Mejoras de estabilidad.</span><span class="sxs-lookup"><span data-stu-id="d8901-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="d8901-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="d8901-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="d8901-142">Protocolo interno cambia toomake análisis y más confiable de inserción.</span><span class="sxs-lookup"><span data-stu-id="d8901-142">Internal protocol changes toomake analytics and push more reliable.</span></span>
* <span data-ttu-id="d8901-143">Inserción nativa (GCM/ADM) ahora también se utiliza para las notificaciones en aplicación por lo que debe configurar credenciales de inserción nativa de Hola para cualquier tipo de campaña de inserción.</span><span class="sxs-lookup"><span data-stu-id="d8901-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="d8901-144">Corrección de la notificación con imagen grande: se mostraban solo 10 s después de insertarse.</span><span class="sxs-lookup"><span data-stu-id="d8901-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="d8901-145">Corregir un error en la vista web: al hacer clic en un vínculo también estaba ejecutando la URL de acción predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8901-145">Fix a bug in web view: clicking on a link was also executing hello default action URL.</span></span>
* <span data-ttu-id="d8901-146">Se ha corregido un bloqueo excepcional relacionados con la administración de almacenamiento de toolocal.</span><span class="sxs-lookup"><span data-stu-id="d8901-146">Fix a rare crash related toolocal storage management.</span></span>
* <span data-ttu-id="d8901-147">Corrección de la administración dinámica de cadenas de configuración.</span><span class="sxs-lookup"><span data-stu-id="d8901-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="d8901-148">Actualización del CLUF.</span><span class="sxs-lookup"><span data-stu-id="d8901-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="d8901-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="d8901-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="d8901-150">Versión inicial de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8901-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="d8901-151">La configuración de appID se reemplaza por una configuración de cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="d8901-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="d8901-152">Quitar toosend de API y recibir mensajes XMPP arbitrarios de entidades XMPP arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="d8901-152">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="d8901-153">Quitar toosend de API y recibir mensajes entre los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d8901-153">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="d8901-154">Mejoras de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d8901-154">Security improvements.</span></span>
* <span data-ttu-id="d8901-155">Seguimiento de SmartAd y Google Play eliminados.</span><span class="sxs-lookup"><span data-stu-id="d8901-155">Google Play and SmartAd tracking removed.</span></span>

