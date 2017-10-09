---
title: "límites de aaaService en búsqueda de Azure | Documentos de Microsoft"
description: "Límites de servicio usados en la planeación de la capacidad y los límites máximos de solicitudes y respuestas de Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Límites de servicio en la Búsqueda de Azure
Los límites máximos del almacenamiento, las cargas de trabajo y las cantidades de índices, documentos y otros objetos dependen de si [aprovisiona Azure Search](search-create-service-portal.md) conforme a un plan de tarifa **Gratis**, **Básico** o **Estándar**.

* **Gratis** es un servicio multiinquilino compartido incluido en su suscripción de Azure. Es una opción de ningún costo adicional para los suscriptores existentes que le permite tooexperiment con el servicio de hello antes de registrarse para recursos dedicados.
* El plan **Básico** proporciona recursos de proceso dedicados para cargas de trabajo de producción a escala más pequeña.
* **Estándar** se ejecuta en máquinas dedicadas, con más almacenamiento y capacidad de procesamiento en cada nivel. Standard incluye cuatro niveles: S1, S2, S3 y S3 High Density (S3 HD).

> [!NOTE]
> Un servicio se aprovisiona en un nivel específico. Si necesita más capacidad toojump niveles tooget, debe proporcionar un nuevo servicio (no hay ninguna actualización en contexto). Para más información, vea [Selección de SKU o plan de tarifa](search-sku-tier.md). toolearn más acerca del ajuste de capacidad dentro de un servicio ha aprovisionado ya, consulte [escalar los niveles de recursos de consulta e indización las cargas de trabajo](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Límites por suscripción
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Por límites de servicio
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Por límites de índice
Hay una correspondencia uno a uno entre los límites de los índices y los límites de los indexadores. Proporciona un límite de 200 índices, Hola límite máximo para los indizadores es también 200 para hello mismo servicio.

| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Índice: campos máximos por índice |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Índice: perfiles de puntuación máximos por índice |100 |100 |100 |100 |100 |100 |
| Índice: funciones máximas por perfil |8 |8 |8 |8 |8 |8 |
| Indexadores: carga máxima de indexación por invocación |10 000 documentos |Limitado solamente por el número máximo de documentos |Limitado solamente por el número máximo de documentos |Limitado solamente por el número máximo de documentos |Limitado solamente por el número máximo de documentos |N/D <sup>2</sup> |
| Indexadores: tiempo de ejecución máximo | De 1 a 3 minutos <sup>3</sup> |24 horas |24 horas |24 horas |24 horas |N/D <sup>2</sup> |
| Indexador de blobs: tamaño máximo de blob, MB |16 |16 |128 |256 |256 |N/D <sup>2</sup> |
| Indexador de blobs: número máximo de caracteres del contenido extraído de un blob |32 000 |64 000 |4 millones |4 millones |4 millones |N/D <sup>2</sup> |

<sup>1</sup> nivel básico es Hola solo SKU con un límite de 100 campos por índice.

<sup>2</sup> S3 HD actualmente no admite indexadores. Póngase en contacto con el soporte técnico de Azure si necesita urgentemente esta funcionalidad.

<sup>3</sup> indizador de tiempo de ejecución máximo para el nivel gratis hello es 3 minutos para los orígenes de blob y 1 minuto para todos los demás orígenes de datos.

## <a name="document-size-limits"></a>Límites de tamaño de documento
| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Tamaño de documento individual por API de índice |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |<16 MB |

Se refiere a tamaño máximo del documento de toohello al llamar a una API de índice. Tamaño del documento es realmente un límite de tamaño de Hola de hello cuerpo de la solicitud de API de índice. Puesto que puede pasar un lote de varios documentos toohello API de índice a la vez, el límite de tamaño de Hola realmente depende de cuántos documentos se encuentran en el lote de Hola. Para un lote con un único documento, tamaño máximo del documento de hello es 16 MB de JSON.

tamaño del documento tookeep hacia abajo, recuerde tooexclude no se puede consultar datos de solicitud de saludo. Imágenes y otros datos binarios no son directamente consultables y no deben almacenarse en el índice de Hola. toointegrate no se puede consultar datos de los resultados de búsqueda, definir un campo de no búsqueda que almacena un recurso de toohello de referencia de dirección URL.

## <a name="workload-limits-queries-per-second"></a>Límites de carga de trabajo (consultas por segundo)
| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |N/D  |~ 3 por réplica |~ 15 por réplica |~ 60 por réplica |>60 por réplica |>60 por réplica |

Las consultas por segundo (QPS) es una aproximación basada en la heurística, con los valores de tooderive estimado de las cargas de trabajo simulada y real por el cliente. Rendimiento QPS exacto varía según la naturaleza de hello y datos de consulta de Hola.

Aunque se proporcionan cálculos aproximados anteriormente, una tasa real es toodetermine difícil, especialmente en hello que libre había compartido servicio donde el rendimiento se basa en el ancho de banda disponible y la competición por los recursos del sistema. En el nivel gratuito de hello, recursos de proceso y almacenamiento se comparten por varios suscriptores, por lo que el segundo de su solución siempre variará dependiendo de cuántas otras cargas de trabajo se ejecutan en hello mismo tiempo.

Nivel Hola estándar, puede hacer una estimación QPS más estrechamente porque tiene control sobre varios de los parámetros de Hola. Consulte la sección de procedimientos recomendado de hello en [administrar la solución de búsqueda](search-manage.md) para obtener instrucciones sobre cómo toocalculate QPS para las cargas de trabajo.

## <a name="api-request-limits"></a>Límites de solicitud de API
* Máximo de 16 MB por solicitud <sup>1</sup>
* Longitud máxima de dirección URL de 8 KB
* Máximo de 1000 documentos por lote del índice de cargas de índices, combinaciones o eliminaciones
* Máximo de 32 campos en cláusula $orderby
* El tamaño máximo del término de búsqueda es de 32 766 bytes (32 KB menos 2 bytes) de texto con codificación UTF-8

<sup>1</sup> en búsqueda de Azure, el cuerpo de Hola de una solicitud es límite tooan asunto de 16 MB, impone un límite práctico en contenido de Hola de campos individuales o colecciones que no están restringidas en caso contrario por límites teóricos (vea [compatibles tipos de datos](https://msdn.microsoft.com/library/azure/dn798938.aspx) para obtener más información acerca de la composición de campos y restricciones).

## <a name="api-response-limits"></a>Límites de respuesta de API
* Máximo de 1000 documentos devueltos por página de resultados de búsqueda
* Máximo de 100 sugerencias devueltas por solicitud de Sugerir API

## <a name="api-key-limits"></a>Límites de clave de API
Las claves de API se usan para la autenticación del servicio. Hay dos tipos. Las claves de administración se especifican en el encabezado de solicitud de Hola y conceder el servicio de toohello de acceso completo de lectura y escritura. Las claves de consulta son de solo lectura, especificado en la dirección URL de Hola y aplicaciones distribuidas normalmente tooclient.

* Máximo de 2 claves de administración por servicio
* Máximo de 50 claves de consultas por servicio
