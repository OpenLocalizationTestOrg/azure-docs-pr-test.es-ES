---
title: "aaaReplicate máquinas virtuales de Hyper-V tooa sitio VMM secundario con Azure Site Recovery | Documentos de Microsoft"
description: "Proporciona información general para la replicación de sitio máquinas virtuales de Hyper-V tooa VMM secundario con hello portal de Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicar máquinas virtuales de Hyper-V en el sitio secundario de VMM de VMM nubes tooa

> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clásico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell: administrador de recursos](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Este artículo proporciona información general de hello pasos necesarios tooreplicate máquinas de virtuales de Hyper-V (máquinas virtuales) administradas en nubes de System Center Virtual Machine Manager (VMM), tooa la ubicación secundaria de VMM, locales mediante [Azure Site Recovery](site-recovery-overview.md)Hola portal de Azure.

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Paso 1: Revisar la arquitectura del escenario de Hola

Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello debe toodeploy.

Vaya demasiado[paso 1: revisar la arquitectura de hello](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Paso 2: Revisión de los requisitos previos y las limitaciones

Asegúrese de que comprende las limitaciones y requisitos previos de implementación de Hola.

**Requisitos previos de Azure**: se necesita una suscripción de Microsoft Azure y servicios de recuperación de Azure del almacén, tooorchestrate y administrar la replicación.
**Servidores VMM locales y hosts de Hyper-V**: asegúrese de que los servidores VMM y los hosts de Hyper-V son compatibles y están preparados para la implementación de Site Recovery.

Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Paso 3: Planeamiento de redes

Debe toodo algunos tooensure que puede configurar la asignación de red entre redes de VM de VMM al implementar el escenario de Hola de planeación de una red.

Vaya demasiado[paso 3: planear las redes](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Paso 4: Preparación de VMM y de Hyper-V

Preparar servidores VMM de Hola y hosts de Hyper-V para la implementación de Site Recovery.

Vaya demasiado[paso 4: preparar servidores locales](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Paso 5: Configuración de un almacén

Configure un almacén de Recovery Services. Hola almacén contiene valores de configuración y organiza la replicación.

Vaya al [paso 5: Configuración de un almacén](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>Paso 6: Configuración de los valores de origen y destino

Configurar ubicaciones de VMM de replicación de origen y destino Hola. Agregar el almacén de toohello de servidores VMM hello y descargar archivos de instalación de Hola para los componentes de Site Recovery. Ejecute el programa de instalación del proveedor de Azure Site Recovery en el servidor VMM Hola. El programa de instalación instala Hola proveedor en el servidor VMM de Hola y registra el servidor hello en el almacén de Hola. Instalar a agente de servicios de recuperación de Microsoft de hello en cada host de Hyper-V.

Vaya demasiado[paso 6: configurar los parámetros de origen y de destino de hello](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Paso 7: Configuración de la asignación de red

Asigne redes de VM de VMM en las ubicaciones de origen y destino de Hola. Después de la conmutación por error, las máquinas virtuales se crean en la red de destino de hello esa red de VM de origen de mapas toohello en qué Hola se encuentra una VM de Hyper-V de origen.

Vaya demasiado[paso 7: configurar la asignación de red](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Paso 8: Configurar una directiva de replicación

Especifique cómo se replicarán las máquinas virtuales entre las ubicaciones de VMM.

Vaya demasiado[paso 8: configurar una directiva de replicación](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Paso 9: Habilitación de la replicación para máquinas virtuales

Seleccione hello las máquinas virtuales que desee tooreplicate. Habilitación de una máquina virtual para el sitio secundario de toohello de replicación inicial de Hola de replicación desencadenadores, seguido de la replicación de datos en curso.

Vaya demasiado[paso 9: Habilitar replicación](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Paso 10: Ejecución de una conmutación por error de prueba

Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.

Vaya demasiado[paso 10: ejecutar una prueba de conmutación por error](vmm-to-vmm-walkthrough-test-failover.md).
