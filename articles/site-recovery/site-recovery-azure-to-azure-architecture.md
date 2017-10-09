---
title: "¿aaaHow realiza la replicación de máquina virtual de Azure entre el trabajo de regiones de Azure en Azure Site Recovery?  | Microsoft Docs"
description: "Este artículo proporciona información general de componentes y arquitectura que se usa al replicar máquinas virtuales de Azure entre regiones de Azure mediante el servicio de Azure Site Recovery Hola."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>¿Cómo funciona la replicación de máquinas virtuales de Azure en Site Recovery?


Este artículo describen los componentes de Hola y procesos implicados en la replicación y recuperación de máquinas virtuales de Azure (VM) desde una región tooanother mediante el uso de hello [Azure Site Recovery](site-recovery-overview.md) servicio.

>[!NOTE]
>Replicación de máquina virtual de Azure con hello servicio Site Recovery está actualmente en vista previa.

Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architectural-components"></a>Componentes de la arquitectura

Hola siguiente diagrama proporciona una visión general de un entorno de máquina virtual de Azure en una región específica (en este ejemplo, hello ubicación UU). En un entorno de máquina virtual de Azure:
- Las aplicaciones pueden ejecutarse en máquinas virtuales con discos repartidos entre cuentas de almacenamiento.
- Hola máquinas virtuales puede incluirse en una o más subredes dentro de una red virtual.

![Entorno de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Obtenga información acerca de los requisitos previos de implementación de Hola y los requisitos en hello [matriz de compatibilidad](site-recovery-support-matrix-azure-to-azure.md).

## <a name="replication-process"></a>Proceso de replicación

### <a name="step-1"></a>Paso 1

Cuando se habilita la replicación de máquina virtual de Azure en hello portal de Azure, Hola recursos que se muestran en hello después de diagrama y la tabla se crean automáticamente en la región de destino de Hola. De forma predeterminada, los recursos se crean en función de la configuración de la región de origen. Puede personalizar la configuración de destino de hello según sea necesario. [Más información](site-recovery-replicate-azure-to-azure.md).

![Habilitación del proceso de replicación, paso 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

**Recurso** | **Detalles**
--- | ---
**Grupo de recursos de destino** | Hola toowhich de grupo de recursos pertenecen máquinas virtuales replicadas después de la conmutación por error.
**Red virtual de destino** | red virtual de Hello en el que se encuentran máquinas virtuales replicadas después de la conmutación por error. Se crea una asignación de red entre las redes virtuales de origen y de destino y viceversa.
**Cuentas de almacenamiento en caché** | Antes de que los cambios en el origen de que las máquinas virtuales repliquen toohello cuenta de almacenamiento de destino, se realiza un seguimiento y envían toohello cuenta de almacenamiento de caché en la ubicación de destino de Hola. Esto garantiza un impacto mínimo en aplicaciones de producción que se ejecutan en VM de Hola.
**Cuentas de almacenamiento de destino**  | Cuentas de almacenamiento de datos de hello destino ubicación toowhich Hola se replica.
**Conjuntos de disponibilidad de destino**  | Conjuntos de disponibilidad de qué Hola replicar las máquinas virtuales se encuentran después de la conmutación por error.

### <a name="step-2"></a>Paso 2

Como la replicación está habilitada, Hola extensión servicio de movilidad de Site Recovery se instala automáticamente en hello máquina virtual. se produce el siguiente Hello:

1. Hola VM está registrado con Site Recovery.

2. La replicación continua está configurada para hello máquina virtual. Escrituras de datos en hello VM discos estén continuamente transfieren toohello cuenta de almacenamiento de caché en la ubicación de origen de Hola.

   ![Habilitación del proceso de replicación, paso 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > Recuperación del sitio nunca necesita conectividad entrante toohello máquina virtual. Hola VM debe solo direcciones de TCP/IP direcciones URL del servicio de recuperación de tooSite de conectividad saliente, Office 365 autenticación direcciones URL y direcciones IP y direcciones IP de cuenta de almacenamiento de caché. Para obtener más información, vea hello [Guía de red para la replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure-networking-guidance.md) artículo.

## <a name="continuous-replication-process"></a>Proceso de replicación continua

Después de que funciona la replicación continua, disco escribe inmediatamente transfiere toohello cuenta de almacenamiento de caché. Recuperación de sitio procesa los datos de Hola y envía toohello cuenta de almacenamiento de destino. Después de que se procesan los datos de hello, puntos de recuperación se generan en la cuenta de almacenamiento de destino de hello cada pocos minutos.

## <a name="failover-process"></a>Proceso de conmutación por error

Cuando se inicia una conmutación por error, hello y hello que las máquinas virtuales se crean en el grupo de recursos de destino de hello, la red virtual de destino, la subred de destino conjunto de disponibilidad de destino. Durante una conmutación por error, puede usar cualquier punto de recuperación.

![Proceso de conmutación por error](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>Pasos siguientes

- Aprenda sobre las [redes](site-recovery-azure-to-azure-networking-guidance.md) para la replicación de máquinas virtuales de Azure.
- Siga un tutorial demasiado[replicar máquinas virtuales de Azure.](site-recovery-azure-to-azure.md)
