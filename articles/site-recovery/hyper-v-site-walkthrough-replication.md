---
title: "aaaSet una directiva de replicación para máquinas virtuales de Hyper-V tooAzure de replicación (sin System Center VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Resume los pasos de hello necesita tooset una directiva de replicación al replicar las máquinas virtuales de Hyper-V tooAzure almacenamiento"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="18b5e-103">Paso 9: Configurar una directiva de replicación para tooAzure de replicación de máquina virtual de Hyper-V</span><span class="sxs-lookup"><span data-stu-id="18b5e-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="18b5e-104">Este artículo se describe cómo tooset una directiva de replicación al replicar máquinas virtuales de Hyper-V tooAzure (sin System Center VMM) mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="18b5e-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="18b5e-105">Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="18b5e-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="18b5e-106">Acerca de las instantáneas</span><span class="sxs-lookup"><span data-stu-id="18b5e-106">About snapshots</span></span>

<span data-ttu-id="18b5e-107">Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="18b5e-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="18b5e-108">Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="18b5e-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="18b5e-109">Si habilita las instantáneas coherentes con la aplicación, afectará al rendimiento de Hola de aplicaciones que se ejecutan en máquinas virtuales de origen.</span><span class="sxs-lookup"><span data-stu-id="18b5e-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="18b5e-110">Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.</span><span class="sxs-lookup"><span data-stu-id="18b5e-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="18b5e-111">Configurar una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="18b5e-111">Set up a replication policy</span></span>

1. <span data-ttu-id="18b5e-112">toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.</span><span class="sxs-lookup"><span data-stu-id="18b5e-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Red](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="18b5e-114">En **Crear y asociar directiva**, especifique un nombre de directiva.</span><span class="sxs-lookup"><span data-stu-id="18b5e-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="18b5e-115">En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="18b5e-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="18b5e-116">No se admite una frecuencia de segundo 30 al replicar toopremium almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="18b5e-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="18b5e-117">limitación de Hello viene determinado por el número de Hola de instantáneas por blob (100) compatible con almacenamiento premium.</span><span class="sxs-lookup"><span data-stu-id="18b5e-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="18b5e-118">[Más información](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="18b5e-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="18b5e-119">En **retención de punto de recuperación**, especifique en horas cuánto tiempo es el período de retención de Hola para cada punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="18b5e-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="18b5e-120">Las máquinas virtuales se pueden recuperar tooany punto dentro de una ventana.</span><span class="sxs-lookup"><span data-stu-id="18b5e-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="18b5e-121">En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="18b5e-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="18b5e-122">En **hora de inicio de la replicación inicial**, especifique cuándo toostart Hola la replicación inicial.</span><span class="sxs-lookup"><span data-stu-id="18b5e-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="18b5e-123">se produce la replicación de Hello sobre el ancho de banda de internet por lo que conviene tooschedule que fuera de su horario ocupado.</span><span class="sxs-lookup"><span data-stu-id="18b5e-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="18b5e-124">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="18b5e-124">Then click **OK**.</span></span>

    ![Directiva de replicación](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="18b5e-126">Cuando se crea una nueva directiva, automáticamente tiene asociadas con el sitio de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="18b5e-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="18b5e-127">Puede asociar un sitio de Hyper-V (hello las máquinas virtuales en ella y) con varias directivas de replicación en **replicación** > nombre de directiva > **asociar el sitio de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="18b5e-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="18b5e-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18b5e-128">Next steps</span></span>

<span data-ttu-id="18b5e-129">Vaya demasiado[paso 10: habilitar la replicación](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="18b5e-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
