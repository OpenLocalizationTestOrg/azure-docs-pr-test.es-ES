---
title: "aaaPlan capacidad y escalado de máquinas virtuales de Hyper-V tooAzure de replicación (sin WMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Use este artículo tooplan capacidad y el escalado al replicar las máquinas virtuales de Hyper-V tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a><span data-ttu-id="2f24d-103">Paso 3: Planear la capacidad y ajuste de escala para la replicación de Hyper-V tooAzure</span><span class="sxs-lookup"><span data-stu-id="2f24d-103">Step 3: Plan capacity and scaling for Hyper-V tooAzure replication</span></span>

<span data-ttu-id="2f24d-104">Utilice este toofigure artículo planear la capacidad y el ajuste de escala, al replicar tooAzure de máquinas virtuales de Hyper-V (sin System Center VMM) local con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f24d-104">Use this article toofigure out planning for capacity and scaling, when replicating on-premises Hyper-V VMs (without System Center VMM) tooAzure with [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="2f24d-105">Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2f24d-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="how-do-i-start-capacity-planning"></a><span data-ttu-id="2f24d-106">¿Cómo se puede iniciar el planeamiento de la capacidad?</span><span class="sxs-lookup"><span data-stu-id="2f24d-106">How do I start capacity planning?</span></span>


<span data-ttu-id="2f24d-107">Recopilar información acerca de su entorno de replicación y, a continuación, planear la capacidad de usar esta información, junto con las consideraciones de hello resaltado en este artículo.</span><span class="sxs-lookup"><span data-stu-id="2f24d-107">You gather information about your replication environment, and then plan capacity using this information, together with hello considerations highlighted in this article.</span></span>


## <a name="gather-information"></a><span data-ttu-id="2f24d-108">Recopilación de información</span><span class="sxs-lookup"><span data-stu-id="2f24d-108">Gather information</span></span>

1. <span data-ttu-id="2f24d-109">Recopilar información sobre su entorno de replicación, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.</span><span class="sxs-lookup"><span data-stu-id="2f24d-109">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
2. <span data-ttu-id="2f24d-110">Identifique la tasa de cambio (renovación) diaria para los datos replicados.</span><span class="sxs-lookup"><span data-stu-id="2f24d-110">Identify your daily change (churn) rate for replicated data.</span></span> <span data-ttu-id="2f24d-111">Descargar hello [herramienta de planeación de capacidad de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) tasa de cambio de tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="2f24d-111">Download hello [Hyper-V capacity planning tool](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello change rate.</span></span> <span data-ttu-id="2f24d-112">Se recomienda que ejecutar esta herramienta en una semana toocapture promedios.</span><span class="sxs-lookup"><span data-stu-id="2f24d-112">We recommend you run this tool over a week toocapture averages.</span></span>
 

## <a name="figure-out-capacity"></a><span data-ttu-id="2f24d-113">Averiguar la capacidad</span><span class="sxs-lookup"><span data-stu-id="2f24d-113">Figure out capacity</span></span>

<span data-ttu-id="2f24d-114">Según se haya recopilación de información de hello, ejecute hello [herramienta de planificador de capacidad de recuperación de sitios](http://aka.ms/asr-capacity-planner-excel) tooanalyze su entorno de origen y las cargas de trabajo, calcular las necesidades de ancho de banda y los recursos del servidor de ubicación de origen de Hola y Hola recursos (máquinas virtuales y almacenamiento etcetera), que necesita en la ubicación de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f24d-114">Based on hello information you've gather, you run hello [Site Recovery Capacity Planner Tool](http://aka.ms/asr-capacity-planner-excel) tooanalyze your source environment and workloads, estimate bandwidth needs and server resources for hello source location, and hello resources (virtual machines and storage etc), that you need in hello target location.</span></span> <span data-ttu-id="2f24d-115">Puede ejecutar la herramienta Hola de dos modos:</span><span class="sxs-lookup"><span data-stu-id="2f24d-115">You can run hello tool in a couple of modes:</span></span>

- <span data-ttu-id="2f24d-116">Planificación rápida: ejecutar la herramienta de hello en este modo tooget red y el servidor las proyecciones basadas en un número medio de las máquinas virtuales, discos, almacenamiento y tasa de cambio.</span><span class="sxs-lookup"><span data-stu-id="2f24d-116">Quick planning: Run hello tool in this mode tooget network and server projections based on an average number of VMs, disks, storage, and change rate.</span></span>
- <span data-ttu-id="2f24d-117">Planificación detallada: ejecutar la herramienta de hello en este modo y proporcionar detalles de cada carga de trabajo en el nivel de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f24d-117">Detailed planning: Run hello tool in this mode, and provide details of each workload at VM level.</span></span> <span data-ttu-id="2f24d-118">Analice la compatibilidad de la máquina virtual y obtenga proyecciones de red y del servidor.</span><span class="sxs-lookup"><span data-stu-id="2f24d-118">Analyze VM compatibility and get network and server projections.</span></span>

<span data-ttu-id="2f24d-119">Ahora ejecute la herramienta de hello:</span><span class="sxs-lookup"><span data-stu-id="2f24d-119">Now run hello tool:</span></span>

1. <span data-ttu-id="2f24d-120">Descargar hello [herramienta](http://aka.ms/asr-capacity-planner-excel)</span><span class="sxs-lookup"><span data-stu-id="2f24d-120">Download hello [tool](http://aka.ms/asr-capacity-planner-excel)</span></span>
2. <span data-ttu-id="2f24d-121">planificador rápido de toorun hello, siga [estas instrucciones](site-recovery-capacity-planner.md#run-the-quick-planner)y seleccione Hola escenario **tooAzure de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="2f24d-121">toorun hello quick planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-quick-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>
3. <span data-ttu-id="2f24d-122">toorun Hola planner detallada, siga [estas instrucciones](site-recovery-capacity-planner.md#run-the-detailed-planner)y el escenario de hello seleccione **tooAzure de Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="2f24d-122">toorun hello detailed planner, follow [these instructions](site-recovery-capacity-planner.md#run-the-detailed-planner), and select hello scenario **Hyper-V tooAzure**.</span></span>

## <a name="control-network-bandwidth"></a><span data-ttu-id="2f24d-123">Ancho de banda de red de control</span><span class="sxs-lookup"><span data-stu-id="2f24d-123">Control network bandwidth</span></span>

<span data-ttu-id="2f24d-124">Cuando se haya ancho de banda de hello calculado que necesita, tiene un par de opciones para controlar cantidad Hola de ancho de banda utilizado para la replicación:</span><span class="sxs-lookup"><span data-stu-id="2f24d-124">After you've calculated hello bandwidth you need, you have a couple of options for controlling hello amount of bandwidth used for replication:</span></span>

* <span data-ttu-id="2f24d-125">**Limitar ancho de banda**: tráfico de Hyper-V que replica tooAzure pasa a través de un host de Hyper-V específico.</span><span class="sxs-lookup"><span data-stu-id="2f24d-125">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="2f24d-126">También puede limitar el ancho de banda en el servidor de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f24d-126">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="2f24d-127">**Influir en el ancho de banda**: puede influir en el ancho de banda de hello utilizado para la replicación con un par de claves del registro.</span><span class="sxs-lookup"><span data-stu-id="2f24d-127">**Influence bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="2f24d-128">Limitar el ancho de banda</span><span class="sxs-lookup"><span data-stu-id="2f24d-128">Throttle bandwidth</span></span>
1. <span data-ttu-id="2f24d-129">Abra Hola MMC de copia de seguridad de Microsoft Azure complemento en el servidor de host de Hyper-V de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f24d-129">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="2f24d-130">De forma predeterminada un acceso directo para copia de seguridad de Microsoft Azure está disponible en el escritorio de Hola o en Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f24d-130">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="2f24d-131">En el complemento hello, haga clic en **cambiar las propiedades de**.</span><span class="sxs-lookup"><span data-stu-id="2f24d-131">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="2f24d-132">En hello **limitación** ficha seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**y establecer los límites de hello para el trabajo y no laborables horas.</span><span class="sxs-lookup"><span data-stu-id="2f24d-132">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="2f24d-133">Intervalo válido es de 512 Kbps too102 Mbps por segundo.</span><span class="sxs-lookup"><span data-stu-id="2f24d-133">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![Limitar el ancho de banda](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

<span data-ttu-id="2f24d-135">También puede usar hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitación.</span><span class="sxs-lookup"><span data-stu-id="2f24d-135">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="2f24d-136">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2f24d-136">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="2f24d-137">**Set-OBMachineSetting -NoThrottle** indica que no se requiere ninguna limitación.</span><span class="sxs-lookup"><span data-stu-id="2f24d-137">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="2f24d-138">Control del uso de ancho de banda de red</span><span class="sxs-lookup"><span data-stu-id="2f24d-138">Influence network bandwidth</span></span>
1. <span data-ttu-id="2f24d-139">En el registro de hello navegue demasiado**Backup\Replication de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.</span><span class="sxs-lookup"><span data-stu-id="2f24d-139">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="2f24d-140">tráfico de ancho de banda de hello tooinfluence en un disco de la replicación, modificar Hola Hola de valor **UploadThreadsPerVM**, también puede crear la clave de hello si no existe.</span><span class="sxs-lookup"><span data-stu-id="2f24d-140">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="2f24d-141">ancho de banda de tooinfluence hello para el tráfico de la conmutación por recuperación de Azure, modifique el valor de hello **DownloadThreadsPerVM**.</span><span class="sxs-lookup"><span data-stu-id="2f24d-141">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="2f24d-142">valor predeterminado de Hello es 4.</span><span class="sxs-lookup"><span data-stu-id="2f24d-142">hello default value is 4.</span></span> <span data-ttu-id="2f24d-143">En una red de "sobreaprovisionada", estas claves del registro deben cambiarse de valores predeterminados de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f24d-143">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="2f24d-144">Hola máximo es 32.</span><span class="sxs-lookup"><span data-stu-id="2f24d-144">hello maximum is 32.</span></span> <span data-ttu-id="2f24d-145">Supervisar el tráfico toooptimize Hola valor.</span><span class="sxs-lookup"><span data-stu-id="2f24d-145">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f24d-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f24d-146">Next steps</span></span>

<span data-ttu-id="2f24d-147">Vaya demasiado[paso 4: planear las redes](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="2f24d-147">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
