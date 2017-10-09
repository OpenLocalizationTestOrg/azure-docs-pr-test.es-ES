---
title: "aaaUse una solución de problemas de VM con hello Azure CLI 2.0 de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot VM de Linux que se emite por conexión Hola SO disco tooa recuperación VM mediante Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="f79db-103">Solucionar problemas de una VM Linux adjuntando Hola SO disco tooa máquina virtual de recuperación con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f79db-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="f79db-104">Si la máquina virtual (VM) de Linux se encuentra un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="f79db-105">Un ejemplo común sería una entrada no válida en `/etc/fstab` que impide Hola VM pueda tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="f79db-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="f79db-106">Este artículo se detallan cómo toouse Hola CLI de Azure 2.0 tooconnect su virtual rígida tooanother toofix de VM de Linux en disco los errores, a continuación, volver a crea la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="f79db-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="f79db-107">También puede realizar estos pasos con hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f79db-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="f79db-108">Introducción al proceso de recuperación</span><span class="sxs-lookup"><span data-stu-id="f79db-108">Recovery process overview</span></span>
<span data-ttu-id="f79db-109">proceso de solución de problemas de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="f79db-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="f79db-110">Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="f79db-111">Adjuntar y montar tooanother de disco duro virtual de hello VM de Linux para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="f79db-112">Conectar toohello solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="f79db-113">Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="f79db-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="f79db-114">Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="f79db-115">Crear una máquina virtual mediante hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="f79db-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="f79db-116">tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f79db-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f79db-117">En hello en los ejemplos siguientes, reemplace los nombres de parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="f79db-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="f79db-118">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="f79db-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="f79db-119">Determinación de los problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="f79db-119">Determine boot issues</span></span>
<span data-ttu-id="f79db-120">Examine Hola salida serie toodetermine ¿por qué la máquina virtual no es capaz de tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="f79db-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="f79db-121">Un ejemplo común es una entrada válida en `/etc/fstab`, u Hola subyacente de disco duro virtual que se va a eliminar o mover.</span><span class="sxs-lookup"><span data-stu-id="f79db-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="f79db-122">Obtener registros de arranque de hello con [diagnóstico de arranque de vm az get-arranque-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="f79db-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="f79db-123">Hello en el ejemplo siguiente se obtiene Hola serie resultado Hola máquina virtual denominada `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f79db-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f79db-124">Revise Hola salida serie toodetermine ¿por qué hello VM está fallando tooboot.</span><span class="sxs-lookup"><span data-stu-id="f79db-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="f79db-125">Si salida serie hello no proporciona ninguna indicación, puede que tenga archivos de registro de tooreview en `/var/log` una vez que tenga Hola virtual disco duro conectado tooa solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="f79db-126">Visualización de los detalles del disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="f79db-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="f79db-127">Antes de que puede asociar la máquina virtual de tooanother de disco duro virtual (VHD), debe tooidentify Hola URI de disco del sistema operativo Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="f79db-128">Vea información acerca de la máquina virtual con [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="f79db-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="f79db-129">Hola de uso `--query` el disco toohello OS URI de marca tooextract Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="f79db-130">Hello en el ejemplo siguiente se obtiene información de disco para la máquina virtual denominada hello `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f79db-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="f79db-131">Hola URI es similar demasiado**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="f79db-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="f79db-132">Eliminación de la VM existente</span><span class="sxs-lookup"><span data-stu-id="f79db-132">Delete existing VM</span></span>
<span data-ttu-id="f79db-133">Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="f79db-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="f79db-134">Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="f79db-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="f79db-135">Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="f79db-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="f79db-136">Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="f79db-137">Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="f79db-138">concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.</span><span class="sxs-lookup"><span data-stu-id="f79db-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="f79db-139">Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio.</span><span class="sxs-lookup"><span data-stu-id="f79db-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="f79db-140">Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f79db-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="f79db-141">Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="f79db-142">Eliminar Hola VM con [eliminar vm az](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="f79db-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="f79db-143">Después de eliminaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` del grupo de recursos de hello denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f79db-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="f79db-144">Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="f79db-145">concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="f79db-146">Adjuntar tooanother de disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="f79db-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="f79db-147">Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="f79db-148">Adjuntar toothis Hola de disco duro virtual existente toobrowse VM de solución de problemas y editar el contenido del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="f79db-149">Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f79db-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="f79db-150">Elija o cree otro toouse de máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="f79db-151">Conectar disco duro virtual existente del Hola con [adjuntar az vm no administrada de disco](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="f79db-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="f79db-152">Cuando conecte un disco de duro virtual existente hello, especifique disco toohello Hola URI que obtuvo en hello anterior `az vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="f79db-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="f79db-153">Hello en el ejemplo siguiente se asocia un toohello de disco duro virtual existente solución de problemas de máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f79db-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="f79db-154">Montar el disco de datos adjuntos de Hola</span><span class="sxs-lookup"><span data-stu-id="f79db-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="f79db-155">Hello en los ejemplos siguientes detallan los pasos de hello necesarios en una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f79db-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="f79db-156">Si usas una distribución de Linux diferentes, por ejemplo, Red Hat Enterprise Linux o SUSE, ubicaciones de archivos de registro de hello y `mount` comandos pueden ser ligeramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="f79db-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="f79db-157">Consulte la documentación de toohello para su distribución específica para los cambios adecuados de hello en comandos.</span><span class="sxs-lookup"><span data-stu-id="f79db-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="f79db-158">SSH tooyour de solución de problemas de máquina virtual con las credenciales adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="f79db-159">Si este disco es Hola primera datos disco conectado tooyour solución de problemas de máquina virtual, es probable que está conectado a disco Hola demasiado`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="f79db-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="f79db-160">Use `dmseg` tooview discos conectados:</span><span class="sxs-lookup"><span data-stu-id="f79db-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="f79db-161">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f79db-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="f79db-162">En el anterior ejemplo de Hola, disco de hello SO está en `/dev/sda` y proporcionadas para cada máquina virtual está en el disco temporal hello `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="f79db-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="f79db-163">Si hubiera varios discos de datos, deben estar en `/dev/sdd`, `/dev/sde`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="f79db-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="f79db-164">Cree un directorio toomount el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f79db-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="f79db-165">Hello en el ejemplo siguiente se crea un directorio denominado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="f79db-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="f79db-166">Si tiene varias particiones en el disco duro virtual existente, monte partición Hola necesario.</span><span class="sxs-lookup"><span data-stu-id="f79db-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="f79db-167">Hello en el ejemplo siguiente se monta primera partición primaria hello en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f79db-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="f79db-168">Procedimiento recomendado es toomount discos de datos en máquinas virtuales en Azure mediante Hola identificador único universal (UUID) de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="f79db-169">En este escenario de solución de problemas corto, el montaje Hola disco duro con hello UUID no es necesario.</span><span class="sxs-lookup"><span data-stu-id="f79db-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="f79db-170">Sin embargo, en condiciones normales, edición `/etc/fstab` discos duros virtuales toomount mediante el nombre de dispositivo en lugar de UUID puede provocar Hola VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="f79db-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="f79db-171">Solución de problemas en el disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="f79db-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="f79db-172">Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f79db-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="f79db-173">Una vez que se ha solucionado problemas hello, continúe con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="f79db-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="f79db-174">Desmontaje y desconexión del disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="f79db-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="f79db-175">Una vez que se resuelven los errores, desmonta y separar hello: disco duro virtual existente de la máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="f79db-176">No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="f79db-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="f79db-177">De tooyour de sesión SSH de hello VM de solución de problemas, desmonte hello: disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f79db-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="f79db-178">Cambie primero fuera del directorio principal de hello para el punto de montaje:</span><span class="sxs-lookup"><span data-stu-id="f79db-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="f79db-179">Desmonte ahora hello: disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f79db-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="f79db-180">Hello en el ejemplo siguiente se desmonta dispositivo hello en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f79db-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="f79db-181">Ahora separar Hola de disco duro virtual de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="f79db-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="f79db-182">Salga de hello SSH sesión tooyour solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f79db-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="f79db-183">Hola lista adjunta datos discos tooyour solución de problemas de máquina virtual con [lista de discos no administrada de vm de az](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="f79db-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="f79db-184">el ejemplo siguiente se enumeran Hola discos de datos Hello adjunta toohello máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f79db-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="f79db-185">Anote el nombre de hello para el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="f79db-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="f79db-186">Por ejemplo, nombre de Hola de un disco con Hola URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** es **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="f79db-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="f79db-187">Desconectar el disco de datos de hello de la máquina virtual [separar az vm no administrada de disco](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="f79db-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="f79db-188">Hello en el ejemplo siguiente se separa con el nombre de disco de hello `myVHD` de máquina virtual denominada hello `myVMRecovery` en hello `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="f79db-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="f79db-189">Creación de máquina virtual a partir del disco duro original</span><span class="sxs-lookup"><span data-stu-id="f79db-189">Create VM from original hard disk</span></span>
<span data-ttu-id="f79db-190">usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="f79db-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="f79db-191">plantilla JSON real de Hello está en hello siguiente vínculo:</span><span class="sxs-lookup"><span data-stu-id="f79db-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="f79db-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f79db-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="f79db-193">plantilla Hello implementa una máquina virtual mediante Hola URI de VHD de hello comando anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f79db-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="f79db-194">Implementar la plantilla de hello con [Crear implementación de grupo az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="f79db-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="f79db-195">Proporcionar Hola URI tooyour VHD original y, a continuación, especifique Hola SO tipo, tamaño de máquina virtual y nombre de máquina virtual como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f79db-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="f79db-196">Rehabilitación de los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="f79db-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="f79db-197">Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f79db-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="f79db-198">Habilite el diagnóstico de arranque con [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="f79db-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="f79db-199">Hello en el ejemplo siguiente se habilita extensión de diagnóstico de hello en hello máquina virtual denominada `myDeployedVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f79db-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="f79db-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f79db-200">Next steps</span></span>
<span data-ttu-id="f79db-201">Si tiene problemas para conectarse tooyour VM, consulte [solucionar problemas de SSH conexiones tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f79db-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f79db-202">Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual de Linux en Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f79db-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
