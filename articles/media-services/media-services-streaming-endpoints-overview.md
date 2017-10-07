---
title: "información general sobre el extremo de transmisión por secuencias los servicios multimedia de aaaAzure | Documentos de Microsoft"
description: "En este tema se proporciona información general sobre los puntos de conexión de streaming de Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Información general de los puntos de conexión de streaming 

##<a name="overview"></a>Información general

En Microsoft Azure Media Services (AMS), un **extremo de transmisión por secuencias** representa un servicio de streaming que puede entregar contenido directamente tooa aplicación de reproducción de cliente o tooa red de entrega de contenido (CDN) para su distribución posterior. Servicios multimedia también proporciona integración sin problemas de CDN de Azure. flujo de salida de Hello de un servicio de StreamingEndpoint puede ser una secuencia en directo, un vídeo a petición o la descarga progresiva del recurso en su cuenta de servicios multimedia. Cada cuenta de Azure Media Services incluye un punto de conexión de streaming predeterminado. StreamingEndpoints adicionales pueden crearse en la cuenta de hello. Existen dos versiones de puntos de conexión de streaming: 1.0 y 2.0. A partir del 10 de enero de 2017, las cuentas recién creadas de AMS incluirán de manera **predeterminada** la versión 2.0 del punto de conexión de streaming. Agregar cuenta de toothis de extremos de streaming adicional también será versión 2.0. Este cambio no afectará a las cuentas existentes de hello; StreamingEndpoints existente serán versión 1.0 y pueden ser actualizado tooversion 2.0. Con este cambio, habrá cambios de comportamiento, la facturación y la característica (para obtener más información, vea hello **tipos y versiones de transmisión por secuencias** sección documenta a continuación).

Además, empezando con la versión de Hola 2.15 (publicada en enero de 2017), servicios multimedia de Azure agregado Hola después de la entidad de extremo de transmisión por secuencias de propiedades toohello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Para obtener información general detallada de estas propiedades, consulte [aquí](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Cuando se crea una cuenta de servicios multimedia de Azure predeterminado extremo de transmisión por secuencias estándar se crea automáticamente en hello **detenido** estado. No se puede eliminar predeterminado Hola extremo de streaming. Dependiendo de la disponibilidad de red CDN de Azure en región de destino de Hola Hola, valor predeterminado recién creado de forma predeterminada extremo de streaming también incluye "StandardVerizon" CDN integración de proveedor. 

>[!NOTE]
>Integración de CDN de Azure puede deshabilitarse antes de iniciar el extremo de streaming de Hola.

Este tema ofrece una visión general de las funcionalidades principales Hola que proceden de los extremos de streaming.

## <a name="streaming-types-and-versions"></a>Tipos y versiones de streaming

### <a name="standardpremium-types-version-20"></a>Tipos estándar o premium (versión 2.0)

A partir de versión de enero de 2017 Hola de Media Services, tiene dos tipos de transmisión por secuencias: **estándar** y **Premium**. Estos tipos forman parte de la versión de punto de conexión de la transmisión por secuencias de Hola "2.0".

Tipo|Descripción
---|---
**Standard**|Esta es la opción de valor predeterminado de Hola que podría funcionar para la mayoría de Hola de los escenarios de Hola.<br/>Con esta opción, obtendrá fija o limitado SLA, primeros 15 días después de iniciar Hola extremo de streaming es gratuito.<br/>Si crea más de una transmisión por secuencias los puntos de conexión, solo hello primero uno es gratuita para hello primeros 15 días, Hola otros se facturan en cuanto se inicie. <br/>Tenga en cuenta que prueba gratuita sólo se aplica toonewly creado cuentas de servicios de medios y extremo de streaming de manera predeterminada. Los extremos de transmisión por secuencias existentes y los extremos de streaming además creados no incluye gratuita período incluso son actualizado tooversion 2.0 o se crean como versión 2.0.
**Premium**|Esta opción es la preferible para escenarios profesionales en los que se requiere mayor escala o control.<br/>Con un Acuerdo de Nivel de Servicio variable que se basa en la capacidad adquirida de la unidad de streaming premium, los puntos de conexión de streaming dedicados residen en un entorno aislado y no compiten por los recursos.

Para obtener más información, vea hello **comparar Streaming tipos** pasos de la sección.

### <a name="classic-type-version-10"></a>Tipo clásico (versión 1.0)

Para los usuarios que crean cuentas AMS toohello anteriores 10 de enero de 2017, tendrá un **clásico** tipo de un extremo de streaming. Este tipo es parte del programa Hola streaming endpoint versión "1.0".

Si su **versión "1.0"** extremo de streaming tiene > = 1 premium (SU), unidades de streaming será el extremo de streaming de premium y proporcionarán todas las características de AMS (al igual que hello **estándar o Premium** tipo) sin ningún paso de configuración adicional.

>[!NOTE]
>Los puntos de conexión de streaming **clásicos** (versión "1.0" y 0 unidades de streaming) ofrecen características limitadas y no incluyen un Acuerdo de Nivel de Servicio. Se recomienda toomigrate demasiado**estándar** escriba tooget una mejor experiencia y toouse de características como la codificación o empaquetado dinámico y otras características que se suministran con hello **estándar** tipo. toomigrate toohello **estándar** escriba, vaya toohello [portal de Azure](https://portal.azure.com/) y seleccione **participación en tooStandard**. Para obtener más información acerca de la migración, vea hello [migración](#migration-between-types) sección.
>
>Tenga en cuenta que esta operación no se puede revertir y afectará al precio.
>
 
## <a name="comparing-streaming-types"></a>Comparación de tipos de streaming

### <a name="versions"></a>Versiones

|Escriba|Versión de punto de conexión de streaming|Unidades de escalado|CDN|Facturación|Contrato de nivel de servicio| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Clásico|1.0|0|N/D|Gratuito|N/D|
|Punto de conexión de streaming estándar|2.0|0|Sí|De pago|Sí|
|Unidades de streaming premium|1.0|>0|Sí|De pago|Sí|
|Unidades de streaming premium|2.0|>0|Sí|De pago|Sí|

### <a name="features"></a>Características

Característica|Estándar|Premium
---|---|---
Gratis los primeros 15 días| Sí |No
Rendimiento |Seguridad too600 Mbps cuando no se utiliza la red CDN de Azure. Se puede ampliar con la red CDN.|200 Mbps por unidad de streaming. Se puede ampliar con la red CDN.
Contrato de nivel de servicio | 99,9|99,9 (200 Mbps por unidad de streaming).
CDN|Red CDN de Azure, red de entrega de contenido de terceros o ninguna red de entrega de contenido.|Red CDN de Azure, red de entrega de contenido de terceros o ninguna red de entrega de contenido.
La facturación se prorratea| Diario|Diario
Cifrado dinámico|Sí|Sí
Empaquetado dinámico|Sí|Sí
Escala|Rendimiento toohello de destino se amplía automáticamente.|Unidades de streaming adicionales
Filtrado de IP/G20/host personalizado|Sí|Sí
Descarga progresiva|Sí|Sí
Uso recomendado |Se recomienda para la gran mayoría de los escenarios de transmisión por secuencias de Hola.|Uso profesional.<br/>Si considera que puede tener necesidades más allá del nivel Estándar. Póngase en contacto con nosotros (amsstreaming@microsoft.com) si prevé una audiencia simultánea superior a 50.000 visualizaciones.


## <a name="migration-between-types"></a>Migración entre tipos

De | demasiado| Acción
---|---|---
Clásico|Estándar|Necesidad de tooopt
Clásico|Premium| Escala (unidades de streaming adicionales)
Estándar/Premium|Clásico|No está disponible (si la versión de punto de conexión de streaming es 1.0. Se permite toochange tooclassic con configuración scaleunits demasiado "0")
Estándar (con o sin red CDN)|Premium con hello configuraciones|Permitido en hello **iniciado** estado. (mediante Azure Portal)
Premium (con o sin red CDN)|Estándar con hello configuraciones|Permitido en hello **iniciado** estado (a través del portal de Azure)
Estándar (con o sin red CDN)|Premium con diferente configuración|Permitido en hello **detenido** estado (a través del portal de Azure). No se permite en hello estado de ejecución.
Premium (con o sin red CDN)|Estándar con diferente configuración|Permitido en hello **detenido** estado (a través del portal de Azure). No se permite en hello estado de ejecución.
Versión 1.0 con al menos una unidad de streaming en red CDN|Estándar o Premium sin ninguna red CDN|Permitido en hello **detenido** estado. No se permite en hello **iniciado** estado.
Versión 1.0 con al menos una unidad de streaming en red CDN|Estándar con o sin red CDN|Permitido en hello **detenido** estado. No se permite en hello **iniciado** estado. La red CDN de la versión 1.0 se eliminará y se creará e iniciará una nueva.
Versión 1.0 con al menos una unidad de streaming en red CDN|Premium con o sin red CDN|Permitido en hello **detenido** estado. No se permite en hello **iniciado** estado. La red CDN clásica se eliminará y se creará e iniciará una nueva.

## <a name="next-steps"></a>Pasos siguientes
Consulte las rutas de aprendizaje de Servicios multimedia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

