---
title: aaaCreate un disco administrado desde un disco duro virtual en Azure | Documentos de Microsoft
description: "Crear un disco administrado desde un disco duro virtual está actualmente en una cuenta de almacenamiento de Azure, mediante el modelo de implementación del Administrador de recursos de Hola."
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
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="18e84-103">Creación de discos administrados a partir de discos no administrados en una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="18e84-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="18e84-104">Se puede crear un disco administrado a partir de un disco de datos existente o de un disco del SO que actualmente se encuentra en la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="18e84-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="18e84-105">También puede crear un disco vacío que puede usarse como un nuevo disco de datos para una VM.</span><span class="sxs-lookup"><span data-stu-id="18e84-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="18e84-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="18e84-106">Before you begin</span></span>
<span data-ttu-id="18e84-107">Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18e84-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="18e84-108">Ejecutar Hola siguientes tooinstall de comando.</span><span class="sxs-lookup"><span data-stu-id="18e84-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="18e84-109">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="18e84-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="18e84-110">Creación de un disco administrado a partir de un VHD en una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="18e84-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="18e84-111">En el ejemplo de Hola se cree un disco de un disco duro virtual como disco administrado y asígnela parámetro toohello **$Disco1** toouse más tarde.</span><span class="sxs-lookup"><span data-stu-id="18e84-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="18e84-112">Hello disco administrado se creará en hello **oeste-US** ubicación, en un grupo de recursos denominado **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="18e84-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="18e84-113">disco de Hola se denominará **myDisk** y se crearán desde un archivo de disco duro virtual denominado **myDisk.vhd** se cargó previamente tooa cuenta de almacenamiento denominada **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="18e84-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="18e84-114">disco administrado Hola se creará en el almacenamiento de premium localmente redundante (LRS).</span><span class="sxs-lookup"><span data-stu-id="18e84-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="18e84-115">StandardLRS y PremiumLRS son solo hello **- AccountType** discos administran por las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="18e84-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="18e84-116">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="18e84-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="18e84-117">Crear disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e84-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="18e84-118">Creación de un disco de datos vacío como un disco administrado</span><span class="sxs-lookup"><span data-stu-id="18e84-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="18e84-119">En el ejemplo de Hola se cree un disco de datos vacíos como disco administrado y asígnela parámetro toohello **$dataDisk2** toouse más tarde.</span><span class="sxs-lookup"><span data-stu-id="18e84-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="18e84-120">Un disco de datos vacíos necesitará toobe inicializado toohello VM de inicio de sesión y usar diskmgmt.msc o [de forma remota con WinRM y una secuencia de comandos](attach-disk-ps.md#initialize-the-disk), una vez se haya conectado tooa ejecutando la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="18e84-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="18e84-121">se creará el disco de datos vacíos de Hola Hola **oeste Ee.uu. Central** ubicación, en un grupo de recursos denominado **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="18e84-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="18e84-122">disco de Hola se denominará **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="18e84-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="18e84-123">disco vacío de Hola se creará en el almacenamiento de premium localmente redundante (LRS).</span><span class="sxs-lookup"><span data-stu-id="18e84-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="18e84-124">StandardLRS y PremiumLRS son solo hello **- AccountType** discos administran por las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="18e84-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="18e84-125">tamaño de disco de Hello en este ejemplo es 128GB, pero debe elegir un tamaño que satisfaga las necesidades de Hola de las aplicaciones que se ejecutan en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="18e84-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="18e84-126">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="18e84-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="18e84-127">Crear disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="18e84-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="18e84-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18e84-128">Next Steps</span></span>   
- <span data-ttu-id="18e84-129">Si ya tiene una VM, puede [conectar un disco de datos](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18e84-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
