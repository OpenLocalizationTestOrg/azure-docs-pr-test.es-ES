---
title: "aaaDisaster escenarios de recuperación para máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de qué toodo en caso de Hola que una interrupción del servicio Azure afecta a máquinas virtuales de Azure."
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>¿Qué toodo en caso de Hola que una interrupción del servicio Azure afecta a máquinas virtuales de Azure
En Microsoft, trabajamos duro toomake garantizan que nuestros servicios estén siempre disponible tooyou cuando los necesite. En ocasiones, debido a factores externos que escapan de nuestro control, se producen interrupciones de servicio no planeadas.

Microsoft proporciona Acuerdos de Nivel de Servicio para sus servicios como un compromiso en cuanto al tiempo de actividad y la conectividad. Hola SLA para servicios individuales de Azure se puede encontrar en [contratos de nivel de servicio de Azure](https://azure.microsoft.com/support/legal/sla/).

Azure ya integra en su plataforma muchas características que admiten aplicaciones de alta disponibilidad. Para obtener más información sobre estos servicios, lea [Recuperación ante desastres y alta disponibilidad para aplicaciones de Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

En este artículo se trata un escenario de recuperación ante desastres es true, al toda una región experimenta una interrupción inesperada debido a catástrofes naturales toomajor o interrupción del servicio generalizada. Estas son rara vez, pero debe preparar para la posibilidad de Hola que hay una interrupción de toda una región. Si una región entera experimenta una interrupción del servicio, las copias redundantes locales de Hola de los datos temporalmente estarían disponibles. Si ha habilitado la replicación geográfica, se almacenan en una región distinta tres copias adicionales de los blobs y las tablas de Azure Storage. En caso de hello de una interrupción regional completa o un desastre en qué Hola región principal no es recuperable, Azure reasignará todas de región de replicación geográfica de hello DNS entradas toohello.

toohelp controlar estos rara vez, proporcionamos Hola instrucciones para máquinas virtuales de Azure en caso de hello de una interrupción del servicio de región todo Hola donde se implementa la aplicación de la máquina virtual de Azure.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Opción 1: inicio de una conmutación por error mediante Azure Site Recovery
Puede configurar Azure Site Recovery para las VM de modo que pueda recuperar la aplicación con un solo clic en cuestión de minutos. Puede replicar tooAzure región de su elección y regiones de toopaired no restringido. Puede empezar por [replicar las máquinas virtuales](https://aka.ms/a2a-getting-started). También puede [crear un plan de recuperación](../site-recovery/site-recovery-create-recovery-plans.md) para que se puede automatizar el proceso de todo conmutación por error de hello para la aplicación. También puede [su conmutaciones por error de prueba](../site-recovery/site-recovery-test-failover-to-azure.md) con antelación sin afectar a la replicación en curso de Hola o aplicación de producción. En caso de hello de una interrupción de la región principal, acaba [iniciar una conmutación por error](../site-recovery/site-recovery-failover.md) y volver a poner la aplicación en la región de destino.


## <a name="option-2-wait-for-recovery"></a>Opción 2: espera para recuperación
En este caso, no se requieren acciones por su parte. Saber que estamos trabajando diligentemente toorestore disponibilidad del servicio. Puede ver el estado actual del servicio hello en nuestro [panel de estado del servicio de Azure](https://azure.microsoft.com/status/).

Esto es Hola mejor opción si no ha configurado Azure Site Recovery, almacenamiento con redundancia geográfica con acceso de lectura o interrupción de toohello anterior de almacenamiento con redundancia geográfica. Si configuró almacenamiento con redundancia geográfica o almacenamiento con redundancia geográfica de acceso de lectura para la cuenta de almacenamiento de Hola donde se almacenan los discos duros virtuales (VHD) de VM, puede buscar la imagen base de toorecover Hola VHD e intente tooprovision una nueva máquina virtual del mismo. Esta no es la mejor opción, ya que no hay ninguna garantía de sincronización de datos. Por lo tanto, esta opción no está garantizada toowork.


> [!NOTE]
> Tenga en cuenta que no tiene ningún control sobre este proceso y que solo se producirá si se produce una interrupción del servicio en toda la región. Por este motivo, también debe basarse en otra estrategias de copia de seguridad específica de la aplicación tooachieve Hola máximo nivel de disponibilidad. Para obtener más información, vea la sección de hello en [estrategias de datos para la recuperación ante desastres](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Pasos siguientes

- Empiece a [proteger las aplicaciones que se ejecuten en máquinas virtuales de Azure](https://aka.ms/a2a-getting-started) con Azure Site Recovery.

- más información acerca de cómo tooimplement una recuperación ante desastres y estrategia de alta disponibilidad, vea toolearn [recuperación ante desastres y alta disponibilidad para las aplicaciones de Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- vea una descripción técnica detallada de capacidades de la plataforma de nube, toodevelop [orientación técnica de Azure resistencia](../resiliency/resiliency-technical-guidance.md).


- Si las instrucciones de hello no se desactive, o si desea que las operaciones de Microsoft toodo hello en su nombre, póngase en contacto con [soporte al cliente](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
