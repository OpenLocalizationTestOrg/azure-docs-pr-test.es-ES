---
title: "requisitos previos de hello aaaReview para la replicación de tooAzure de Hyper-V (con System Center VMM) mediante Azure Site Recovery | Documentos de Microsoft"
description: "Describe los requisitos previos de Hola para configurar la replicación, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V local en tooAzure de nubes VMM, con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a1c30fd5-c979-473c-af44-4f725ad3e3ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: raynew
ms.openlocfilehash: de13a2d80b1a9a5d968a180d559f661ab11e70c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-with-vmm-tooazure-replication"></a>Paso 2: Revisar los requisitos previos de hello para la replicación de Hyper-V (con VMM) tooAzure

Una vez que está revisado hello [arquitectura del escenario](vmm-to-azure-walkthrough-architecture.md), lea este toomake artículo debe comprender los requisitos previos de implementación de Hola. 

## <a name="prerequisites-and-limitations"></a>Requisitos previos y limitaciones

**Requisito** | **Detalles**
--- | ---
**Cuenta de Azure** | Necesita una [cuenta de Microsoft Azure](http://azure.microsoft.com/).
**Almacenamiento de Azure** | Necesita un toostore replicado de datos de la cuenta de almacenamiento de Azure.<br/><br/> cuenta de almacenamiento de Hello debe estar en hello misma región que hello del almacén de servicios de recuperación de Azure.<br/><br/>Puede usar [almacenamiento con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) o almacenamiento con redundancia local. Se recomienda el almacenamiento con redundancia geográfica. Con el almacenamiento con redundancia geográfica, datos son resistente a errores si se produce una interrupción regional, o si no se puede recuperar la región principal de Hola.<br/><br/> Puede usar una cuenta de almacenamiento de Azure estándar o puede usar Azure [Premium Storage](../storage/common/storage-premium-storage.md). Premium Storage puede hospedar cargas de trabajo de E/S intensas y, normalmente, se usa para las máquinas virtuales que necesitan un alto rendimiento constante de E/S y latencia baja. Si utiliza Premium Storage para los datos replicados, también necesitará una cuenta de almacenamiento estándar Una cuenta de almacenamiento estándar almacena los registros de replicación que capturen datos tooon local de los cambios en curso.
**Red de Azure** | Necesita un [red Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md), toowhich máquinas virtuales de Azure conectarse después de la conmutación por error. red de Azure Hello debe ser una en hello misma región que hello del almacén de servicios de recuperación.
**Servidores de VMM locales** | Necesita uno o más servidores de VMM con System Center 2012 R2 o versiones posteriores.<br/><br/> Todos los servidores de VMM deben tener una o varias nubes privadas. Cada nube necesita uno o más grupos host.<br/><br/> servidor VMM Hola necesita acceso a internet.
**Hyper-V local** | Servidores de host de Hyper-V deben ejecutar al menos Windows Server 2012 R2 con habilitado el rol de Hyper-V de Hola o Microsoft Hyper-V Server 2012 R2. las actualizaciones más recientes de Hello deben instalarse.<br/><br/> host de Hyper-V de Hello debe encontrarse en un grupo de host VMM (que se encuentra en una nube VMM).<br/><br/> Un host debe tener una o más máquinas virtuales que desea tooreplicated.<br/><br/> Hosts de Hyper-V deben estar conectado toohello para tooAzure de replicación, directamente o con un servidor proxy de internet. Servidores de Hyper-V deben tener correcciones Hola descritas en el artículo [2961977](https://support.microsoft.com/kb/2961977).
**Máquinas virtuales de Hyper-V locales** | Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). nombre de la máquina virtual de Hola se puede modificar después de la replicación está habilitada. 




## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 3: planear la capacidad](vmm-to-azure-walkthrough-capacity.md)
