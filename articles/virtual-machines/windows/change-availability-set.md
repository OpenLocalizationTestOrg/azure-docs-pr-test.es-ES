---
title: "Cambio de un conjunto de disponibilidad de máquina virtual | Microsoft Docs"
description: "Aprenda a cambiar un conjunto de disponibilidad para sus máquinas virtuales mediante Azure Portal o Azure PowerShell con el modelo de implementación de Resource Manager."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 44c90f90-bc9a-4260-a36f-5465e2a1ef94
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: drewm
ms.openlocfilehash: d1daa01191480eaeb81727416b2134b00c698dc3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="e7cd1-103">Cambio del conjunto de disponibilidad de una máquina virtual Windows</span><span class="sxs-lookup"><span data-stu-id="e7cd1-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="e7cd1-104">En los pasos siguientes se describe cómo cambiar el conjunto de disponibilidad de una máquina virtual con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="e7cd1-105">Una máquina virtual solo puede agregarse a un conjunto de disponibilidad cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="e7cd1-106">Para poder cambiar el conjunto de disponibilidad, debe eliminar la máquina virtual y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set-using-powershell"></a><span data-ttu-id="e7cd1-107">Cambio del conjunto de disponibilidad con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7cd1-107">Change the availability set using PowerShell</span></span>
1. <span data-ttu-id="e7cd1-108">Obtenga la siguiente información importante de la máquina virtual que se va a modificar.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-108">Capture the following key details from the VM to be modified.</span></span>
   
    <span data-ttu-id="e7cd1-109">Nombre de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e7cd1-109">Name of the VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="e7cd1-110">Tamaño de VM</span><span class="sxs-lookup"><span data-stu-id="e7cd1-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="e7cd1-111">Interfaz de red principal de la red y las interfaces de red opcional si existen en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e7cd1-111">Network primary network interface and optional network interfaces if they exist on the VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="e7cd1-112">Perfil de disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e7cd1-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="e7cd1-113">Perfiles de disco de cada disco de datos</span><span class="sxs-lookup"><span data-stu-id="e7cd1-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="e7cd1-114">Extensiones de máquina virtual instaladas</span><span class="sxs-lookup"><span data-stu-id="e7cd1-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="e7cd1-115">Elimine la máquina virtual sin eliminar los discos o las interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-115">Delete the VM without deleting any of the disks or the network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="e7cd1-116">Si todavía no existe, cree el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-116">Create the availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="e7cd1-117">Vuelva a crear la máquina virtual con el nuevo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-117">Recreate the VM using the new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="e7cd1-118">Agregue discos de datos y extensiones.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-118">Add data disks and extensions.</span></span> <span data-ttu-id="e7cd1-119">Para más información, vea [Cómo conectar un disco de datos administrado a una VM con Windows en Azure Portal](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [Extensiones en Plantillas de Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="e7cd1-119">For more information, see [Attach Data Disk to VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="e7cd1-120">Los discos de datos y las extensiones pueden agregarse a la máquina virtual mediante PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="e7cd1-121">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="e7cd1-121">Example Script</span></span>
<span data-ttu-id="e7cd1-122">El script siguiente proporciona un ejemplo de recopilación de la información necesaria: se elimina la máquina virtual original y, luego, se vuelve a crear en un nuevo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details to file
    "VM Name: " | Out-File -FilePath $outFile 
    $OriginalVM.Name | Out-File -FilePath $outFile -Append

    "Extensions: " | Out-File -FilePath $outFile -Append
    $OriginalVM.Extensions | Out-File -FilePath $outFile -Append

    "VMSize: " | Out-File -FilePath $outFile -Append
    $OriginalVM.HardwareProfile.VmSize | Out-File -FilePath $outFile -Append

    "NIC: " | Out-File -FilePath $outFile -Append
    $OriginalVM.NetworkProfile.NetworkInterfaces[0].Id | Out-File -FilePath $outFile -Append

    "OSType: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.OsType | Out-File -FilePath $outFile -Append

    "OS Disk: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.Vhd.Uri | Out-File -FilePath $outFile -Append

    if ($OriginalVM.StorageProfile.DataDisks) {
    "Data Disk(s): " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.DataDisks | Out-File -FilePath $outFile -Append
    }

    #Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create the basic configuration for the replacement VM
    $newVM = New-AzureRmVMConfig -VMName $OriginalVM.Name -VMSize $OriginalVM.HardwareProfile.VmSize -AvailabilitySetId $availSet.Id
    Set-AzureRmVMOSDisk -VM $NewVM -VhdUri $OriginalVM.StorageProfile.OsDisk.Vhd.Uri  -Name $OriginalVM.Name -CreateOption Attach -Windows

    #Add Data Disks
    foreach ($disk in $OriginalVM.StorageProfile.DataDisks ) { 
    Add-AzureRmVMDataDisk -VM $newVM -Name $disk.Name -VhdUri $disk.Vhd.Uri -Caching $disk.Caching -Lun $disk.Lun -CreateOption Attach -DiskSizeInGB $disk.DiskSizeGB
    }

    #Add NIC(s)
    foreach ($nic in $OriginalVM.NetworkInterfaceIDs) {
        Add-AzureRmVMNetworkInterface -VM $NewVM -Id $nic
    }

    #Create the VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="e7cd1-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e7cd1-123">Next steps</span></span>
<span data-ttu-id="e7cd1-124">Agregue almacenamiento adicional a la máquina virtual mediante la adición de un [disco de datos](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)adicional.</span><span class="sxs-lookup"><span data-stu-id="e7cd1-124">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

