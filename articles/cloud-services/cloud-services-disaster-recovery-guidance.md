---
title: "aaaWhat toodo en caso de hello de una interrupción del servicio de Azure que afecta a los servicios de nube de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué toodo en caso de hello de una interrupción del servicio de Azure que afecta a los servicios de nube de Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>¿Qué toodo en caso de hello de una interrupción del servicio de Azure que afecta a los servicios de nube de Azure
En Microsoft, trabajamos duro toomake garantizan que nuestros servicios estén siempre disponible tooyou cuando los necesite. En ocasiones, debido a factores externos que escapan de nuestro control, se producen interrupciones de servicio no planeadas.

Microsoft proporciona Acuerdos de Nivel de Servicio para sus servicios como un compromiso en cuanto al tiempo de actividad y la conectividad. Hola SLA para servicios individuales de Azure se puede encontrar en [contratos de nivel de servicio de Azure](https://azure.microsoft.com/support/legal/sla/).

Azure ya integra en su plataforma muchas características que admiten aplicaciones de alta disponibilidad. Para obtener más información sobre estos servicios, lea [Recuperación ante desastres y alta disponibilidad para aplicaciones de Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

En este artículo se trata un escenario de recuperación ante desastres es true, al toda una región experimenta una interrupción inesperada debido a catástrofes naturales toomajor o interrupción del servicio generalizada. Estas son rara vez, pero debe preparar para la posibilidad de Hola que hay una interrupción de toda una región. Si una región entera experimenta una interrupción del servicio, las copias redundantes locales de Hola de los datos temporalmente estarían disponibles. Si ha habilitado la replicación geográfica, se almacenan en una región distinta tres copias adicionales de los blobs y las tablas de Azure Storage. En caso de hello de una interrupción regional completa o un desastre en qué Hola región principal no es recuperable, Azure reasignará todas de región de replicación geográfica de hello DNS entradas toohello.

> [!NOTE]
> Tenga en cuenta que no tiene ningún control sobre este proceso y que solo se producirá si se da una interrupción del servicio en todo el centro de datos. Por este motivo, también debe basarse en otra estrategias de copia de seguridad específica de la aplicación tooachieve Hola máximo nivel de disponibilidad. Para más información, consulte [Recuperación ante desastres y alta disponibilidad para aplicaciones creadas en Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Si desea que toobe pueda tooaffect su propio conmutación por error, conviene uso de hello tooconsider de [almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), que crea una copia de solo lectura de los datos en otra región.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Opción 1: uso de una implementación de copia de seguridad a través de Azure Traffic Manager
solución de recuperación ante desastres más sólida Hola implica mantener varias implementaciones de la aplicación en diferentes regiones para después utilizarla [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) toodirect tráfico entre ellas. Traffic Manager de Azure proporciona varias [métodos de enrutamiento](../traffic-manager/traffic-manager-routing-methods.md), por lo que puede elegir si toomanage las implementaciones con un modelo de copia de seguridad o principal o toosplit tráfico entre ellos.

![Equilibrio de Azure Cloud Services en distintas regiones con Azure Traffic Manager](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Hola más rápida respuesta toohello pérdida de una región, es importante configurar Traffic Manager [supervisión de extremos](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Opción 2: Implementar la nueva área de aplicación tooa
Mantener varias implementaciones activas tal como se describe en la opción anterior Hola incurre en los costes adicionales. Si su objetivo de tiempo de recuperación (RTO) es lo suficientemente flexible y tiene código original de Hola o paquete de servicios en la nube compilada, puede crear una nueva instancia de la aplicación en otra región y actualizar el DNS registros toopoint toohello nueva implementación.

Para obtener información más detallada acerca de cómo toocreate e implementar una aplicación de servicio de nube, consulte [cómo toocreate e implementar un servicio de nube](cloud-services-how-to-create-deploy-portal.md).

Dependiendo de los orígenes de datos de aplicación, puede necesitar procedimientos de recuperación de toocheck hello para el origen de datos de aplicación.

* Para los orígenes de datos de almacenamiento de Azure, consulte [replicación de almacenamiento de Azure](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck opciones de Hola que están disponibles en función de Hola eligió model de replicación para la aplicación.
* Para los orígenes de la base de datos SQL, leer [información general: negocio continuidad y la base de datos de recuperación ante desastres con base de datos SQL en la nube](../sql-database/sql-database-business-continuity.md) toocheck opciones de Hola que están disponibles en función de modelo de replicación de hello elegido para la aplicación.


## <a name="option-3-wait-for-recovery"></a>Opción 3: espera a la recuperación
En este caso, se requiere ninguna acción por su parte, pero el servicio no estará disponible hasta que se restaure la región de Hola. Puede ver el estado actual del servicio hello en hello [panel de estado del servicio de Azure](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Pasos siguientes
más información acerca de cómo tooimplement una recuperación ante desastres y estrategia de alta disponibilidad, vea toolearn [recuperación ante desastres y alta disponibilidad para las aplicaciones de Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

vea una descripción técnica detallada de capacidades de la plataforma de nube, toodevelop [orientación técnica de Azure resistencia](../resiliency/resiliency-technical-guidance.md).
