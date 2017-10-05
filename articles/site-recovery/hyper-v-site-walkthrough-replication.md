---
title: "Configurar una directiva de replicación para la replicación de máquinas virtuales de Hyper-V (sin System Center VMM) en Azure con Azure Site Recovery | Microsoft Docs"
description: "Resume los pasos necesarios para configurar una directiva de replicación al replicar máquinas virtuales de Hyper-V en Azure Storage"
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
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="45ec2-103">Paso 9: configuración de una directiva de replicación para replicar máquinas virtuales de Hyper-V en Azure</span><span class="sxs-lookup"><span data-stu-id="45ec2-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="45ec2-104">En este artículo se describe cómo configurar una directiva de replicación al replicar máquinas virtuales de Hyper-V en Azure mediante el servicio [Azure Site Recovery](site-recovery-overview.md) en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="45ec2-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="45ec2-105">Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="45ec2-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="45ec2-106">Acerca de las instantáneas</span><span class="sxs-lookup"><span data-stu-id="45ec2-106">About snapshots</span></span>

<span data-ttu-id="45ec2-107">Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de toda la máquina virtual y una instantánea coherente con la aplicación que toma una instantánea en un momento concreto de los datos de la aplicación dentro de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45ec2-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="45ec2-108">Las instantáneas coherentes con la aplicación utilizan el Servicio de instantáneas de volumen (VSS) para asegurarse de que las aplicaciones se encuentren en un estado coherente cuando se captura la instantánea.</span><span class="sxs-lookup"><span data-stu-id="45ec2-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="45ec2-109">S habilita las instantáneas coherentes con la aplicación, se verá afectado el rendimiento de aplicaciones que se ejecutan en las máquinas virtuales de origen.</span><span class="sxs-lookup"><span data-stu-id="45ec2-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="45ec2-110">Asegúrese de que el valor establecido es menor que el número de puntos de recuperación adicionales configurados.</span><span class="sxs-lookup"><span data-stu-id="45ec2-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="45ec2-111">Configurar una directiva de replicación</span><span class="sxs-lookup"><span data-stu-id="45ec2-111">Set up a replication policy</span></span>

1. <span data-ttu-id="45ec2-112">Para crear una nueva directiva de replicación, haga clic en **Preparar infraestructura** > **Configuración de la replicación** > **+Crear y asociar**.</span><span class="sxs-lookup"><span data-stu-id="45ec2-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Red](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="45ec2-114">En **Crear y asociar directiva**, especifique un nombre de directiva.</span><span class="sxs-lookup"><span data-stu-id="45ec2-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="45ec2-115">En **Frecuencia de copia**, especifique la frecuencia con la que desea replicar diferencias de datos después de la replicación inicial (cada 30 segundos, 5 o 15 minutos).</span><span class="sxs-lookup"><span data-stu-id="45ec2-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="45ec2-116">Cuando la replicación se realiza en Premium Storage, no se admite una frecuencia de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="45ec2-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="45ec2-117">La limitación viene determinada por el número de instantáneas por blob (100) que admite Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="45ec2-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="45ec2-118">[Más información](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="45ec2-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="45ec2-119">En **Retención de punto de recuperación**, especifique la duración en horas del período de retención para cada punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="45ec2-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="45ec2-120">Las máquinas virtuales se pueden recuperar en cualquier punto dentro de un período.</span><span class="sxs-lookup"><span data-stu-id="45ec2-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="45ec2-121">En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="45ec2-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="45ec2-122">En **Hora de inicio de la replicación inicial**, especifique cuándo debe comenzar la replicación inicial.</span><span class="sxs-lookup"><span data-stu-id="45ec2-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="45ec2-123">La replicación se produce utilizando el ancho de banda de Internet, así que puede que deba programarla fuera del horario de trabajo.</span><span class="sxs-lookup"><span data-stu-id="45ec2-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="45ec2-124">y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="45ec2-124">Then click **OK**.</span></span>

    ![Directiva de replicación](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="45ec2-126">Cuando se crea una nueva directiva, esta se asocia automáticamente con el sitio Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="45ec2-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="45ec2-127">Puede asociar un sitio Hyper-V y las máquinas virtuales que contiene con varias directivas de replicación en **Replicación** > nombre de directiva > **Associate Hyper-V Site** (Asociar sitio Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="45ec2-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="45ec2-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45ec2-128">Next steps</span></span>

<span data-ttu-id="45ec2-129">Vaya a [Paso 10: Habilitación de la replicación](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="45ec2-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
