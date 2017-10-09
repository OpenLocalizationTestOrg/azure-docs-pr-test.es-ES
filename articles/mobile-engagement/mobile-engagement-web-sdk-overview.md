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
# <a name="azure-mobile-engagement-web-sdk"></a>SDK web para Azure Mobile Engagement
Empiece aquí para Hola a todos los detalles acerca de cómo toointegrate Azure Mobile Engagement en una aplicación web. Si desea que toogive un bloque try antes de comenzar con su propia aplicación web, vea nuestra [15 minutos tutorial](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Procedimientos de integración
1. Obtenga información acerca de [cómo toointegrate Mobile Engagement en la aplicación web](mobile-engagement-web-integrate-engagement.md).
2. Para la implementación del plan de etiqueta, obtenga información acerca de [cómo toouse Hola avanzada etiquetado API en su aplicación web de Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Notas de la versión
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* Bloqueo corregido en exploración privada (Safari).
* Bloqueo corregido en exploradores con cookies deshabilitadas.

Para todas las versiones, vea hello [completar notas de la versión](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Procedimientos de actualización
### <a name="upgrade-from-121-too200"></a>Actualización desde 1.2.1 too2.0.0
Hello secciones siguientes describen cómo toomigrate una integración del SDK de Mobile Engagement Web del servicio de Capptain hello, que ofrece Capptain SAS, aplicación de Azure Mobile Engagement tooan. Si va a migrar desde una versión anterior que 1.2.1, consulte hello Capptain sitio Web toomigrate too1.2.1 en primer lugar y luego aplique Hola procedimientos siguientes.

No es compatible con esta versión de hello Web SDK de Mobile Engagement TV inteligente de Samsung, Opera TV, webOS o característica de cobertura de Hola.

> [!IMPORTANT]
> Capptain y Azure Mobile Engagement no son Hola el mismo servicio y Hola procedimientos resalte sólo cómo toomigrate Hola aplicación cliente. Migrar hello Web SDK de Mobile Engagement en la aplicación hello no migrará los datos de un servidor de Mobile Engagement Capptain server tooa.
> 
> 

#### <a name="javascript-files"></a>Archivos de JavaScript
Reemplace Hola de archivo capptain sdk.js por archivo de hello azure-engagement.js y actualice el script se importa en consecuencia.

#### <a name="remove-capptain-reach"></a>Eliminación de la cobertura de Capptain
Esta versión de hello SDK de Mobile Engagement Web no admite la característica de cobertura de Hola. Si ha integrado Capptain alcance en la aplicación, necesita tooremove lo.

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

#### <a name="remove-deprecated-apis"></a>Eliminación de las API en desuso
Algunas API de Capptain está desusada en hello Web SDK de Mobile Engagement.

Quite cualquier toohello de llamadas después de API: `agent.connect`, `agent.disconnect`, `agent.pause`, y `agent.sendMessageToDevice`.

Quite cualquier Hola siguiendo las devoluciones de llamada de la configuración de Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, y `onPushMessageReceived`.

#### <a name="configuration"></a>Configuración
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

cadena de conexión de Hello para la aplicación se muestra en hello portal de Azure.

#### <a name="javascript-apis"></a>API de JavaScript
objeto global de JavaScript de Hello `window.capptain` ha cambiado `window.azureEngagement`, pero puede usar hello `window.engagement` alias para las llamadas API. No se puede usar esta configuración de SDK de alias toodefine Hola.

Por ejemplo: `capptain.deviceId` se convierte en `engagement.deviceId`, `capptain.agent.startActivity` se convierte en `engagement.agent.startActivity`, etc.

Si ya ha integrado una versión anterior de hello Web SDK de Azure Mobile Engagement en la aplicación, lea acerca de [actualizar procedimientos](mobile-engagement-web-upgrade-procedure.md).

