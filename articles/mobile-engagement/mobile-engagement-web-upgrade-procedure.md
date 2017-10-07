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
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Procedimientos de actualización del SDK web de Azure Mobile Engagement
Si ya ha integrado una versión anterior de hello Web SDK de Azure Mobile Engagement en la aplicación web, deberá hello tooconsider siguientes puntos cuando actualice Hola SDK.

Si omite varias versiones del SDK de Mobile Engagement Web hello, tendrá que toocomplete varios procedimientos durante el proceso de actualización de Hola. Por ejemplo, si migra desde 1.4.0 too1.6.0, primer seguimiento Hola procedimientos tooupgrade de 1.4.0 too1.5.0. A continuación, siga Hola procedimientos tooupgrade de 1.5.0 too1.6.0.

Cualquier versión de actualizar, reemplazar cualquier versión anterior del archivo de hello azure-engagement.js con la versión más reciente de Hola de archivo hello.

## <a name="upgrade-from-121-too200"></a>Actualización desde 1.2.1 too2.0.0
Esta sección describe cómo toomigrate una integración del SDK de Mobile Engagement Web del servicio de Capptain hello, que ofrece Capptain SAS, aplicación de Azure Mobile Engagement tooan. Si va a migrar desde una versión anterior, por favor, consulte hello toofirst del sitio Web de Capptain migrar too1.2.1 y, a continuación, aplicar Hola procedimientos siguientes.

No es compatible con esta versión de hello Web SDK de Mobile Engagement TV inteligente de Samsung, Opera TV, webOS o característica de cobertura de Hola.

> [!IMPORTANT]
> Capptain y Azure Mobile Engagement no son Hola mismo servicio. Hola procedimiento resalta solo cómo toomigrate Hola aplicación cliente. Migrar hello Web SDK de Mobile Engagement en la aplicación hello no migrará los datos de un servidor de Mobile Engagement Capptain server tooa.
> 
> 

### <a name="javascript-files"></a>Archivos de JavaScript
Reemplace Hola de archivo capptain sdk.js por archivo de hello azure-engagement.js y actualice el script se importa en consecuencia.

### <a name="remove-capptain-reach"></a>Eliminación de la cobertura de Capptain
Esta versión de hello SDK de Mobile Engagement Web no admite la característica de cobertura de Hola. Si integra Capptain alcance en la aplicación, necesita tooremove lo.

Quitar Hola CSS llegar a importar desde la página y eliminar archivo .css relacionados de hello (capptain-reach.css, de forma predeterminada).

Eliminar Hola alcance recursos siguientes: Hola Cerrar imagen (capptain-close.png, de forma predeterminada) y el icono de marca de hello (capptain--icono de notificación, de forma predeterminada).

Quitar Hola llegar a la interfaz de usuario para las notificaciones de la aplicación. diseño de Hello predeterminado tiene el siguiente aspecto:

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

Quitar Hola llegar a la interfaz de usuario para sondeos y anuncios de texto y web. diseño de Hello predeterminado tiene el siguiente aspecto:

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

Quitar hello `reach` del objeto de la configuración, si existe. Su aspecto es similar a este:

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Quite cualquier otra personalización de Reach, como las categorías.

### <a name="remove-deprecated-apis"></a>Eliminación de las API en desuso
Algunas API de Capptain está desusada en hello Web SDK de Mobile Engagement.

Quite cualquier toohello de llamadas después de API: `agent.connect`, `agent.disconnect`, `agent.pause`, y `agent.sendMessageToDevice`.

Quite todas las instancias de hello siguiendo las devoluciones de llamada de la configuración de Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, y `onPushMessageReceived`.

### <a name="configuration"></a>Configuración
Mobile Engagement usa una cadena tooconfigure SDK identificadores de conexión de, por ejemplo, el identificador de la aplicación hello.

Reemplace el identificador de la aplicación hello con la cadena de conexión. Tenga en cuenta ese objeto global Hola de hello configuración SDK cambia de `capptain` demasiado`azureEngagement`.

Antes de la migración:

    window.capptain = {
      appId: ...,
      [...]
    };

Después de la migración:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

cadena de conexión de Hello para la aplicación se muestra en hello Portal de Azure.

### <a name="javascript-apis"></a>API de JavaScript
objeto global de JavaScript de Hello `window.capptain` ha cambiado `window.azureEngagement` , pero puede usar hello `window.engagement` alias para las llamadas API. No puede usar la configuración de SDK de hello alias toodefine Hola.

Por ejemplo: `capptain.deviceId` se convierte en `engagement.deviceId`, `capptain.agent.startActivity` se convierte en `engagement.agent.startActivity`, etc.

