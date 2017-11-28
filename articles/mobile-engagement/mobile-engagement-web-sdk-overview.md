---
title: "Información general del SDK web de Azure Mobile Engagement | Microsoft Docs"
description: "Actualizaciones y procedimientos más recientes para el SDK web para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="6bd16-103">SDK web para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="6bd16-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="6bd16-104">Comience aquí a obtener todos los detalles sobre cómo integrar Azure Mobile Engagement en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="6bd16-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="6bd16-105">Si desea probarlo antes de comenzar con su propia aplicación web, consulte nuestro [tutorial de 15 minutos](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6bd16-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="6bd16-106">Procedimientos de integración</span><span class="sxs-lookup"><span data-stu-id="6bd16-106">Integration procedures</span></span>
1. <span data-ttu-id="6bd16-107">Aprenda a [integrar Mobile Engagement en su aplicación web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="6bd16-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="6bd16-108">Para la implementación del plan de etiquetas: aprenda a [usar la API de etiquetado avanzado de Mobile Engagement en su aplicación web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="6bd16-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="6bd16-109">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="6bd16-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="6bd16-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="6bd16-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="6bd16-111">Bloqueo corregido en exploración privada (Safari).</span><span class="sxs-lookup"><span data-stu-id="6bd16-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="6bd16-112">Bloqueo corregido en exploradores con cookies deshabilitadas.</span><span class="sxs-lookup"><span data-stu-id="6bd16-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="6bd16-113">Para todas las versiones, consulte [todas las notas de la versión](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="6bd16-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="6bd16-114">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="6bd16-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="6bd16-115">Actualizar desde 1.2.1 a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="6bd16-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="6bd16-116">En las siguientes secciones se describe cómo migrar una integración de SDK web de Mobile Engagement desde el servicio de Capptain, ofrecido por Capptain SAS, a una aplicación de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6bd16-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="6bd16-117">Si va a migrar desde una versión anterior a la 1.2.1, consulte el sitio web de Capptain para migrar a 1.2.1 en primer lugar y luego aplique los siguientes procedimientos.</span><span class="sxs-lookup"><span data-stu-id="6bd16-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="6bd16-118">Esta versión del SDK web de Mobile Engagement no es compatible con Samsung Smart TV, Opera TV, webOS o la característica Reach.</span><span class="sxs-lookup"><span data-stu-id="6bd16-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bd16-119">Capptain y Azure Mobile Engagement no son el mismo servicio, y los procedimientos siguientes destacan únicamente cómo migrar la aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="6bd16-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="6bd16-120">La migración del SDK web de Mobile Engagement en la aplicación no migrará los datos desde un servidor Capptain a un servidor Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6bd16-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="6bd16-121">Archivos de JavaScript</span><span class="sxs-lookup"><span data-stu-id="6bd16-121">JavaScript files</span></span>
<span data-ttu-id="6bd16-122">Reemplace el archivo capptain-sdk.js por el archivo azure-engagement.js y luego actualice las importaciones del script en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="6bd16-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="6bd16-123">Eliminación de la cobertura de Capptain</span><span class="sxs-lookup"><span data-stu-id="6bd16-123">Remove Capptain Reach</span></span>
<span data-ttu-id="6bd16-124">Esta versión del SDK web de Mobile Engagement no admite la característica Reach.</span><span class="sxs-lookup"><span data-stu-id="6bd16-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="6bd16-125">Si ha integrado Capptain Reach en su aplicación, debe quitarlo.</span><span class="sxs-lookup"><span data-stu-id="6bd16-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="6bd16-126">Quite la importación de CSS de Reach de su página y elimine el archivo .css relacionado (de forma predeterminada, capptain-reach.css).</span><span class="sxs-lookup"><span data-stu-id="6bd16-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="6bd16-127">Elimine los siguientes recursos de Reach: la imagen de cierre (de forma predeterminada, capptain-close.png) y el icono de marca (de forma predeterminada, capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="6bd16-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="6bd16-128">Quite la interfaz de usuario de Reach para las notificaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6bd16-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="6bd16-129">El diseño predeterminado tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="6bd16-129">The default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="6bd16-130">Quite el texto, los anuncios web y los sondeos de la interfaz de usuario de Reach.</span><span class="sxs-lookup"><span data-stu-id="6bd16-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="6bd16-131">El diseño predeterminado tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="6bd16-131">The default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="6bd16-132">Quite el objeto `reach` de la configuración, si existe.</span><span class="sxs-lookup"><span data-stu-id="6bd16-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="6bd16-133">Su aspecto es similar a este:</span><span class="sxs-lookup"><span data-stu-id="6bd16-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="6bd16-134">Quite cualquier otra personalización de Reach, como las categorías.</span><span class="sxs-lookup"><span data-stu-id="6bd16-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="6bd16-135">Eliminación de las API en desuso</span><span class="sxs-lookup"><span data-stu-id="6bd16-135">Remove deprecated APIs</span></span>
<span data-ttu-id="6bd16-136">Algunas API de Capptain están en desuso en el SDK web de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6bd16-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="6bd16-137">Quite cualquier llamada a las API siguientes: `agent.connect`, `agent.disconnect`, `agent.pause` y `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="6bd16-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="6bd16-138">Quite todas las siguientes devoluciones de llamada de la configuración de Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` y `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="6bd16-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="6bd16-139">Configuración</span><span class="sxs-lookup"><span data-stu-id="6bd16-139">Configuration</span></span>
<span data-ttu-id="6bd16-140">Mobile Engagement usa una cadena de conexión para configurar los identificadores del SDK, como el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6bd16-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="6bd16-141">Reemplace el identificador de la aplicación por la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="6bd16-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="6bd16-142">Tenga en cuenta que el objeto global para la configuración del SDK cambia de `capptain` a `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="6bd16-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="6bd16-143">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="6bd16-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="6bd16-144">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="6bd16-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="6bd16-145">La cadena de conexión de la aplicación se muestra en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6bd16-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="6bd16-146">API de JavaScript</span><span class="sxs-lookup"><span data-stu-id="6bd16-146">JavaScript APIs</span></span>
<span data-ttu-id="6bd16-147">El objeto global de JavaScript `window.capptain` ha cambiado de nombre a `window.azureEngagement`, pero puede usar el alias `window.engagement` para las llamadas de API.</span><span class="sxs-lookup"><span data-stu-id="6bd16-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="6bd16-148">No se puede utilizar este alias para definir la configuración del SDK.</span><span class="sxs-lookup"><span data-stu-id="6bd16-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="6bd16-149">Por ejemplo: `capptain.deviceId` se convierte en `engagement.deviceId`, `capptain.agent.startActivity` se convierte en `engagement.agent.startActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="6bd16-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="6bd16-150">Si ya ha integrado una versión anterior del SDK web de Azure Mobile Engagement en su aplicación, consulte los [procedimientos de actualización](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="6bd16-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

