---
title: "aaaMigrate las máquinas virtuales de IaaS de Azure entre regiones de Azure | Documentos de Microsoft"
description: "Use máquinas de virtuales de Azure Site Recovery toomigrate IaaS de Azure de tooanother de una región de Azure."
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
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="20e24-103">Migración de máquinas virtuales de IaaS de Azure entre regiones de Azure con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="20e24-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="20e24-104">Información general</span><span class="sxs-lookup"><span data-stu-id="20e24-104">Overview</span></span>
<span data-ttu-id="20e24-105">Bienvenido tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="20e24-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="20e24-106">Use este artículo si desea toomigrate máquinas virtuales de Azure entre regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="20e24-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="20e24-107">Antes de comenzar, tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="20e24-107">Before you start, note that:</span></span>

* <span data-ttu-id="20e24-108">Azure tiene dos modelos de implementación diferentes para crear y utilizar recursos: Azure Resource Manager y el portal clásico.</span><span class="sxs-lookup"><span data-stu-id="20e24-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="20e24-109">Azure también tiene dos portales: Hola portal de Azure clásico que admite el modelo de implementación clásica de Hola y Hola portal de Azure con compatibilidad para dos modelos de implementación.</span><span class="sxs-lookup"><span data-stu-id="20e24-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="20e24-110">pasos básicos de Hello para la migración son Hola mismo si va a configurar la recuperación del sitio en el Administrador de recursos o en clásico.</span><span class="sxs-lookup"><span data-stu-id="20e24-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="20e24-111">Sin embargo Hola instrucciones de la interfaz de usuario y capturas de pantalla en este artículo son relevantes para hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="20e24-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="20e24-112">**Actualmente sólo se pueden migrar desde una región tooanother. Puede conmutar las máquinas virtuales de tooanother de una región de Azure, pero no puede realizar conmutación por recuperación ellos nuevo.**</span><span class="sxs-lookup"><span data-stu-id="20e24-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="20e24-113">Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="20e24-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20e24-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="20e24-114">Prerequisites</span></span>
<span data-ttu-id="20e24-115">Requisitos para realizar esta implementación:</span><span class="sxs-lookup"><span data-stu-id="20e24-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="20e24-116">**Máquinas virtuales de IaaS**: Hola máquinas virtuales que desee toomigrate.</span><span class="sxs-lookup"><span data-stu-id="20e24-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="20e24-117">Migrará estas máquinas virtuales tratándolas como máquinas físicas.</span><span class="sxs-lookup"><span data-stu-id="20e24-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="20e24-118">Pasos de implementación</span><span class="sxs-lookup"><span data-stu-id="20e24-118">Deployment steps</span></span>
<span data-ttu-id="20e24-119">Esta sección describen los pasos de implementación de hello en el nuevo portal de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="20e24-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="20e24-120">[Cree un almacén](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="20e24-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="20e24-121">[Habilite la replicación](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="20e24-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="20e24-122">Habilitar la replicación de hello las máquinas virtuales que desee toomigrate y elija Azure como origen.</span><span class="sxs-lookup"><span data-stu-id="20e24-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="20e24-123">[ Ejecute una conmutación por error no planeada](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="20e24-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="20e24-124">Una vez completada la replicación inicial, puede ejecutar una conmutación por error no planeada desde tooanother de una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="20e24-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="20e24-125">Si lo desea, puede crear un plan de recuperación y ejecutar varias máquinas virtuales de un error no planeadas, toomigrate entre regiones.</span><span class="sxs-lookup"><span data-stu-id="20e24-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="20e24-126">[Obtenga más información](site-recovery-create-recovery-plans.md) sobre los planes de recuperación.</span><span class="sxs-lookup"><span data-stu-id="20e24-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20e24-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20e24-127">Next steps</span></span>
<span data-ttu-id="20e24-128">Obtenga más información sobre otros escenarios de replicación en [¿Qué es Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="20e24-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
