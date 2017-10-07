---
title: "requisitos previos de hello aaaReview para la replicación de tooAzure de Hyper-V (sin System Center VMM) mediante Azure Site Recovery | Documentos de Microsoft"
description: "Describe los requisitos previos de Hola para configurar la replicación, la conmutación por error y la recuperación de tooAzure de máquinas virtuales de Hyper-V local con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="15e78-103">Paso 2: Revisar los requisitos previos de hello para la replicación de Hyper-V (sin WMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="15e78-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="15e78-104">requisitos previos de Hola se resumen en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="15e78-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="15e78-105">**Requisito previo**</span><span class="sxs-lookup"><span data-stu-id="15e78-105">**Prerequisite**</span></span> | <span data-ttu-id="15e78-106">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="15e78-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="15e78-107">**Las tablas de Azure**</span><span class="sxs-lookup"><span data-stu-id="15e78-107">**Azure**</span></span> | <span data-ttu-id="15e78-108">Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)</span><span class="sxs-lookup"><span data-stu-id="15e78-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="15e78-109">**Servidores locales**</span><span class="sxs-lookup"><span data-stu-id="15e78-109">**On-premises servers**</span></span> | <span data-ttu-id="15e78-110">[Obtener más información](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre los requisitos para hosts de Hyper-V de hello en local.</span><span class="sxs-lookup"><span data-stu-id="15e78-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="15e78-111">**Máquinas virtuales de Hyper-V locales**</span><span class="sxs-lookup"><span data-stu-id="15e78-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="15e78-112">Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="15e78-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="15e78-113">**Direcciones URL de Azure**</span><span class="sxs-lookup"><span data-stu-id="15e78-113">**Azure URLs**</span></span> | <span data-ttu-id="15e78-114">Hosts de Hyper-V necesitan tener acceso a direcciones URL toothese:</span><span class="sxs-lookup"><span data-stu-id="15e78-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="15e78-115">Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.</span><span class="sxs-lookup"><span data-stu-id="15e78-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="15e78-116">Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="15e78-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="15e78-117">Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).</span><span class="sxs-lookup"><span data-stu-id="15e78-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="15e78-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15e78-118">Next steps</span></span>

- <span data-ttu-id="15e78-119">Si está realizando una implementación completa, vaya demasiado[paso 3: planear la capacidad](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="15e78-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="15e78-120">Si está realizando una implementación de prueba simple, vaya demasiado[paso 4: planear las redes](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="15e78-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
