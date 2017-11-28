---
title: "imágenes de aaaSelect Windows VM de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Azure PowerSHell toodetermine Hola publisher, oferta, SKU y versión para imágenes de máquina virtual de Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="23808-103">Cómo imágenes toofind VM de Windows en hello Azure Marketplace con PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="23808-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="23808-104">Este tema describe cómo toouse toofind de PowerShell de Azure VM imágenes en hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="23808-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="23808-105">Utilice este toospecify una imagen de Marketplace de información cuando se crea una máquina virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="23808-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="23808-106">Asegúrese de que instaló y configuró hello más reciente [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="23808-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="23808-107">Tabla de imágenes de Windows más usadas</span><span class="sxs-lookup"><span data-stu-id="23808-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="23808-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="23808-108">PublisherName</span></span> | <span data-ttu-id="23808-109">Oferta</span><span class="sxs-lookup"><span data-stu-id="23808-109">Offer</span></span> | <span data-ttu-id="23808-110">SKU</span><span class="sxs-lookup"><span data-stu-id="23808-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="23808-111">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="23808-112">Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-112">WindowsServer</span></span> |<span data-ttu-id="23808-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="23808-113">2016-Datacenter</span></span> |
| <span data-ttu-id="23808-114">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="23808-115">Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-115">WindowsServer</span></span> |<span data-ttu-id="23808-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="23808-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="23808-117">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="23808-118">Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-118">WindowsServer</span></span> |<span data-ttu-id="23808-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="23808-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="23808-120">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="23808-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-121">WindowsServer</span></span> |<span data-ttu-id="23808-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="23808-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="23808-123">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="23808-124">Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-124">WindowsServer</span></span> |<span data-ttu-id="23808-125">Centro de datos de 2012-R2</span><span class="sxs-lookup"><span data-stu-id="23808-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="23808-126">Microsoft Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="23808-127">Windows Server</span><span class="sxs-lookup"><span data-stu-id="23808-127">WindowsServer</span></span> |<span data-ttu-id="23808-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="23808-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="23808-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="23808-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="23808-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="23808-130">DynamicsNAV</span></span> |<span data-ttu-id="23808-131">2017</span><span class="sxs-lookup"><span data-stu-id="23808-131">2017</span></span> |
| <span data-ttu-id="23808-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="23808-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="23808-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="23808-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="23808-134">2016</span><span class="sxs-lookup"><span data-stu-id="23808-134">2016</span></span> |
| <span data-ttu-id="23808-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="23808-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="23808-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="23808-136">SQL2016-WS2016</span></span> |<span data-ttu-id="23808-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="23808-137">Enterprise</span></span> |
| <span data-ttu-id="23808-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="23808-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="23808-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="23808-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="23808-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="23808-140">Enterprise</span></span> |
| <span data-ttu-id="23808-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="23808-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="23808-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="23808-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="23808-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="23808-143">2012R2</span></span> |
| <span data-ttu-id="23808-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="23808-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="23808-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="23808-145">WindowsServerEssentials</span></span> |<span data-ttu-id="23808-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="23808-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="23808-147">Búsqueda de imágenes específicas</span><span class="sxs-lookup"><span data-stu-id="23808-147">Find specific images</span></span>


<span data-ttu-id="23808-148">Al crear una nueva máquina virtual con el Administrador de recursos de Azure, en algunos casos debe toospecify una imagen con combinación de Hola de hello propiedades de imagen siguientes:</span><span class="sxs-lookup"><span data-stu-id="23808-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="23808-149">Publicador</span><span class="sxs-lookup"><span data-stu-id="23808-149">Publisher</span></span>
* <span data-ttu-id="23808-150">Oferta</span><span class="sxs-lookup"><span data-stu-id="23808-150">Offer</span></span>
* <span data-ttu-id="23808-151">SKU</span><span class="sxs-lookup"><span data-stu-id="23808-151">SKU</span></span>

<span data-ttu-id="23808-152">Por ejemplo, utilice estos valores con hello [AzureRMVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet de PowerShell, o con una plantilla de grupo de recursos en el que debe especificar el tipo de Hola de toobe de máquina virtual que creó.</span><span class="sxs-lookup"><span data-stu-id="23808-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="23808-153">Si necesita toodetermine estos valores, puede ejecutar hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), y [AzureRMVMImageSku Get](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets imágenes de hello toonavigate.</span><span class="sxs-lookup"><span data-stu-id="23808-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="23808-154">Determine estos valores:</span><span class="sxs-lookup"><span data-stu-id="23808-154">You determine these values:</span></span>

1. <span data-ttu-id="23808-155">Editores de imagen de Hola de lista.</span><span class="sxs-lookup"><span data-stu-id="23808-155">List hello image publishers.</span></span>
2. <span data-ttu-id="23808-156">Para un publicador determinado, enumeración de sus ofertas.</span><span class="sxs-lookup"><span data-stu-id="23808-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="23808-157">Para una oferta determinada, enumeración de sus SKU.</span><span class="sxs-lookup"><span data-stu-id="23808-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="23808-158">En primer lugar, lista publicadores Hola con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="23808-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="23808-159">Rellene el nombre del publicador elegido y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="23808-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="23808-160">Rellene el nombre de la oferta elegida y ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="23808-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="23808-161">De salida de hello de hello `Get-AzureRMVMImageSku` comando tiene toda la información de hello necesita imagen de hello toospecify para una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="23808-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="23808-162">Hola continuación, muestra un ejemplo completo:</span><span class="sxs-lookup"><span data-stu-id="23808-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="23808-163">Salida:</span><span class="sxs-lookup"><span data-stu-id="23808-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="23808-164">Para el publicador de "Microsoft Windows Server" hello:</span><span class="sxs-lookup"><span data-stu-id="23808-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="23808-165">Salida:</span><span class="sxs-lookup"><span data-stu-id="23808-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="23808-166">Para la oferta de "Windows Server" hello:</span><span class="sxs-lookup"><span data-stu-id="23808-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="23808-167">Salida:</span><span class="sxs-lookup"><span data-stu-id="23808-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="23808-168">En esta lista, copie Hola elegido el nombre de SKU y tiene toda la información de Hola de hello `Set-AzureRMVMSourceImage` cmdlet de PowerShell o una plantilla de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="23808-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23808-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23808-169">Next steps</span></span>
<span data-ttu-id="23808-170">Ahora puede elegir exactamente Hola imagen desea toouse.</span><span class="sxs-lookup"><span data-stu-id="23808-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="23808-171">toocreate una máquina virtual rápidamente mediante el uso de información de la imagen de hello, que acaba de encontrar, consulte [crear una máquina virtual de Windows con PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="23808-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
