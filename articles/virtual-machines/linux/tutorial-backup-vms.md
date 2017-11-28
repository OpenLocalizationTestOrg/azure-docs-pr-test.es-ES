---
title: "Copia de seguridad de máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Para proteger máquinas virtuales Linux, realice una copia de seguridad mediante Azure Backup."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="800fd-103">Copia de seguridad de máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="800fd-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="800fd-104">Para proteger sus datos realice copias de seguridad a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="800fd-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="800fd-105">Azure Backup crea puntos de recuperación que se almacenan en almacenes de recuperación con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="800fd-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="800fd-106">Cuando se restaura desde un punto de recuperación, puede restaurar Hola toda máquina virtual o simplemente algunos archivos.</span><span class="sxs-lookup"><span data-stu-id="800fd-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="800fd-107">Este artículo explica cómo toorestore un único archivo tooa nginx de ejecución de VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="800fd-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="800fd-108">Si aún no tiene un toouse de máquina virtual, puede crear uno mediante hello [inicio rápido de Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="800fd-109">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="800fd-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="800fd-110">Crear una copia de seguridad de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="800fd-111">Programar una copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="800fd-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="800fd-112">Restaurar un archivo desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="800fd-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="800fd-113">Introducción a Backup</span><span class="sxs-lookup"><span data-stu-id="800fd-113">Backup overview</span></span>

<span data-ttu-id="800fd-114">Cuando Hola servicio copia de seguridad de Azure inicia una copia de seguridad, desencadena Hola extensión de reserva tootake una instantánea en un momento.</span><span class="sxs-lookup"><span data-stu-id="800fd-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="800fd-115">Hola servicio de copia de seguridad de Azure usa hello _VMSnapshotLinux_ extensión en Linux.</span><span class="sxs-lookup"><span data-stu-id="800fd-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="800fd-116">extensión de Hola se instala durante la copia de seguridad primera VM Hola si Hola máquina virtual se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="800fd-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="800fd-117">Si hello no se está ejecutando, Hola servicio de copia de seguridad toma una instantánea de hello almacenamiento subyacente (debido a que ninguna aplicación de escritura aparecen al Hola que VM está en estado detenido).</span><span class="sxs-lookup"><span data-stu-id="800fd-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="800fd-118">De forma predeterminada, copia de seguridad de Azure toma una copia de seguridad coherente sistema para VM de Linux, pero puede ser configurado tootake [aplicación copia de seguridad coherente con marco script previo y posterior a la secuencia de comandos](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="800fd-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="800fd-119">Una vez Hola servicio de copia de seguridad de Azure toma instantáneas de hello, datos de hello están el almacén de toohello transferidos.</span><span class="sxs-lookup"><span data-stu-id="800fd-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="800fd-120">toomaximize eficacia, servicio de hello identifica y transfiere únicamente los bloques de datos que han cambiado desde la copia de seguridad anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="800fd-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="800fd-121">Una vez completada la transferencia de datos hello, instantánea Hola se quita y se crea un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="800fd-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="800fd-122">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="800fd-122">Create a backup</span></span>
<span data-ttu-id="800fd-123">Crear una sencilla programado diario copia de seguridad tooa almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="800fd-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="800fd-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="800fd-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="800fd-125">En el menú de Hola Hola izquierda, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="800fd-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="800fd-126">En lista de hello, seleccione tooback de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="800fd-127">En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="800fd-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="800fd-128">Hola **habilitar copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="800fd-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="800fd-129">En **del almacén de servicios de recuperación**, haga clic en **crear nuevo** y proporcione el nombre de hello para el nuevo almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="800fd-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="800fd-130">Se crea un nuevo almacén en hello mismo grupo de recursos y la ubicación como máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="800fd-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="800fd-131">Haga clic en **Directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="800fd-131">Click **Backup policy**.</span></span> <span data-ttu-id="800fd-132">En este ejemplo, mantenga los valores predeterminados de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="800fd-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="800fd-133">En hello **habilitar copia de seguridad** hoja, haga clic en **habilitar la copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="800fd-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="800fd-134">Esto crea una copia de seguridad diaria según la programación predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="800fd-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="800fd-135">un punto de recuperación inicial, en hello toocreate **copia de seguridad** hoja haga clic en **una copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="800fd-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="800fd-136">En hello **copia de seguridad ahora** hoja, haga clic en el icono del calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="800fd-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="800fd-137">Hola **copia de seguridad** hoja para la máquina virtual, verá Hola número de puntos de recuperación que están completos.</span><span class="sxs-lookup"><span data-stu-id="800fd-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Puntos de recuperación](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="800fd-139">primera copia de seguridad de Hello tarda aproximadamente 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="800fd-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="800fd-140">Una vez finalizada la copia de seguridad, continúe toohello siguiente parte de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="800fd-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="800fd-141">Restauración de un archivo</span><span class="sxs-lookup"><span data-stu-id="800fd-141">Restore a file</span></span>

<span data-ttu-id="800fd-142">Si eliminar ni hacer cambios tooa archivo accidentalmente, puede usar el archivo de hello toorecover de recuperación de archivos desde el almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="800fd-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="800fd-143">Recuperación de archivos utiliza una secuencia de comandos que se ejecuta en hello VM, punto de recuperación de hello toomount como unidad local.</span><span class="sxs-lookup"><span data-stu-id="800fd-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="800fd-144">Estas unidades permanecerá montadas durante 12 horas para que pueda copiar archivos de punto de recuperación de Hola y restaurarlas toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="800fd-145">En este ejemplo, mostramos cómo toorecover Hola predeterminado nginx página web /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="800fd-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="800fd-146">Hola de dirección IP pública de la máquina virtual en este ejemplo es *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="800fd-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="800fd-147">Puede encontrar la dirección IP de saludo de la vm con:</span><span class="sxs-lookup"><span data-stu-id="800fd-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="800fd-148">En el equipo local, abra un explorador y escriba en la dirección IP pública de saludo de la página web VM toosee Hola predeterminada nginx.</span><span class="sxs-lookup"><span data-stu-id="800fd-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Página web predeterminada de nginx](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="800fd-150">Utilice SSH en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="800fd-151">Elimine /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="800fd-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="800fd-152">En el equipo local, actualice el Explorador de hello presionando CTRL + F5 toosee esos valores predeterminados de página nginx ha desaparecido.</span><span class="sxs-lookup"><span data-stu-id="800fd-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Página web predeterminada de nginx](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="800fd-154">En el equipo local, inicie sesión toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="800fd-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="800fd-155">En el menú de Hola Hola izquierda, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="800fd-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="800fd-156">En lista de hello, seleccione Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="800fd-157">En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="800fd-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="800fd-158">Hola **copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="800fd-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="800fd-159">En menú hello en parte superior de Hola de hoja de hello, seleccione **recuperación de archivos**.</span><span class="sxs-lookup"><span data-stu-id="800fd-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="800fd-160">Hola **recuperación de archivos** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="800fd-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="800fd-161">En **paso 1: seleccione el punto de recuperación**, seleccione un punto de recuperación de Hola de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="800fd-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="800fd-162">En **paso 2: Descargar script toobrowse y recuperar archivos**, haga clic en hello **descargar ejecutable** botón.</span><span class="sxs-lookup"><span data-stu-id="800fd-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="800fd-163">Guarde el equipo local de hello archivo descargado tooyour.</span><span class="sxs-lookup"><span data-stu-id="800fd-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="800fd-164">Haga clic en **descargar script** archivo de script de Hola de toodownload localmente.</span><span class="sxs-lookup"><span data-stu-id="800fd-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="800fd-165">Abra un Hola de símbolo del sistema y el tipo de Bash siguientes, reemplazando *Linux_myVM_05-05-2017.sh* con hello corregir la ruta de acceso y nombre de archivo de script de Hola que ha descargado, *azureuser* con nombre de usuario de Hola para hello VM y *13.69.75.209* con la dirección IP pública de hello para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="800fd-166">En el equipo local, abra una toohello de conexión SSH máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="800fd-167">En la máquina virtual, agregue ejecutar el archivo de secuencia de comandos de toohello de permisos.</span><span class="sxs-lookup"><span data-stu-id="800fd-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="800fd-168">En la máquina virtual, ejecute punto de recuperación de hello script toomount Hola como un sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="800fd-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="800fd-169">Hola de salida de hello script proporciona que Hola ruta de acceso de punto de montaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="800fd-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="800fd-170">salida de Hello tiene un aspecto similar toothis:</span><span class="sxs-lookup"><span data-stu-id="800fd-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="800fd-171">En la máquina virtual, copie hello nginx página web desde el punto de montaje hello toowhere atrás eliminar archivo hello.</span><span class="sxs-lookup"><span data-stu-id="800fd-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="800fd-172">En el equipo local, abra la pestaña del explorador de Hola que está conectado toohello dirección IP de hello máquina virtual que muestra hello nginx de forma predeterminada la página.</span><span class="sxs-lookup"><span data-stu-id="800fd-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="800fd-173">Presione CTRL + F5 página del explorador toorefresh Hola.</span><span class="sxs-lookup"><span data-stu-id="800fd-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="800fd-174">Ahora debería ver ese Hola página predeterminada está funcionando de nuevo.</span><span class="sxs-lookup"><span data-stu-id="800fd-174">You should now see that hello default page is working again.</span></span>

    ![Página web predeterminada de nginx](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="800fd-176">En el equipo local, volver atrás toohello pestaña del explorador para hello portal de Azure y en **paso 3: desmontar discos Hola después de la recuperación** haga clic en hello **desmontar discos** botón.</span><span class="sxs-lookup"><span data-stu-id="800fd-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="800fd-177">Si olvida este paso toodo, el punto de montaje de hello conexión toohello es cerrar automáticamente después de 12 horas.</span><span class="sxs-lookup"><span data-stu-id="800fd-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="800fd-178">Después de esas 12 horas, debe toodownload un toocreate de script nuevo un nuevo punto de montaje.</span><span class="sxs-lookup"><span data-stu-id="800fd-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="800fd-179">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="800fd-179">Next steps</span></span>

<span data-ttu-id="800fd-180">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="800fd-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="800fd-181">Crear una copia de seguridad de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="800fd-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="800fd-182">Programar una copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="800fd-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="800fd-183">Restaurar un archivo desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="800fd-183">Restore a file from a backup</span></span>

<span data-ttu-id="800fd-184">Avanzar toohello toolearn de tutorial siguiente sobre la supervisión de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="800fd-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="800fd-185">Supervisión de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="800fd-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

