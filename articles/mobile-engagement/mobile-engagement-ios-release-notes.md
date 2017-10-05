---
title: "Notas de la versión del SDK de iOS de Azure Mobile Engagement | Microsoft Docs"
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
ms.openlocfilehash: 9bdaa57f9902373ccf796ff109332b64c66bf9e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="28c2b-103">Notas de la versión del SDK de iOS de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="28c2b-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="28c2b-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="28c2b-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="28c2b-105">Se han corregido las notificaciones borradas en el fondo.</span><span class="sxs-lookup"><span data-stu-id="28c2b-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="28c2b-106">Se han corregido las advertencias de XCode 9 sobre las API a las que no se llamaba en cola principal.</span><span class="sxs-lookup"><span data-stu-id="28c2b-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="28c2b-107">Se ha corregido una fuga de memoria en los sondeos de cobertura.</span><span class="sxs-lookup"><span data-stu-id="28c2b-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="28c2b-108">Se ha eliminado el soporte técnico para iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="28c2b-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="28c2b-109">A partir de esta versión, el destino de implementación de la aplicación tiene que ser como mínimo iOS 7.</span><span class="sxs-lookup"><span data-stu-id="28c2b-109">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="28c2b-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="28c2b-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="28c2b-111">Entrega de registros en segundo plano mejorada</span><span class="sxs-lookup"><span data-stu-id="28c2b-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="28c2b-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="28c2b-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="28c2b-113">Notificación fija no ejecutada en dispositivos iOS 10.</span><span class="sxs-lookup"><span data-stu-id="28c2b-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="28c2b-114">XCode 7 en desuso.</span><span class="sxs-lookup"><span data-stu-id="28c2b-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="28c2b-115">3.2.4 (30/06/2016)</span><span class="sxs-lookup"><span data-stu-id="28c2b-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="28c2b-116">Agregación fija entre registros técnicos y otros registros.</span><span class="sxs-lookup"><span data-stu-id="28c2b-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="28c2b-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="28c2b-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="28c2b-118">Se corrigió el error donde los comentarios de entrega no se notifican cuando la aplicación funciona en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="28c2b-118">Fixed the bug where delivery feedback is not reported when app is in the background.</span></span>
* <span data-ttu-id="28c2b-119">Se ha optimizado el envío de registros técnicos.</span><span class="sxs-lookup"><span data-stu-id="28c2b-119">Optimized the sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="28c2b-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="28c2b-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="28c2b-121">Se ha corregido el error en la cancelación de solicitud HTTP que provocaba a veces bloqueos.</span><span class="sxs-lookup"><span data-stu-id="28c2b-121">Fixed bug on HTTP request cancellation which sometimes leads to crash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="28c2b-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="28c2b-123">Se ha corregido el retraso que se produce cuando se desencadena una nueva instancia de aplicación por una notificación con vínculos profundos.</span><span class="sxs-lookup"><span data-stu-id="28c2b-123">Fixed the delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="28c2b-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="28c2b-125">Se habilitó Bitcode en el SDK para que funcione con **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="28c2b-125">Enabled Bitcode in the SDK to make it work with **Xcode 7**.</span></span>
* <span data-ttu-id="28c2b-126">Se corrigieron los errores relacionados con las notificaciones desde la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28c2b-126">Fixed bugs related to in-app notifications.</span></span>
* <span data-ttu-id="28c2b-127">Las notificaciones desde la aplicación ahora son más fiables en caso de que, por ejemplo, la batería esté baja.</span><span class="sxs-lookup"><span data-stu-id="28c2b-127">Made the in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="28c2b-128">Se quitaron registros de la consola adicionales generados por la biblioteca de terceros.</span><span class="sxs-lookup"><span data-stu-id="28c2b-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="28c2b-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="28c2b-130">Corrija los errores de compatibilidad de iOS 9 con una biblioteca de terceros.</span><span class="sxs-lookup"><span data-stu-id="28c2b-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="28c2b-131">Generaban bloqueos al enviar resultados de sondeo, información de la aplicación o datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="28c2b-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="28c2b-132">3.0.0 (19/06/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="28c2b-133">Mobile Engagement usa notificaciones push silenciosas.</span><span class="sxs-lookup"><span data-stu-id="28c2b-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="28c2b-134">Soporte de iOS 4.X eliminado.</span><span class="sxs-lookup"><span data-stu-id="28c2b-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="28c2b-135">A partir de esta versión, el destino de implementación de la aplicación debe ser como mínimo iOS 6.</span><span class="sxs-lookup"><span data-stu-id="28c2b-135">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="28c2b-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="28c2b-137">El identificador de dispositivo de Mobile Engagement para dispositivos anteriores a iOS 6 ahora se basa en un GUID que se genera durante la instalación.</span><span class="sxs-lookup"><span data-stu-id="28c2b-137">The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="28c2b-138">2.1.0 (24/04/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="28c2b-139">Agregada compatibilidad con Swift.</span><span class="sxs-lookup"><span data-stu-id="28c2b-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="28c2b-140">Al hacer clic en una notificación, la dirección URL de la acción se ejecuta ahora justo después de abrir la aplicación.</span><span class="sxs-lookup"><span data-stu-id="28c2b-140">When clicking on a notification, the action URL is now executed right after the application is opened.</span></span>
* <span data-ttu-id="28c2b-141">Se ha agregado el archivo de encabezado que faltaba en el paquete del SDK.</span><span class="sxs-lookup"><span data-stu-id="28c2b-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="28c2b-142">Se ha corregido un problema cuando se deshabilitaba el generador de informes de error de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="28c2b-142">Fixed an issue when the Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="28c2b-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="28c2b-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="28c2b-144">Versión inicial de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="28c2b-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="28c2b-145">La configuración de appId o sdkKey se sustituye por una configuración de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="28c2b-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="28c2b-146">Se ha eliminado la API para enviar y recibir mensajes XMPP arbitrarios de entidades XMPP arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="28c2b-146">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="28c2b-147">Se ha eliminado la API para enviar y recibir mensajes entre dispositivos.</span><span class="sxs-lookup"><span data-stu-id="28c2b-147">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="28c2b-148">Mejoras de seguridad.</span><span class="sxs-lookup"><span data-stu-id="28c2b-148">Security improvements.</span></span>
* <span data-ttu-id="28c2b-149">Se ha eliminado el seguimiento de SmartAd.</span><span class="sxs-lookup"><span data-stu-id="28c2b-149">SmartAd tracking removed.</span></span>
