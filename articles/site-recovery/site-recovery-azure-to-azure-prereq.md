---
title: "aaaPrerequisites para tooAzure de replicación mediante el uso de Azure Site Recovery | Documentos de Microsoft"
description: "En este artículo se resume los requisitos previos para la replicación de máquinas virtuales y máquinas físicas tooAzure mediante el servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/01/2017
ms.author: rajanaki
ms.openlocfilehash: c66cea8b097a872bae57e7b42e659e58c4b0b1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replicating-azure-virtual-machines-tooanother-region-by-using-azure-site-recovery"></a>Requisitos previos para la replicación de máquinas virtuales de Azure tooanother región mediante el uso de Azure Site Recovery

> [!div class="op_single_selector"]
> * [Replicar desde Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [Replicar desde tooAzure local](site-recovery-prereq.md)

Hola servicio Azure Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR) mediante la coordinación:
* Replicación de máquinas virtuales de Azure tooanother región de Azure.
* Replicación de local máquinas virtuales y servidores tooAzure o tooa secundaria centro de datos físico. 

Cuando se producen interrupciones en la ubicación principal, puede conmutar tooa ubicación secundaria tookeep aplicaciones y cargas de trabajo disponibles. Puede producir un error de ubicación principal tooyour atrás cuando devuelve las operaciones de toonormal. Consulte [¿Qué es Site Recovery?](site-recovery-overview.md) para más información sobre Site Recovery.

En este artículo se resume Hola requisitos previos necesarios toobegin replicación de Site Recovery de tooAzure local.

Registrar cualquier comentario final Hola de artículo de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="azure-requirements"></a>Requisitos de Azure

**Requisito** | **Detalles**
--- | ---
**Cuenta de Azure** | Una cuenta de [Microsoft Azure](http://azure.microsoft.com/) .<br/><br/> Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
**Servicio Site Recovery** | Para más información sobre los precios de Site Recovery, consulte los [precios de Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). Le recomendamos que cree un almacén de servicios de recuperación de destino de hello región de Azure que desea toouse como una ubicación de recuperación ante desastres. Por ejemplo, si el origen de las máquinas virtuales se ejecutan en UU y desea tooreplicate tooCentral nos, recomendamos que cree el almacén de hello zona horaria del Pacífico Central.|
**Capacidad de Azure** | Hola destino de región de Azure que desea toouse sea su ubicación de recuperación ante desastres, debe toohave una suscripción con una capacidad suficiente para máquinas virtuales, las cuentas de almacenamiento y componentes de red. Puede ponerse en contacto con soporte tooadd mayor capacidad.
**Instrucciones sobre almacenamiento** | Asegúrese de seguir hello [instrucciones sobre el almacenamiento](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) para el origen de virtual de Azure máquinas tooavoid cualquier problema de rendimiento. Si sigue la configuración predeterminada de hello, Site Recovery crea cuentas de almacenamiento de hello necesaria en función de la configuración del origen de Hola. Si ha personalizado y seleccione su propia configuración, asegúrese de seguir hello [objetivos de escalabilidad de discos de máquina virtual](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Instrucciones sobre redes** | Necesita conectividad saliente de hello toowhitelist desde la VM de Azure para intervalos de direcciones URL o una dirección IP específica. Para obtener más información, consulte toohello [redes orientación para la replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md) artículo.
**MV de Azure** | Asegúrese de que todos los certificados raíz de la últimos Hola están presentes en Windows hello o VM de Linux. Si no hay certificados raíz más recientes de hello, Hola VM no puede ser registrado tooSite recuperación debido a restricciones de toosecurity.

>[!NOTE]
>Para obtener más detalles sobre la compatibilidad para configuraciones específicas, lea hello [matriz de compatibilidad](site-recovery-support-matrix-azure-to-azure.md).

## <a name="next-steps"></a>Pasos siguientes
- Para más información, consulte el artículo [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) (Instrucciones de redes para la replicación de máquinas virtuales de Azure).
- Comience a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure.md).
