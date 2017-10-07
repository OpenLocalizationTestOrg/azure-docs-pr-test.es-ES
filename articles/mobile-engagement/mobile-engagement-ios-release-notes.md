---
title: "aaaAzure notas de la versión de SDK de Mobile Engagement iOS | Documentos de Microsoft"
description: "Actualizaciones y procedimientos más recientes para el SDK de iOS para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="e4696-103">Notas de la versión del SDK de iOS de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e4696-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="e4696-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="e4696-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="e4696-105">Se han corregido las notificaciones borradas en el fondo.</span><span class="sxs-lookup"><span data-stu-id="e4696-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="e4696-106">Se han corregido las advertencias de XCode 9 sobre las API a las que no se llamaba en cola principal.</span><span class="sxs-lookup"><span data-stu-id="e4696-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="e4696-107">Se ha corregido una fuga de memoria en los sondeos de cobertura.</span><span class="sxs-lookup"><span data-stu-id="e4696-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="e4696-108">Se ha eliminado el soporte técnico para iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="e4696-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="e4696-109">A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 7.</span><span class="sxs-lookup"><span data-stu-id="e4696-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="e4696-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="e4696-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="e4696-111">Entrega de registros en segundo plano mejorada</span><span class="sxs-lookup"><span data-stu-id="e4696-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="e4696-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="e4696-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="e4696-113">Notificación fija no ejecutada en dispositivos iOS 10.</span><span class="sxs-lookup"><span data-stu-id="e4696-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="e4696-114">XCode 7 en desuso.</span><span class="sxs-lookup"><span data-stu-id="e4696-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="e4696-115">3.2.4 (30/06/2016)</span><span class="sxs-lookup"><span data-stu-id="e4696-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="e4696-116">Agregación fija entre registros técnicos y otros registros.</span><span class="sxs-lookup"><span data-stu-id="e4696-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="e4696-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="e4696-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="e4696-118">Error de hello fijo en comentarios de entrega no se notifican cuando la aplicación se encuentra en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4696-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="e4696-119">Hola optimizado envío de registros técnicos.</span><span class="sxs-lookup"><span data-stu-id="e4696-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="e4696-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="e4696-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="e4696-121">Ha corregido el error en la cancelación de la solicitud HTTP que conduce a veces toocrash.</span><span class="sxs-lookup"><span data-stu-id="e4696-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="e4696-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="e4696-123">Retraso de hello fijo cuando se desencadena una nueva instancia de la aplicación mediante una notificación con vínculos profundos</span><span class="sxs-lookup"><span data-stu-id="e4696-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="e4696-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="e4696-125">Habilitado Bitcode en hello SDK toomake funciona con **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="e4696-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="e4696-126">Los errores corregidos relacionados con las notificaciones de la aplicación tooin.</span><span class="sxs-lookup"><span data-stu-id="e4696-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="e4696-127">Realiza las notificaciones de la aplicación hello más confiable en el caso de batería baja y otros escenarios de este tipo.</span><span class="sxs-lookup"><span data-stu-id="e4696-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="e4696-128">Se quitaron registros de la consola adicionales generados por la biblioteca de terceros.</span><span class="sxs-lookup"><span data-stu-id="e4696-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="e4696-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="e4696-130">Corrija los errores de compatibilidad de iOS 9 con una biblioteca de terceros.</span><span class="sxs-lookup"><span data-stu-id="e4696-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="e4696-131">Generaban bloqueos al enviar resultados de sondeo, información de la aplicación o datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="e4696-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="e4696-132">3.0.0 (19/06/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="e4696-133">Mobile Engagement usa notificaciones push silenciosas.</span><span class="sxs-lookup"><span data-stu-id="e4696-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="e4696-134">Soporte de iOS 4.X eliminado.</span><span class="sxs-lookup"><span data-stu-id="e4696-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="e4696-135">A partir de este destino de implementación de Hola de versión de la aplicación debe tener como mínimo iOS 6.</span><span class="sxs-lookup"><span data-stu-id="e4696-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="e4696-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="e4696-137">Id. de dispositivo de Hello Mobile Engagement para dispositivos < iOS 6 se basa ahora en un GUID generado durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="e4696-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="e4696-138">2.1.0 (24/04/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="e4696-139">Agregada compatibilidad con Swift.</span><span class="sxs-lookup"><span data-stu-id="e4696-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="e4696-140">Al hacer clic en una notificación, acción de hello que dirección URL es ahora ejecuta derecha cuando se abre la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e4696-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="e4696-141">Se ha agregado el archivo de encabezado que faltaba en el paquete del SDK.</span><span class="sxs-lookup"><span data-stu-id="e4696-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="e4696-142">Se corrigió un problema cuando se deshabilitó el indicador de bloqueo de Mobile Engagement Hola.</span><span class="sxs-lookup"><span data-stu-id="e4696-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="e4696-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="e4696-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="e4696-144">Versión inicial de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e4696-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="e4696-145">La configuración de appId o sdkKey se sustituye por una configuración de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="e4696-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="e4696-146">Quitar toosend de API y recibir mensajes XMPP arbitrarios de entidades XMPP arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="e4696-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="e4696-147">Quitar toosend de API y recibir mensajes entre los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e4696-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="e4696-148">Mejoras de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e4696-148">Security improvements.</span></span>
* <span data-ttu-id="e4696-149">Se ha eliminado el seguimiento de SmartAd.</span><span class="sxs-lookup"><span data-stu-id="e4696-149">SmartAd tracking removed.</span></span>
