---
title: "aaaReplicate máquinas virtuales de Azure entre regiones de Azure | Documentos de Microsoft"
description: "Resume Hola pasos necesarios tooreplicate máquinas virtuales de Azure entre regiones de Azure con el servicio de Azure Site Recovery Hola Hola portal de Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="cf779-103">Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="cf779-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="cf779-104">Este artículo proporciona información general de hello pasos necesarios tooreplicate Azure máquinas virtuales (VM) en una región de Azure tooAzure máquinas virtuales en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="cf779-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="cf779-105">La replicación de VM de Azure se encuentra en una versión preliminar en este momento.</span><span class="sxs-lookup"><span data-stu-id="cf779-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="cf779-106">Envíe los comentarios y preguntas en parte inferior de este artículo o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cf779-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="cf779-107">Paso 1: Revisión de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="cf779-107">Step 1: Review architecture</span></span>

<span data-ttu-id="cf779-108">Antes de empezar la implementación, revise arquitectura del escenario de Hola y componentes de Hola que necesita toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cf779-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="cf779-109">Vaya demasiado[paso 1: revisar la arquitectura de Hola](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="cf779-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="cf779-110">Paso 2: revisión de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cf779-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="cf779-111">Compruebe que haya Hola requisitos previos de Azure en sitios, incluida una suscripción, redes virtuales, cuentas de almacenamiento y requisitos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf779-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="cf779-112">Vaya demasiado[paso 2: comprobar los requisitos previos y limitaciones](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="cf779-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="cf779-113">Paso 3: Planeamiento de redes</span><span class="sxs-lookup"><span data-stu-id="cf779-113">Step 3: Plan networking</span></span>

<span data-ttu-id="cf779-114">Compruebe que la conectividad saliente está configurado en máquinas virtuales de Azure que desee tooreplicate y que se configuran las conexiones desde el entorno local.</span><span class="sxs-lookup"><span data-stu-id="cf779-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="cf779-115">Vaya demasiado[paso 4: planear las redes](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="cf779-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="cf779-116">Paso 4: Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="cf779-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="cf779-117">Necesita tooset seguridad un tooorchestrate de almacén de servicios de recuperación y administrar la replicación y especificar la región de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf779-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="cf779-118">Vaya demasiado[paso 4: crear un almacén](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="cf779-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="cf779-119">Paso 5: Habilitamiento de la replicación</span><span class="sxs-lookup"><span data-stu-id="cf779-119">Step 5: Enable replication</span></span>


<span data-ttu-id="cf779-120">replicación de tooenable, configurar opciones de ubicación de destino, configurar una directiva de replicación y seleccione hello en las máquinas virtuales de Azure que desea tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="cf779-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="cf779-121">Después de habilitar esta opción, se produce la replicación inicial de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cf779-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="cf779-122">Vaya demasiado[paso 5: habilitar la replicación](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cf779-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="cf779-123">Paso 6: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="cf779-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="cf779-124">Después de que finalice la replicación inicial y replicación de datos se está ejecutando, puede ejecutar una toomake de conmutación por error de prueba seguro de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="cf779-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="cf779-125">Vaya demasiado[paso 6: ejecutar una prueba de conmutación por error](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="cf779-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


