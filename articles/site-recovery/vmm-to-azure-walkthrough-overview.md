---
title: "nubes de máquinas virtuales de Hyper-V en VMM aaaReplicate tooAzure con Azure Site Recovery | Documentos de Microsoft"
description: "Proporciona información general para la replicación de máquinas virtuales de Hyper-V en tooAzure de nubes VMM con el servicio de Azure Site Recovery Hola"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM con Site Recovery en hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-vmm-to-azure.md)
> * [Azure clásico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell clásico](site-recovery-deploy-with-powershell.md)


Este artículo se proporciona una visión general de hello pasos necesarios tooreplicate máquinas de virtuales de Hyper-V (VM) administradas en tooAzure de nubes de System Center Virtual Machine Manager (VMM), con hello local [Azure Site Recovery](site-recovery-overview.md) servicio en Hola portal de Azure.

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Paso 1: Revisar la arquitectura del escenario de Hola

Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello debe toodeploy.

Vaya demasiado[paso 1: revisar la arquitectura de Hola](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Paso 2: Revisión de los requisitos previos y las limitaciones

Asegúrese de que comprende las limitaciones y requisitos previos de implementación de Hola.

**Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.
**Servidores VMM locales y hosts de Hyper-V**: asegúrese de que los servidores VMM y los hosts de Hyper-V son compatibles y están preparados para la implementación de Site Recovery.
**Replicar máquinas virtuales**: Compruebe que las máquinas virtuales que desee tooreplicate cumplan con requisitos de Azure.

Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Paso 3: planeamiento de la capacidad

Si está realizando una implementación completa, deberá toofigure qué recursos de replicación que se necesita. Hay un par de toohelp de herramientas disponibles para ello. Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.

Vaya demasiado[paso 3: planear la capacidad](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Paso 4: planeamiento de las redes

Debe toodo alguna de las redes planeación tooensure que puede configurar la asignación de red al implementar el escenario de hello, máquinas virtuales de Azure será tooAzure conectado las redes virtuales después de que se produce la conmutación por error y que estén asignados IP adecuado se resuelve.

Vaya demasiado[paso 4: planear las redes](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Paso 5: preparación de los recursos de Azure

Configure almacenamiento, redes y una cuenta de Azure. Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.

Vaya demasiado[paso 5: preparar Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Paso 6: Preparación de VMM y Hyper-V

Preparar servidores VMM locales de Hola y hosts de Hyper-V para la implementación de Site Recovery.

Vaya demasiado[paso 6: preparar servidores locales](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Paso 7: configuración de un almacén

Configure un almacén de Recovery Services. Hola almacén contiene valores de configuración y organiza la replicación.

[Step 7: Set up a vault](vmm-to-azure-walkthrough-create-vault.md) (Paso 7: Configuración de un almacén)

## <a name="step-8-configure-source-and-target-settings"></a>Paso 8: configuración de los valores de origen y destino

Configurar ubicaciones de replicación de origen y destino de Hola. Agregar el almacén de toohello de servidor VMM hello y descargar archivos de instalación de Hola para los componentes de Site Recovery. Ejecute el programa de instalación del proveedor de Azure Site Recovery en el servidor VMM Hola. El programa de instalación instala Hola proveedor en el servidor VMM de Hola y registra el servidor hello en el almacén de Hola. Instalar a agente de servicios de recuperación de Microsoft de hello en cada host de Hyper-V.

Vaya demasiado[paso 8: configurar opciones de origen y de destino](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Paso 9: Configuración de la asignación de red

Asignación de redes virtuales de tooAzure de redes de VM de VMM en local. Después de la conmutación por error, máquinas virtuales de Azure se crean en hello red de Azure que se asigna la red de máquina virtual local toohello en qué Hola Hyper-V de origen se encuentra.

Vaya demasiado[paso 9: configurar la asignación de red](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Paso 10: Configuración de una directiva de replicación

Especificar cómo máquinas virtuales locales serán tooAzure replicada.

Vaya demasiado[paso 10: configurar una directiva de replicación](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Paso 11: Habilitación de la replicación para máquinas virtuales

Seleccione hello las máquinas virtuales que desee tooreplicate. Habilitación de una máquina virtual para tooAzure de replicación inicial de Hola de desencadenadores de replicación, seguido de la replicación de datos en curso.

Vaya demasiado[paso 11: habilitar la replicación](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Paso 12: Ejecución de una conmutación por error de prueba

Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.

Vaya demasiado[paso 12: ejecutar una prueba de conmutación por error](vmm-to-azure-walkthrough-test-failover.md)


