---
title: "Creación de un disco administrado a partir de un VHD en Azure | Microsoft Docs"
description: "Cree un disco administrado a partir de un VHD que actualmente se encuentra en la cuenta de almacenamiento de Azure, mediante el modelo de implementación de Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="ee7b3-103">Creación de discos administrados a partir de discos no administrados en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ee7b3-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="ee7b3-104">Se puede crear un disco administrado a partir de un disco de datos existente o de un disco del SO que actualmente se encuentra en la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="ee7b3-105">También puede crear un disco vacío que puede usarse como un nuevo disco de datos para una VM.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="ee7b3-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ee7b3-106">Before you begin</span></span>
<span data-ttu-id="ee7b3-107">Si usa PowerShell, asegúrese de que tiene la versión más reciente del módulo de PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="ee7b3-108">Ejecute el siguiente comando para instalarla.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="ee7b3-109">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ee7b3-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="ee7b3-110">Creación de un disco administrado a partir de un VHD en una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ee7b3-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="ee7b3-111">En el ejemplo se crea un disco a partir de un VHD como disco administrado y se asigna al parámetro **$disk1** para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="ee7b3-112">El disco administrado se creará en la ubicación **Oeste de EE. UU.**, en un grupo de recursos denominado **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="ee7b3-113">El disco se denominará **myDisk** y se creará a partir de un archivo de VHD denominado **myDisk.vhd** que se cargó previamente en una cuenta de almacenamiento llamada **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="ee7b3-114">El disco administrado se creará en el almacenamiento Premium con redundancia local (LRS).</span><span class="sxs-lookup"><span data-stu-id="ee7b3-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="ee7b3-115">StandardLRS y PremiumLRS son las únicas opciones de **-AccountType** disponibles para los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="ee7b3-116">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="ee7b3-117">Conecte el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="ee7b3-118">Creación de un disco de datos vacío como un disco administrado</span><span class="sxs-lookup"><span data-stu-id="ee7b3-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="ee7b3-119">En el ejemplo se crea un disco de datos vacío como disco administrado y se asigna al parámetro **$dataDisk2** para usarlo más adelante.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="ee7b3-120">Será necesario inicializar un disco de datos vacío iniciando sesión en la VM y usando diskmgmt.msc o [mediante el uso remoto de WinRM y de un script](attach-disk-ps.md#initialize-the-disk), una vez que se conecta a una VM en ejecución.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="ee7b3-121">El disco de datos vacío se creará en la ubicación **Centro occidental de EE.UU.**, en un grupo de recursos denominado **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="ee7b3-122">El disco se denominará **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="ee7b3-123">El disco vacío se creará en el almacenamiento Premium con redundancia local (LRS).</span><span class="sxs-lookup"><span data-stu-id="ee7b3-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="ee7b3-124">StandardLRS y PremiumLRS son las únicas opciones de **-AccountType** disponibles para los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="ee7b3-125">El tamaño del disco en este ejemplo es 128 GB, pero debe elegir un tamaño que satisfaga las necesidades de todas las aplicaciones que se ejecutan en la VM.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="ee7b3-126">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="ee7b3-127">Conecte el disco de datos.</span><span class="sxs-lookup"><span data-stu-id="ee7b3-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="ee7b3-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee7b3-128">Next Steps</span></span>   
- <span data-ttu-id="ee7b3-129">Si ya tiene una VM, puede [conectar un disco de datos](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee7b3-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
