---
title: "aaaUse una solución de problemas de VM en el portal de Azure Hola de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot problemas de máquinas virtuales de Linux conexión usando máquinas virtuales de recuperación tooa de hello SO disco Hola portal de Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="c5f9f-103">Solucionar problemas de una VM de Linux mediante la asociación de la máquina virtual de recuperación de tooa del disco de hello SO utilizando Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c5f9f-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="c5f9f-104">Si la máquina virtual (VM) de Linux se encuentra un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="c5f9f-105">Un ejemplo común sería una entrada no válida en `/etc/fstab` que impide Hola VM pueda tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="c5f9f-106">Este artículo se detallan cómo toouse Hola tooconnect portal Azure su virtual rígida tooanother toofix de VM de Linux en disco los errores, a continuación, volver a crea la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="c5f9f-107">Introducción al proceso de recuperación</span><span class="sxs-lookup"><span data-stu-id="c5f9f-107">Recovery process overview</span></span>
<span data-ttu-id="c5f9f-108">proceso de solución de problemas de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="c5f9f-109">Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="c5f9f-110">Adjuntar y montar tooanother de disco duro virtual de hello VM de Linux para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="c5f9f-111">Conectar toohello solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="c5f9f-112">Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="c5f9f-113">Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="c5f9f-114">Crear una máquina virtual mediante hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="c5f9f-115">Determinación de los problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="c5f9f-115">Determine boot issues</span></span>
<span data-ttu-id="c5f9f-116">Examine el diagnóstico de arranque hello y toodetermine de captura de pantalla VM por qué la máquina virtual no es capaz de tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="c5f9f-117">Un ejemplo habitual sería una entrada no válida en `/etc/fstab` o un disco duro virtual subyacente que se va a eliminar o mover.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="c5f9f-118">Seleccione la máquina virtual en el portal de hello y, a continuación, desplácese hacia abajo de toohello **soporte técnico y solución de problemas** sección.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="c5f9f-119">Haga clic en **diagnósticos de arranque** tooview mensajes de la consola de hello transmite por secuencias desde la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="c5f9f-120">Revisión Hola registros de la consola toosee si puede determinar por qué hello VM experimenta un problema.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="c5f9f-121">Hello en el ejemplo siguiente se muestra que una máquina virtual atascada en el modo de mantenimiento que requiere la intervención manual:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Visualización de los registros de consola de diagnóstico de arranque](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="c5f9f-123">También puede hacer clic en **captura de pantalla de** en parte superior de Hola de hello arranque diagnósticos registro toodownload una captura de hello captura de pantalla de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="c5f9f-124">Visualización de los detalles del disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="c5f9f-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="c5f9f-125">Para poder adjuntar su tooanother de disco duro virtual, necesita tooidentify Hola nombre de disco duro virtual (VHD) de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="c5f9f-126">Seleccione el grupo de recursos desde el portal de hello, a continuación, seleccione la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="c5f9f-127">Haga clic en **Blobs**, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-127">Click **Blobs**, as in hello following example:</span></span>

![Selección de blobs de almacenamiento](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="c5f9f-129">Normalmente, suele tener un contenedor denominado **vhds** que almacena los discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="c5f9f-130">Seleccione el contenedor de hello tooview una lista de discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="c5f9f-131">Nombre de Hola de nota de su disco duro virtual (prefijo Hola suele Hola nombre de la máquina virtual):</span><span class="sxs-lookup"><span data-stu-id="c5f9f-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Identificación del disco duro virtual en el contenedor de almacenamiento](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="c5f9f-133">Seleccione el disco duro virtual existente de la lista de Hola y copiar dirección URL de Hola para su uso en hello pasos:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Copia de la dirección URL del disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="c5f9f-135">Eliminación de la VM existente</span><span class="sxs-lookup"><span data-stu-id="c5f9f-135">Delete existing VM</span></span>
<span data-ttu-id="c5f9f-136">Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="c5f9f-137">Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="c5f9f-138">Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="c5f9f-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="c5f9f-139">Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="c5f9f-140">Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="c5f9f-141">concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="c5f9f-142">Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="c5f9f-143">Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="c5f9f-144">Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="c5f9f-145">Seleccione la máquina virtual en el portal de hello, a continuación, haga clic en **eliminar**:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-145">Select your VM in hello portal, then click **Delete**:</span></span>

![Captura de pantalla de diagnósticos de arranque de máquina virtual que muestran un error de arranque](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="c5f9f-147">Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="c5f9f-148">concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="c5f9f-149">Adjuntar tooanother de disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="c5f9f-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="c5f9f-150">Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="c5f9f-151">Adjuntar toothis Hola de disco duro virtual existente toobrowse capaz de VM toobe de solución de problemas y editar el contenido del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="c5f9f-152">Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="c5f9f-153">Elija o cree otro toouse de máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="c5f9f-154">Seleccione el grupo de recursos desde el portal de hello, a continuación, seleccione la máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="c5f9f-155">Seleccione **Discos** y, a continuación, haga clic en **Conectar existente**:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Adjuntar disco existente en el portal de Hola](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="c5f9f-157">tooselect su disco duro virtual existente, haga clic en **archivo VHD**:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Busque el disco duro virtual existente.](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="c5f9f-159">Seleccione la cuenta de almacenamiento y el contenedor y, a continuación, haga clic en el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="c5f9f-160">Haga clic en hello **seleccione** botón tooconfirm su elección:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Seleccione el disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="c5f9f-162">Con un VHD ahora seleccionado, haga clic en **Aceptar** tooattach Hola disco duro virtual existente:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Confirmación de la conexión del disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="c5f9f-164">Después de unos segundos, Hola **discos** panel para la máquina virtual muestra el disco duro virtual existente conectado como disco de datos:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disco duro virtual existente conectado como disco de datos](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="c5f9f-166">Montar el disco de datos adjuntos de Hola</span><span class="sxs-lookup"><span data-stu-id="c5f9f-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="c5f9f-167">Hello en los ejemplos siguientes detallan los pasos de hello necesarios en una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="c5f9f-168">Si usas una distribución de Linux diferentes, por ejemplo, Red Hat Enterprise Linux o SUSE, ubicaciones de archivos de registro de hello y `mount` comandos pueden ser ligeramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="c5f9f-169">Consulte la documentación de toohello para su distribución específica para los cambios adecuados de hello en comandos.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="c5f9f-170">SSH tooyour de solución de problemas de máquina virtual con las credenciales adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="c5f9f-171">Si este disco es Hola primera datos disco conectado tooyour solución de problemas de máquina virtual, es probable que está conectado demasiado`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="c5f9f-172">Use `dmseg` toolist discos conectados:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="c5f9f-173">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="c5f9f-174">En el anterior ejemplo de Hola, disco de hello SO está en `/dev/sda` y proporcionadas para cada máquina virtual está en el disco temporal hello `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="c5f9f-175">Si hubiera varios discos de datos, deben estar en `/dev/sdd`, `/dev/sde`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="c5f9f-176">Cree un directorio toomount el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="c5f9f-177">Hello en el ejemplo siguiente se crea un directorio denominado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="c5f9f-178">Si tiene varias particiones en el disco duro virtual existente, monte partición Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="c5f9f-179">Hello en el ejemplo siguiente se monta primera partición primaria hello en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="c5f9f-180">Procedimiento recomendado es toomount discos de datos en máquinas virtuales en Azure mediante Hola identificador único universal (UUID) de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="c5f9f-181">En este escenario de solución de problemas corto, el montaje Hola disco duro con hello UUID no es necesario.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="c5f9f-182">Sin embargo, en condiciones normales, edición `/etc/fstab` discos duros virtuales toomount mediante el nombre de dispositivo en lugar de UUID puede provocar Hola VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="c5f9f-183">Solución de problemas en el disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="c5f9f-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="c5f9f-184">Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="c5f9f-185">Una vez que se ha solucionado problemas hello, continúe con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="c5f9f-186">Desmontaje y desconexión del disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="c5f9f-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="c5f9f-187">Una vez que se resuelven los errores, desconecte el disco duro virtual existente del saludo de la máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="c5f9f-188">No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="c5f9f-189">De tooyour de sesión SSH de hello VM de solución de problemas, desmonte hello: disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="c5f9f-190">Cambie primero fuera del directorio principal de hello para el punto de montaje:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="c5f9f-191">Desmonte ahora hello: disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="c5f9f-192">Hello en el ejemplo siguiente se desmonta dispositivo hello en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="c5f9f-193">Ahora separar Hola de disco duro virtual de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="c5f9f-194">Seleccione la máquina virtual en el portal de Hola y haga clic en **discos**.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="c5f9f-195">Seleccione el disco duro virtual existente y, a continuación, haga clic en **Desasociar**:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Desconecte el disco duro virtual existente](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="c5f9f-197">Espere hasta que Hola VM desconectó correctamente el disco de datos de hello antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="c5f9f-198">Creación de máquina virtual a partir del disco duro original</span><span class="sxs-lookup"><span data-stu-id="c5f9f-198">Create VM from original hard disk</span></span>
<span data-ttu-id="c5f9f-199">usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c5f9f-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="c5f9f-200">plantilla de Hello implementa una máquina virtual en una red virtual existente, mediante Hola dirección URL del VHD de hello comando anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="c5f9f-201">Haga clic en hello **implementar tooAzure** botón como sigue:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Implementación de máquina virtual desde una plantilla de GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="c5f9f-203">plantilla de Hola se carga en hello portal de Azure para la implementación.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="c5f9f-204">Especificar nombres de hello para la nueva máquina virtual y los recursos de Azure existentes y pegue Hola URL tooyour disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="c5f9f-205">implementación de hello toobegin, haga clic en **compra**:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-205">toobegin hello deployment, click **Purchase**:</span></span>

![Implementación de una máquina virtual a partir de una plantilla](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="c5f9f-207">Rehabilitación de los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="c5f9f-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="c5f9f-208">Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="c5f9f-209">toocheck Hola estado de diagnóstico de arranque y activar si es necesario, seleccione la máquina virtual en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="c5f9f-210">En **Supervisión**, haga clic en **Configuración de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="c5f9f-211">Asegúrese de estado de hello es **en**, y Hola marca de verificación junto a demasiado**diagnósticos de arranque** está seleccionada.</span><span class="sxs-lookup"><span data-stu-id="c5f9f-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="c5f9f-212">Si realiza cambios, haga clic en **Guardar**:</span><span class="sxs-lookup"><span data-stu-id="c5f9f-212">If you make any changes, click **Save**:</span></span>

![Actualización de la configuración de los diagnósticos de arranque](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="c5f9f-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5f9f-214">Next steps</span></span>
<span data-ttu-id="c5f9f-215">Si tiene problemas para conectarse tooyour VM, consulte [solucionar problemas de SSH conexiones tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5f9f-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c5f9f-216">Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual de Linux en Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5f9f-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c5f9f-217">Para más información sobre el uso de Resource Manager, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c5f9f-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
