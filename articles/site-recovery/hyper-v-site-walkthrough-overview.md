---
title: "aaaReplicate tooAzure de máquinas virtuales de Hyper-V con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo la replicación tooorchestrate, conmutación por error y recuperación de local Hyper-V VM tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>Replicar tooAzure de máquinas virtuales (sin WMM) de Hyper-V 

> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure clásico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell: administrador de recursos](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

Este artículo proporciona información general de hello pasos necesarios tooreplicate local Hyper-V máquinas virtuales tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) Hola portal de Azure. En esta implementación, las máquinas virtuales de Hyper-V no están administradas por System Center Virtual Machine Manager (VMM).


Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Paso 1: revisión de la arquitectura y requisitos previos

Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello necesita toodeploy

Vaya demasiado[paso 1: revisar la arquitectura de Hola](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Paso 2: revisión de los requisitos previos

Asegúrese de que tiene requisitos previos de hello en su lugar para cada componente de implementación:

- **Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.
- **Requisitos previos de Hyper-V local**: asegúrese de que los hosts de Hyper-V están preparados para la implementación de Site Recovery.
- **Replicar máquinas virtuales**: las máquinas virtuales que desee tooreplicate necesita toocomply requisitos de Azure.

Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Paso 3: planeamiento de la capacidad

Si está realizando una implementación completa debe toofigure qué recursos de replicación que se necesita. Hay un par de toohelp de herramientas disponibles para ello. Vaya tooStep 2. Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.

Vaya demasiado[paso 3: planear la capacidad](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Paso 4: planeamiento de las redes

Debe toodo algunos planeación tooensure que máquinas virtuales de Azure son toonetworks conectado después de producirse la conmutación por error, y que disponen de hello derecho de direcciones IP de una red.

Vaya demasiado[paso 4: planear las redes](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Paso 5: preparación de los recursos de Azure

Antes de empezar hay que configurar las redes y el almacenamiento de Azure. Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.

Vaya demasiado[paso 5: preparar Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Paso 6: preparación de Hyper-V

Asegúrese de que los servidores de Hyper-V cumplen los requisitos de implementación de Site Recovery.

Vaya demasiado[paso 6: preparar Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Paso 7: configuración de un almacén

Necesita tooset seguridad un tooorchestrate de almacén de servicios de recuperación y administrar la replicación. Al configurar el almacén de hello, especifique qué desea tooreplicate, y donde quiera tooreplicate a.

Vaya demasiado[paso 7: crear un almacén](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Paso 8: configuración de los valores de origen y destino

Configurar origen de Hola y de destino que se usa para la replicación. Establecer la configuración de origen incluye la adición de hosts de Hyper-V tooa sitio de Hyper-V, instalar Hola proveedor de Site Recovery y el agente de servicios de recuperación en cada host de Hyper-V y registrar sitio Hola Hola que del almacén de servicios de recuperación.

Vaya demasiado[paso 8: configurar el origen de Hola y de destino](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Paso 9: configuración de una directiva de replicación

Configurar una configuración de directiva toospecify replicación para máquinas virtuales de Hyper-V en el almacén de Hola.

Vaya demasiado[paso 9: configurar una directiva de replicación](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Paso 10: habilitación de la replicación

Una vez que una directiva de replicación en su lugar, después de habilitar, se produce la replicación inicial de hello máquina virtual.

Vaya demasiado[paso 10: habilitar la replicación](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Paso 11: ejecución de una conmutación por error de prueba

Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.

Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](hyper-v-site-walkthrough-test-failover.md)
