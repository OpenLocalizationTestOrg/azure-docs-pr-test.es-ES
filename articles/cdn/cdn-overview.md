---
title: "información general de la red CDN aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de qué hello es la red de entrega de contenido (CDN) de Azure y cómo toouse se toodeliver contenido de gran ancho de banda almacenando en memoria caché los blobs y el contenido estático."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Información general de hello red de entrega de contenido (CDN) de Azure
> [!NOTE]
> Este documento describe qué hello es la red de entrega de contenido (CDN) de Azure, cómo funciona y características de Hola de cada producto de la red CDN de Azure.  Si desea que esta información tooskip y vaya tooa recta tutorial acerca de cómo toocreate un extremo de red CDN, vea [CDN de Azure utilizando](cdn-create-new-endpoint.md).  Si desea toosee una lista de ubicaciones actuales de nodos de CDN, vea [ubicaciones de POP de CDN de Azure](cdn-pop-locations.md).
> 
> 

Hola red de entrega de contenido (CDN) de Azure almacena en caché el contenido web estático en el rendimiento máximo de tooprovide situadas estratégicamente para entregar contenido toousers.  Hola CDN ofrece a los desarrolladores una solución global para entregar contenido con alto ancho de banda al almacenar en caché contenido de hello en nodos físicos a través de Hola a todos. 

Hola ventajas del uso de recursos de sitio web de toocache CDN Hola se incluyen:

* Mejor rendimiento y experiencia de usuario para los usuarios finales, especialmente cuando el uso de aplicaciones donde es varios ida y vuelta necesarios contenido tooload.
* Gran escala toobetter identificador cargas instantáneas pesadas, como en el inicio de Hola de un producto de iniciar el evento.
* Al distribuir las solicitudes de usuario y que sirve al contenido de los servidores de borde, menos tráfico se envía toohello origen.

## <a name="how-it-works"></a>Cómo funciona
![Información general de la red CDN](./media/cdn-overview/cdn-overview.png)

1. Un usuario (Alice) solicita un archivo (también denominado un recurso) mediante una dirección URL con un nombre de dominio especial, como `<endpointname>.azureedge.net`.  DNS enruta la ubicación de punto de presencia (POP) mejor rendimiento de hello solicitud toohello.  Normalmente, se trata de hello POP que sea usuario de toohello más cercano geográficamente.
2. Si servidores perimetrales de Hola Hola POP no tiene archivo hello en la memoria caché, hello borde servidor solicita archivo hello origen Hola.  Hola origen puede ser una aplicación Web de Azure, servicio de nube de Azure, cuenta de almacenamiento de Azure o cualquier servidor web accesible públicamente.
3. origen de Hello devuelve Hola archivo toohello borde del servidor, incluidos los encabezados HTTP opcionales que describen Time-to-Live del archivo hello (TTL).
4. servidor perimetral de Hello almacena en caché archivo hello y devuelve el solicitante original de hello archivo toohello (Alicia).  archivo Hello permanece en la caché en el servidor perimetral de hello hasta que expire Hola TTL.  Si el origen de hello no especifica un valor de TTL, el TTL predeterminado de hello es siete días.
5. Los usuarios adicionales pueden Hola de solicitud mismo archivo con esa misma dirección URL y, también puede ser dirigido toothat mismo POP.
6. Si no ha expirado hello TTL para archivo hello, servidor perimetral de hello devuelve archivo hello de memoria caché de Hola.  Esto genera una experiencia de usuario más rápida y una mayor capacidad de respuesta.

## <a name="azure-cdn-features"></a>Características de la red CDN de Azure
Hay tres productos del servicio CDN de Azure: **Azure CDN Standard de Akamai**, **Azure CDN Standard de Verizon** y **Azure CDN Premium de Verizon**.  Hello siguiente tabla enumeran Hola características disponibles con cada producto.

|  | Estándar de Akamai | Estándar de Verizon | Premium de Verizone |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Características de rendimiento y optimizaciones__ |
| [Aceleración de sitios dinámicos](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&amp;#x2713;**  | **&amp;#x2713;** | **&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  [Aceleración de sitio dinámico: compresión de imagen adaptable](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&amp;#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  [Aceleración de sitio dinámico: precarga de objetos](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&amp;#x2713;**  |  |  |
| [Optimización de streaming multimedia](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&amp;#x2713;**  | \* |  \* |
| [Optimización de archivos grandes](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&amp;#x2713;**  | \* |  \* |
| [Equilibrio de carga del servidor global (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Purga rápida](cdn-purge-endpoint.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Carga previa de activos](cdn-preload-endpoint.md) | |**&amp;#x2713;** |**&amp;#x2713;** |
| [Almacenamiento en caché de cadena de consulta](cdn-query-string.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| Pila dual IPv4/IPv6 |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Compatibilidad con HTTP/2](cdn-http2.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Seguridad__ |
| Compatibilidad con HTTPS con el punto de conexión de red CDN |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Dominio personalizado HTTPS](cdn-custom-ssl.md) | |**&amp;#x2713;** |**&amp;#x2713;** |
| [Compatibilidad con nombre de dominio personalizado](cdn-map-content-to-custom-domain.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Filtrado geográfico](cdn-restrict-access-by-country.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Autenticación de token](cdn-token-auth.md)|  |  |**&amp;#x2713;**| 
| [Protección contra DDOS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Análisis e informes__ |
| [Análisis esencial](cdn-analyze-usage-patterns.md) | **&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Informes de HTTP avanzados](cdn-advanced-http-reports.md) | | |**&amp;#x2713;** |
| [Estadísticas en tiempo real](cdn-real-time-stats.md) | | |**&amp;#x2713;** |
| [Alertas en tiempo real](cdn-real-time-alerts.md) | | |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Facilidad de uso__ |
| Fácil integración con servicios de Azure, como [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md) y [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| Se puede administrar mediante la [API de REST](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) o [PowerShell](cdn-manage-powershell.md). |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Motor de entrega de contenido personalizable, basado en reglas](cdn-rules-engine.md) | | |**&amp;#x2713;** |
| Configuración de la memoria caché o del encabezado (mediante un [motor de reglas](cdn-rules-engine.md)) | | |**&amp;#x2713;** |
| Redirección/rescritura de direcciones URL (mediante un [motor de reglas](cdn-rules-engine.md)) | | |**&amp;#x2713;** |
| Reglas de dispositivos móviles (mediante un [motor de reglas](cdn-rules-engine.md)) | | |**&amp;#x2713;** |

\* Verizon admite la entrega de archivos de gran tamaño y de elementos multimedia directamente a través de la entrega web general.


> [!TIP]
> ¿Hay una característica que te gustaría toosee en la red CDN de Azure?  [Envíenos sus comentarios](https://feedback.azure.com/forums/169397-cdn). 
> 
> 

## <a name="next-steps"></a>Pasos siguientes
tooget partió CDN, vea [CDN de Azure utilizando](cdn-create-new-endpoint.md).

Si es un cliente existente de la red CDN, ahora puede administrar los extremos de red CDN mediante hello [portal de Microsoft Azure](https://portal.azure.com) o con [PowerShell](cdn-manage-powershell.md).

toosee Hola CDN en acción, visite hello [vídeo de la sesión de 2016 de compilación](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Obtenga información acerca de cómo tooautomate CDN de Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).

Para más información sobre los precios, consulte [Precios de Red de entrega de contenido (CDN)](https://azure.microsoft.com/pricing/details/cdn/).

