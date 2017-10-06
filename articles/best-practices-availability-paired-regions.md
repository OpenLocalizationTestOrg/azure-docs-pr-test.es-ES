---
title: "Continuidad empresarial y recuperación ante desastres (BCDR): regiones emparejadas de Azure | Microsoft Docs"
description: "Obtenga información sobre Azure tooensure regional de emparejamiento, que las aplicaciones sean resistentes durante los errores de centro de datos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>Continuidad empresarial y recuperación ante desastres (BCDR): regiones emparejadas de Azure

## <a name="what-are-paired-regions"></a>¿Qué son las regiones emparejadas?

Azure opera en varias ubicaciones geográficas alrededor de Hola a todos. Una geografía Azure es un área definida de Hola a todos que contiene al menos una región de Azure. Una región de Azure es un área dentro de una ubicación geográfica que contiene uno o varios centros de datos.

Cada región de Azure se empareja con otra región dentro de hello mismo geography, realizar juntos un par regional. excepción de Hello es sur de Brasil, que se empareja con una región de fuera de su ubicación geográfica.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Ilustración 1: Diagrama de pareja regional de Azure

| Geography | Regiones emparejadas |  |
|:--- |:--- |:--- |
| Asia |Asia oriental |Sudeste asiático |
| Australia |Australia Oriental |Sudeste de Australia |
| Canadá |Centro de Canadá |Este de Canadá |
| China |Norte de China |Este de China|
| India |India Central |Sur de la India |
| Japón |Este de Japón |Oeste de Japón |
| Corea |Corea Central |Corea del Sur |
| Norteamérica |Centro-Norte de EE. UU |Centro-Sur de EE. UU |
| Norteamérica |Este de EE. UU. |Oeste de EE. UU. |
| Norteamérica |Este de EE. UU. 2 |Central EE. UU.: |
| Norteamérica |Oeste de EE. UU. 2 |Centro occidental de EE.UU. |
| Europa |Europa del Norte |Europa occidental |
| Japón |Este de Japón |Oeste de Japón |
| Brasil |Sur de Brasil (1) |Centro-Sur de EE. UU |
| Gobierno de Estados Unidos |Gobierno de EE. UU. - Iowa |Gobierno de EE. UU. - Virginia |
| Gobierno de Estados Unidos |Gobierno de EE. UU. - Virginia |Gobierno de EE. UU.: Texas |
| Gobierno de Estados Unidos |Gobierno de EE. UU.: Texas |Gobierno de EE. UU.: Arizona |
| Gobierno de Estados Unidos |Gobierno de EE. UU.: Arizona |Gobierno de EE. UU.: Texas |
| Reino Unido |Oeste de Reino Unido |Sur del Reino Unido 2 |
| Alemania |Centro de Alemania |Noreste de Alemania |

Tabla 1: Asignación de las parejas regionales de Azure

> Sur de Brasil (1) es un caso único porque se empareja con una región fuera de su propia ubicación geográfica. La región secundaria del Sur de Brasil es Centro y Sur de EE. UU., pero la región secundaria de esta última no es el Sur de Brasil.


Se recomienda que replique las cargas de trabajo entre pares regional toobenefit de directivas de aislamiento y la disponibilidad de Azure. Por ejemplo, se implementan las actualizaciones del sistema Azure planeada secuencialmente (no en hello mismo tiempo) a través de regiones emparejadas. Esto significa que incluso en el caso poco frecuente de Hola de una actualización defectuosa, ambas regiones no afectarán al mismo tiempo. Además, en hello improbable caso de una interrupción amplia, recuperación de al menos una región de cada par es un nivel de prioridad.

## <a name="an-example-of-paired-regions"></a>Un ejemplo de regiones emparejadas
La figura 2 muestra una aplicación hipotética que usa par regional hello para la recuperación ante desastres. Hola verde números resalte las actividades entre regiones de hello tres servicios de Azure (Azure cálculo, almacenamiento y la base de datos) y cómo estén configurados tooreplicate entre las regiones. ventajas exclusivas de Hola de implementación a través de regiones emparejadas se resaltan en los números de hello naranja.

![Información general sobre las ventajas de las regiones emparejadas](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Ilustración 2: Pareja regional de Azure hipotética

## <a name="cross-region-activities"></a>Actividades entre regiones
La figura 2 como tooin que se hace referencia.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **cálculo de Azure (PaaS)** : debe proporcionar recursos de proceso adicional de antemano tooensure recursos están disponibles en otra región durante un desastre. Para obtener más información, consulte [Guía técnica sobre resistencia en Azure](resiliency/resiliency-technical-guidance.md).

![Storage](./media/best-practices-availability-paired-regions/2Green.png)**Azure Storage**: el almacenamiento con redundancia geográfica (GRS) se configura de manera predeterminada cuando se crea una cuenta de Azure Storage. Con la GRS, los datos se replican automáticamente tres veces dentro de la región principal de Hola y tres veces en la región emparejada Hola. Para obtener más información, consulte [Opciones de redundancia de Almacenamiento de Azure](storage/common/storage-redundancy.md).

![SQL Azure](./media/best-practices-availability-paired-regions/3Green.png) **bases de datos de SQL Azure** – con Azure SQL replicación geográfica estándar, puede configurar la replicación asincrónica de región emparejada tooa de transacciones. Con la replicación geográfica premium, puede configurar región tooany de replicación de Hola a todos; Sin embargo, se recomienda que implementar estos recursos en una región emparejada para la mayoría de los escenarios de recuperación de desastres. Para más información, consulte [Replicación geográfica en Azure SQL Database](sql-database/sql-database-geo-replication-overview.md).

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png)**Azure Resource Manager**: Azure Resource Manager proporciona de forma inherente aislamiento lógico para los componentes de administración de servicios entre regiones. Esto significa que los errores lógicos en una región son tooimpact menos probable que otra.

## <a name="benefits-of-paired-regions"></a>Ventajas de las regiones emparejadas
La figura 2 como tooin que se hace referencia.  

![Aislamiento](./media/best-practices-availability-paired-regions/5Orange.png)
**Aislamiento físico**: cuando sea posible, Azure prefiere por lo menos 300 millas de separación entre los centros de datos de un emparejamiento regional, aunque esto no será práctico o posible en todo el mundo. Separación de centro de datos físico reduce la probabilidad de Hola de desastres naturales, disturbios civiles, cortes del suministro eléctrico o interrupciones de red física a la vez que afectan a ambas regiones. El aislamiento es restricciones de toohello asunto dentro de geography de hello (tamaño de geography, disponibilidad de la infraestructura de red o de alimentación, normativas, etcetera).  

![Replicación](./media/best-practices-availability-paired-regions/6Orange.png)
**replicación proporcionada por la plataforma** -algunos servicios, como el almacenamiento con redundancia geográfica proporcionar región emparejada de toohello de replicación automática.

![Recuperación](./media/best-practices-availability-paired-regions/7Orange.png)
**orden de recuperación de región** : en caso de hello de una amplia interrupción, se establece una prioridad de recuperación de una región fuera de cada par. Se garantiza que las aplicaciones que se implementan a través de regiones emparejadas toohave una de las regiones de hello recuperado con prioridad. Si una aplicación se implementa en diferentes regiones que no están emparejadas, podría retrasarse recuperación: Hola peor regiones elegido Hola casos se puede Hola toobe dos últimas recuperado.

![Las actualizaciones de](./media/best-practices-availability-paired-regions/8Orange.png)
**actualizaciones secuenciales** : actualizaciones del sistema Azure planeada se implementan regiones toopaired secuencialmente (no en hello vez) toominimize de tiempo de inactividad, efecto Hola de errores y errores lógicos en evento poco habitual de Hola de una actualización incorrecta.

![Datos](./media/best-practices-availability-paired-regions/9Orange.png)
**residencia datos** – una región encuentra en hello mismo geography como su par (con excepción de Hola de sur de Brasil) en los requisitos de residencia de orden toomeet datos para fines de jurisdicción de cumplimiento de impuestos y derecho.
