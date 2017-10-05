---
title: "Preparar los recursos de Azure para replicar servidores físicos locales en Azure con Azure Site Recovery | Microsoft Docs"
description: "Describe lo que necesita tener listo en Azure antes de iniciar la replicación de servidores locales en Azure con el servicio Azure Site Recovery"
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
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a><span data-ttu-id="0bebd-103">Paso 5: Preparación de los recursos de Azure para la replicación de servidor físico en Azure</span><span class="sxs-lookup"><span data-stu-id="0bebd-103">Step 5: Prepare Azure resources for physical server replication to Azure</span></span>


<span data-ttu-id="0bebd-104">Siga las instrucciones de este artículo para preparar los recursos de Azure para replicar servidores locales en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0bebd-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="0bebd-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0bebd-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0bebd-106">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="0bebd-106">Before you start</span></span>

<span data-ttu-id="0bebd-107">Asegúrese de que ha leído los [requisitos previos](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="0bebd-107">Make sure you've read the [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="0bebd-108">Configuración de una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="0bebd-108">Set up an Azure account</span></span>

- <span data-ttu-id="0bebd-109">Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0bebd-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="0bebd-110">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bebd-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="0bebd-111">Compruebe las regiones admitidas para Site Recovery, consultando **Disponibilidad geográfica** en [Detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="0bebd-111">Check the supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="0bebd-112">Obtenga información de los [precios de Site Recovery](site-recovery-faq.md#pricing) y los [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="0bebd-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="0bebd-113">Configurar una red de Azure</span><span class="sxs-lookup"><span data-stu-id="0bebd-113">Set up an Azure network</span></span>

- <span data-ttu-id="0bebd-114">Configure una red de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bebd-114">Set up an Azure network.</span></span> <span data-ttu-id="0bebd-115">Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0bebd-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="0bebd-116">Site Recovery en Azure Portal puede usar redes configuradas en [Resource Manager](../resource-manager-deployment-model.md) o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="0bebd-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="0bebd-117">La red debe estar en la misma región que el almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0bebd-117">The network should be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="0bebd-118">Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="0bebd-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="0bebd-119">Obtenga más información sobre la [conectividad de la máquina virtual de Azure](physical-walkthrough-network.md) después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0bebd-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="0bebd-120">Configurar una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="0bebd-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="0bebd-121">Site Recovery replica servidores locales en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0bebd-121">Site Recovery replicates on-premises servers to Azure storage.</span></span> <span data-ttu-id="0bebd-122">Las máquinas virtuales de Azure se crean en el almacenamiento después de producirse la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="0bebd-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="0bebd-123">Configure una [cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account) para los datos replicados.</span><span class="sxs-lookup"><span data-stu-id="0bebd-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="0bebd-124">Site Recovery en Azure Portal puede usar cuentas de almacenamiento configuradas en Resource Manager o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="0bebd-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="0bebd-125">La cuenta de almacenamiento puede ser estándar o [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0bebd-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="0bebd-126">Si configura una cuenta de premium, también necesitará una cuenta estándar adicional para los datos de registro.</span><span class="sxs-lookup"><span data-stu-id="0bebd-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0bebd-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0bebd-127">Next steps</span></span>

<span data-ttu-id="0bebd-128">Vaya a [Paso 6: Configuración de un almacén](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="0bebd-128">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
