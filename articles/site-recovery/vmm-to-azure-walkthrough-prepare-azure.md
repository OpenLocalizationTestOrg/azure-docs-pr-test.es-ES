---
title: "tooAzure de máquinas virtuales de Hyper-V (con System Center VMM) de tooreplicate aaaPrepare recursos de Azure con Azure Site Recovery | Documentos de Microsoft"
description: "Describe lo que necesita en su lugar en Azure antes de iniciar la replicación de máquinas virtuales de Hyper-V (con VMM) tooAzure, con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a>Paso 5: Preparar los recursos de Azure para tooAzure de replicación (con VMM) de Hyper-V

Después de comprobar [requisitos de red](vmm-to-azure-walkthrough-network.md), utilice instrucciones de hello en este tooprepare artículo Azure recursos para que puedan replicar máquinas virtuales de Hyper-V local en tooAzure de nubes de System Center Virtual Machine Manager (VMM), usar Hola [Azure Site Recovery](site-recovery-overview.md) servicio.

Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-an-azure-account"></a>Configuración de una cuenta de Azure

- Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).
- Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Busque regiones Hola admitida la recuperación del sitio, en disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Obtenga información acerca de [precios de Site Recovery](site-recovery-faq.md#pricing)y obtener hello [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).
- Asegúrese de que su cuenta de Azure tiene Hola correcto [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate máquinas virtuales de Azure. [Más información](../active-directory/role-based-access-built-in-roles.md) sobre el control de acceso basado en roles de Azure.


## <a name="set-up-an-azure-network"></a>Configurar una red de Azure

- Configure una [red de Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md). Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.
- red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación
- Site Recovery en hello portal de Azure puede usar redes configuradas en [el Administrador de recursos](../resource-manager-deployment-model.md), o en modo clásico.
- Es recomendable configurar una red antes de empezar. Si no lo hace, deberá toodo durante la implementación de Site Recovery.
- Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Configurar una cuenta de almacenamiento de Azure

- Recuperación del sitio replica de máquinas tooAzure almacenamiento local. Máquinas virtuales de Azure se crean desde el almacenamiento de hello después de producirse la conmutación por error.
- Configurar un estándar o premium [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold datos replican tooAzure.
- [Almacenamiento Premium](../storage/common/storage-premium-storage.md) se utiliza normalmente para las máquinas virtuales que necesitan un rendimiento de E/S alto y cargas de trabajo intensivas de baja latencia toohost E/S.
- Si desea que toouse un toostore de cuenta premium los datos replicados, también necesita un registros de replicación toostore de la cuenta de almacenamiento estándar que captura continua cambia datos tooon locales.
- Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configure una cuenta en [modo de administrador de recursos](../storage/common/storage-create-storage-account.md), o [modo clásico](../storage/common/storage-create-storage-account.md).
- Es recomendable configurar una cuenta de almacenamiento antes de empezar. Si no lo hace, necesita toodo durante la implementación de Site Recovery. Hola cuentas deben Hola misma región que hello del almacén de servicios de recuperación.
- No se puede mover cuentas de almacenamiento utilizan por Site Recovery en grupos de recursos dentro de hello misma suscripción, o a través de distintas suscripciones.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 6: preparar VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)
