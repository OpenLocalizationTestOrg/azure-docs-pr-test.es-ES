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
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="ddd90-103">Paso 5: Preparar los recursos de Azure para tooAzure de replicación (con VMM) de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ddd90-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="ddd90-104">Después de comprobar [requisitos de red](vmm-to-azure-walkthrough-network.md), utilice instrucciones de hello en este tooprepare artículo Azure recursos para que puedan replicar máquinas virtuales de Hyper-V local en tooAzure de nubes de System Center Virtual Machine Manager (VMM), usar Hola [Azure Site Recovery](site-recovery-overview.md) servicio.</span><span class="sxs-lookup"><span data-stu-id="ddd90-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="ddd90-105">Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ddd90-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="ddd90-106">Configuración de una cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="ddd90-106">Set up an Azure account</span></span>

- <span data-ttu-id="ddd90-107">Obtenga una [cuenta de Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="ddd90-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="ddd90-108">Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddd90-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="ddd90-109">Busque regiones Hola admitida la recuperación del sitio, en disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="ddd90-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="ddd90-110">Obtenga información acerca de [precios de Site Recovery](site-recovery-faq.md#pricing)y obtener hello [detalles de precios](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="ddd90-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="ddd90-111">Asegúrese de que su cuenta de Azure tiene Hola correcto [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd90-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="ddd90-112">[Más información](../active-directory/role-based-access-built-in-roles.md) sobre el control de acceso basado en roles de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd90-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="ddd90-113">Configurar una red de Azure</span><span class="sxs-lookup"><span data-stu-id="ddd90-113">Set up an Azure network</span></span>

- <span data-ttu-id="ddd90-114">Configure una [red de Azure](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="ddd90-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="ddd90-115">Las VM de Azure se colocarán en esta red cuando se creen después de la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ddd90-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="ddd90-116">red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="ddd90-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="ddd90-117">Site Recovery en hello portal de Azure puede usar redes configuradas en [el Administrador de recursos](../resource-manager-deployment-model.md), o en modo clásico.</span><span class="sxs-lookup"><span data-stu-id="ddd90-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="ddd90-118">Es recomendable configurar una red antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="ddd90-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="ddd90-119">Si no lo hace, deberá toodo durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ddd90-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="ddd90-120">Obtenga información de [precios de red virtual](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="ddd90-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="ddd90-121">Configurar una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ddd90-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="ddd90-122">Recuperación del sitio replica de máquinas tooAzure almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="ddd90-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="ddd90-123">Máquinas virtuales de Azure se crean desde el almacenamiento de hello después de producirse la conmutación por error.</span><span class="sxs-lookup"><span data-stu-id="ddd90-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="ddd90-124">Configurar un estándar o premium [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold datos replican tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ddd90-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="ddd90-125">[Almacenamiento Premium](../storage/common/storage-premium-storage.md) se utiliza normalmente para las máquinas virtuales que necesitan un rendimiento de E/S alto y cargas de trabajo intensivas de baja latencia toohost E/S.</span><span class="sxs-lookup"><span data-stu-id="ddd90-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="ddd90-126">Si desea que toouse un toostore de cuenta premium los datos replicados, también necesita un registros de replicación toostore de la cuenta de almacenamiento estándar que captura continua cambia datos tooon locales.</span><span class="sxs-lookup"><span data-stu-id="ddd90-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="ddd90-127">Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configure una cuenta en [modo de administrador de recursos](../storage/common/storage-create-storage-account.md), o [modo clásico](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddd90-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="ddd90-128">Es recomendable configurar una cuenta de almacenamiento antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="ddd90-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="ddd90-129">Si no lo hace, necesita toodo durante la implementación de Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ddd90-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="ddd90-130">Hola cuentas deben Hola misma región que hello del almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="ddd90-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="ddd90-131">No se puede mover cuentas de almacenamiento utilizan por Site Recovery en grupos de recursos dentro de hello misma suscripción, o a través de distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="ddd90-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ddd90-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ddd90-132">Next steps</span></span>

<span data-ttu-id="ddd90-133">Vaya demasiado[paso 6: preparar VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="ddd90-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
