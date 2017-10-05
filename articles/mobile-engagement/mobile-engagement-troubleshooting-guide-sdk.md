---
title: "Guía de solución de problemas de Azure Mobile Engagement - SDK"
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
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="853f9-103">Guía de solución de problemas de la integración de SDK</span><span class="sxs-lookup"><span data-stu-id="853f9-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="853f9-104">Los siguientes son posibles problemas que pueden producirse con cómo Azure Mobile Engagement se integra en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="853f9-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="853f9-105">Problemas SDK descubiertos por un error en otra área de la aplicación</span><span class="sxs-lookup"><span data-stu-id="853f9-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="853f9-106">Problema</span><span class="sxs-lookup"><span data-stu-id="853f9-106">Issue</span></span>
* <span data-ttu-id="853f9-107">Error de colección de datos de interfaz de usuario (en el análisis, supervisión, segmentación o paneles).</span><span class="sxs-lookup"><span data-stu-id="853f9-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="853f9-108">Errores de inserción (las inserciones no funcionan en la aplicación, fuera de la aplicación o en ambos).</span><span class="sxs-lookup"><span data-stu-id="853f9-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="853f9-109">Fallos de función avanzados (no funcionan el seguimiento, la geolocalización o las inserciones específicas de plataforma).</span><span class="sxs-lookup"><span data-stu-id="853f9-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="853f9-110">Errores de la API (las API fallan a menudo de manera silenciosa sin que se muestren mensajes de error).</span><span class="sxs-lookup"><span data-stu-id="853f9-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="853f9-111">Errores del servicio (ninguno de los Azure Mobile Engagement funciona para su aplicación).</span><span class="sxs-lookup"><span data-stu-id="853f9-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="853f9-112">Causas</span><span class="sxs-lookup"><span data-stu-id="853f9-112">Causes</span></span>
* <span data-ttu-id="853f9-113">La mayoría de errores que necesitan resolverse con el SDK de Azure Mobile Engagement se descubrirán mediante un fallo en su aplicación (por ejemplo, un error de recopilación de datos de interfaz de usuario, un error de inserción, un error de función avanzada, un error de API, bloqueos de aplicación o una interrupción del servicio aparente).</span><span class="sxs-lookup"><span data-stu-id="853f9-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="853f9-114">Si una función determinada de Azure Mobile Engagement nunca ha funcionado en la aplicación antes, deberá completar la integración.</span><span class="sxs-lookup"><span data-stu-id="853f9-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="853f9-115">Si una función determinada de Azure Mobile Engagement funcionaba y se detuvo, puede que necesite actualizar a la última versión con el SDK de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="853f9-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="853f9-116">Recuerde que hay una versión diferente del SDK de Azure Mobile Engagement para cada plataforma compatible con Azure Mobile Engagement (Android, iOS, Windows y Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="853f9-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="853f9-117">Integración de SDK</span><span class="sxs-lookup"><span data-stu-id="853f9-117">SDK Integration</span></span>
* <span data-ttu-id="853f9-118">Azure Mobile Engagement no integrado correctamente en el SDK (análisis).</span><span class="sxs-lookup"><span data-stu-id="853f9-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="853f9-119">Cobertura no integrada correctamente en SDK (inserciones dentro y fuera de la aplicación).</span><span class="sxs-lookup"><span data-stu-id="853f9-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="853f9-120">Certificado caducado o PROD frente a DEV incorrecto (únicamente iOS).</span><span class="sxs-lookup"><span data-stu-id="853f9-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="853f9-121">GCM o ADM incorrectamente integrado en el SDK (solo en Android - Inserciones específicas del servicio).</span><span class="sxs-lookup"><span data-stu-id="853f9-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="853f9-122">Seguimiento incorrectamente integrado en el SDK (instalar el seguimiento de la tienda).</span><span class="sxs-lookup"><span data-stu-id="853f9-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="853f9-123">Ubicación diferida o ubicación de GPS incorrectamente integrada en el SDK (orientación mediante ubicación geográfica).</span><span class="sxs-lookup"><span data-stu-id="853f9-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="853f9-124">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="853f9-124">**See also:**</span></span>

* <span data-ttu-id="853f9-125">[Documentación del SDK - Guías de integración][Link 5]</span><span class="sxs-lookup"><span data-stu-id="853f9-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="853f9-126">[Guía de solución de problemas - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="853f9-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="853f9-127">Actualización del SDK</span><span class="sxs-lookup"><span data-stu-id="853f9-127">SDK Upgrade</span></span>
* <span data-ttu-id="853f9-128">Debe actualizar el SDK para resolver problemas con versiones anteriores del SDK (a menudo relacionados con las versiones más recientes del sistema operativo del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="853f9-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="853f9-129">Desinstale todas las versiones anteriores de la aplicación del dispositivo y vuelva a instalar la versión más reciente de la aplicación, vuelva a registrar el identificador de dispositivo desde la interfaz de usuario de Azure Mobile Engagement para confirmar que el dispositivo está utilizando la versión más reciente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="853f9-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="853f9-130">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="853f9-130">**See also:**</span></span>

* [<span data-ttu-id="853f9-131">Documentación del SDK - Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="853f9-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="853f9-132">Documentación del SDK - Guía de actualización</span><span class="sxs-lookup"><span data-stu-id="853f9-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="853f9-133">Otros errores del SDK</span><span class="sxs-lookup"><span data-stu-id="853f9-133">SDK Other</span></span>
* <span data-ttu-id="853f9-134">Los errores en el manifiesto de la aplicación "AndroidManifest.xml" pueden provocar que Azure Mobile Engagement no funcione (solo en Android).</span><span class="sxs-lookup"><span data-stu-id="853f9-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="853f9-135">Un problema común con la integración del SDK y el uso de la API es confundir la clave del SDK y la clave de la API.</span><span class="sxs-lookup"><span data-stu-id="853f9-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="853f9-136">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="853f9-136">**See also:**</span></span>

* <span data-ttu-id="853f9-137">[Conceptos - Glosario][Link 6]</span><span class="sxs-lookup"><span data-stu-id="853f9-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="853f9-138">Problemas de codificación avanzados</span><span class="sxs-lookup"><span data-stu-id="853f9-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="853f9-139">Problema</span><span class="sxs-lookup"><span data-stu-id="853f9-139">Issue</span></span>
* <span data-ttu-id="853f9-140">Un código específico de plataforma no relacionado directamente con Azure Mobile Engagement puede causar problemas en Windows Phone, iOS y Android.</span><span class="sxs-lookup"><span data-stu-id="853f9-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="853f9-141">Causas</span><span class="sxs-lookup"><span data-stu-id="853f9-141">Causes</span></span>
* <span data-ttu-id="853f9-142">Muchos problemas de codificación avanzada con Azure Mobile Engagement están provocados por códigos específicos de plataforma escritos incorrectamente no relacionados directamente con Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="853f9-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="853f9-143">Deberá consultar la documentación específica de la plataforma para la que está desarrollando además de la documentación de Azure Mobile Engagement (Android, iOS, Web, Windows y Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="853f9-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="853f9-144">No configurar correctamente las "categorías" impide la vinculación desde una notificación a otra ubicación dentro o fuera de la aplicación (solo Android).</span><span class="sxs-lookup"><span data-stu-id="853f9-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="853f9-145">No establecer "UIKit.framework" en "opcional" en el código de iOS provoca que se muestre un "Error de símbolo no encontrado" o bloqueos en los dispositivos iOS antiguos (únicamente en iOS).</span><span class="sxs-lookup"><span data-stu-id="853f9-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="853f9-146">Los certificados caducados o que no usan la versión de DEV o PROD correctamente causan errores de inserción (únicamente iOS).</span><span class="sxs-lookup"><span data-stu-id="853f9-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="853f9-147">Existen algunas limitaciones inherentes a una plataforma que Azure Mobile Engagement no puede controlar (por ejemplo, cómo funciona el centro del sistema para las inserciones fuera de la aplicación en iOS y Android).</span><span class="sxs-lookup"><span data-stu-id="853f9-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="853f9-148">Azure Mobile Engagement publica una lista completa de los paquetes internos utilizados por Azure Mobile Engagement para iOS y Android a modo de referencia.</span><span class="sxs-lookup"><span data-stu-id="853f9-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="853f9-149">Tenga en cuenta que algunas funciones de Azure Mobile Engagement son específicas de la plataforma (Android, iOS, Web, Windows y Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="853f9-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="853f9-150">Consulte también</span><span class="sxs-lookup"><span data-stu-id="853f9-150">See also</span></span>
* <span data-ttu-id="853f9-151">[Guía de solución de problemas - Push][Link 23]</span><span class="sxs-lookup"><span data-stu-id="853f9-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="853f9-152">[Documentación del SDK - Notas de la versión][Link 5]</span><span class="sxs-lookup"><span data-stu-id="853f9-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="853f9-153">[Documentación del SDK - Guía de actualización][Link 5]</span><span class="sxs-lookup"><span data-stu-id="853f9-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="853f9-154">Bloqueos de la aplicación</span><span class="sxs-lookup"><span data-stu-id="853f9-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="853f9-155">Problema</span><span class="sxs-lookup"><span data-stu-id="853f9-155">Issue</span></span>
* <span data-ttu-id="853f9-156">La aplicación se bloquea en el dispositivo de los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="853f9-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="853f9-157">Causas</span><span class="sxs-lookup"><span data-stu-id="853f9-157">Causes</span></span>
* <span data-ttu-id="853f9-158">La información del bloqueo se puede ver en la *interfaz de usuario de análisis* o en la *API de análisis*.</span><span class="sxs-lookup"><span data-stu-id="853f9-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="853f9-159">Puede encontrar el identificador del dispositivo de su dispositivo de prueba y realizar la misma acción que provocó que la aplicación se bloquee para un usuario final para ayudar a identificar la causa de su bloqueo.</span><span class="sxs-lookup"><span data-stu-id="853f9-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="853f9-160">Los problemas conocidos con el SDK de Azure Mobile Engagement que provocan que las aplicaciones se bloqueen a veces se resuelven con la actualización a la versión más reciente del SDK.</span><span class="sxs-lookup"><span data-stu-id="853f9-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="853f9-161">Asegúrese de comprobar las notas de la versión de la plataforma cuando investigue los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="853f9-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="853f9-162">Consulte también</span><span class="sxs-lookup"><span data-stu-id="853f9-162">See also</span></span>
* <span data-ttu-id="853f9-163">[Documentación del SDK - Notas de la versión][Link 5]</span><span class="sxs-lookup"><span data-stu-id="853f9-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="853f9-164">[Documentación del SDK - Guía de actualización][Link 5]</span><span class="sxs-lookup"><span data-stu-id="853f9-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="853f9-165">Fallos de carga de la tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="853f9-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="853f9-166">Problema</span><span class="sxs-lookup"><span data-stu-id="853f9-166">Issue</span></span>
* <span data-ttu-id="853f9-167">Errores relacionados con la carga de la versión más reciente de su aplicación a Apple, Google o la tienda de aplicaciones Windows.</span><span class="sxs-lookup"><span data-stu-id="853f9-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="853f9-168">Causas</span><span class="sxs-lookup"><span data-stu-id="853f9-168">Causes</span></span>
* <span data-ttu-id="853f9-169">Las tiendas de aplicaciones a veces bloquean aplicaciones con ciertas funciones habilitadas (por ejemplo, Apple Store impide el uso de IDFV en las aplicaciones de la tienda y la tienda GooglePlay impide el uso compartido de información de la aplicación entre las aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="853f9-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="853f9-170">Asegúrese de comprobar las notas de la versión acerca de la plataforma y la versión actual del SDK si tiene dificultades para cargar una aplicación en la tienda.</span><span class="sxs-lookup"><span data-stu-id="853f9-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

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

