---
title: "Copia de seguridad de máquinas virtuales de Azure | Microsoft Docs"
description: "Detecte y registre máquinas virtuales de Azure y haga copias de seguridad de las mismas en un almacén de Recovery Services."
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
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="08ce6-104">Copia de seguridad de máquinas virtuales de Azure en un almacén de Recovery Services</span><span class="sxs-lookup"><span data-stu-id="08ce6-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08ce6-105">Copia de seguridad de VM en el almacén de servicios de recuperación</span><span class="sxs-lookup"><span data-stu-id="08ce6-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="08ce6-106">Copia de seguridad de VM en el almacén de Copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="08ce6-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="08ce6-107">En este artículo se proporcionan detalles para realizar una copia de seguridad de VM de Azure (con el modelo de implementación de Resource Manager y el modelo clásico) en un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="08ce6-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="08ce6-108">La mayoría del trabajo de la copia de seguridad de máquinas virtuales se basa en la preparación.</span><span class="sxs-lookup"><span data-stu-id="08ce6-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="08ce6-109">Antes de poder realizar una copia de seguridad de una máquina virtual, o protegerla, es necesario realizar una serie de tareas que son [requisito previo](backup-azure-arm-vms-prepare.md) con el fin de preparar el entorno para la protección de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="08ce6-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="08ce6-110">Cuando haya realizado estas tareas, puede iniciar la operación de copia de seguridad para tomar instantáneas de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="08ce6-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="08ce6-111">Para más información, vea los artículos sobre cómo [planear la infraestructura de copia de seguridad de máquinas virtuales en Azure](backup-azure-vms-introduction.md) y sobre [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="08ce6-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="08ce6-112">Desencadenamiento del trabajo de copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="08ce6-112">Triggering the backup job</span></span>
<span data-ttu-id="08ce6-113">La directiva asociada con el almacén de Recovery Services define con qué frecuencia y cuándo se ejecuta la operación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="08ce6-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="08ce6-114">De forma predeterminada, la primera copia de seguridad programada es la copia de seguridad inicial.</span><span class="sxs-lookup"><span data-stu-id="08ce6-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="08ce6-115">Hasta que se realice la copia de seguridad inicial, el estado de la última copia aparecerá como **Advertencia (copia de seguridad inicial pendiente)** en la hoja **Trabajos de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Copia de seguridad pendiente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="08ce6-117">A menos que la copia de seguridad inicial vaya a comenzar pronto, se recomienda ejecutar **Hacer ahora una copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="08ce6-118">El procedimiento siguiente se inicia desde el panel del almacén.</span><span class="sxs-lookup"><span data-stu-id="08ce6-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="08ce6-119">Este procedimiento sirve para ejecutar el trabajo de copia de seguridad inicial después de haber completado todos los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="08ce6-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="08ce6-120">Si ya se ha ejecutado el trabajo de copia de seguridad inicial, este procedimiento no está disponible.</span><span class="sxs-lookup"><span data-stu-id="08ce6-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="08ce6-121">La directiva de copia de seguridad asociada determina el siguiente trabajo de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="08ce6-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="08ce6-122">Para ejecutar el trabajo de copia de seguridad inicial:</span><span class="sxs-lookup"><span data-stu-id="08ce6-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="08ce6-123">En el panel del almacén, haga clic en el número situado bajo **Elementos de copia de seguridad** o haga clic en el icono **Elementos de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="08ce6-124">
  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="08ce6-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="08ce6-125">Se abrirá la hoja **Elementos de copia de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="08ce6-125">The **Backup Items** blade opens.</span></span>

  ![Elementos de copias de seguridad](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="08ce6-127">En la hoja **Elementos de copia de seguridad**, seleccione el elemento.</span><span class="sxs-lookup"><span data-stu-id="08ce6-127">On the **Backup Items** blade, select the item.</span></span>

  ![Icono Configuración](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="08ce6-129">Se abrirá la lista **Elementos de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-129">The **Backup Items** list opens.</span></span> <br/>

  ![Trabajo de copia de seguridad desencadenado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="08ce6-131">En la lista **Elementos de copia de seguridad**, haga clic en el botón de puntos suspensivos **...** para abrir el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="08ce6-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="08ce6-133">Aparece el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="08ce6-133">The Context menu appears.</span></span>

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="08ce6-135">En el menú contextual, haga clic en **Realizar copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-135">On the Context menu, click **Backup now**.</span></span>

  ![Menú contextual](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="08ce6-137">Se abrirá la hoja Realizar copia de seguridad ahora.</span><span class="sxs-lookup"><span data-stu-id="08ce6-137">The Backup Now blade opens.</span></span>

  ![muestra la hoja Realizar copia de seguridad ahora](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="08ce6-139">En la hoja Realizar copia de seguridad ahora, haga clic en el icono del calendario, use el control del calendario para seleccionar el último día en el que se mantendrá este punto de recuperación y haga clic en **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![establece el último día en que se mantiene el punto de recuperación de Realizar copia de seguridad ahora](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="08ce6-141">Las notificaciones de implementación le permiten saber si se ha desencadenado el trabajo de copia de seguridad y que puede supervisar el progreso del trabajo en la página de trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="08ce6-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="08ce6-142">Según el tamaño de la máquina virtual, la creación de la copia de seguridad inicial puede tardar un tiempo.</span><span class="sxs-lookup"><span data-stu-id="08ce6-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="08ce6-143">Para ver o realizar el seguimiento del estado de la copia de seguridad inicial, en el panel del almacén, en el icono **Trabajos de copia de seguridad**, haga clic en **En curso**.</span><span class="sxs-lookup"><span data-stu-id="08ce6-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="08ce6-145">Se abrirá la hoja Trabajos de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="08ce6-145">The Backup Jobs blade opens.</span></span>

  ![Icono de Trabajos de copia de seguridad](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="08ce6-147">En la hoja **Trabajos de copia de seguridad** , puede ver el estado de todos los trabajos.</span><span class="sxs-lookup"><span data-stu-id="08ce6-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="08ce6-148">Compruebe si el trabajo de copia de seguridad para la máquina virtual aún está en curso o si se ha terminado.</span><span class="sxs-lookup"><span data-stu-id="08ce6-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="08ce6-149">Cuando finalice un trabajo de copia de seguridad, el estado será *Completado*.</span><span class="sxs-lookup"><span data-stu-id="08ce6-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="08ce6-150">Como parte de la operación de copia de seguridad, el servicio Azure Backup emite un comando a la extensión de copia de seguridad en cada máquina virtual para vaciar toda la escritura y tomar una instantánea coherente.</span><span class="sxs-lookup"><span data-stu-id="08ce6-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="08ce6-151">Solución de errores</span><span class="sxs-lookup"><span data-stu-id="08ce6-151">Troubleshooting errors</span></span>
<span data-ttu-id="08ce6-152">Si se encuentra con problemas mientras realiza la copia de seguridad de la máquina virtual, vea el [artículo sobre cómo solucionar problemas de máquinas virtuales](backup-azure-vms-troubleshoot.md) para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="08ce6-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08ce6-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08ce6-153">Next steps</span></span>
<span data-ttu-id="08ce6-154">Ahora que ha protegido su máquina virtual, vea los siguientes artículos para obtener información sobre las tareas de administración de las máquinas virtuales y cómo restaurarlas.</span><span class="sxs-lookup"><span data-stu-id="08ce6-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="08ce6-155">Administración y supervisión de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="08ce6-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="08ce6-156">Restauración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="08ce6-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
