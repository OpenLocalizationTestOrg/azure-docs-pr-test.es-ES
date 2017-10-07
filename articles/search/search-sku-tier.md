---
title: "aaaChoose una SKU o nivel de precios para la búsqueda de Azure | Documentos de Microsoft"
description: "El servicio Búsqueda de Azure puede aprovisionarse en estas SKU: Gratis, Básico o Estándar; este último está disponible en varias configuraciones de recursos y niveles de capacidad."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Selección de SKU o plan de tarifa de Búsqueda de Azure
En Azure Search, un [servicio se aprovisiona](search-create-service-portal.md) en un plan de tarifa específico o SKU. Las opciones incluyen los niveles **Gratis**, **Básico** o **Estándar**; **este último** está disponible en varias configuraciones y capacidades.

Hola de este artículo sirve toohelp elegir un nivel. Si la capacidad de un nivel resulta toobe demasiado bajo, necesitará tooprovision un nuevo servicio en el nivel superior de hello y, a continuación, volver a cargar los índices. No hay ninguna actualización en contexto de hello mismo servicio desde un tooanother SKU.

> [!NOTE]
> Después de elegir un nivel y [aprovisionar un servicio de búsqueda](search-create-service-portal.md), puede aumentar la réplica y recuentos de partición de servicio de Hola. Para obtener instrucciones, consulte [Escalado de niveles de recursos para cargas de trabajo de indexación y consulta](search-capacity-planning.md).
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>¿Cómo tooapproach un precio de nivel de decisión
En búsqueda de Azure, nivel de Hola determina la capacidad, disponibilidad de las características no. Generalmente, todas las características están disponibles en cada nivel, incluidas las de vista previa. Hola única excepción no es se admite para los indizadores en HD S3.

> [!TIP]
> Se recomienda que aprovisione siempre un servicio **gratis** (uno por cada suscripción sin expiración) para que esté fácilmente disponible para los proyectos ligeros. Hola de uso **libre** de servicio de prueba y evaluación; crear un segundo servicio facturable en hello **básica** o **estándar** nivel para mayores cargas de trabajo de prueba o producción.
>
>

Capacidad y los costos de ejecutar el servicio de hello van en la mano. Información de este artículo puede ayudarle a decidir qué SKU ofrece equilibrio adecuado de hello, pero para la parte de ella toobe útil, necesita al menos cálculos aproximados en siguientes hello:

* Número y tamaño de los índices tiene previsto toocreate
* Número y tamaño de tooupload de documentos
* Una idea del volumen de consultas, en términos de consultas por segundo (QPS)

Número y tamaño son importantes porque se alcanzan los límites máximos a través de un límite fijo en el recuento de Hola de índices o de documentos en un servicio o en los recursos (almacenamiento de información o réplicas) utilizados por el servicio de Hola. Hola límite real para el servicio es lo que se usa primero: recursos u objetos.

Con las estimaciones de mano, Hola pasos debe simplificar el proceso de hello:

* **Paso 1** revisar las descripciones de SKU de hello debajo toolearn sobre las opciones disponibles.
* **Paso 2** responder a preguntas de hello debajo tooarrive en una decisión preliminar.
* **Paso 3** Finalizar la decisión revisando los límites estrictos de almacenamiento y precios.

## <a name="sku-descriptions"></a>Descripciones de las SKU
Hello en la tabla siguiente proporciona descripciones de cada nivel.

| Nivel: | Escenarios principales |
| --- | --- |
| **Gratis** |Un servicio compartido gratuito utilizado para cargas de trabajo de evaluación o investigación reducidas. Dado que se comparte con otros suscriptores, rendimiento de la consulta e indización varía en función de quién más está utilizando el servicio de Hola. La capacidad es pequeña (50 MB o tres índices con hasta 10.000 documentos cada uno). |
| **Básica** |Cargas de trabajo de producción reducidas en hardware específico. Se trata de un nivel de alta disponibilidad. La capacidad es too3 réplicas y 1 partición (2 GB). |
| **S1** |Estándar 1 admite combinaciones flexibles de particiones (12) y réplicas (12). Se utiliza para cargas de trabajo de producción normales en hardware específico. Puede asignar particiones y réplicas en combinaciones que admitan un máximo de 36 unidades de búsqueda facturables. En este nivel, las particiones son de 25 GB cada una y QPS es aproximadamente de 15 consultas por segundo. |
| **S2** |2 estándar se ejecuta mayores cargas de trabajo de producción con unidades de búsqueda de hello 36 mismo como S1 pero con las réplicas y particiones de un tamaño mayor. En este nivel, las particiones tienen 100 GB y QPS es aproximadamente de 60 consultas por segundo. |
| **S3** |3 estándar se ejecuta proporcionalmente mayores cargas de trabajo de producción en sistemas más avanzados, en configuraciones de seguridad de las particiones de too12 o 12 réplicas en 36 unidades de búsqueda. En este nivel, las particiones son de 200 GB cada una y QPS tiene más de 60 consultas por segundo. |
| **S3 HD** |Estándar 3 de alta densidad está diseñado para un gran número de índices más pequeños. Puede tener hasta too3 particiones, en 200 GB. QPS tiene más de 60 consultas por segundo. |

> [!NOTE]
> Valores máximos de réplica y la partición se facturan como unidades de búsqueda (unidad 36 máximo por servicio), que impone un límite inferior de efectivo que implica el máximo de hello en valor nominal. Por ejemplo, toouse máximo de Hola de 12 réplicas, podría tener como máximo 3 particiones (3 * 12 = 36 unidades). De forma similar, toouse particiones máximas, reducir too3 de réplicas. Consulte [Planeación de la capacidad en Búsqueda de Azure](search-capacity-planning.md) para ver un gráfico de las combinaciones que pueden realizarse.
>
>

## <a name="review-limits-per-tier"></a>Revisión de los límites por nivel
Hello gráfico siguiente es un subconjunto de los límites de Hola de [límites de servicio de búsqueda de Azure](search-limits-quotas-capacity.md). Muestra hello factores probablemente tooimpact una decisión de SKU. Gráfico de toothis puede hacer referencia al revisar las siguientes preguntas de Hola.

| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrato de nivel de servicio (SLA) |No <sup>1</sup> |Sí |Sí |Sí |Sí |yes |
| Límites de índice |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Límites de documento |10 000 en total |1 millón por servicio |15 millones por partición |60 millones por partición |120 millones por partición |1 millón por índice |
| Número máximo de particiones |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Tamaño de la partición |50 MB en total |2 GB por servicio |25 GB por partición |100 GB por partición (arriba tooa máximo de 1,2 TB por servicio) |200 GB por partición (arriba tooa máximo de 2,4 TB por servicio) |200 GB (arriba tooa máximo de 600 GB por servicio) |
| Número máximo de réplicas |N/D |3 |12 |12 |12 |12 |
| Consultas por segundo |N/D |~ 3 por réplica |~ 15 por réplica |~ 60 por réplica |>60 por réplica |>60 por réplica |

<sup>1</sup> Las versiones gratuitas y preliminares no incluyen contratos de nivel de servicio (SLA). Para todos los niveles facturables, los SLA tomarán efecto cuando se aprovisione suficiente redundancia para el servicio. Son necesarias dos o más réplicas para el SLA de consulta (lectura). Son necesarias tres o más réplicas para el SLA de consulta e indexación (lectura y escritura). número de Hola de particiones no es una consideración de SLA. 

<sup>2</sup> S3 y S3 HD están respaldados por la misma infraestructura de alta capacidad, pero cada uno de ellos alcanza su límite máximo de maneras diferentes. S3 se dirige a un menor número de índices muy grandes. Como tal, su límite máximo es el límite de recursos (2,4 TB para cada servicio). S3 HD se dirige a un gran número de índices muy pequeños. En los índices de 1.000, S3 HD alcanza sus límites en forma de Hola de restricciones de índice. Si es un cliente de S3 HD que requiera más de 1.000 índices, póngase en contacto con Microsoft Support para obtener información acerca de cómo tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Eliminación de las SKU que no cumplen los requisitos
Hola siguientes preguntas puede ayudarle a llegar a la decisión de SKU correcta de hello para la carga de trabajo.

1. ¿Tiene requisitos de **SLA** ? Puede usar cualquier nivel facturable (Básico y superiores), pero debe configurar el servicio en pos de la redundancia. Son necesarias dos o más réplicas para el SLA de consulta (lectura). Son necesarias tres o más réplicas para el SLA de consulta e indexación (lectura y escritura). número de Hola de particiones no es una consideración de SLA.
2. ¿**Cuántos índices** necesita? Uno de variables mayores Hola factorizar en una decisión de SKU es el número de Hola de índices compatibles con cada SKU. La compatibilidad con índices es en gran medida distintos niveles de hello inferior los niveles de precios. Los requisitos de número de índices podrían ser un factor determinante para decidir qué SKU elegir.
3. **Cuántos documentos** se va a cargar en cada índice? Hola número y tamaño de los documentos determinará el tamaño final de Hola de índice de Hola. Suponiendo que se puede calcular Hola tamaño previsto de índice de hello, puede comparar ese número en el tamaño de la partición de Hola por SKU, que se extiende por número de Hola de particiones necesarios toostore un índice de ese tamaño.
4. **¿Qué es la carga de consulta esperado de hello**? Una vez que entiende los requisitos de almacenamiento, tenga en cuenta las cargas de trabajo de consultas. Las SKU de los niveles S2 y S3 ofrecen prácticamente el mismo rendimiento, pero los requisitos de SLA excluirán todas las SKU de vista previa.
5. Si está pensando en Hola S2 o S3 capa, determinar si necesita [indizadores](search-indexer-overview.md). Los indizadores todavía no están disponibles para el nivel de hello S3 HD. Solución alternativa es toouse un modelo de inserción para las actualizaciones del índice, donde se escribe toopush de código de aplicación, un índice de tooan del conjunto de datos.

Mayoría de los clientes puede regla una SKU específica o no en función de su toohello respuestas sobre preguntas. Si todavía no está seguro de qué toogo SKU con, puede publicar preguntas tooMSDN o foros de StackOverflow o póngase en contacto con el soporte técnico de Azure para obtener más información.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>¿Validación de decisión: Hola SKU proporcionan suficiente espacio de almacenamiento y el segundo?
Como último paso, volver a visitar hello [página de precios](https://azure.microsoft.com/pricing/details/search/) hello y [secciones por servicio y por índice de límites de servicio](search-limits-quotas-capacity.md) toodouble comprobación sus estimaciones en límites de suscripción y el servicio.

Si ambos requisitos de almacenamiento o el precio de hello están fuera de los límites, conviene cargas de trabajo de toorefactor Hola entre varios servicios más pequeños (por ejemplo). En el nivel más granular, podría volver a diseñar índices toobe más pequeño, utilice filtros o toomake consultas más eficaces.

> [!NOTE]
> Los requisitos de almacenamiento pueden ser demasiado excesivos si los documentos contienen datos extraños. Lo ideal es que los documentos contengan solamente datos utilizables en búsquedas o metadatos. Datos binarios no permite búsquedas y deben almacenarse por separado (por ejemplo, en un almacenamiento de tablas o blobs de Azure) con un campo de índice de hello toohold un datos externos de dirección URL referencia toohello. tamaño máximo de Hola de un documento individual es 16 MB (o menos si es masiva cargar varios documentos en una sola solicitud). Consulte [Límites de servicio en la Búsqueda de Azure](search-limits-quotas-capacity.md) para obtener más información.
>
>

## <a name="next-step"></a>Paso siguiente
Una vez que sepa que SKU es hello ajustarse a la derecha, continúe con estos pasos:

* [Crear un servicio de búsqueda en el portal de Hola](search-create-service-portal.md)
* [Cambiar el servicio de asignación de Hola de tooscale particiones y réplicas](search-capacity-planning.md)
