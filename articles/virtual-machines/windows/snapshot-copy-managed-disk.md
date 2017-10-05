---
title: "Creación de una copia de un disco administrado de Azure para copia de seguridad | Microsoft Docs"
description: "Obtenga información sobre cómo crear una copia de un disco administrado de Azure que se usará para copias de seguridad o solucionar problemas del disco."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: a7527b12f4f0d2b45713a0c0109d81ff51293fd8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="70861-103">Creación de una copia de un VHD almacenado como un disco administrado de Azure mediante instantáneas administradas</span><span class="sxs-lookup"><span data-stu-id="70861-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="70861-104">Cree una instantánea de un disco administrado para copias de seguridad o cree un disco administrado a partir de la instantánea y conéctelo a una máquina virtual de prueba para fines de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="70861-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from the snapshot and attach it to a test virtual machine to troubleshoot.</span></span> <span data-ttu-id="70861-105">Una instantánea administrada es una copia completa a partir de un momento específico de un disco administrado de VM.</span><span class="sxs-lookup"><span data-stu-id="70861-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="70861-106">Crea una copia de solo lectura del VHD y, de forma predeterminada, se almacena como un Disco administrado estándar.</span><span class="sxs-lookup"><span data-stu-id="70861-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="70861-107">Para más información sobre Managed Disks, consulte [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Introducción a Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="70861-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="70861-108">Para información sobre los precios, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="70861-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="70861-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="70861-109">Before you begin</span></span>
<span data-ttu-id="70861-110">Si usa PowerShell, asegúrese de que tiene la versión más reciente del módulo de PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="70861-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="70861-111">Ejecute el siguiente comando para instalarla.</span><span class="sxs-lookup"><span data-stu-id="70861-111">Run the following command to install it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="70861-112">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="70861-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-the-vhd-with-a-snapshot"></a><span data-ttu-id="70861-113">Copia del VHD con una instantánea</span><span class="sxs-lookup"><span data-stu-id="70861-113">Copy the VHD with a snapshot</span></span>
<span data-ttu-id="70861-114">Use Azure Portal o PowerShell para crear una instantánea del disco administrado.</span><span class="sxs-lookup"><span data-stu-id="70861-114">Use either the Azure portal or PowerShell to take a snapshot of the Managed Disk.</span></span>

### <a name="use-azure-portal-to-take-a-snapshot"></a><span data-ttu-id="70861-115">Uso de Azure Portal para crear una instantánea</span><span class="sxs-lookup"><span data-stu-id="70861-115">Use Azure portal to take a snapshot</span></span> 

1. <span data-ttu-id="70861-116">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70861-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="70861-117">En la parte superior izquierda, haga clic en **Nuevo** y busque **instantánea**.</span><span class="sxs-lookup"><span data-stu-id="70861-117">Starting in the upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="70861-118">En la hoja Instantánea, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="70861-118">In the Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="70861-119">Escriba un **nombre** para la instantánea.</span><span class="sxs-lookup"><span data-stu-id="70861-119">Enter a **Name** for the snapshot.</span></span>
5. <span data-ttu-id="70861-120">Seleccione un valor de [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) existente o escriba el nombre para crear uno.</span><span class="sxs-lookup"><span data-stu-id="70861-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span> 
6. <span data-ttu-id="70861-121">Seleccione una ubicación del centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="70861-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="70861-122">Como **disco de origen**, seleccione el disco administrado para la instantánea.</span><span class="sxs-lookup"><span data-stu-id="70861-122">For **Source disk**, select the Managed Disk to snapshot.</span></span>
8. <span data-ttu-id="70861-123">Seleccione el **tipo de cuenta** que se usará para almacenar la instantánea.</span><span class="sxs-lookup"><span data-stu-id="70861-123">Select the **Account type** to use to store the snapshot.</span></span> <span data-ttu-id="70861-124">Se recomienda **Standard_LRS**, a menos que necesite almacenarla en un disco de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="70861-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="70861-125">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="70861-125">Click **Create**.</span></span>

### <a name="use-powershell-to-take-a-snapshot"></a><span data-ttu-id="70861-126">Uso de PowerShell para crear una instantánea</span><span class="sxs-lookup"><span data-stu-id="70861-126">Use PowerShell to take a snapshot</span></span>
<span data-ttu-id="70861-127">Los pasos siguientes le muestran cómo obtener el disco VHD que se copiará, crear las configuraciones de instantánea y crear una instantánea del disco con el cmdlet New-AzureRmSnapshot<!--Add link to cmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="70861-127">The following steps show you how to get the VHD disk to be copied, create the snapshot configurations, and take a snapshot of the disk by using the New-AzureRmSnapshot cmdlet<!--Add link to cmdlet when available-->.</span></span> 

1. <span data-ttu-id="70861-128">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="70861-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="70861-129">Reemplace los valores de parámetro:</span><span class="sxs-lookup"><span data-stu-id="70861-129">Replace the parameter values:</span></span>
  -  <span data-ttu-id="70861-130">"myResourceGroup", con el grupo de recursos de la VM.</span><span class="sxs-lookup"><span data-stu-id="70861-130">"myResourceGroup" with the VM's resource group.</span></span>
  -  <span data-ttu-id="70861-131">"southeastasia", con la ubicación geográfica en la que desea almacenar la instantánea administrada.</span><span class="sxs-lookup"><span data-stu-id="70861-131">"southeastasia" with the geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="70861-132">"ContosoMD_datadisk1", con el nombre del disco VHD que desea copiar.</span><span class="sxs-lookup"><span data-stu-id="70861-132">"ContosoMD_datadisk1" with the name of the VHD disk that you want to copy.</span></span>
  -  <span data-ttu-id="70861-133">"ContosoMD_datadisk1_snapshot1", con el nombre que desea usar para la instantánea nueva.</span><span class="sxs-lookup"><span data-stu-id="70861-133">"ContosoMD_datadisk1_snapshot1" with the name you want to use for the new snapshot.</span></span>

2. <span data-ttu-id="70861-134">Obtenga el disco VHD que se copiará.</span><span class="sxs-lookup"><span data-stu-id="70861-134">Get the VHD disk to be copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="70861-135">Cree las configuraciones de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="70861-135">Create the snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="70861-136">Tome la instantánea.</span><span class="sxs-lookup"><span data-stu-id="70861-136">Take the snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="70861-137">Si tiene previsto utilizar la instantánea para crear un disco administrado y conectarle una VM que precisa de un alto rendimiento, use el parámetro `-AccountType Premium_LRS` con el comando New-AzureRmSnapshot.</span><span class="sxs-lookup"><span data-stu-id="70861-137">If you plan to use the snapshot to create a Managed Disk and attach it a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="70861-138">El parámetro crea la instantánea para que se almacene como disco administrado Premium.</span><span class="sxs-lookup"><span data-stu-id="70861-138">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="70861-139">Managed Disks Premium son más costosos que los Estándar.</span><span class="sxs-lookup"><span data-stu-id="70861-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="70861-140">Por lo tanto, asegúrese de que realmente necesita discos Premium antes de usar el parámetro.</span><span class="sxs-lookup"><span data-stu-id="70861-140">So be sure you really need Premium before using that parameter.</span></span>


