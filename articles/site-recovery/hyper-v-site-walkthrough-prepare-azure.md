---
title: "Preparar los recursos de Azure para replicar máquinas virtuales de Hyper-V (sin System Center VMM) en Azure con Azure Site Recovery | Microsoft Docs"
description: "Describe lo que necesita tener listo en Azure antes de iniciar la replicación de máquinas virtuales de Hyper-V (sin VMM) en Azure con Azure Site Recovery"
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
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="0399b-103">Paso 5: preparación de los recursos de Azure para la replicación de Hyper-V en Azure</span><span class="sxs-lookup"><span data-stu-id="0399b-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="0399b-104">Siga las instrucciones de este artículo para preparar los recursos de Azure para replicar máquinas virtuales de Hyper-V local (sin System Center VMM) en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0399b-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="0399b-105">Cuando haya terminado de leer este artículo, publique cualquier comentario o pregunta que tenga en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0399b-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0399b-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="0399b-106">Before you start</span></span>

<span data-ttu-id="0399b-107">Asegúrese de que ha leído los [requisitos previos](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0399b-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="0399b-108">Configurar una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="0399b-108">Set up an Azure account</span></span>

- <span data-ttu-id="0399b-109">Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0399b-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="0399b-110">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0399b-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="0399b-111">Para comprobar las regiones admitidas para Site Recovery, consulte Disponibilidad geográfica en [Detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="0399b-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="0399b-112">Obtenga información de los [precios de Site Recovery](site-recovery-faq.md#pricing) y los [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="0399b-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="0399b-113">Configurar una red de Azure</span><span class="sxs-lookup"><span data-stu-id="0399b-113">Set up an Azure network</span></span>

- <span data-ttu-id="0399b-114">Configure una red de Azure.</span><span class="sxs-lookup"><span data-stu-id="0399b-114">Set up an Azure network.</span></span> <span data-ttu-id="0399b-115">Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0399b-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="0399b-116">La red debe estar en la misma región que el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0399b-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="0399b-117">Site Recovery en Azure Portal puede usar redes configuradas en [Resource Manager](../resource-manager-deployment-model.md) o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="0399b-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="0399b-118">Es recomendable configurar una red antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="0399b-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="0399b-119">Si no lo hace, deberá hacerlo durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0399b-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="0399b-120">Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="0399b-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="0399b-121">Configurar una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0399b-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="0399b-122">Site Recovery replica máquinas virtuales locales en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0399b-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="0399b-123">Las máquinas virtuales de Azure se crean en el almacenamiento después de producirse la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0399b-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="0399b-124">Configurar una [cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account) estándar o premium para almacenar los datos replicados en Azure.</span><span class="sxs-lookup"><span data-stu-id="0399b-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="0399b-125">[Premium Storage](../storage/common/storage-premium-storage.md) se usa normalmente para las máquinas virtuales que necesitan un alto rendimiento constante de E/S y latencia baja para hospedar cargas de trabajo intensivas de E/S.</span><span class="sxs-lookup"><span data-stu-id="0399b-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="0399b-126">Si desea utilizar una cuenta premium para almacenar los datos replicados, también necesita una cuenta de almacenamiento estándar para almacenar los registros de replicación que capturan los cambios continuos de los datos locales.</span><span class="sxs-lookup"><span data-stu-id="0399b-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="0399b-127">Según el modelo de recursos que desee usar para las máquinas virtuales de Azure conmutadas por error, configure una cuenta en [modo Resource Manager](../storage/common/storage-create-storage-account.md) o en [modo clásico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0399b-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="0399b-128">Es recomendable configurar una cuenta de almacenamiento antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="0399b-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="0399b-129">Si no lo hace, deberá hacerlo durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0399b-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="0399b-130">Las cuentas deben estar en la misma región que el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0399b-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="0399b-131">No se pueden mover cuentas de almacenamiento que usa Site Recovery en grupos de recursos dentro de la misma suscripción, o bien en distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="0399b-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0399b-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0399b-132">Next steps</span></span>

<span data-ttu-id="0399b-133">Vaya al [paso 6: preparación de los recursos de Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="0399b-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
