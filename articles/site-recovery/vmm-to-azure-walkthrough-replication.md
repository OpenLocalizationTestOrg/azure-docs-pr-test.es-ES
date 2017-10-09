---
title: "aaaSet una directiva de replicación para tooAzure de replicación de máquina virtual de Hyper-V (con VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooset una directiva de replicación para tooAzure de replicación de máquina virtual de Hyper-V (con VMM) con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="b334e-103">Paso 10: Configurar una directiva de replicación de máquina virtual de Hyper-V tooAzure de replicación (con VMM)</span><span class="sxs-lookup"><span data-stu-id="b334e-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="b334e-104">Después de configurar [asignación de red](vmm-to-azure-walkthrough-network-mapping.md), use este tooconfigure artículo una directiva de replicación T\tooreplicate máquinas virtuales de Hyper-V administrados en tooAzure de nubes de System Center Virtual Machine Manager (VMM) local, utilizando Hola [ Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b334e-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="b334e-105">Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b334e-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="b334e-106">Para crear una directiva</span><span class="sxs-lookup"><span data-stu-id="b334e-106">Create a policy</span></span>

1. <span data-ttu-id="b334e-107">toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.</span><span class="sxs-lookup"><span data-stu-id="b334e-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Red](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="b334e-109">En **Crear y asociar directiva**, especifique un nombre de directiva.</span><span class="sxs-lookup"><span data-stu-id="b334e-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="b334e-110">En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="b334e-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="b334e-111">No se admite una frecuencia de segundo 30 al replicar toopremium almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b334e-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="b334e-112">limitación de Hello viene determinado por el número de Hola de instantáneas por blob (100) compatible con almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="b334e-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="b334e-113">Más información</span><span class="sxs-lookup"><span data-stu-id="b334e-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="b334e-114">En **retención de punto de recuperación**, especifique en horas cuánto va un período de retención Hola para cada punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="b334e-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="b334e-115">Equipos protegidos pueden ser recuperado tooany punto dentro de una ventana.</span><span class="sxs-lookup"><span data-stu-id="b334e-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="b334e-116">En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b334e-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="b334e-117">Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b334e-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="b334e-118">Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="b334e-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="b334e-119">Tenga en cuenta que si habilita las instantáneas coherentes con la aplicación, afectará Hola rendimiento de aplicaciones que se ejecutan en máquinas virtuales de origen.</span><span class="sxs-lookup"><span data-stu-id="b334e-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="b334e-120">Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.</span><span class="sxs-lookup"><span data-stu-id="b334e-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="b334e-121">En **hora de inicio de la replicación inicial**, indicar al toostart Hola la replicación inicial.</span><span class="sxs-lookup"><span data-stu-id="b334e-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="b334e-122">se produce la replicación de Hello sobre el ancho de banda de internet por lo que conviene tooschedule que fuera de su horario ocupado.</span><span class="sxs-lookup"><span data-stu-id="b334e-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="b334e-123">En **cifrar los datos almacenados en Azure**, especifique si tooencrypt datos de rest de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="b334e-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="b334e-124">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b334e-124">Then click **OK**.</span></span>

    ![Directiva de replicación](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="b334e-126">Cuando se crea una nueva directiva automáticamente tiene asociadas con hello nube de VMM.</span><span class="sxs-lookup"><span data-stu-id="b334e-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="b334e-127">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b334e-127">Click **OK**.</span></span> <span data-ttu-id="b334e-128">Puede asociar más nubes de VMM (hello y máquinas virtuales en ellos) con esta directiva de replicación en **replicación** > nombre de directiva > **asociar la nube de VMM**.</span><span class="sxs-lookup"><span data-stu-id="b334e-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Directiva de replicación](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="b334e-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b334e-130">Next steps</span></span>

<span data-ttu-id="b334e-131">Vaya demasiado[paso 11: habilitar la replicación](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="b334e-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
