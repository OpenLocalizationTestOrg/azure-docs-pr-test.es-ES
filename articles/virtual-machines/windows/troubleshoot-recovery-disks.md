---
title: "aaaUse una aplicación de Windows, solución de problemas de máquina virtual con PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo emite tootroubleshoot VM de Windows en Azure mediante la conexión de recuperación de tooa de disco de hello SO máquina virtual mediante PowerShell de Azure"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="2f50a-103">Solucionar problemas de una VM de Windows mediante una asociación recuperación tooa de disco Hola SO máquina virtual mediante PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="2f50a-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="2f50a-104">Si la máquina virtual de Windows (VM) en Azure detecta un error de disco o de arranque, debe tooperform pasos en el disco duro virtual Hola propio para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="2f50a-105">Un ejemplo común sería una actualización de la aplicación que ha fallado que impide que Hola VM se pueda tooboot correctamente.</span><span class="sxs-lookup"><span data-stu-id="2f50a-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="2f50a-106">Este artículo detalles de cómo toouse Azure PowerShell tooconnect su toofix de disco duro virtual tooanother VM de Windows los errores, a continuación, volver a crear la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="2f50a-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="2f50a-107">Introducción al proceso de recuperación</span><span class="sxs-lookup"><span data-stu-id="2f50a-107">Recovery process overview</span></span>
<span data-ttu-id="2f50a-108">proceso de solución de problemas de Hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="2f50a-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="2f50a-109">Eliminar Hola VM encontrar problemas, mantener los discos duros virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="2f50a-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="2f50a-110">Adjuntar y montar tooanother de disco duro virtual de hello VM de Windows para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="2f50a-111">Conectar toohello solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f50a-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="2f50a-112">Editar archivos o ejecute cualquier herramienta toofix problemas en hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="2f50a-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="2f50a-113">Desmonte y desconecte Hola de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="2f50a-114">Crear una máquina virtual mediante hello: disco duro virtual original.</span><span class="sxs-lookup"><span data-stu-id="2f50a-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="2f50a-115">Asegúrese de que dispone de [Hola más reciente de PowerShell de Azure](/powershell/azure/overview) instalado y registrado en tooyour suscripción:</span><span class="sxs-lookup"><span data-stu-id="2f50a-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="2f50a-116">En hello en los ejemplos siguientes, reemplace los nombres de parámetros con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="2f50a-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="2f50a-117">Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `mystorageaccount` y `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2f50a-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="2f50a-118">Determinación de los problemas de arranque</span><span class="sxs-lookup"><span data-stu-id="2f50a-118">Determine boot issues</span></span>
<span data-ttu-id="2f50a-119">Puede ver una captura de pantalla de la máquina virtual en Azure toohelp solucionar problemas de arranque.</span><span class="sxs-lookup"><span data-stu-id="2f50a-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="2f50a-120">Esta captura de pantalla puede ayudar a identificar por qué se produce un error en una máquina virtual tooboot.</span><span class="sxs-lookup"><span data-stu-id="2f50a-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="2f50a-121">Hello en el ejemplo siguiente se obtiene Hola captura de pantalla de máquina virtual de Windows denominada Hola `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f50a-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="2f50a-122">Revise toodetermine de captura de pantalla de hello ¿por qué no Hola VM puede tooboot.</span><span class="sxs-lookup"><span data-stu-id="2f50a-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="2f50a-123">Tenga en cuenta todos los mensajes de error o códigos de error específicos proporcionados.</span><span class="sxs-lookup"><span data-stu-id="2f50a-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="2f50a-124">Visualización de los detalles del disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="2f50a-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="2f50a-125">Para poder adjuntar su tooanother de disco duro virtual, necesita tooidentify Hola nombre de disco duro virtual (VHD) de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f50a-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="2f50a-126">Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello `myVM` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f50a-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="2f50a-127">Busque `Vhd URI` en hello `StorageProfile` sección de salida de hello de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="2f50a-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="2f50a-128">siguiente salida de ejemplo truncados Hello muestra hello `Vhd URI` hacia el final de Hola Hola del bloque de código:</span><span class="sxs-lookup"><span data-stu-id="2f50a-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="2f50a-129">Eliminación de la VM existente</span><span class="sxs-lookup"><span data-stu-id="2f50a-129">Delete existing VM</span></span>
<span data-ttu-id="2f50a-130">Los discos duros virtuales y las máquinas virtuales son dos recursos diferentes de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f50a-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="2f50a-131">Un disco duro virtual es donde se almacenan el propio sistema de operativo hello, aplicaciones y configuraciones.</span><span class="sxs-lookup"><span data-stu-id="2f50a-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="2f50a-132">Hola propia máquina virtual es solo de los metadatos que define el tamaño de Hola o la ubicación y hace referencia a recursos, como un disco duro virtual o una tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="2f50a-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="2f50a-133">Cada disco duro virtual tiene una concesión que se asigna cuando adjunta tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f50a-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="2f50a-134">Aunque los discos de datos se pueden conectados y desconectados incluso mientras se está ejecutando Hola VM, no se puede desasociar el disco del sistema operativo Hola a menos que se elimine Hola recurso de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f50a-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="2f50a-135">concesión de Hello continúa disco de SO hello tooassociate con una máquina virtual incluso cuando esa máquina virtual está en un estado detenido o desasignado.</span><span class="sxs-lookup"><span data-stu-id="2f50a-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="2f50a-136">Hola primera toorecover paso la máquina virtual es el recurso de máquina virtual de hello toodelete propio.</span><span class="sxs-lookup"><span data-stu-id="2f50a-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="2f50a-137">Eliminando Hola VM deja Hola los discos duros virtuales en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2f50a-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="2f50a-138">Después de Hola que se elimina la máquina virtual, adjuntar Hola disco duro virtual tooanother VM tootroubleshoot y resolver errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f50a-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="2f50a-139">Después de eliminaciones de ejemplo de Hola Hola máquina virtual denominada `myVM` del grupo de recursos de hello denominado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f50a-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="2f50a-140">Espere a que termine Hola VM eliminar antes de adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="2f50a-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="2f50a-141">concesión de Hello en disco duro virtual Hola que asocia a Hola VM debe toobe publicado para poderla adjuntar hello tooanother de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="2f50a-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="2f50a-142">Adjuntar tooanother de disco duro virtual existente</span><span class="sxs-lookup"><span data-stu-id="2f50a-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="2f50a-143">Para a continuación Hola pocos pasos, usar otra máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="2f50a-144">Adjuntar toothis Hola de disco duro virtual existente toobrowse VM de solución de problemas y editar el contenido del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f50a-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="2f50a-145">Este proceso le permite toocorrect los errores de configuración o revisión adicional para la aplicación o sistema de archivos de registro, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2f50a-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="2f50a-146">Elija o cree otro toouse de máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="2f50a-147">Al adjuntar hello: disco duro virtual existente, especifique el disco de toohello de dirección URL de hello obtenido en hello anterior `Get-AzureRmVM` comando.</span><span class="sxs-lookup"><span data-stu-id="2f50a-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="2f50a-148">Hello en el ejemplo siguiente se asocia un toohello de disco duro virtual existente solución de problemas de máquina virtual denominada `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f50a-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="2f50a-149">Agregar un disco, requiere toospecify Hola un tamaño de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f50a-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="2f50a-150">Se adjunta un disco existente, Hola `-DiskSizeInGB` se especifica como `$null`.</span><span class="sxs-lookup"><span data-stu-id="2f50a-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="2f50a-151">Este valor garantiza disco de datos de hello está correctamente conectado y sin Hola necesita toodetermine Hola tamaño real del disco de datos.</span><span class="sxs-lookup"><span data-stu-id="2f50a-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="2f50a-152">Montar el disco de datos adjuntos de Hola</span><span class="sxs-lookup"><span data-stu-id="2f50a-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="2f50a-153">RDP tooyour de solución de problemas de máquina virtual con las credenciales adecuadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="2f50a-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="2f50a-154">Hello en el ejemplo siguiente se descarga Hola archivo de conexión de RDP para la máquina virtual denominada hello `myVMRecovery` en grupo de recursos de hello llamado `myResourceGroup`y lo descarga demasiado`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="2f50a-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="2f50a-155">disco de datos de Hola se detecta automáticamente y se adjunta.</span><span class="sxs-lookup"><span data-stu-id="2f50a-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="2f50a-156">Ver lista de hello volúmenes conectados toodetermine Hola letra de unidad como sigue:</span><span class="sxs-lookup"><span data-stu-id="2f50a-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="2f50a-157">Después de la salida de ejemplo de Hola muestra el disco duro virtual de hello conectado un disco **2**.</span><span class="sxs-lookup"><span data-stu-id="2f50a-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="2f50a-158">(También puede usar `Get-Volume` letra de unidad de hello tooview):</span><span class="sxs-lookup"><span data-stu-id="2f50a-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="2f50a-159">Solución de problemas en el disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="2f50a-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="2f50a-160">Con hello disco duro virtual existente montado, ahora puede realizar cualquier tarea de mantenimiento y solución de problemas de pasos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2f50a-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="2f50a-161">Una vez que se ha solucionado problemas hello, continúe con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="2f50a-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="2f50a-162">Desmontaje y desconexión del disco duro virtual original</span><span class="sxs-lookup"><span data-stu-id="2f50a-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="2f50a-163">Una vez que se resuelven los errores, desmonta y separar hello: disco duro virtual existente de la máquina virtual para solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="2f50a-164">No se puede usar el disco duro virtual con cualquier otra máquina virtual hasta que se libera la concesión de hello adjuntar toohello de disco duro virtual de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="2f50a-165">Desde dentro de la sesión RDP, desmonte el disco de datos de hello en la máquina virtual de recuperación.</span><span class="sxs-lookup"><span data-stu-id="2f50a-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="2f50a-166">Se necesita número de disco de Hola de hello anterior `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f50a-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="2f50a-167">A continuación, utilice `Set-Disk` tooset disco de hello como sin conexión:</span><span class="sxs-lookup"><span data-stu-id="2f50a-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="2f50a-168">Confirme el disco de hello ahora está establecido como sin conexión mediante `Get-Disk` nuevo.</span><span class="sxs-lookup"><span data-stu-id="2f50a-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="2f50a-169">Hello siguiente salida de ejemplo muestra el disco de hello ahora está establecido como sin conexión:</span><span class="sxs-lookup"><span data-stu-id="2f50a-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="2f50a-170">Salga de la sesión RDP.</span><span class="sxs-lookup"><span data-stu-id="2f50a-170">Exit your RDP session.</span></span> <span data-ttu-id="2f50a-171">En la sesión de PowerShell de Azure, quite disco duro virtual de Hola Hola VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="2f50a-172">Creación de máquina virtual a partir del disco duro original</span><span class="sxs-lookup"><span data-stu-id="2f50a-172">Create VM from original hard disk</span></span>
<span data-ttu-id="2f50a-173">usar una máquina virtual desde el disco duro virtual original de toocreate [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="2f50a-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="2f50a-174">plantilla JSON real de Hello está en hello siguiente vínculo:</span><span class="sxs-lookup"><span data-stu-id="2f50a-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="2f50a-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f50a-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="2f50a-176">plantilla de Hello implementa una máquina virtual en una red virtual existente, mediante Hola dirección URL del VHD de hello comando anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2f50a-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="2f50a-177">Hello en el ejemplo siguiente se implementa grupo de recursos de toohello Hola plantilla llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f50a-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="2f50a-178">Hola de respuesta solicita plantilla hello como nombre de máquina virtual, el tipo de sistema operativo y el tamaño VM.</span><span class="sxs-lookup"><span data-stu-id="2f50a-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="2f50a-179">Hola `osDiskVhdUri` es Hola mismo utiliza anteriormente al adjuntar toohello Hola de disco duro virtual existente VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="2f50a-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="2f50a-180">Rehabilitación de los diagnósticos de arranque</span><span class="sxs-lookup"><span data-stu-id="2f50a-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="2f50a-181">Cuando se crea la máquina virtual de hello: disco duro virtual existente, el diagnóstico de arranque puede no se habilita automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2f50a-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="2f50a-182">Hello en el ejemplo siguiente se habilita extensión de diagnóstico de hello en hello máquina virtual denominada `myVMDeployed` en grupo de recursos de hello llamado `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="2f50a-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="2f50a-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f50a-183">Next steps</span></span>
<span data-ttu-id="2f50a-184">Si tiene problemas para conectarse tooyour VM, consulte [tooan de las conexiones RDP solucionar problemas de máquina virtual de Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f50a-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2f50a-185">Para problemas con el acceso a aplicaciones que se ejecutan en su máquina virtual, consulte [Solucionar problemas de conectividad de aplicaciones en una máquina virtual Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f50a-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2f50a-186">Para más información sobre el uso de Resource Manager, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f50a-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
