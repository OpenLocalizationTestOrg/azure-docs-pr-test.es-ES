---
title: "aaaReplicate física tooAzure de servidores con Azure Site Recovery local | Documentos de Microsoft"
description: "Proporciona información general de los pasos de hello para la replicación de las cargas de trabajo que se ejecutan en local tooAzure de servidores físicos de Windows/Linux con hello servicio Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Replicar servidores físicos tooAzure con Site Recovery

Este artículo proporciona información general de hello pasos necesarios tooreplicate local Windows/Linux servidores físicos tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Paso 1: revisión de la arquitectura y requisitos previos

Antes de iniciar la implementación, revise la arquitectura del escenario de Hola y asegúrese de que comprende todos los componentes de hello deberá tooset la implementación de Hola.

Vaya demasiado[paso 1: revisar la arquitectura de Hola](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Paso 2: revisión de los requisitos previos

Asegúrese de que tiene requisitos previos de hello en su lugar para cada componente de implementación:

- **Requisitos previos de Azure**: necesita una cuenta de Microsoft Azure, redes de Azure y cuentas de almacenamiento.
- **Componentes locales de Site Recovery**: necesita una máquina que ejecute componentes locales de Site Recovery.
- **Replicar máquinas**: servidores que desea tooreplicate necesitan toocomply con local y requisitos de Azure.

Vaya demasiado[paso 2: revisar los requisitos previos y limitaciones](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Paso 3: planeamiento de la capacidad

Si está realizando una implementación completa debe toofigure qué recursos de replicación que se necesita. Si está realizando una rápida configurar tootest Hola entorno, puede omitir este paso.

Vaya demasiado[paso 3: planear la capacidad](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Paso 4: planeamiento de las redes

Debe toodo algunos planeación tooensure que máquinas virtuales de Azure son toonetworks conectado después de producirse la conmutación por error, y que disponen de hello derecho de direcciones IP de una red.

Vaya demasiado[paso 4: planear las redes](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Paso 5: preparación de los recursos de Azure

Antes de empezar hay que configurar las redes y el almacenamiento de Azure. 

Vaya demasiado[paso 5: preparar Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Paso 6: Configurar un almacén

Configurar una tooorchestrate de almacén de servicios de recuperación y administrar la replicación. Al configurar el almacén de hello, especifique qué desea tooreplicate, y donde quiera tooreplicate a.

Vaya demasiado[paso 6: configurar un almacén](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Paso 7: Configurar los valores de origen y destino

Configurar las opciones para el origen de Hola y sitio (Azure) de destino. Configuración de código fuente incluye ejecutando el programa de instalación unificada tooinstall componentes de Site Recovery de hello locales.

Vaya demasiado[paso 7: configurar el origen de Hola y de destino](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Paso 8: Configurar una directiva de replicación

Configurar una directiva toospecify cómo físico de servidores deben replicar.

Vaya demasiado[paso 8: configurar una directiva de replicación](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Paso 9: Instalar el servicio de movilidad de Hola

servicio de movilidad de Hello debe estar instalado en cada servidor que desee tooreplicate. Hay unos tooset formas servicio hello, con la instalación de inserción o extracción.

Vaya demasiado[paso 9: instalar el servicio de movilidad de Hola](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Paso 10: habilitación de la replicación

Después de hello Mobility service se ejecuta en un servidor, puede habilitar la replicación. Después de habilitar esta opción, se produce la replicación inicial de hello máquina virtual.

Vaya demasiado[paso 10: habilitar la replicación](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Paso 11: ejecución de una conmutación por error de prueba

Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.

Vaya demasiado[paso 11: ejecutar una prueba de conmutación por error](physical-walkthrough-test-failover.md)

