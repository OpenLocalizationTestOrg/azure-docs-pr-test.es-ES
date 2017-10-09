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
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="7b8f8-103">Paso 5: Preparar los recursos de Azure para tooAzure de replicación del servidor físico</span><span class="sxs-lookup"><span data-stu-id="7b8f8-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="7b8f8-104">Utilice instrucciones de hello en este tooprepare artículo Azure recursos para que puedan replicar tooAzure de servidores locales con hello [Azure Site Recovery](site-recovery-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="7b8f8-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7b8f8-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="7b8f8-106">Before you start</span></span>

<span data-ttu-id="7b8f8-107">Asegúrese de que ha leído hello [requisitos previos](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="7b8f8-108">Configuración de una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="7b8f8-108">Set up an Azure account</span></span>

- <span data-ttu-id="7b8f8-109">Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="7b8f8-110">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="7b8f8-111">Buscar regiones Hola admitida la recuperación del sitio, en **disponibilidad geográfica** en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="7b8f8-112">Obtenga información acerca de [precios de Site Recovery](site-recovery-faq.md#pricing)y obtener hello [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="7b8f8-113">Configurar una red de Azure</span><span class="sxs-lookup"><span data-stu-id="7b8f8-113">Set up an Azure network</span></span>

- <span data-ttu-id="7b8f8-114">Configure una red de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-114">Set up an Azure network.</span></span> <span data-ttu-id="7b8f8-115">Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="7b8f8-116">Site Recovery en hello portal de Azure puede usar redes configuradas en [el Administrador de recursos](../resource-manager-deployment-model.md), o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="7b8f8-117">red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="7b8f8-118">Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="7b8f8-119">Obtenga más información sobre la [conectividad de la máquina virtual de Azure](physical-walkthrough-network.md) después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="7b8f8-120">Configurar una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7b8f8-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="7b8f8-121">Recuperación del sitio replica de servidores tooAzure almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="7b8f8-122">Máquinas virtuales de Azure se crean desde el almacenamiento de hello después de producirse la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="7b8f8-123">Configure una [cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account) para los datos replicados.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="7b8f8-124">Site Recovery en hello portal de Azure puede utilizar cuentas de almacenamiento configuradas en el Administrador de recursos, o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="7b8f8-125">cuenta de almacenamiento de Hello puede ser estándar o [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="7b8f8-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="7b8f8-126">Si configura una cuenta de premium, también necesitará una cuenta estándar adicional para los datos de registro.</span><span class="sxs-lookup"><span data-stu-id="7b8f8-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7b8f8-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b8f8-127">Next steps</span></span>

<span data-ttu-id="7b8f8-128">Vaya demasiado[paso 6: configurar un almacén](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="7b8f8-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
