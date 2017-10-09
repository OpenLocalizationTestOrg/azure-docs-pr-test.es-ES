---
title: "aaaBackup máquinas virtuales de Windows Azure | Documentos de Microsoft"
description: "Para proteger las máquinas virtuales Windows, realice una copia de seguridad de ellas mediante Azure Backup."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="eeaed-103">Copia de seguridad de máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="eeaed-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="eeaed-104">Para proteger sus datos realice copias de seguridad a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="eeaed-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="eeaed-105">Azure Backup crea puntos de recuperación que se almacenan en almacenes de recuperación con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="eeaed-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="eeaed-106">Cuando se restaura desde un punto de recuperación, puede restaurar Hola toda máquina virtual o simplemente algunos archivos.</span><span class="sxs-lookup"><span data-stu-id="eeaed-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="eeaed-107">Este artículo explica cómo toorestore un único archivo tooa VM ejecuta Windows Server e IIS.</span><span class="sxs-lookup"><span data-stu-id="eeaed-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="eeaed-108">Si aún no tiene un toouse de máquina virtual, puede crear uno mediante hello [inicio rápido de Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eeaed-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="eeaed-109">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="eeaed-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eeaed-110">Crear una copia de seguridad de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="eeaed-111">Programar una copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="eeaed-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="eeaed-112">Restaurar un archivo desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="eeaed-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="eeaed-113">Introducción a Backup</span><span class="sxs-lookup"><span data-stu-id="eeaed-113">Backup overview</span></span>

<span data-ttu-id="eeaed-114">Cuando Hola servicio copia de seguridad de Azure inicia un trabajo de copia de seguridad, desencadena Hola extensión de reserva tootake una instantánea en un momento.</span><span class="sxs-lookup"><span data-stu-id="eeaed-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="eeaed-115">Hola servicio de copia de seguridad de Azure usa hello _VMSnapshot_ extensión.</span><span class="sxs-lookup"><span data-stu-id="eeaed-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="eeaed-116">extensión de Hola se instala durante la copia de seguridad primera VM Hola si Hola máquina virtual se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="eeaed-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="eeaed-117">Si hello no se está ejecutando, Hola servicio de copia de seguridad toma una instantánea de hello almacenamiento subyacente (debido a que ninguna aplicación de escritura aparecen al Hola que VM está en estado detenido).</span><span class="sxs-lookup"><span data-stu-id="eeaed-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="eeaed-118">Cuando se toma una instantánea de máquinas virtuales de Windows, servicio de copia de seguridad de Hola coordina con tooget de servicio de instantáneas de volumen (VSS) de hello una instantánea coherente de los discos de la máquina virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="eeaed-119">Una vez Hola servicio de copia de seguridad de Azure toma instantáneas de hello, datos de hello están el almacén de toohello transferidos.</span><span class="sxs-lookup"><span data-stu-id="eeaed-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="eeaed-120">toomaximize eficacia, servicio de hello identifica y transfiere únicamente los bloques de datos que han cambiado desde la copia de seguridad anterior de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="eeaed-121">Una vez completada la transferencia de datos hello, instantánea Hola se quita y se crea un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="eeaed-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="eeaed-122">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="eeaed-122">Create a backup</span></span>
<span data-ttu-id="eeaed-123">Crear una sencilla programado diario copia de seguridad tooa almacén de servicios de recuperación.</span><span class="sxs-lookup"><span data-stu-id="eeaed-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="eeaed-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="eeaed-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="eeaed-125">En el menú de Hola Hola izquierda, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="eeaed-126">En lista de hello, seleccione tooback de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="eeaed-127">En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="eeaed-128">Hola **habilitar copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="eeaed-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="eeaed-129">En **del almacén de servicios de recuperación**, haga clic en **crear nuevo** y proporcione el nombre de hello para el nuevo almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="eeaed-130">Se crea un nuevo almacén en hello mismo grupo de recursos y la ubicación como máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="eeaed-131">Haga clic en **Directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-131">Click **Backup policy**.</span></span> <span data-ttu-id="eeaed-132">En este ejemplo, mantenga los valores predeterminados de Hola y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="eeaed-133">En hello **habilitar copia de seguridad** hoja, haga clic en **habilitar la copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="eeaed-134">Esto crea una copia de seguridad diaria según la programación predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="eeaed-135">un punto de recuperación inicial, en hello toocreate **copia de seguridad** hoja haga clic en **una copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="eeaed-136">En hello **copia de seguridad ahora** hoja, haga clic en el icono del calendario de hello, usar Hola calendario control tooselect hello último día de este punto de recuperación se conservan y haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="eeaed-137">Hola **copia de seguridad** hoja para la máquina virtual, verá Hola número de puntos de recuperación que están completos.</span><span class="sxs-lookup"><span data-stu-id="eeaed-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Puntos de recuperación](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="eeaed-139">primera copia de seguridad de Hello tarda aproximadamente 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="eeaed-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="eeaed-140">Una vez finalizada la copia de seguridad, continúe toohello siguiente parte de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="eeaed-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="eeaed-141">Recuperación de un archivo</span><span class="sxs-lookup"><span data-stu-id="eeaed-141">Recover a file</span></span>

<span data-ttu-id="eeaed-142">Si eliminar ni hacer cambios tooa archivo accidentalmente, puede usar el archivo de hello toorecover de recuperación de archivos desde el almacén de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="eeaed-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="eeaed-143">Recuperación de archivos utiliza una secuencia de comandos que se ejecuta en hello VM, punto de recuperación de hello toomount como unidad local.</span><span class="sxs-lookup"><span data-stu-id="eeaed-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="eeaed-144">Estas unidades permanecerá montadas durante 12 horas para que pueda copiar archivos de punto de recuperación de Hola y restaurarlas toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="eeaed-145">En este ejemplo, mostramos cómo toorecover Hola archivo de imagen que se usa en la página web de hello predeterminada de IIS.</span><span class="sxs-lookup"><span data-stu-id="eeaed-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="eeaed-146">Abra un explorador y conéctese toohello dirección IP de página IIS predeterminada de hello VM tooshow Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Página web predeterminada de IIS](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="eeaed-148">Conectar toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="eeaed-149">En hello VM, abra **Explorador de archivos** navegue too\inetpub\wwwroot y elimine el archivo hello **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="eeaed-150">En el equipo local, la actualización Hola explorador toosee que Hola imagen en la página IIS predeterminada Hola ha desaparecido.</span><span class="sxs-lookup"><span data-stu-id="eeaed-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Página web predeterminada de IIS](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="eeaed-152">En el equipo local, abra una nueva pestaña y vaya Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eeaed-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="eeaed-153">En el menú de Hola Hola izquierda, seleccione **máquinas virtuales** y seleccione Hola VM formulario Hola lista.</span><span class="sxs-lookup"><span data-stu-id="eeaed-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="eeaed-154">En el módulo VM hello, Hola **configuración** sección, haga clic en **copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="eeaed-155">Hola **copia de seguridad** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="eeaed-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="eeaed-156">En menú hello en parte superior de Hola de hoja de hello, seleccione **recuperación de archivos**.</span><span class="sxs-lookup"><span data-stu-id="eeaed-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="eeaed-157">Hola **recuperación de archivos** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="eeaed-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="eeaed-158">En **paso 1: seleccione el punto de recuperación**, seleccione un punto de recuperación de Hola de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="eeaed-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="eeaed-159">En **paso 2: Descargar script toobrowse y recuperar archivos**, haga clic en hello **descargar ejecutable** botón.</span><span class="sxs-lookup"><span data-stu-id="eeaed-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="eeaed-160">Guardar Hola archivo tooyour **descarga** carpeta.</span><span class="sxs-lookup"><span data-stu-id="eeaed-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="eeaed-161">En el equipo local, abra **Explorador de archivos** y navegue tooyour **descarga** Hola de carpeta y copie el archivo de .exe descargado.</span><span class="sxs-lookup"><span data-stu-id="eeaed-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="eeaed-162">nombre de archivo de Hello estará prefijado por su nombre de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="eeaed-163">En la máquina virtual (a través de Hola conexión RDP) Pegar Hola .exe archivo toohello escritorio de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="eeaed-164">Navegue toohello escritorio de la máquina virtual y haga doble clic en .exe Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="eeaed-165">Esto se inicie un símbolo del sistema y a continuación, monte el punto de recuperación de Hola como un recurso compartido de archivos que puede tener acceso.</span><span class="sxs-lookup"><span data-stu-id="eeaed-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="eeaed-166">Cuando finaliza crear recurso compartido de hello, escriba **preguntas** tooclose Hola símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="eeaed-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="eeaed-167">En la máquina virtual, abra **Explorador de archivos** y navegar por la letra de unidad de toohello que se usó para el recurso compartido de archivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="eeaed-168">Navegar por too\inetpub\wwwroot y copia **iisstart.png** desde archivo hello, compartir y pegarlos en \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="eeaed-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="eeaed-169">Por ejemplo, copie F:\inetpub\wwwroot\iisstart.png y péguelo en el archivo de hello toorecover c:\inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="eeaed-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="eeaed-170">En el equipo local, abra la pestaña del explorador de Hola que está conectado toohello dirección IP de hello máquina virtual que muestra hello IIS de forma predeterminada la página.</span><span class="sxs-lookup"><span data-stu-id="eeaed-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="eeaed-171">Presione CTRL + F5 página del explorador toorefresh Hola.</span><span class="sxs-lookup"><span data-stu-id="eeaed-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="eeaed-172">Ahora debería ver ese Hola se ha restaurado la imagen.</span><span class="sxs-lookup"><span data-stu-id="eeaed-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="eeaed-173">En el equipo local, volver atrás toohello pestaña del explorador para hello portal de Azure y en **paso 3: desmontar discos Hola después de la recuperación** haga clic en hello **desmontar discos** botón.</span><span class="sxs-lookup"><span data-stu-id="eeaed-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="eeaed-174">Si olvida este paso toodo, el punto de montaje de hello conexión toohello es cerrar automáticamente después de 12 horas.</span><span class="sxs-lookup"><span data-stu-id="eeaed-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="eeaed-175">Después de esas 12 horas, debe toodownload un toocreate de script nuevo un nuevo punto de montaje.</span><span class="sxs-lookup"><span data-stu-id="eeaed-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eeaed-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eeaed-176">Next steps</span></span>

<span data-ttu-id="eeaed-177">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="eeaed-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eeaed-178">Crear una copia de seguridad de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eeaed-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="eeaed-179">Programar una copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="eeaed-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="eeaed-180">Restaurar un archivo desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="eeaed-180">Restore a file from a backup</span></span>

<span data-ttu-id="eeaed-181">Avanzar toohello toolearn de tutorial siguiente sobre la supervisión de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="eeaed-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eeaed-182">Supervisión de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="eeaed-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









