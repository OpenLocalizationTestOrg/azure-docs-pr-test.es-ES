---
title: aaaCreate una copia de un disco administrado de Azure para copia de seguridad | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una copia de un toouse de disco administrado de Azure para volver arriba o hacia la solución de problemas de disco emite."
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
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="5f1b8-103">Creación de una copia de un VHD almacenado como un disco administrado de Azure mediante instantáneas administradas</span><span class="sxs-lookup"><span data-stu-id="5f1b8-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="5f1b8-104">Crear una instantánea de un disco administrado para copia de seguridad o crear un disco administrado desde la instantánea de Hola y adjuntarlo tootroubleshoot de máquina virtual de prueba tooa.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="5f1b8-105">Una instantánea administrada es una copia completa a partir de un momento específico de un disco administrado de VM.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="5f1b8-106">Crea una copia de solo lectura del VHD y, de forma predeterminada, se almacena como un Disco administrado estándar.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="5f1b8-107">Para más información sobre Managed Disks, consulte [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Introducción a Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="5f1b8-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="5f1b8-108">Para información sobre los precios, consulte [Precios de Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="5f1b8-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5f1b8-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="5f1b8-109">Before you begin</span></span>
<span data-ttu-id="5f1b8-110">Si se usa PowerShell, asegúrese de que tiene versión más reciente de Hola de hello módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5f1b8-111">Ejecutar Hola siguientes tooinstall de comando.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5f1b8-112">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5f1b8-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="5f1b8-113">Copiar Hola VHD con una instantánea</span><span class="sxs-lookup"><span data-stu-id="5f1b8-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="5f1b8-114">Usar Hola portal de Azure o PowerShell tootake una instantánea de hello disco administrado.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="5f1b8-115">Usar tootake portal Azure una instantánea</span><span class="sxs-lookup"><span data-stu-id="5f1b8-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="5f1b8-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f1b8-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5f1b8-117">A partir de la parte superior izquierda de hello, haga clic en **New** y busque **instantánea**.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="5f1b8-118">En la hoja de la instantánea de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="5f1b8-119">Escriba un **nombre** para instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="5f1b8-120">Seleccione una existente [grupo de recursos](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nombre de tipo hello para uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="5f1b8-121">Seleccione una ubicación del centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="5f1b8-122">Para **el disco de origen**, seleccione Hola toosnapshot administrado por disco.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="5f1b8-123">Seleccione hello **tipo de cuenta** instantánea de toouse toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="5f1b8-124">Se recomienda **Standard_LRS**, a menos que necesite almacenarla en un disco de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="5f1b8-125">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="5f1b8-126">Usar PowerShell tootake una instantánea</span><span class="sxs-lookup"><span data-stu-id="5f1b8-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="5f1b8-127">Hello pasos siguientes muestran cómo tooget Hola VHD disco toobe copiar, crear Hola configuraciones de instantáneas y tomar una instantánea del disco de hello utilizando el cmdlet New-AzureRmSnapshot Hola<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="5f1b8-128">Configure algunos parámetros.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="5f1b8-129">Reemplace los valores de parámetro hello:</span><span class="sxs-lookup"><span data-stu-id="5f1b8-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="5f1b8-130">"myResourceGroup" con el grupo de recursos de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="5f1b8-131">"southeastasia" con la ubicación geográfica de Hola donde desea que la instantánea administrados almacenados.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="5f1b8-132">"ContosoMD_datadisk1" con el nombre de Hola de disco del disco duro virtual de Hola que desea toocopy.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="5f1b8-133">Nombre de "ContosoMD_datadisk1_snapshot1" con hello desea toouse para la nueva instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="5f1b8-134">Obtener toobe de disco VHD Hola copiado.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="5f1b8-135">Crear configuraciones de instantáneas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="5f1b8-136">Tomar instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="5f1b8-137">Si piensa toouse Hola instantánea toocreate un disco administrado y adjuntar una máquina virtual que necesita toobe alto rendimiento, use el parámetro hello `-AccountType Premium_LRS` con el comando hello AzureRmSnapshot de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="5f1b8-138">parámetro Hello crea instantáneas de Hola para que se almacena como un disco de Premium administrados.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="5f1b8-139">Managed Disks Premium son más costosos que los Estándar.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="5f1b8-140">Por lo tanto, asegúrese de que realmente necesita discos Premium antes de usar el parámetro.</span><span class="sxs-lookup"><span data-stu-id="5f1b8-140">So be sure you really need Premium before using that parameter.</span></span>


