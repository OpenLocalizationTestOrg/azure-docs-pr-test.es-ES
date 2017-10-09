---
title: "aaaPrepare recursos de Azure tooreplicate tooAzure servidores físicos con Azure Site Recovery local | Documentos de Microsoft"
description: Describe lo que necesita en su lugar en Azure antes de empezar replicar tooAzure de servidores locales, mediante el servicio de Azure Site Recovery Hola
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a>Paso 5: Preparar los recursos de Azure para tooAzure de replicación del servidor físico


Utilice instrucciones de hello en este tooprepare artículo Azure recursos para que puedan replicar tooAzure de servidores locales con hello [Azure Site Recovery](site-recovery-overview.md) servicio.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Antes de comenzar

Asegúrese de que ha leído hello [requisitos previos](physical-walkthrough-prerequisites.md).

## <a name="set-up-an-azure-account"></a>Configuración de una cuenta de Azure

- Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).
- Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
- Buscar regiones Hola admitida la recuperación del sitio, en **disponibilidad geográfica** en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Obtenga información acerca de [precios de Site Recovery](site-recovery-faq.md#pricing)y obtener hello [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Configurar una red de Azure

- Configure una red de Azure. Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.
- Site Recovery en hello portal de Azure puede usar redes configuradas en [el Administrador de recursos](../resource-manager-deployment-model.md), o en modo clásico.
- red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación.
- Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).
- Obtenga más información sobre la [conectividad de la máquina virtual de Azure](physical-walkthrough-network.md) después de la conmutación por error.


## <a name="set-up-an-azure-storage-account"></a>Configurar una cuenta de almacenamiento de Azure

- Recuperación del sitio replica de servidores tooAzure almacenamiento local. Máquinas virtuales de Azure se crean desde el almacenamiento de hello después de producirse la conmutación por error.
- Configure una [cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account) para los datos replicados.
- Site Recovery en hello portal de Azure puede utilizar cuentas de almacenamiento configuradas en el Administrador de recursos, o en modo clásico.
- cuenta de almacenamiento de Hello puede ser estándar o [premium](../storage/common/storage-premium-storage.md).
- Si configura una cuenta de premium, también necesitará una cuenta estándar adicional para los datos de registro.


## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 6: configurar un almacén](physical-walkthrough-create-vault.md)
