---
title: "Revisión de los requisitos previos para la replicación de Hyper-V en Azure (sin System Center VMM) mediante Azure Site Recovery | Microsoft Docs"
description: "Describe los requisitos previos para configurar la replicación, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V locales en Azure con Azure Site Recovery"
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
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="d7db8-103">Paso 2: revisión de los requisitos previos para la replicación de Hyper-V (sin VMM) en Azure</span><span class="sxs-lookup"><span data-stu-id="d7db8-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="d7db8-104">En la tabla se resumen los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="d7db8-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="d7db8-105">**Requisito previo**</span><span class="sxs-lookup"><span data-stu-id="d7db8-105">**Prerequisite**</span></span> | <span data-ttu-id="d7db8-106">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="d7db8-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="d7db8-107">**Las tablas de Azure**</span><span class="sxs-lookup"><span data-stu-id="d7db8-107">**Azure**</span></span> | <span data-ttu-id="d7db8-108">Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)</span><span class="sxs-lookup"><span data-stu-id="d7db8-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="d7db8-109">**Servidores locales**</span><span class="sxs-lookup"><span data-stu-id="d7db8-109">**On-premises servers**</span></span> | <span data-ttu-id="d7db8-110">[Más información](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre los requisitos de los hosts de Hyper-V locales.</span><span class="sxs-lookup"><span data-stu-id="d7db8-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="d7db8-111">**Máquinas virtuales de Hyper-V locales**</span><span class="sxs-lookup"><span data-stu-id="d7db8-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="d7db8-112">Las máquinas virtuales que desee replicar deben ejecutar un [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) y cumplir los [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="d7db8-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="d7db8-113">**Direcciones URL de Azure**</span><span class="sxs-lookup"><span data-stu-id="d7db8-113">**Azure URLs**</span></span> | <span data-ttu-id="d7db8-114">Los hosts de Hyper-V necesitan tener acceso a estas direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="d7db8-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="d7db8-115">Si tiene reglas de firewall basadas en direcciones IP, asegúrese de que permitan la comunicación con Azure.</span><span class="sxs-lookup"><span data-stu-id="d7db8-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="d7db8-116">Permita los [intervalos IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y el puerto HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="d7db8-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="d7db8-117">Permita los intervalos de direcciones IP correspondientes a la región de Azure de su suscripción y del oeste de EE. UU. (se usan para Access Control y para Identity Management).</span><span class="sxs-lookup"><span data-stu-id="d7db8-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="d7db8-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d7db8-118">Next steps</span></span>

- <span data-ttu-id="d7db8-119">Si va a realizar una implementación completa, vaya al [Paso 3: Planeamiento de la capacidad](hyper-v-site-walkthrough-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="d7db8-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="d7db8-120">Si va a realizar una implementación de prueba sencilla, vaya al [Paso 4: Planeamiento de las redes](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="d7db8-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
