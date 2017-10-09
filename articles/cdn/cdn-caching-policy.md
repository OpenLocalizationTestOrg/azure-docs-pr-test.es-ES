---
title: "aaaManage directiva de caché de CDN de Azure en servicios multimedia de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage directiva de caché de CDN de Azure en servicios multimedia de Azure."
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Administración de la directiva de almacenamiento en caché de la red CDN de Azure en Azure Media Services
Servicios multimedia de Azure proporciona streaming adaptable basado en HTTP y descarga progresiva. El streaming basado en HTTP es altamente escalable con ventajas de almacenamiento en caché en proxy y capas CDN, además de almacenamiento en caché del cliente. Los extremos de streaming proporcionan capacidades generales de streaming, así como configuración para encabezados de caché HTTP. Los extremos de streaming establecen Control de caché HTTP: encabezados max-age y Expires. Puede obtener más información sobre los encabezados de caché HTTP en [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>Encabezados de almacenamiento en caché predeterminados
De forma predeterminada, los extremos de streaming aplican encabezados de caché de 3 días para datos de streaming a petición (fragmentos/segmentos multimedia reales) y manifest(playlist). Para streaming en directo, los extremos de streaming aplican encabezados de caché de 3 días para datos (fragmentos/segmentos multimedia reales) y encabezados de caché de 2 segundos para solicitudes de manifest(playlist). Cuando activa el programa en vivo tooon a petición (archivo dinámico), a continuación, se aplican encabezados de caché de transmisión por secuencias a petición.

## <a name="azure-cdn-integration"></a>Integración de CDN de Azure
Servicios multimedia de Azure proporciona una [red CDN integrada](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) para puntos de conexión de streaming. Encabezados Cache-control se aplica en hello igual manera que tooCDN de extremos de streaming habilitados los extremos de streaming. Azure usa CDN streaming tiempo de vida de hello toodefine valores de caché extremo configurado de hello internamente los objetos en caché y también usa esta encabezados de caché de entrega de valor tooset Hola. Cuando el uso de CDN habilitado los extremos de streaming no se recomienda tooset valores de pequeña memoria caché. Establecer valores pequeños disminuirá el rendimiento de hello y reducir la ventaja de Hola de CDN. No se permite encabezados de caché tooset menores de 600 segundos para la red CDN habilitado los extremos de streaming.

> [!IMPORTANT]
>Azure Media Services está totalmente integrado completa con la red CDN de Azure. Con un solo clic puede integrar todos Hola disponible CDN de Azure proveedores (Akamai y Verizon) tooyour extremo incluidos los productos de CDN estándar y Premium de streaming. Para más información, consulte este [anuncio](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Cargos de datos de transmisión por secuencias tooCDN de punto de conexión solo obtiene deshabilitados si CDN Hola está habilitado una por las API de extremo de streaming o mediante la sección punto de conexión de la transmisión por secuencias del portal de administración de Azure. Integración manual o crear directamente un punto de conexión de red CDN mediante las API de red CDN o sección del portal se deshabilitará cargos de datos de Hola.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Configuración de encabezados de caché con Servicios multimedia de Azure
Puede usar el portal de administración de Azure o valores de encabezado de caché de las API de servicios de multimedia de Azure tooconfigure.

1. encabezados de la caché de tooconfigure mediante administración portal consulte demasiado[cómo extremos de Streaming de tooManage](../media-services/media-services-portal-manage-streaming-endpoints.md) hello de la sección Configurar el punto de conexión de la transmisión por secuencias.
2. API de REST de Servicios multimedia de Azure, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. .NET SDK de Servicios multimedia de Azure, [Propiedades de StreamingEndpointCacheControl](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Orden de prioridad de configuración de caché
1. El valor de caché configurado de Servicios multimedia de Azure reemplaza el valor predeterminado.
2. Si no hay ninguna configuración manual, se aplican los valores predeterminados.
3. De forma predeterminada 2 segundos encabezados de la caché se aplica toolive manifest(playlist) independientemente de la configuración de almacenamiento de Azure o Azure multimedia de transmisión por secuencias y el reemplazo de este valor no está disponible.

