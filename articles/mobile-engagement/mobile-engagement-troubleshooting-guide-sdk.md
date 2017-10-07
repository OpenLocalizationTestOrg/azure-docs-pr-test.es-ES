---
title: aaaAzure Mobile Engagement Troubleshooting Guide - SDK
description: "Solución de problemas de integración de SDK en Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="16ae7-103">Guía de solución de problemas de la integración de SDK</span><span class="sxs-lookup"><span data-stu-id="16ae7-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="16ae7-104">los siguientes Hola son posibles problemas que pueden producirse con cómo se integra Azure Mobile Engagement en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16ae7-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="16ae7-105">Problemas SDK descubiertos por un error en otra área de la aplicación</span><span class="sxs-lookup"><span data-stu-id="16ae7-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="16ae7-106">Problema</span><span class="sxs-lookup"><span data-stu-id="16ae7-106">Issue</span></span>
* <span data-ttu-id="16ae7-107">Error de colección de datos de interfaz de usuario (en el análisis, supervisión, segmentación o paneles).</span><span class="sxs-lookup"><span data-stu-id="16ae7-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="16ae7-108">Errores de inserción (las inserciones no funcionan en la aplicación, fuera de la aplicación o en ambos).</span><span class="sxs-lookup"><span data-stu-id="16ae7-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="16ae7-109">Fallos de función avanzados (no funcionan el seguimiento, la geolocalización o las inserciones específicas de plataforma).</span><span class="sxs-lookup"><span data-stu-id="16ae7-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="16ae7-110">Errores de la API (las API fallan a menudo de manera silenciosa sin que se muestren mensajes de error).</span><span class="sxs-lookup"><span data-stu-id="16ae7-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="16ae7-111">Errores del servicio (ninguno de los Azure Mobile Engagement funciona para su aplicación).</span><span class="sxs-lookup"><span data-stu-id="16ae7-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="16ae7-112">Causas</span><span class="sxs-lookup"><span data-stu-id="16ae7-112">Causes</span></span>
* <span data-ttu-id="16ae7-113">Un error en la aplicación (por ejemplo, un error de recopilación de datos de interfaz de usuario, error de inserción, fallos de las funciones avanzadas, error de la API, bloqueos de la aplicación o servicio aparente detectará la mayoría de los problemas que deben toobe resuelto con hello Azure Mobile Engagement SDK interrupción).</span><span class="sxs-lookup"><span data-stu-id="16ae7-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="16ae7-114">Si una característica determinada de Azure Mobile Engagement nunca ha funcionado en la aplicación antes, deberá toocomplete la integración de Hola.</span><span class="sxs-lookup"><span data-stu-id="16ae7-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="16ae7-115">Si una característica determinada de Azure Mobile Engagement estaba funcionando y detiene, deberá tooupgrade toohello última versión hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="16ae7-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="16ae7-116">Recuerde que hay una versión diferente de hello Azure Mobile Engagement SDK para cada plataforma compatible con Azure Mobile Engagement (Android, iOS, Windows y Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="16ae7-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="16ae7-117">Integración de SDK</span><span class="sxs-lookup"><span data-stu-id="16ae7-117">SDK Integration</span></span>
* <span data-ttu-id="16ae7-118">Azure Mobile Engagement no integrado correctamente en el SDK (análisis).</span><span class="sxs-lookup"><span data-stu-id="16ae7-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="16ae7-119">Cobertura no integrada correctamente en SDK (inserciones dentro y fuera de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="16ae7-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="16ae7-120">Certificado caducado o PROD frente a DEV incorrecto (únicamente iOS).</span><span class="sxs-lookup"><span data-stu-id="16ae7-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="16ae7-121">GCM o ADM incorrectamente integrado en el SDK (solo en Android - Inserciones específicas del servicio).</span><span class="sxs-lookup"><span data-stu-id="16ae7-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="16ae7-122">Seguimiento incorrectamente integrado en el SDK (instalar el seguimiento de la tienda).</span><span class="sxs-lookup"><span data-stu-id="16ae7-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="16ae7-123">Ubicación diferida o ubicación de GPS incorrectamente integrada en el SDK (orientación mediante ubicación geográfica).</span><span class="sxs-lookup"><span data-stu-id="16ae7-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="16ae7-124">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="16ae7-124">**See also:**</span></span>

* <span data-ttu-id="16ae7-125">[Documentación del SDK - Guías de integración][Link 5]</span><span class="sxs-lookup"><span data-stu-id="16ae7-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="16ae7-126">[Guía de solución de problemas - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="16ae7-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="16ae7-127">Actualización del SDK</span><span class="sxs-lookup"><span data-stu-id="16ae7-127">SDK Upgrade</span></span>
* <span data-ttu-id="16ae7-128">Tenga problemas de tooresolve tooupgrade SDK con versiones anteriores de hello SDK (toonewer a menudo relacionados versiones de sistema operativo del dispositivo hello).</span><span class="sxs-lookup"><span data-stu-id="16ae7-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="16ae7-129">Desinstale todas las versiones anteriores de la aplicación desde el dispositivo y vuelva a instalar la versión más reciente de saludo de la aplicación, Hola volver a registrar el identificador de dispositivo de hello tooconfirm de interfaz de usuario de Azure Mobile Engagement que el dispositivo está utilizando la versión más reciente de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16ae7-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="16ae7-130">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="16ae7-130">**See also:**</span></span>

* [<span data-ttu-id="16ae7-131">Documentación del SDK - Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="16ae7-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="16ae7-132">Documentación del SDK - Guía de actualización</span><span class="sxs-lookup"><span data-stu-id="16ae7-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="16ae7-133">Otros errores del SDK</span><span class="sxs-lookup"><span data-stu-id="16ae7-133">SDK Other</span></span>
* <span data-ttu-id="16ae7-134">Los errores en el manifiesto de aplicación "AndroidManifest.xml" pueden producir Azure Mobile Engagement no toowork (solo Android).</span><span class="sxs-lookup"><span data-stu-id="16ae7-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="16ae7-135">Un problema común con integración con el SDK y el uso de API es hello tooconfuse clave de SDK y Hola clave de API.</span><span class="sxs-lookup"><span data-stu-id="16ae7-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="16ae7-136">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="16ae7-136">**See also:**</span></span>

* <span data-ttu-id="16ae7-137">[Conceptos - Glosario][Link 6]</span><span class="sxs-lookup"><span data-stu-id="16ae7-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="16ae7-138">Problemas de codificación avanzados</span><span class="sxs-lookup"><span data-stu-id="16ae7-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="16ae7-139">Problema</span><span class="sxs-lookup"><span data-stu-id="16ae7-139">Issue</span></span>
* <span data-ttu-id="16ae7-140">Código específico de plataforma no relacionada directamente tooAzure que Mobile Engagement puede causar problemas en Windows Phone, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="16ae7-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="16ae7-141">Causas</span><span class="sxs-lookup"><span data-stu-id="16ae7-141">Causes</span></span>
* <span data-ttu-id="16ae7-142">Muchos problemas de codificación con Azure Mobile Engagement avanzados causados por plataforma escrito incorrectamente código específico no relacionada directamente tooAzure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="16ae7-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="16ae7-143">Necesitará la plataforma de tooconsult documentación toohello específico que está desarrollando para además tooAzure documentación de Mobile Engagement (Android, iOS, Web, Windows y Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="16ae7-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="16ae7-144">Configurar no correctamente "categorías", impide que vincular desde una ubicación de tooanother notificación dentro o fuera de la aplicación hello (solo Android).</span><span class="sxs-lookup"><span data-stu-id="16ae7-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="16ae7-145">Si no se configura "UIKit.framework" demasiado "opcional" en el código de iOS, se muestra un "Error no encontrado"Symbol"o se bloquea en los dispositivos más antiguos de iOS (solo iOS).</span><span class="sxs-lookup"><span data-stu-id="16ae7-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="16ae7-146">Certificados expirados o no correctamente mediante Hola desarrollo o una versión Prod de cert hello, inserción de causas problemas (solo iOS).</span><span class="sxs-lookup"><span data-stu-id="16ae7-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="16ae7-147">No hay algunos plataforma tooa inherente de limitaciones que no se puede controlar Azure Mobile Engagement (por ejemplo, cómo Hola system center sirve para fuera de la aplicación inserta en iOS y Android).</span><span class="sxs-lookup"><span data-stu-id="16ae7-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="16ae7-148">Azure Mobile Engagement publica una lista completa de paquetes de hello interno utilizado por Azure Mobile Engagement para iOS y Android como referencia.</span><span class="sxs-lookup"><span data-stu-id="16ae7-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="16ae7-149">Tenga en cuenta que algunas características de Azure Mobile Engagement son toohello específico de la plataforma (Android, iOS, Web, Windows y Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="16ae7-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="16ae7-150">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="16ae7-150">See also</span></span>
* <span data-ttu-id="16ae7-151">[Guía de solución de problemas - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="16ae7-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="16ae7-152">[Documentación del SDK - Notas de la versión][Link 5]</span><span class="sxs-lookup"><span data-stu-id="16ae7-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="16ae7-153">[Documentación del SDK - Guía de actualización][Link 5]</span><span class="sxs-lookup"><span data-stu-id="16ae7-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="16ae7-154">Bloqueos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="16ae7-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="16ae7-155">Problema</span><span class="sxs-lookup"><span data-stu-id="16ae7-155">Issue</span></span>
* <span data-ttu-id="16ae7-156">La aplicación se bloquea en el dispositivo de los usuarios de finales de Hola.</span><span class="sxs-lookup"><span data-stu-id="16ae7-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="16ae7-157">Causas</span><span class="sxs-lookup"><span data-stu-id="16ae7-157">Causes</span></span>
* <span data-ttu-id="16ae7-158">Información de bloqueo puede verse en hello *interfaz de usuario de análisis de* o hello *API de análisis*</span><span class="sxs-lookup"><span data-stu-id="16ae7-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="16ae7-159">Puede encontrar Hola Id. de dispositivo del dispositivo de prueba y tomar Hola misma acción que provocó su toocrash de aplicación para un usuario final toohelp identificar la causa de Hola de su bloqueo.</span><span class="sxs-lookup"><span data-stu-id="16ae7-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="16ae7-160">Problemas conocidos con hello Azure Mobile Engagement SDK que generan las aplicaciones toocrash a veces se resuelven mediante la actualización toohello la versión más reciente de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="16ae7-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="16ae7-161">Asegúrese de seguro toocheck Hola notas acerca de la plataforma al investigar los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="16ae7-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="16ae7-162">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="16ae7-162">See also</span></span>
* <span data-ttu-id="16ae7-163">[Documentación del SDK - Notas de la versión][Link 5]</span><span class="sxs-lookup"><span data-stu-id="16ae7-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="16ae7-164">[Documentación del SDK - Guía de actualización][Link 5]</span><span class="sxs-lookup"><span data-stu-id="16ae7-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="16ae7-165">Fallos de carga de la tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="16ae7-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="16ae7-166">Problema</span><span class="sxs-lookup"><span data-stu-id="16ae7-166">Issue</span></span>
* <span data-ttu-id="16ae7-167">Errores relacionados con la versión más reciente de hello toouploading de su aplicación tooApple, Google o almacén de aplicación de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="16ae7-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="16ae7-168">Causas</span><span class="sxs-lookup"><span data-stu-id="16ae7-168">Causes</span></span>
* <span data-ttu-id="16ae7-169">Aplicación a veces almacena bloquear las aplicaciones con ciertas características habilitadas (p. ej. Hola Store de Apple impide el uso de Hola de IDFV en las aplicaciones de almacén de Hola y almacén de hello GooglePlay evita Hola de uso compartido de información entre las aplicaciones de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="16ae7-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="16ae7-170">Asegúrese de que ha activado notas de la versión de Hola acerca de la plataforma y la versión actual de hello SDK si tiene dificultades para cargar un almacén de toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="16ae7-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

