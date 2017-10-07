---
title: "aaaReplicate tooAzure de máquinas virtuales VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Proporciona información general de los pasos de hello para la replicación de las cargas de trabajo que se ejecutan en máquinas virtuales VMware tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Replicar máquinas virtuales VMware tooAzure con Site Recovery

Este artículo proporciona información general de hello pasos necesarios tooreplicate local VMware máquinas virtuales tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


![Proceso de implementación](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Figura 1: Resumen del proceso de implementación**

## <a name="step-1-review-architecture-and-prerequisites"></a>Paso 1: revisión de la arquitectura y requisitos previos

Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello necesita toodeploy

Vaya demasiado[paso 1: revisar la arquitectura de Hola](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Paso 2: revisión de los requisitos previos

Asegúrese de que tiene requisitos previos de hello en su lugar para cada componente de implementación:

- **Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.
- **Componentes locales de Site Recovery**: necesita una máquina que ejecute componentes locales de Site Recovery.
- **Requisitos previos de VMware locales**: necesita tooset cuentas para que la recuperación del sitio puede tener acceso a los servidores de VMware y las máquinas virtuales.
- **Replicar máquinas virtuales**: las máquinas virtuales que desee tooreplicate necesidad toocomply requisitos de Azure y tener instalado el componente de servicio de movilidad de Hola.

Vaya demasiado[paso 2: revisar los requisitos previos y limitaciones](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Paso 3: planeamiento de la capacidad

Si está realizando una implementación completa debe toofigure qué recursos de replicación que se necesita. Hay un par de toohelp de herramientas disponibles para ello. Vaya tooStep 2. Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.

Vaya demasiado[paso 3: planear la capacidad](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Paso 4: planeamiento de las redes

Debe toodo algunos planeación tooensure que máquinas virtuales de Azure son toonetworks conectado después de producirse la conmutación por error, y que disponen de hello derecho de direcciones IP de una red.

Vaya demasiado[paso 4: planear las redes](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Paso 5: preparación de los recursos de Azure

Antes de empezar hay que configurar las redes y el almacenamiento de Azure. Puede hacerlo durante la implementación, pero se recomienda hacerlo antes de empezar.

Vaya demasiado[paso 5: preparar Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Paso 6: Preparación de VMware

Debe tooset las cuentas que va a usar para recuperación de sitio:

- Tooautomatically de servidores de virtualización de VMware de acceso detectar máquinas virtuales.
- Obtener acceso a servicio de movilidad de máquinas virtuales tooinstall Hola. Cada máquina virtual que desee tooreplicate debe tener instalado antes de el agente de servicio de movilidad de hello puede habilitar la replicación.

Vaya demasiado[paso 6: preparar VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Paso 7: configuración de un almacén

Necesita tooset seguridad un tooorchestrate de almacén de servicios de recuperación y administrar la replicación. Al configurar el almacén de hello, especifique qué desea tooreplicate, y donde quiera tooreplicate a.

Vaya demasiado[paso 7: configurar un almacén](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Paso 8: configuración de los valores de origen y destino

Configurar origen de Hola y de destino que se usa para la replicación. Establecer la configuración de origen incluye ejecutando el programa de instalación unificada tooinstall componentes de Site Recovery de hello locales.

Vaya demasiado[paso 8: configurar el origen de Hola y de destino](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Paso 9: configuración de una directiva de replicación

Configurar una configuración de directiva toospecify replicación para máquinas virtuales VMware en el almacén de Hola.

Vaya demasiado[paso 9: configurar una directiva de replicación](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Paso 10: Instalar el servicio de movilidad de Hola

servicio de movilidad de Hello debe estar instalado en cada máquina virtual que desee tooreplicate. Hay unos tooset formas servicio Hola con la instalación de inserción o extracción.

Vaya demasiado[paso 10: instalar el servicio de movilidad de Hola](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Paso 11: Habilitación de la replicación

Después de hello Mobility service se ejecuta en una máquina virtual se puede habilitar la replicación. Después de habilitar esta opción, se produce la replicación inicial de hello máquina virtual.

Vaya demasiado[paso 11: habilitar la replicación](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Paso 12: Ejecución de una conmutación por error de prueba

Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.

Vaya demasiado[paso 12: ejecutar una prueba de conmutación por error](vmware-walkthrough-test-failover.md)
