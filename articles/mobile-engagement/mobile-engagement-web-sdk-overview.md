---
title: "información general del SDK de Mobile Engagement Web aaaAzure | Documentos de Microsoft"
description: "Hola actualizaciones más recientes y procedimientos para hello Web SDK de Azure Mobile Engagement"
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
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="7a886-103">SDK web para Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7a886-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="7a886-104">Empiece aquí para Hola a todos los detalles acerca de cómo toointegrate Azure Mobile Engagement en una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7a886-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="7a886-105">Si desea que toogive un bloque try antes de comenzar con su propia aplicación web, vea nuestra [15 minutos tutorial](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7a886-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="7a886-106">Procedimientos de integración</span><span class="sxs-lookup"><span data-stu-id="7a886-106">Integration procedures</span></span>
1. <span data-ttu-id="7a886-107">Obtenga información acerca de [cómo toointegrate Mobile Engagement en la aplicación web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="7a886-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="7a886-108">Para la implementación del plan de etiqueta, obtenga información acerca de [cómo toouse Hola avanzada etiquetado API en su aplicación web de Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="7a886-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="7a886-109">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="7a886-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="7a886-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="7a886-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="7a886-111">Bloqueo corregido en exploración privada (Safari).</span><span class="sxs-lookup"><span data-stu-id="7a886-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="7a886-112">Bloqueo corregido en exploradores con cookies deshabilitadas.</span><span class="sxs-lookup"><span data-stu-id="7a886-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="7a886-113">Para todas las versiones, vea hello [completar notas de la versión](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="7a886-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="7a886-114">Procedimientos de actualización</span><span class="sxs-lookup"><span data-stu-id="7a886-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="7a886-115">Actualización desde 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="7a886-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="7a886-116">Hello secciones siguientes describen cómo toomigrate una integración del SDK de Mobile Engagement Web del servicio de Capptain hello, que ofrece Capptain SAS, aplicación de Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="7a886-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="7a886-117">Si va a migrar desde una versión anterior que 1.2.1, consulte hello Capptain sitio Web toomigrate too1.2.1 en primer lugar y luego aplique Hola procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="7a886-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="7a886-118">No es compatible con esta versión de hello Web SDK de Mobile Engagement TV inteligente de Samsung, Opera TV, webOS o característica de cobertura de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a886-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a886-119">Capptain y Azure Mobile Engagement no son Hola el mismo servicio y Hola procedimientos resalte sólo cómo toomigrate Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="7a886-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="7a886-120">Migrar hello Web SDK de Mobile Engagement en la aplicación hello no migrará los datos de un servidor de Mobile Engagement Capptain server tooa.</span><span class="sxs-lookup"><span data-stu-id="7a886-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="7a886-121">Archivos de JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a886-121">JavaScript files</span></span>
<span data-ttu-id="7a886-122">Reemplace Hola de archivo capptain sdk.js por archivo de hello azure-engagement.js y actualice el script se importa en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="7a886-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="7a886-123">Eliminación de la cobertura de Capptain</span><span class="sxs-lookup"><span data-stu-id="7a886-123">Remove Capptain Reach</span></span>
<span data-ttu-id="7a886-124">Esta versión de hello SDK de Mobile Engagement Web no admite la característica de cobertura de Hola.</span><span class="sxs-lookup"><span data-stu-id="7a886-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="7a886-125">Si ha integrado Capptain alcance en la aplicación, necesita tooremove lo.</span><span class="sxs-lookup"><span data-stu-id="7a886-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="7a886-126">Quitar Hola CSS llegar a importar desde la página y eliminar archivo .css relacionados de hello (capptain-reach.css, de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="7a886-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="7a886-127">Eliminar Hola alcance recursos siguientes: Hola Cerrar imagen (capptain-close.png, de forma predeterminada) y el icono de marca de hello (capptain--icono de notificación, de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="7a886-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="7a886-128">Quitar Hola llegar a la interfaz de usuario para las notificaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a886-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="7a886-129">diseño de Hello predeterminado tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="7a886-129">hello default layout looks like this:</span></span>

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

<span data-ttu-id="7a886-130">Quitar Hola llegar a la interfaz de usuario para sondeos y anuncios de texto y web.</span><span class="sxs-lookup"><span data-stu-id="7a886-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="7a886-131">diseño de Hello predeterminado tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="7a886-131">hello default layout looks like this:</span></span>

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

<span data-ttu-id="7a886-132">Quitar hello `reach` del objeto de la configuración, si existe.</span><span class="sxs-lookup"><span data-stu-id="7a886-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="7a886-133">Su aspecto es similar a este:</span><span class="sxs-lookup"><span data-stu-id="7a886-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="7a886-134">Quite cualquier otra personalización de Reach, como las categorías.</span><span class="sxs-lookup"><span data-stu-id="7a886-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="7a886-135">Eliminación de las API en desuso</span><span class="sxs-lookup"><span data-stu-id="7a886-135">Remove deprecated APIs</span></span>
<span data-ttu-id="7a886-136">Algunas API de Capptain está desusada en hello Web SDK de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7a886-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="7a886-137">Quite cualquier toohello de llamadas después de API: `agent.connect`, `agent.disconnect`, `agent.pause`, y `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="7a886-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="7a886-138">Quite cualquier Hola siguiendo las devoluciones de llamada de la configuración de Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, y `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="7a886-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="7a886-139">Configuración</span><span class="sxs-lookup"><span data-stu-id="7a886-139">Configuration</span></span>
<span data-ttu-id="7a886-140">Mobile Engagement usa una cadena tooconfigure SDK identificadores de conexión de, por ejemplo, el identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7a886-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="7a886-141">Reemplace el identificador de la aplicación hello con la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="7a886-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="7a886-142">Tenga en cuenta ese objeto global Hola de hello configuración SDK cambia de `capptain` demasiado`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="7a886-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="7a886-143">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="7a886-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="7a886-144">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="7a886-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="7a886-145">cadena de conexión de Hello para la aplicación se muestra en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7a886-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="7a886-146">API de JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a886-146">JavaScript APIs</span></span>
<span data-ttu-id="7a886-147">objeto global de JavaScript de Hello `window.capptain` ha cambiado `window.azureEngagement`, pero puede usar hello `window.engagement` alias para las llamadas API.</span><span class="sxs-lookup"><span data-stu-id="7a886-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="7a886-148">No se puede usar esta configuración de SDK de alias toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="7a886-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="7a886-149">Por ejemplo: `capptain.deviceId` se convierte en `engagement.deviceId`, `capptain.agent.startActivity` se convierte en `engagement.agent.startActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="7a886-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="7a886-150">Si ya ha integrado una versión anterior de hello Web SDK de Azure Mobile Engagement en la aplicación, lea acerca de [actualizar procedimientos](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="7a886-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

