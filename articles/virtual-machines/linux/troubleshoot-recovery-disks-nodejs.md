---
title: "aaaUse una solución de problemas de VM con hello Azure CLI 1.0 de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot VM de Linux que se emite por conexión Hola SO disco tooa recuperación VM mediante Hola 1.0 de CLI de Azure"
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
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="f292e-103">Solucionar problemas de una VM de Linux mediante la asociación de la máquina virtual de recuperación de tooa del disco de hello SO utilizando Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f292e-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="f292e-104">Si la máquina virtual (VM) de Linux se encuentra un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="f292e-105">Un ejemplo común sería una entrada no válida en `/etc/fstab` que impide Hola VM pueda tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="f292e-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="f292e-106">Este artículo se detallan cómo toouse hello Azure CLI 1.0 tooconnect su virtual rígida tooanother toofix de VM de Linux en disco los errores, a continuación, volver a crea la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="f292e-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f292e-107">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="f292e-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f292e-108">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="f292e-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="f292e-109">[Azure 1.0 de CLI](#recovery-process-overview) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="f292e-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f292e-110">[Azure 2.0 CLI](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="f292e-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="f292e-111">Introducción al proceso de recuperación</span><span class="sxs-lookup"><span data-stu-id="f292e-111">Recovery process overview</span></span>
<span data-ttu-id="f292e-112">proceso de solución de problemas de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="f292e-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="f292e-113">Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="f292e-114">Adjuntar y montar tooanother de disco duro virtual de hello VM de Linux para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="f292e-115">Conectar toohello solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="f292e-116">Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="f292e-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="f292e-117">Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="f292e-118">Crear una máquina virtual mediante hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="f292e-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="f292e-119">Asegúrese de que dispone de [Hola 1.0 de CLI de Azure más reciente](../../cli-install-nodejs.md) instalado y registrado en y lo utiliza el modo de administrador de recursos:</span><span class="sxs-lookup"><span data-stu-id="f292e-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="f292e-120">En hello en los ejemplos siguientes, reemplace los nombres de parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f292e-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="f292e-121">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="f292e-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="f292e-122">Determinación de los problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="f292e-122">Determine boot issues</span></span>
<span data-ttu-id="f292e-123">Examine Hola salida serie toodetermine ¿por qué la máquina virtual no es capaz de tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="f292e-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="f292e-124">Un ejemplo común es una entrada válida en `/etc/fstab`, u Hola subyacente de disco duro virtual que se va a eliminar o mover.</span><span class="sxs-lookup"><span data-stu-id="f292e-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="f292e-125">Hello en el ejemplo siguiente se obtiene Hola serie resultado Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f292e-126">Revise Hola salida serie toodetermine ¿por qué hello VM está fallando tooboot.</span><span class="sxs-lookup"><span data-stu-id="f292e-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="f292e-127">Si salida serie hello no proporciona ninguna indicación, puede que tenga archivos de registro de tooreview en `/var/log` una vez que tenga Hola virtual disco duro conectado tooa solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="f292e-128">Visualización de los detalles del disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="f292e-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="f292e-129">Para poder adjuntar su tooanother de disco duro virtual, necesita tooidentify Hola nombre de disco duro virtual (VHD) de Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="f292e-130">Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f292e-131">Busque `Vhd URI` en la salida de hello de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="f292e-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="f292e-132">siguiente salida de ejemplo truncados Hello muestra hello `Vhd URI` en la última línea de hello:</span><span class="sxs-lookup"><span data-stu-id="f292e-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="f292e-133">Eliminación de la VM existente</span><span class="sxs-lookup"><span data-stu-id="f292e-133">Delete existing VM</span></span>
<span data-ttu-id="f292e-134">Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="f292e-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="f292e-135">Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="f292e-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="f292e-136">Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="f292e-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="f292e-137">Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="f292e-138">Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="f292e-139">concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.</span><span class="sxs-lookup"><span data-stu-id="f292e-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="f292e-140">Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio.</span><span class="sxs-lookup"><span data-stu-id="f292e-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="f292e-141">Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f292e-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="f292e-142">Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="f292e-143">Después de eliminaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` del grupo de recursos de hello denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="f292e-144">Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="f292e-145">concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="f292e-146">Adjuntar tooanother de disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="f292e-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="f292e-147">Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="f292e-148">Adjuntar toothis Hola de disco duro virtual existente toobrowse VM de solución de problemas y editar el contenido del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="f292e-149">Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f292e-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="f292e-150">Elija o cree otro toouse de máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="f292e-151">Al adjuntar hello: disco duro virtual existente, especifique el disco de toohello de dirección URL de hello obtenido en hello anterior `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="f292e-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="f292e-152">Hello en el ejemplo siguiente se asocia un toohello de disco duro virtual existente solución de problemas de máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="f292e-153">Montar el disco de datos adjuntos de Hola</span><span class="sxs-lookup"><span data-stu-id="f292e-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="f292e-154">Hello en los ejemplos siguientes detallan los pasos de hello necesarios en una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f292e-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="f292e-155">Si usas una distribución de Linux diferentes, por ejemplo, Red Hat Enterprise Linux o SUSE, ubicaciones de archivos de registro de hello y `mount` comandos pueden ser ligeramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="f292e-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="f292e-156">Consulte la documentación de toohello para su distribución específica para los cambios adecuados de hello en comandos.</span><span class="sxs-lookup"><span data-stu-id="f292e-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="f292e-157">SSH tooyour de solución de problemas de máquina virtual con las credenciales adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="f292e-158">Si este disco es Hola primera datos disco conectado tooyour solución de problemas de máquina virtual, es probable que está conectado a disco Hola demasiado`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="f292e-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="f292e-159">Use `dmseg` tooview discos conectados:</span><span class="sxs-lookup"><span data-stu-id="f292e-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="f292e-160">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f292e-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="f292e-161">En el anterior ejemplo de Hola, disco de hello SO está en `/dev/sda` y proporcionadas para cada máquina virtual está en el disco temporal hello `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="f292e-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="f292e-162">Si hubiera varios discos de datos, deben estar en `/dev/sdd`, `/dev/sde`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="f292e-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="f292e-163">Cree un directorio toomount el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f292e-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="f292e-164">Hello en el ejemplo siguiente se crea un directorio denominado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="f292e-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="f292e-165">Si tiene varias particiones en el disco duro virtual existente, monte partición Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="f292e-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="f292e-166">Hello en el ejemplo siguiente se monta primera partición primaria hello en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f292e-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="f292e-167">Procedimiento recomendado es toomount discos de datos en máquinas virtuales en Azure mediante Hola identificador único universal (UUID) de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="f292e-168">En este escenario de solución de problemas corto, el montaje Hola disco duro con hello UUID no es necesario.</span><span class="sxs-lookup"><span data-stu-id="f292e-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="f292e-169">Sin embargo, en condiciones normales, edición `/etc/fstab` discos duros virtuales toomount mediante el nombre de dispositivo en lugar de UUID puede provocar Hola VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="f292e-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="f292e-170">Solución de problemas en el disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="f292e-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="f292e-171">Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f292e-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="f292e-172">Una vez que se ha solucionado problemas hello, continúe con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="f292e-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="f292e-173">Desmontaje y desconexión del disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="f292e-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="f292e-174">Una vez que se resuelven los errores, desmonta y separar hello: disco duro virtual existente de la máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="f292e-175">No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="f292e-176">De tooyour de sesión SSH de hello VM de solución de problemas, desmonte hello: disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f292e-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="f292e-177">Cambie primero fuera del directorio principal de hello para el punto de montaje:</span><span class="sxs-lookup"><span data-stu-id="f292e-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="f292e-178">Desmonte ahora hello: disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f292e-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="f292e-179">Hello en el ejemplo siguiente se desmonta dispositivo hello en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f292e-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="f292e-180">Ahora separar Hola de disco duro virtual de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="f292e-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="f292e-181">Salga de hello SSH sesión tooyour solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f292e-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="f292e-182">Hola CLI de Azure, primer Hola lista adjunta tooyour de discos de datos VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="f292e-183">el ejemplo siguiente se enumeran Hola discos de datos Hello adjunta toohello máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="f292e-184">Hola Nota `Lun` valor para el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f292e-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="f292e-185">Hello resultado del comando de ejemplo siguiente muestra hello disco virtual conectado en el LUN 0:</span><span class="sxs-lookup"><span data-stu-id="f292e-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="f292e-186">Desconectar el disco de datos de hello de la máquina virtual con hello aplicable `Lun` valor:</span><span class="sxs-lookup"><span data-stu-id="f292e-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="f292e-187">Creación de máquina virtual a partir del disco duro original</span><span class="sxs-lookup"><span data-stu-id="f292e-187">Create VM from original hard disk</span></span>
<span data-ttu-id="f292e-188">usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="f292e-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="f292e-189">plantilla JSON real de Hello está en hello siguiente vínculo:</span><span class="sxs-lookup"><span data-stu-id="f292e-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="f292e-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f292e-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="f292e-191">plantilla de Hello implementa una máquina virtual en una red virtual existente, mediante Hola dirección URL del VHD de hello comando anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f292e-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="f292e-192">Hello en el ejemplo siguiente se implementa grupo de recursos de toohello Hola plantilla llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="f292e-193">Hola de respuesta solicita plantilla hello como nombre de máquina virtual (`myDeployedVM` Hola después ejemplo), tipo de sistema operativo (`Linux`) y el tamaño VM (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="f292e-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="f292e-194">Hola `osDiskVhdUri` es Hola mismo utiliza anteriormente al adjuntar toohello Hola de disco duro virtual existente VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="f292e-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="f292e-195">Un ejemplo de salida del comando hello y preguntar si se es como sigue:</span><span class="sxs-lookup"><span data-stu-id="f292e-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="f292e-196">Rehabilitación de los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="f292e-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="f292e-197">Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f292e-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="f292e-198">Hello en el ejemplo siguiente se habilita extensión de diagnóstico de hello en hello máquina virtual denominada `myDeployedVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f292e-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="f292e-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f292e-199">Next steps</span></span>
<span data-ttu-id="f292e-200">Si tiene problemas para conectarse tooyour VM, consulte [solucionar problemas de SSH conexiones tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f292e-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f292e-201">Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual de Linux en Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f292e-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
