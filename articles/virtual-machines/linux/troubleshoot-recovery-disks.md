---
title: "Uso de una máquina virtual Linux de solución de problemas con la CLI de Azure 2.0 | Microsoft Docs"
description: "Aprenda a solucionar problemas de la máquina virtual Linux mediante la conexión del disco del sistema operativo a una máquina virtual de recuperación mediante la CLI de Azure 2.0"
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
ms.openlocfilehash: 7a28accce1bd328b2b486b588c44d91b03e42122
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-with-the-azure-cli-20"></a><span data-ttu-id="e7862-103">Solución de problemas de una máquina virtual Linux mediante la conexión del disco del sistema operativo a una máquina virtual de recuperación mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="e7862-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="e7862-104">Si la máquina virtual Linux se encuentra un error de disco o de arranque, deberá realizar los pasos para solucionar problemas en el propio disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="e7862-105">Un ejemplo habitual sería una entrada no válida en `/etc/fstab` que impide que la máquina virtual se pueda arrancar correctamente.</span><span class="sxs-lookup"><span data-stu-id="e7862-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="e7862-106">En este artículo se detalla cómo utilizar la CLI de Azure 2.0 para conectar el disco duro virtual a otra máquina virtual Linux para solucionar los errores y, posteriormente, volver a crear la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="e7862-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span> <span data-ttu-id="e7862-107">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7862-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="e7862-108">Introducción al proceso de recuperación</span><span class="sxs-lookup"><span data-stu-id="e7862-108">Recovery process overview</span></span>
<span data-ttu-id="e7862-109">El proceso de solución de problemas es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7862-109">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e7862-110">Elimine la máquina virtual que tiene problemas, conservando los discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="e7862-110">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="e7862-111">Conecte y monte el disco duro virtual en otra máquina virtual Linux con el fin de solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e7862-112">Conéctese a la máquina virtual de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-112">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="e7862-113">Edite los archivos o ejecute cualquier herramienta necesaria para solucionar los problemas del disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="e7862-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="e7862-114">Desmonte y desconecte el disco duro virtual de la máquina virtual de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="e7862-115">Cree una máquina virtual mediante el disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="e7862-115">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="e7862-116">Para realizar estos pasos para la solución de problemas, es preciso tener instalada la [CLI de Azure 2.0](/cli/azure/install-az-cli2) más reciente y haber iniciado sesión en una cuenta de Azure mediante [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e7862-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e7862-117">En los ejemplos siguientes, reemplace los nombres de parámetros por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="e7862-117">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="e7862-118">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e7862-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e7862-119">Determinación de los problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="e7862-119">Determine boot issues</span></span>
<span data-ttu-id="e7862-120">Examine la salida de serie para determinar por qué la máquina virtual no es capaz de arrancar correctamente.</span><span class="sxs-lookup"><span data-stu-id="e7862-120">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="e7862-121">Un ejemplo habitual es una entrada no válida en `/etc/fstab` o el disco duro virtual subyacente que se va a eliminar o mover.</span><span class="sxs-lookup"><span data-stu-id="e7862-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e7862-122">Obtenga los registros de arranque con [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="e7862-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="e7862-123">En el ejemplo siguiente se obtiene la salida de serie de la máquina virtual llamada `myVM` en el grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e7862-124">Revise la salida de serie para determinar por qué la máquina virtual no arranca correctamente.</span><span class="sxs-lookup"><span data-stu-id="e7862-124">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="e7862-125">Si la salida de serie no proporciona ninguna indicación, debe revisar los archivos de registro en `/var/log` una vez que tenga el disco duro virtual conectado a una máquina virtual de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e7862-126">Visualización de los detalles del disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="e7862-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="e7862-127">Para poder conectar el disco duro virtual (VHD) a otra máquina virtual, es preciso que identifique el identificador URI del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e7862-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span></span> 

<span data-ttu-id="e7862-128">Vea información acerca de la máquina virtual con [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="e7862-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="e7862-129">Use la marca `--query` para extraer el identificador URI al disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e7862-129">Use the `--query` flag to extract the URI to the OS disk.</span></span> <span data-ttu-id="e7862-130">En el ejemplo siguiente se obtiene información de los discos de la máquina virtual denominada `myVM` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="e7862-131">El identificador URI es similar a **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="e7862-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="e7862-132">Eliminación de la VM existente</span><span class="sxs-lookup"><span data-stu-id="e7862-132">Delete existing VM</span></span>
<span data-ttu-id="e7862-133">Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7862-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e7862-134">Un disco duro virtual es el recurso donde se almacenan el propio sistema operativo, las aplicaciones y las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="e7862-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e7862-135">La propia máquina virtual consiste solo en metadatos que definen el tamaño o la ubicación y hace referencia a recursos como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="e7862-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e7862-136">Cada disco duro virtual tiene una concesión que se asigna cuando se conecta a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-136">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="e7862-137">Aunque los discos de datos se pueden conectar y desconectar incluso mientras se está ejecutando la máquina virtual, no se puede desasociar el disco del sistema operativo, a menos que se elimine el recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="e7862-138">La concesión continúa para asociar el disco del sistema operativo a una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.</span><span class="sxs-lookup"><span data-stu-id="e7862-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e7862-139">El primer paso para recuperar la máquina virtual es eliminar el propio recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-139">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="e7862-140">Al eliminar la máquina virtual, los discos duros virtuales se dejan en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e7862-140">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="e7862-141">Después de eliminar la máquina virtual, conecte el disco duro virtual a otra máquina virtual para localizar y solucionar los errores.</span><span class="sxs-lookup"><span data-stu-id="e7862-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="e7862-142">Elimine la máquina virtual con [az vm delete](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="e7862-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="e7862-143">En el ejemplo siguiente se elimina la máquina virtual llamada `myVM` del grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="e7862-144">Espere hasta que la máquina virtual haya terminado la eliminación antes de conectar el disco duro virtual a otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="e7862-145">La concesión en el disco duro virtual que lo asocia a la máquina virtual debe liberarse antes de poder conectar el disco duro virtual a otra máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="e7862-146">Conexión del disco duro virtual existente a otra máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e7862-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="e7862-147">Para los pasos siguientes, se usa otra máquina virtual con el fin de solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e7862-148">Conecte el disco duro virtual existente a esta máquina virtual de solución de problemas para examinar y modificar el contenido del disco.</span><span class="sxs-lookup"><span data-stu-id="e7862-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="e7862-149">Por ejemplo, este proceso le permite corregir todos los errores de configuración o revisar archivos de registro adicionales de la aplicación o sistema.</span><span class="sxs-lookup"><span data-stu-id="e7862-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e7862-150">Elija o cree otra máquina virtual que se usará con fines de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="e7862-151">Conecte el disco duro virtual existente con [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="e7862-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="e7862-152">Cuando conecte el disco duro virtual existente, especifique el identificador URI en el disco obtenido en el comando `az vm show` anterior.</span><span class="sxs-lookup"><span data-stu-id="e7862-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span></span> <span data-ttu-id="e7862-153">En el ejemplo siguiente se conecta un disco duro virtual existente a la máquina virtual de solución de problemas con el nombre `myVMRecovery` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="e7862-154">Montaje del disco de datos conectado</span><span class="sxs-lookup"><span data-stu-id="e7862-154">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="e7862-155">Los siguientes ejemplos detallan los pasos necesarios en una máquina virtual Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e7862-155">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="e7862-156">Si usas una distribución de Linux diferente como Red Hat Enterprise Linux o SUSE, el registro de ubicaciones del archivo de registro y los comandos `mount` pueden ser ligeramente diferentes.</span><span class="sxs-lookup"><span data-stu-id="e7862-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="e7862-157">Consulte la documentación para su distribución específica para los cambios apropiados en los comandos.</span><span class="sxs-lookup"><span data-stu-id="e7862-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="e7862-158">SSH en la máquina virtual de solución de problemas con las credenciales apropiadas.</span><span class="sxs-lookup"><span data-stu-id="e7862-158">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="e7862-159">Si este disco es el primer disco de datos conectado a la máquina virtual de solución de problemas, es probable que el disco se conecte a `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="e7862-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="e7862-160">Use `dmseg` para ver los discos conectados:</span><span class="sxs-lookup"><span data-stu-id="e7862-160">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="e7862-161">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e7862-161">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="e7862-162">En el ejemplo anterior, el disco del sistema operativo está en `/dev/sda` y el disco temporal que se proporciona para cada máquina virtual está en `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="e7862-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="e7862-163">Si hubiera varios discos de datos, deben estar en `/dev/sdd`, `/dev/sde`, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="e7862-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="e7862-164">Cree un directorio para montar el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="e7862-164">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="e7862-165">El ejemplo siguiente permite crear un directorio llamado `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="e7862-165">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="e7862-166">Si tiene varias particiones en el disco duro virtual existente, monte la partición requerida.</span><span class="sxs-lookup"><span data-stu-id="e7862-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="e7862-167">En el ejemplo siguiente, se monta la primera partición principal en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e7862-167">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="e7862-168">El procedimiento recomendado consiste en montar los discos de datos en máquinas virtuales en Azure con el identificador único universal (UUID) del disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="e7862-169">En este breve escenario de solución de problemas, no es necesario montar el disco duro virtual con el UUID.</span><span class="sxs-lookup"><span data-stu-id="e7862-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="e7862-170">Sin embargo, en circunstancias normales, editar `/etc/fstab` para montar los discos duros virtuales mediante el nombre de dispositivo en lugar del UUID puede provocar que la máquina virtual no se pueda arrancar.</span><span class="sxs-lookup"><span data-stu-id="e7862-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e7862-171">Solución de problemas en el disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="e7862-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e7862-172">Con el disco duro virtual existente montado, ahora puede realizar todos los pasos de mantenimiento y solución de problemas según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e7862-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e7862-173">Una vez que se han resuelto los problemas, continúe con los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="e7862-173">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e7862-174">Desmontaje y desconexión del disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="e7862-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e7862-175">Una vez resueltos los errores, desmonte y desconecte el disco duro virtual existente de la máquina virtual de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e7862-176">No se podrá usar el disco duro virtual en ninguna otra máquina virtual hasta que se libere la concesión que conecta el disco duro virtual a la máquina virtual de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e7862-177">Desde la sesión SSH a la máquina virtual de solución de problemas, desmonte el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="e7862-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="e7862-178">Cambie primero el directorio primario del punto de montaje:</span><span class="sxs-lookup"><span data-stu-id="e7862-178">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="e7862-179">Ahora, desmonte el disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="e7862-179">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="e7862-180">El siguiente ejemplo desmonta el dispositivo en `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e7862-180">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="e7862-181">Ahora, desconecte el disco duro virtual de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e7862-181">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="e7862-182">Salga de la sesión SSH a la máquina virtual de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="e7862-182">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="e7862-183">Enumere los discos de datos conectados a la máquina virtual de solución de problemas con [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="e7862-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="e7862-184">En el ejemplo siguiente se muestran los discos de datos conectados a la máquina virtual denominada `myVMRecovery` en el grupo de recursos denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="e7862-185">Anote el nombre del disco duro virtual existente.</span><span class="sxs-lookup"><span data-stu-id="e7862-185">Note the name for your existing virtual hard disk.</span></span> <span data-ttu-id="e7862-186">Por ejemplo, el nombre de un disco con el identificador URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** es **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="e7862-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="e7862-187">Desconecte el disco de datos de la máquina virtual [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="e7862-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="e7862-188">En el ejemplo siguiente se desconecta el disco llamado `myVHD` de la máquina virtual llamada `myVMRecovery` del grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e7862-189">Creación de máquina virtual a partir del disco duro original</span><span class="sxs-lookup"><span data-stu-id="e7862-189">Create VM from original hard disk</span></span>
<span data-ttu-id="e7862-190">Para crear una máquina virtual a partir del disco duro virtual original, utilice [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="e7862-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="e7862-191">La plantilla JSON real está en el siguiente vínculo:</span><span class="sxs-lookup"><span data-stu-id="e7862-191">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="e7862-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="e7862-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="e7862-193">La plantilla implementa una máquina virtual mediante el identificador URI del VHD del comando anterior.</span><span class="sxs-lookup"><span data-stu-id="e7862-193">The template deploys a VM using the VHD URI from the earlier command.</span></span> <span data-ttu-id="e7862-194">Implemente la plantilla con [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="e7862-194">Deploy the template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="e7862-195">Especifique el identificador URI en el VHD original y, después, especifique tanto el tipo de sistema operativo, como el tamaño y nombre de la máquina virtual como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="e7862-195">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e7862-196">Rehabilitación de los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="e7862-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="e7862-197">Cuando se crea la máquina virtual desde el disco duro virtual existente, puede que no se habilite automáticamente el diagnóstico de arranque.</span><span class="sxs-lookup"><span data-stu-id="e7862-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e7862-198">Habilite el diagnóstico de arranque con [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="e7862-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="e7862-199">En el ejemplo siguiente se habilita la extensión de diagnóstico en la máquina virtual denominada `myDeployedVM` en el grupo de recursos `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e7862-199">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="e7862-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7862-200">Next steps</span></span>
<span data-ttu-id="e7862-201">Si tiene problemas para conectarse a la máquina virtual, consulte [Solución de problemas de conexiones SSH a una máquina virtual Linux de Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7862-201">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e7862-202">Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual de Linux en Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7862-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>