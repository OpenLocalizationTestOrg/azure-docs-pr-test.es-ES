---
title: "Migración de máquinas virtuales de IaaS de Azure entre regiones de Azure | Microsoft Docs"
description: "Use Azure Site Recovery para migrar máquinas virtuales de IaaS de Azure de una región de Azure a otra."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="0ac91-103">Migración de máquinas virtuales de IaaS de Azure entre regiones de Azure con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0ac91-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="0ac91-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0ac91-104">Overview</span></span>
<span data-ttu-id="0ac91-105">Bienvenido a Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0ac91-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="0ac91-106">Utilice este artículo si quiere migrar máquinas virtuales de Azure de una región de Azure a otra.</span><span class="sxs-lookup"><span data-stu-id="0ac91-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="0ac91-107">Antes de comenzar, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ac91-107">Before you start, note that:</span></span>

* <span data-ttu-id="0ac91-108">Azure tiene dos modelos de implementación diferentes para crear y utilizar recursos: Azure Resource Manager y el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="0ac91-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0ac91-109">Azure también tiene dos portales: el Portal de Azure clásico que admite el modelo de implementación clásico y el Portal de Azure que es compatible con ambos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="0ac91-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="0ac91-110">Los pasos básicos para la migración son los mismos, con independencia de que vaya a configurar Site Recovery en Resource Manager o en el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="0ac91-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="0ac91-111">Sin embargo, las instrucciones de la interfaz de usuario y las capturas de pantalla del artículo son pertinentes para el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac91-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="0ac91-112">**Actualmente, solo puede efectuar la migración de una región a otra. Puede conmutar por error las máquinas virtuales de una región de Azure a otra, pero no podrá volver a realizar este proceso con estas máquinas más adelante.**</span><span class="sxs-lookup"><span data-stu-id="0ac91-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="0ac91-113">Publique cualquier comentario o pregunta que tenga en la parte inferior de este artículo, o bien en el [foro de Servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0ac91-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ac91-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0ac91-114">Prerequisites</span></span>
<span data-ttu-id="0ac91-115">Requisitos para realizar esta implementación:</span><span class="sxs-lookup"><span data-stu-id="0ac91-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="0ac91-116">**Máquinas virtuales IaaS**: las máquinas virtuales que desea migrar.</span><span class="sxs-lookup"><span data-stu-id="0ac91-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="0ac91-117">Migrará estas máquinas virtuales tratándolas como máquinas físicas.</span><span class="sxs-lookup"><span data-stu-id="0ac91-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="0ac91-118">Pasos de implementación</span><span class="sxs-lookup"><span data-stu-id="0ac91-118">Deployment steps</span></span>
<span data-ttu-id="0ac91-119">En esta sección se describen los pasos de implementación en el nuevo Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac91-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="0ac91-120">[Cree un almacén](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0ac91-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="0ac91-121">[Habilite la replicación](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0ac91-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="0ac91-122">Habilite la replicación en las máquinas virtuales que quiera migrar y elija Azure como origen.</span><span class="sxs-lookup"><span data-stu-id="0ac91-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="0ac91-123">[ Ejecute una conmutación por error no planeada](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="0ac91-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="0ac91-124">Una vez completada la replicación inicial, puede ejecutar una conmutación por error no planeada desde una región de Azure a otra.</span><span class="sxs-lookup"><span data-stu-id="0ac91-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="0ac91-125">Si lo desea, puede crear un plan de recuperación y una conmutación por error no planeada para migrar varias máquinas virtuales entre las regiones.</span><span class="sxs-lookup"><span data-stu-id="0ac91-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="0ac91-126">[Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="0ac91-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ac91-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ac91-127">Next steps</span></span>
<span data-ttu-id="0ac91-128">Obtenga más información sobre otros escenarios de replicación en [¿Qué es Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0ac91-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
