---
title: "Réplica de máquinas virtuales de Azure entre regiones de Azure | Microsoft Docs"
description: "Resume los pasos necesarios para replicar máquinas virtuales de Azure entre regiones de Azure con el servicio de Azure Site Recovery en Azure portal"
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
ms.openlocfilehash: 9258613161a61e36b1d0c5796d5763c916d66859
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="55511-103">Replicación de máquinas virtuales de Azure entre regiones con Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="55511-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="55511-104">Este artículo proporciona información general sobre los pasos necesarios para replicar Azure Virtual Machines (VM) en una región de Azure en máquinas virtuales de Azure situadas en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="55511-104">This article provides an overview of the steps required to replicate Azure virtual machines (VMs) in one Azure region to Azure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="55511-105">La replicación de la máquina virtual de Azure actualmente se encuentra en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="55511-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="55511-106">Cualquier comentario o pregunta que tenga puede publicarlo en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="55511-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="55511-107">Paso 1: Revisión de la arquitectura</span><span class="sxs-lookup"><span data-stu-id="55511-107">Step 1: Review architecture</span></span>

<span data-ttu-id="55511-108">Antes de empezar la implementación, revise la arquitectura del escenario y los componentes que necesita implementar.</span><span class="sxs-lookup"><span data-stu-id="55511-108">Before you start deployment, review the scenario architecture, and the components you need to deploy.</span></span>

<span data-ttu-id="55511-109">Vaya al [paso 1: revisión de la arquitectura](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="55511-109">Go to [Step 1: Review the architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="55511-110">Paso 2: revisión de los requisitos previos</span><span class="sxs-lookup"><span data-stu-id="55511-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="55511-111">Compruebe que tiene los requisitos previos de Azure en sitios, incluidos una suscripción, redes virtuales, cuentas de almacenamiento y requisitos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="55511-111">Check that you have the Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="55511-112">Vaya a [Paso 2: Comprobación de los requisitos previos y las limitaciones](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="55511-112">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="55511-113">Paso 3: Planeamiento de redes</span><span class="sxs-lookup"><span data-stu-id="55511-113">Step 3: Plan networking</span></span>

<span data-ttu-id="55511-114">Compruebe que la conectividad de salida está configurada en máquinas virtuales de Azure que desee replicar y que se configuran las conexiones desde el entorno local.</span><span class="sxs-lookup"><span data-stu-id="55511-114">Check that outbound connectivity is set up on Azure VMs you want to replicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="55511-115">Vaya al [paso 4: planeamiento de las redes](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="55511-115">Go to [Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="55511-116">Paso 4: Creación de un almacén</span><span class="sxs-lookup"><span data-stu-id="55511-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="55511-117">Debe configurar un almacén de Recovery Services para organizar y administrar la replicación y especificar la región de origen.</span><span class="sxs-lookup"><span data-stu-id="55511-117">You need to set up a Recovery Services vault to orchestrate and manage replication, and specify the source region.</span></span>

<span data-ttu-id="55511-118">Vaya al [Paso 4: Creación de un almacén](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="55511-118">Go to [Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="55511-119">Paso 5: Habilitamiento de la replicación</span><span class="sxs-lookup"><span data-stu-id="55511-119">Step 5: Enable replication</span></span>


<span data-ttu-id="55511-120">Para habilitar la replicación, configure opciones de ubicación de destino y una directiva de replicación y seleccione las máquinas virtuales de Azure que desea replicar.</span><span class="sxs-lookup"><span data-stu-id="55511-120">To enable replication, you configure target location settings, set up a replication policy, and select the Azure VMs that you want to replicate.</span></span> <span data-ttu-id="55511-121">Después de habilitarla, se produce la replicación inicial de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="55511-121">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="55511-122">Vaya a [Paso 5: Habilitación de la replicación](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="55511-122">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="55511-123">Paso 6: Ejecución de una conmutación por error de prueba</span><span class="sxs-lookup"><span data-stu-id="55511-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="55511-124">Una vez que termina la replicación inicial y que se está ejecutando la replicación diferencial, puede ejecutar una conmutación por error de prueba para asegurarse de que todo funciona según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="55511-124">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="55511-125">Vaya a [Paso 6: Ejecución de una conmutación por error de prueba](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="55511-125">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


