---
title: "aaaBack las máquinas virtuales de Azure | Documentos de Microsoft"
description: "Detectar, registrar y realizar copias de seguridad de almacén de servicios de recuperación de máquinas virtuales de Azure tooa."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "copia de seguridad de máquinas virtuales; hacer copia de seguridad de máquinas virtuales; copia de seguridad y recuperación ante desastres; copia de seguridad de arm"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="e3dd9-104">Máquinas virtuales de Azure de copia de seguridad del almacén de servicios de recuperación de tooa</span><span class="sxs-lookup"><span data-stu-id="e3dd9-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3dd9-105">Copia el almacén de servicios de máquinas virtuales tooRecovery</span><span class="sxs-lookup"><span data-stu-id="e3dd9-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="e3dd9-106">Realizar copias de las máquinas virtuales tooBackup almacén</span><span class="sxs-lookup"><span data-stu-id="e3dd9-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="e3dd9-107">Este artículo detalla cómo almacén tooback seguridad tooa servicios de recuperación de máquinas virtuales de Azure (implementado por el Administrador de recursos e implementado clásico).</span><span class="sxs-lookup"><span data-stu-id="e3dd9-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="e3dd9-108">La mayoría del trabajo de Hola para copia de seguridad de máquinas virtuales es preparación Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="e3dd9-109">Para poder realizar una copia o proteger una máquina virtual, debe completar hello [requisitos previos](backup-azure-arm-vms-prepare.md) tooprepare su entorno para proteger las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="e3dd9-110">Después de completar los requisitos previos de hello, a continuación, puede iniciar las instantáneas de tootake de hello operación de copia de seguridad de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="e3dd9-111">Para obtener más información, vea los artículos de hello en [planear la infraestructura de copia de seguridad de máquina virtual en Azure](backup-azure-vms-introduction.md) y [máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="e3dd9-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="e3dd9-112">Activación de trabajo de copia de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="e3dd9-112">Triggering hello backup job</span></span>
<span data-ttu-id="e3dd9-113">Directiva de copia de seguridad de Hello asociada Hola que del almacén de servicios de recuperación define la frecuencia y cuándo se ejecuta la operación de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="e3dd9-114">De forma predeterminada, copia de seguridad programada Hola primer es copia de seguridad inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="e3dd9-115">Hasta que se produzca la copia de seguridad inicial de hello, Hola último estado de copia de seguridad en hello **trabajos de copia de seguridad** hoja se muestra como **advertencia (copia de seguridad inicial pendiente)**.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="e3dd9-117">A menos que la copia de seguridad inicial vence toobegin pronto, se recomienda que ejecute **realizar una copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="e3dd9-118">Hello procedimiento siguiente se inicia desde el panel de almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="e3dd9-119">Este procedimiento sirve para ejecutar el trabajo de copia de seguridad inicial de hello después de haber completado todos los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="e3dd9-120">Si ya se ha ejecutado el trabajo de copia de seguridad inicial de hello, este procedimiento no está disponible.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="e3dd9-121">Hello directiva de copia de seguridad asociada determina siguiente trabajo de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="e3dd9-122">toorun Hola trabajo inicial de copia de seguridad:</span><span class="sxs-lookup"><span data-stu-id="e3dd9-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="e3dd9-123">En el panel de almacén de hello, haga clic en número de hello en **elementos de copia de seguridad**, o haga clic en hello **elementos de copia de seguridad** icono.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="e3dd9-124">
  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="e3dd9-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="e3dd9-125">Hola **elementos de copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-125">hello **Backup Items** blade opens.</span></span>

  ![Elementos de copias de seguridad](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="e3dd9-127">En hello **elementos de copia de seguridad** hoja, elemento de hello select.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="e3dd9-129">Hola **elementos de copia de seguridad** lista se abre.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Trabajo de copia de seguridad desencadenado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="e3dd9-131">En hello **elementos de copia de seguridad** lista, haga clic en el botón de puntos suspensivos hello **...**  menú contextual de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="e3dd9-133">aparece el menú contextual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-133">hello Context menu appears.</span></span>

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="e3dd9-135">En el menú contextual de hello, haga clic en **una copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-135">On hello Context menu, click **Backup now**.</span></span>

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="e3dd9-137">se abre la hoja de copia de seguridad ahora Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-137">hello Backup Now blade opens.</span></span>

  ![Muestra la hoja de copia de seguridad ahora Hola](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="e3dd9-139">En hoja iniciar copia de seguridad de hello, haga clic en el icono de calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![se conserva el conjunto Hola último día Hola punto de recuperación de copia de seguridad ahora](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="e3dd9-141">Las notificaciones de implementación le permiten saber se ha desencadenado el trabajo de copia de seguridad de Hola y que puede supervisar el progreso de hello del trabajo de hello en la página de trabajos de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="e3dd9-142">Según el tamaño de saludo de la máquina virtual, crear copia de seguridad inicial de hello puede tardar unos instantes.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="e3dd9-143">estado de hello tooview o el seguimiento de hello copia de seguridad inicial, en panel de almacén de hello, vaya a hello **trabajos de copia de seguridad** icono haga clic en **en curso**.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="e3dd9-145">se abre la hoja de trabajos de copia de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-145">hello Backup Jobs blade opens.</span></span>

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="e3dd9-147">Hola **trabajos de copia de seguridad** hoja, puede ver el estado de Hola de todos los trabajos.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="e3dd9-148">Compruebe si el trabajo de copia de seguridad de hello para la máquina virtual aún está en curso, o si se ha terminado.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="e3dd9-149">Cuando finaliza un trabajo de copia de seguridad, estado de hello es *completado*.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e3dd9-150">Como parte de la operación de copia de seguridad de hello, Hola servicio copia de seguridad de Azure emite una extensión de copia de seguridad de toohello de comando en cada tooflush VM todos escribe y tome una instantánea coherente.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="e3dd9-151">Solución de errores</span><span class="sxs-lookup"><span data-stu-id="e3dd9-151">Troubleshooting errors</span></span>
<span data-ttu-id="e3dd9-152">Si surgen problemas durante la copia de seguridad de la máquina virtual, vea hello [artículo de solución de problemas de VM](backup-azure-vms-troubleshoot.md) para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3dd9-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e3dd9-153">Next steps</span></span>
<span data-ttu-id="e3dd9-154">Ahora que ha protegido la máquina virtual, vea Hola después toolearn artículos acerca de las tareas de administración de máquinas virtuales y cómo toorestore las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e3dd9-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="e3dd9-155">Administración y supervisión de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e3dd9-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="e3dd9-156">Restauración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="e3dd9-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
