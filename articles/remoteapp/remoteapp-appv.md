---
title: aplicaciones de App-V aaaUsing con Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de App-V toouse en Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a>Uso de aplicaciones App-V en RemoteApp de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Puede usar aplicaciones App-V en una colección híbrida de Azure RemoteApp, que requiera unión a dominio.

Antes de comenzar, asegúrese de cliente de App-V 5.1 de Hola de tooinstall seguro con las últimas actualizaciones de Hola. Deberá toocreate un [imagen personalizada](remoteapp-create-custom-image.md) que incluye el cliente de App-V Hola.  

Es fácil toouse su infraestructura de App-V con Azure RemoteApp. Dado que una colección híbrida se implementa en una red virtual de Azure que tiene el controlador de dominio de acceso tooyour y hello las máquinas virtuales están unidos a un dominio, puede aprovechar su existente aplicación App-v infraestructura e implementación métodos tooeasyily host App-V en Azure RemoteApp. Estas son algunas consideraciones que debe tener en cuenta en función de tipo de Hola de implementación de App-V que tiene actualmente:

| Opciones de configuración |  | Positive | Negative |
| --- | --- | --- | --- |
| Método de entrega |Streaming (a petición) |Aplicación siempre es hello más reciente y actualizado |Primera latencia |
| Montado |Más rápido; aplicación ya está presente en hello VM |Sobredimensionamiento: se usa el espacio de la imagen (límite de 127 GB) | |
| Almacenamiento de ubicación de aplicaciones |Contenido compartido |La aplicación se ejecuta en la memoria de la instancia de RemoteApp de Azure. |Come memoria y conexión buena toostreaming (archivo) del servidor donde reside la aplicación hello |
| Disco (en caché) |Ejecución rápida La aplicación no depende de la disponibilidad del origen del contenido. |Sobredimensionamiento: se usa el espacio de la imagen (límite de 127 GB) | |
| Destinatarios |Usuario |Requiere la infraestructura de App-V independiente completa. | |
| Global (equipo) |Publique previamente o seleccione el destino mediante el servidor de publicación |Necesita tooupdate la imagen de Azure si desea que tooupdate Hola aplicación (enorme). Ocupa espacio en la imagen. | |

 Después de crear la imagen personalizada y su colección híbrida, publicar la aplicación, asignar a usuarios y disfrute de las aplicaciones de App-V existentes hospedadas en Azure RemoteApp entregado tooany dispositivo en cualquier parte.

