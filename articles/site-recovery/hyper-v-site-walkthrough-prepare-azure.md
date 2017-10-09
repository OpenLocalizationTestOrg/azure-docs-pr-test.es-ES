---
title: "tooAzure de máquinas virtuales de Hyper-V (sin System Center VMM) de tooreplicate aaaPrepare recursos de Azure con Azure Site Recovery | Documentos de Microsoft"
description: "Describe lo que necesita en su lugar en Azure antes de que empiece a replicar tooAzure de máquinas virtuales de Hyper-V (sin VMM) mediante Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="4cdf3-103">Paso 5: Preparar los recursos de Azure para tooAzure de replicación de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="4cdf3-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="4cdf3-104">Siga las instrucciones de hello en este tooprepare artículo Azure recursos para que puedan replicar local máquinas virtuales de Hyper-V (sin System Center VMM) tooAzure con hello [Azure Site Recovery](site-recovery-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="4cdf3-105">Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="4cdf3-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="4cdf3-106">Before you start</span></span>

<span data-ttu-id="4cdf3-107">Asegúrese de que ha leído hello [requisitos previos](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="4cdf3-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="4cdf3-108">Configuración de una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="4cdf3-108">Set up an Azure account</span></span>

- <span data-ttu-id="4cdf3-109">Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="4cdf3-110">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="4cdf3-111">Busque regiones Hola admitida la recuperación del sitio, en disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="4cdf3-112">Obtenga información acerca de [precios de Site Recovery](site-recovery-faq.md#pricing)y obtener hello [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="4cdf3-113">Configurar una red de Azure</span><span class="sxs-lookup"><span data-stu-id="4cdf3-113">Set up an Azure network</span></span>

- <span data-ttu-id="4cdf3-114">Configure una red de Azure.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-114">Set up an Azure network.</span></span> <span data-ttu-id="4cdf3-115">Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="4cdf3-116">red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="4cdf3-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="4cdf3-117">Site Recovery en hello portal de Azure puede usar redes configuradas en [el Administrador de recursos](../resource-manager-deployment-model.md), o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="4cdf3-118">Es recomendable configurar una red antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="4cdf3-119">Si no lo hace, deberá toodo durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="4cdf3-120">Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="4cdf3-121">Configurar una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="4cdf3-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="4cdf3-122">Recuperación del sitio replica de máquinas tooAzure almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="4cdf3-123">Máquinas virtuales de Azure se crean desde el almacenamiento de hello después de producirse la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="4cdf3-124">Configurar un estándar o premium [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold datos replican tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="4cdf3-125">[Almacenamiento Premium](../storage/common/storage-premium-storage.md) se utiliza normalmente para las máquinas virtuales que necesitan un rendimiento de E/S alto y cargas de trabajo intensivas de baja latencia toohost E/S.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="4cdf3-126">Si desea que toouse un toostore de cuenta premium los datos replicados, también necesita un registros de replicación toostore de la cuenta de almacenamiento estándar que captura continua cambia datos tooon locales.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="4cdf3-127">Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configure una cuenta en [modo de administrador de recursos](../storage/common/storage-create-storage-account.md), o [modo clásico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4cdf3-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="4cdf3-128">Es recomendable configurar una cuenta de almacenamiento antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="4cdf3-129">Si no lo hace, necesita toodo durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="4cdf3-130">Hola cuentas deben Hola misma región que hello del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="4cdf3-131">No se puede mover cuentas de almacenamiento utilizan por Site Recovery en grupos de recursos dentro de hello misma suscripción, o a través de distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="4cdf3-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4cdf3-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4cdf3-132">Next steps</span></span>

<span data-ttu-id="4cdf3-133">Vaya demasiado[paso 6: recursos de Hyper-V preparar](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="4cdf3-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
