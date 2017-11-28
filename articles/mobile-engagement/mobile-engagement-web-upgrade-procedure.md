---
title: "los procedimientos de actualización de SDK de Mobile Engagement Web aaaAzure | Documentos de Microsoft"
description: "Hola actualizaciones más recientes y procedimientos para hello Web SDK de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="09d5b-103">Procedimientos de actualización del SDK web de Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="09d5b-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="09d5b-104">Si ya ha integrado una versión anterior de hello Web SDK de Azure Mobile Engagement en la aplicación web, deberá hello tooconsider siguientes puntos cuando actualice Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="09d5b-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="09d5b-105">Si omite varias versiones del SDK de Mobile Engagement Web hello, tendrá que toocomplete varios procedimientos durante el proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="09d5b-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="09d5b-106">Por ejemplo, si migra desde 1.4.0 too1.6.0, primer seguimiento Hola procedimientos tooupgrade de 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="09d5b-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="09d5b-107">A continuación, siga Hola procedimientos tooupgrade de 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="09d5b-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="09d5b-108">Cualquier versión de actualizar, reemplazar cualquier versión anterior del archivo de hello azure-engagement.js con la versión más reciente de Hola de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="09d5b-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="09d5b-109">Actualización desde 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="09d5b-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="09d5b-110">Esta sección describe cómo toomigrate una integración del SDK de Mobile Engagement Web del servicio de Capptain hello, que ofrece Capptain SAS, aplicación de Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="09d5b-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="09d5b-111">Si va a migrar desde una versión anterior, por favor, consulte hello toofirst del sitio Web de Capptain migrar too1.2.1 y, a continuación, aplicar Hola procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="09d5b-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="09d5b-112">No es compatible con esta versión de hello Web SDK de Mobile Engagement TV inteligente de Samsung, Opera TV, webOS o característica de cobertura de Hola.</span><span class="sxs-lookup"><span data-stu-id="09d5b-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09d5b-113">Capptain y Azure Mobile Engagement no son Hola mismo servicio.</span><span class="sxs-lookup"><span data-stu-id="09d5b-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="09d5b-114">Hola procedimiento resalta solo cómo toomigrate Hola aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="09d5b-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="09d5b-115">Migrar hello Web SDK de Mobile Engagement en la aplicación hello no migrará los datos de un servidor de Mobile Engagement Capptain server tooa.</span><span class="sxs-lookup"><span data-stu-id="09d5b-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="09d5b-116">Archivos de JavaScript</span><span class="sxs-lookup"><span data-stu-id="09d5b-116">JavaScript files</span></span>
<span data-ttu-id="09d5b-117">Reemplace Hola de archivo capptain sdk.js por archivo de hello azure-engagement.js y actualice el script se importa en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="09d5b-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="09d5b-118">Eliminación de la cobertura de Capptain</span><span class="sxs-lookup"><span data-stu-id="09d5b-118">Remove Capptain Reach</span></span>
<span data-ttu-id="09d5b-119">Esta versión de hello SDK de Mobile Engagement Web no admite la característica de cobertura de Hola.</span><span class="sxs-lookup"><span data-stu-id="09d5b-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="09d5b-120">Si integra Capptain alcance en la aplicación, necesita tooremove lo.</span><span class="sxs-lookup"><span data-stu-id="09d5b-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="09d5b-121">Quitar Hola CSS llegar a importar desde la página y eliminar archivo .css relacionados de hello (capptain-reach.css, de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="09d5b-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="09d5b-122">Eliminar Hola alcance recursos siguientes: Hola Cerrar imagen (capptain-close.png, de forma predeterminada) y el icono de marca de hello (capptain--icono de notificación, de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="09d5b-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="09d5b-123">Quitar Hola llegar a la interfaz de usuario para las notificaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="09d5b-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="09d5b-124">diseño de Hello predeterminado tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="09d5b-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="09d5b-125">Quitar Hola llegar a la interfaz de usuario para sondeos y anuncios de texto y web.</span><span class="sxs-lookup"><span data-stu-id="09d5b-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="09d5b-126">diseño de Hello predeterminado tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="09d5b-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="09d5b-127">Quitar hello `reach` del objeto de la configuración, si existe.</span><span class="sxs-lookup"><span data-stu-id="09d5b-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="09d5b-128">Su aspecto es similar a este:</span><span class="sxs-lookup"><span data-stu-id="09d5b-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="09d5b-129">Quite cualquier otra personalización de Reach, como las categorías.</span><span class="sxs-lookup"><span data-stu-id="09d5b-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="09d5b-130">Eliminación de las API en desuso</span><span class="sxs-lookup"><span data-stu-id="09d5b-130">Remove deprecated APIs</span></span>
<span data-ttu-id="09d5b-131">Algunas API de Capptain está desusada en hello Web SDK de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="09d5b-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="09d5b-132">Quite cualquier toohello de llamadas después de API: `agent.connect`, `agent.disconnect`, `agent.pause`, y `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="09d5b-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="09d5b-133">Quite todas las instancias de hello siguiendo las devoluciones de llamada de la configuración de Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, y `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="09d5b-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="09d5b-134">Configuración</span><span class="sxs-lookup"><span data-stu-id="09d5b-134">Configuration</span></span>
<span data-ttu-id="09d5b-135">Mobile Engagement usa una cadena tooconfigure SDK identificadores de conexión de, por ejemplo, el identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="09d5b-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="09d5b-136">Reemplace el identificador de la aplicación hello con la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="09d5b-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="09d5b-137">Tenga en cuenta ese objeto global Hola de hello configuración SDK cambia de `capptain` demasiado`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="09d5b-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="09d5b-138">Antes de la migración:</span><span class="sxs-lookup"><span data-stu-id="09d5b-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="09d5b-139">Después de la migración:</span><span class="sxs-lookup"><span data-stu-id="09d5b-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="09d5b-140">cadena de conexión de Hello para la aplicación se muestra en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="09d5b-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="09d5b-141">API de JavaScript</span><span class="sxs-lookup"><span data-stu-id="09d5b-141">JavaScript APIs</span></span>
<span data-ttu-id="09d5b-142">objeto global de JavaScript de Hello `window.capptain` ha cambiado `window.azureEngagement` , pero puede usar hello `window.engagement` alias para las llamadas API.</span><span class="sxs-lookup"><span data-stu-id="09d5b-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="09d5b-143">No puede usar la configuración de SDK de hello alias toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="09d5b-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="09d5b-144">Por ejemplo: `capptain.deviceId` se convierte en `engagement.deviceId`, `capptain.agent.startActivity` se convierte en `engagement.agent.startActivity`, etc.</span><span class="sxs-lookup"><span data-stu-id="09d5b-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

