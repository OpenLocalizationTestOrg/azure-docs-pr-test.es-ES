---
title: "Copia de seguridad de máquinas virtuales Windows de Azure | Microsoft Docs'"
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
ms.openlocfilehash: 8e58a2290e5034ef393f65cbcddb86e18cf4a6ec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="d2749-103">Copia de seguridad de máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="d2749-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="d2749-104">Para proteger sus datos realice copias de seguridad a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="d2749-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="d2749-105">Azure Backup crea puntos de recuperación que se almacenan en almacenes de recuperación con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="d2749-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="d2749-106">Cuando se realiza una restauración desde un punto de recuperación, se puede restaurar toda una máquina virtual o solo determinados archivos.</span><span class="sxs-lookup"><span data-stu-id="d2749-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="d2749-107">En este artículo se explica cómo restaurar un único archivo en una máquina virtual que ejecuta Windows Server e IIS.</span><span class="sxs-lookup"><span data-stu-id="d2749-107">This article explains how to restore a single file to a VM running Windows Server and IIS.</span></span> <span data-ttu-id="d2749-108">Si aún no tiene una máquina virtual que pueda usar, puede crear una mediante la guía de [inicio rápido de Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2749-108">If you don't already have a VM to use, you can create one using the [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="d2749-109">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="d2749-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2749-110">Crear una copia de seguridad de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="d2749-111">Programar una copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="d2749-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="d2749-112">Restaurar un archivo desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d2749-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="d2749-113">Introducción a Backup</span><span class="sxs-lookup"><span data-stu-id="d2749-113">Backup overview</span></span>

<span data-ttu-id="d2749-114">Cuando el servicio Azure Backup inicia una copia de seguridad, desencadena la extensión de copia de seguridad para que tome una instantánea de un momento dado.</span><span class="sxs-lookup"><span data-stu-id="d2749-114">When the Azure Backup service initiates a backup job, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="d2749-115">El servicio Azure Backup usa la extensión _VMSnapshot_.</span><span class="sxs-lookup"><span data-stu-id="d2749-115">The Azure Backup service uses the _VMSnapshot_ extension.</span></span> <span data-ttu-id="d2749-116">La extensión se instala cuando se realiza la primera copia de seguridad de la máquina virtual, en caso de que esta esté en ejecución.</span><span class="sxs-lookup"><span data-stu-id="d2749-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="d2749-117">Si no se está ejecutando la máquina virtual, el servicio Azure Backup toma una instantánea del almacenamiento subyacente (ya que no se produce ninguna escritura de la aplicación mientras se detiene la máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="d2749-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="d2749-118">Cuando se toma una instantánea de las máquinas virtuales de Windows, el servicio Azure Backup se coordina con el servicio de instantáneas de volumen (VSS) para obtener una instantánea coherente de los discos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-118">When taking a snapshot of Windows VMs, the Backup service coordinates with the Volume Shadow Copy Service (VSS) to get a consistent snapshot of the virtual machine's disks.</span></span> <span data-ttu-id="d2749-119">Después de que el servicio Azure Backup toma la instantánea, se transfieren los datos al almacén.</span><span class="sxs-lookup"><span data-stu-id="d2749-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="d2749-120">Para que el proceso resulte más eficaz, el servicio identifica y transfiere únicamente los bloques de datos que han cambiado desde la última copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d2749-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="d2749-121">Cuando finaliza la transferencia de datos, se elimina la instantánea y se crea un punto de recuperación.</span><span class="sxs-lookup"><span data-stu-id="d2749-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="d2749-122">Creación de una copia de seguridad</span><span class="sxs-lookup"><span data-stu-id="d2749-122">Create a backup</span></span>
<span data-ttu-id="d2749-123">Cree una copia de seguridad diaria programada simple en un almacén de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="d2749-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="d2749-124">Inicie sesión en el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d2749-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d2749-125">En el menú de la izquierda, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="d2749-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="d2749-126">En la lista, seleccione la máquina virtual de la que quiere realizar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d2749-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="d2749-127">En la hoja de la máquina virtual, en la sección **Configuración**, haga clic en **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="d2749-128">Se abre la hoja **Habilitar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="d2749-129">En **Almacén de Recovery Services**, haga clic en **Create new** (Crear nuevo) y especifique el nombre del nuevo almacén.</span><span class="sxs-lookup"><span data-stu-id="d2749-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="d2749-130">Se crea un nuevo almacén en el grupo de recursos y ubicación en que se encuentra la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="d2749-131">Haga clic en **Directiva de copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-131">Click **Backup policy**.</span></span> <span data-ttu-id="d2749-132">En este ejemplo, conserve los valores predeterminados y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d2749-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="d2749-133">En la hoja **Habilitar copia de seguridad**, haga clic en **Habilitar copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="d2749-134">De esta forma se crea una copia de seguridad diaria según la programación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d2749-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="d2749-135">Para crear un punto de recuperación inicial, en la hoja **Copia de seguridad** haga clic en **Realizar copia de seguridad ahora**.</span><span class="sxs-lookup"><span data-stu-id="d2749-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="d2749-136">En la hoja **Realizar copia de seguridad ahora**, haga clic en el icono del calendario, use el control de calendario para seleccionar el último día en que se mantendrá este punto de recuperación y haga clic en **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="d2749-137">En la hoja **Copia de seguridad** de la máquina virtual, verá el número de puntos de recuperación completos.</span><span class="sxs-lookup"><span data-stu-id="d2749-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![Puntos de recuperación](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="d2749-139">La primera copia de seguridad tarda aproximadamente 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="d2749-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="d2749-140">Cuando la copia de seguridad finalice, pase a la parte siguiente de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d2749-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="d2749-141">Recuperación de un archivo</span><span class="sxs-lookup"><span data-stu-id="d2749-141">Recover a file</span></span>

<span data-ttu-id="d2749-142">Si accidentalmente elimina o realiza cambios en un archivo, puede usar Recuperación de archivos para recuperar el archivo del almacén de Backup.</span><span class="sxs-lookup"><span data-stu-id="d2749-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="d2749-143">Recuperación de archivos usa un script que se ejecuta en la máquina virtual para montar el punto de recuperación como unidad local.</span><span class="sxs-lookup"><span data-stu-id="d2749-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="d2749-144">Estas unidades permanecerán montadas durante 12 horas para que pueda copiar archivos desde el punto de recuperación y restaurarlos en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="d2749-145">En este ejemplo, se muestra cómo recuperar el archivo de imagen que se usa en la página web predeterminada de IIS.</span><span class="sxs-lookup"><span data-stu-id="d2749-145">In this example, we show how to recover the image file that is used in the default web page for IIS.</span></span> 

1. <span data-ttu-id="d2749-146">Abra un explorador y conéctese a la dirección IP de la máquina virtual para mostrar la página predeterminada de IIS.</span><span class="sxs-lookup"><span data-stu-id="d2749-146">Open a browser and connect to the IP address of the VM to show the default IIS page.</span></span>

    ![Página web predeterminada de IIS](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="d2749-148">Conéctese a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-148">Connect to the VM.</span></span>
3. <span data-ttu-id="d2749-149">En la máquina virtual, abra el **Explorador de archivos**, vaya a \inetpub\wwwroot y elimine el archivo **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="d2749-149">On the VM, open **File Explorer** and navigate to \inetpub\wwwroot and delete the file **iisstart.png**.</span></span>
4. <span data-ttu-id="d2749-150">En el equipo local, actualice el explorador para ver que la imagen en la página predeterminada de IIS ha desaparecido.</span><span class="sxs-lookup"><span data-stu-id="d2749-150">On your local computer, refresh the browser to see that the image on the default IIS page is gone.</span></span>

    ![Página web predeterminada de IIS](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="d2749-152">En el equipo local, abra una nueva pestaña y vaya al [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2749-152">On your local computer, open a new tab and go the the [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="d2749-153">En el menú de la izquierda, seleccione **Máquinas virtuales** y seleccione la máquina virtual de la lista.</span><span class="sxs-lookup"><span data-stu-id="d2749-153">In the menu on the left, select **Virtual machines** and select the VM form the list.</span></span>
8. <span data-ttu-id="d2749-154">En la hoja de la máquina virtual, en la sección **Configuración**, haga clic en **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-154">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="d2749-155">Se abre la hoja **Copia de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="d2749-155">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="d2749-156">En el menú de la parte superior de la hoja, seleccione **Recuperación de archivos**.</span><span class="sxs-lookup"><span data-stu-id="d2749-156">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="d2749-157">Se abrirá la hoja **Recuperación de archivos**.</span><span class="sxs-lookup"><span data-stu-id="d2749-157">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="d2749-158">En **Paso 1: Seleccionar punto de recuperación**, seleccione un punto de recuperación en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="d2749-158">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="d2749-159">En **Paso 2: Descargar script para examinar y recuperar archivos**, haga clic en el botón **Download Executable** (Descargar ejecutable).</span><span class="sxs-lookup"><span data-stu-id="d2749-159">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="d2749-160">Guarde el archivo en la carpeta **Descargas**.</span><span class="sxs-lookup"><span data-stu-id="d2749-160">Save the file to your **Downloads** folder.</span></span>
12. <span data-ttu-id="d2749-161">En el equipo local, abra el **Explorador de archivos**, vaya a la carpeta **Descargas** y copie el archivo .exe descargado.</span><span class="sxs-lookup"><span data-stu-id="d2749-161">On your local computer, open **File Explorer** and navigate to your **Downloads** folder and copy the downloaded .exe file.</span></span> <span data-ttu-id="d2749-162">El nombre de archivo llevará delante el nombre de su máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-162">The filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="d2749-163">En la máquina virtual (a través de la conexión RDP), pegue el archivo .exe en el escritorio de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-163">On your VM (over the RDP connection) paste the .exe file to the Desktop of your VM.</span></span> 
14. <span data-ttu-id="d2749-164">Vaya al escritorio de la máquina virtual y haga doble clic en el archivo .exe.</span><span class="sxs-lookup"><span data-stu-id="d2749-164">Navigate to the desktop of your VM and double-click on the .exe.</span></span> <span data-ttu-id="d2749-165">Se inicia un símbolo del sistema y luego se monta el punto de recuperación como un recurso compartido de archivos al que puede obtener acceso.</span><span class="sxs-lookup"><span data-stu-id="d2749-165">This will launch a command prompt and then mount the recovery point as a file share that you can access.</span></span> <span data-ttu-id="d2749-166">Cuando se termine de crear el recurso compartido, escriba **q** para cerrar el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="d2749-166">When it is finished creating the share, type **q** to close the command prompt.</span></span>
15. <span data-ttu-id="d2749-167">En la máquina virtual, abra el **Explorador de archivos** y vaya a la letra de unidad que se usó para el recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="d2749-167">On your VM, open **File Explorer** and navigate to the drive letter that was used for the file share.</span></span>
16. <span data-ttu-id="d2749-168">Vaya a \inetpub\wwwroot, copie **iisstart.png** del recurso compartido de archivos y péguelo en \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="d2749-168">Navigate to \inetpub\wwwroot and copy **iisstart.png** from the file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="d2749-169">Por ejemplo, copie F:\inetpub\wwwroot\iisstart.png y péguelo en c:\inetpub\wwwroot para recuperar el archivo.</span><span class="sxs-lookup"><span data-stu-id="d2749-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot to recover the file.</span></span>
17. <span data-ttu-id="d2749-170">En el equipo local, abra la pestaña del explorador en el que está conectado a la dirección IP de la máquina virtual que muestra la página predeterminada de IIS.</span><span class="sxs-lookup"><span data-stu-id="d2749-170">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the IIS default page.</span></span> <span data-ttu-id="d2749-171">Presione CTRL + F5 para actualizar la página del explorador.</span><span class="sxs-lookup"><span data-stu-id="d2749-171">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="d2749-172">Ahora debería ver que la imagen se ha restaurado.</span><span class="sxs-lookup"><span data-stu-id="d2749-172">You should now see that the image has been restored.</span></span>
18. <span data-ttu-id="d2749-173">En el equipo local, vuelva a la pestaña de explorador de Azure Portal y en **Paso 3: Desmontar los discos después de la recuperación**, haga clic en el botón **Desmontar discos**.</span><span class="sxs-lookup"><span data-stu-id="d2749-173">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="d2749-174">Si olvida realizar este paso, la conexión al punto de montaje se cierra automáticamente tras 12 horas.</span><span class="sxs-lookup"><span data-stu-id="d2749-174">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="d2749-175">A las 12 horas, es preciso que descargue un script nuevo para crear un nuevo punto de montaje.</span><span class="sxs-lookup"><span data-stu-id="d2749-175">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d2749-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d2749-176">Next steps</span></span>

<span data-ttu-id="d2749-177">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="d2749-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d2749-178">Crear una copia de seguridad de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2749-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="d2749-179">Programar una copia de seguridad diaria.</span><span class="sxs-lookup"><span data-stu-id="d2749-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="d2749-180">Restaurar un archivo desde una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d2749-180">Restore a file from a backup</span></span>

<span data-ttu-id="d2749-181">En el siguiente tutorial se explica cómo supervisar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="d2749-181">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2749-182">Supervisión de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="d2749-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









