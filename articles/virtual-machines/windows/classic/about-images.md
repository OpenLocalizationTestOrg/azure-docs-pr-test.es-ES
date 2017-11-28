---
title: "aaaAbout imágenes para máquinas virtuales de Windows | Documentos de Microsoft"
description: "Obtenga información sobre cómo se usan las imágenes con máquinas virtuales con Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="9f074-103">Acerca de las imágenes para máquinas virtuales Windows</span><span class="sxs-lookup"><span data-stu-id="9f074-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f074-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9f074-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9f074-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="9f074-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="9f074-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f074-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9f074-107">Para obtener información acerca de cómo buscar y usar imágenes en el modelo de administrador de recursos de hello, consulte [aquí](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f074-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="9f074-108">Trabajo con imágenes</span><span class="sxs-lookup"><span data-stu-id="9f074-108">Working with images</span></span>

<span data-ttu-id="9f074-109">Puede usar el módulo de PowerShell de Azure de Hola y Hola toomanage portal Azure Hola imágenes disponibles tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9f074-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="9f074-110">módulo de Azure PowerShell Hola proporciona más opciones de comando, para que pueda localizar exactamente lo que desea toosee o siga.</span><span class="sxs-lookup"><span data-stu-id="9f074-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="9f074-111">Hola portal de Azure proporciona una interfaz gráfica de usuario para muchas de las tareas administrativas diarias Hola.</span><span class="sxs-lookup"><span data-stu-id="9f074-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="9f074-112">Estos son algunos ejemplos que usan el módulo de Azure PowerShell Hola.</span><span class="sxs-lookup"><span data-stu-id="9f074-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="9f074-113">**Obtener todas las imágenes de**:`Get-AzureVMImage`devuelve una lista de todas las imágenes de hello disponibles en su suscripción actual: las imágenes y las proporcionadas por Azure o sus asociados.</span><span class="sxs-lookup"><span data-stu-id="9f074-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="9f074-114">lista de Hello resultante puede ser grande.</span><span class="sxs-lookup"><span data-stu-id="9f074-114">hello resulting list could be large.</span></span> <span data-ttu-id="9f074-115">Hola siguiente ejemplos se muestra cómo tooget una lista más corta.</span><span class="sxs-lookup"><span data-stu-id="9f074-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="9f074-116">**Obtener familias de imágenes**: `Get-AzureVMImage | select ImageFamily` obtiene una lista de familias de imágenes mostrando cadenas de propiedad **ImageFamily**.</span><span class="sxs-lookup"><span data-stu-id="9f074-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="9f074-117">**Obtener todas las imágenes de una familia concreta**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="9f074-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="9f074-118">**Buscar imágenes de máquina virtual**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` este cmdlet funciona mediante el filtrado de la propiedad DataDiskConfiguration de hello, que solo se aplica a imágenes de tooVM.</span><span class="sxs-lookup"><span data-stu-id="9f074-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="9f074-119">En este ejemplo también filtra hello tooonly Hola label e image nombre de salida.</span><span class="sxs-lookup"><span data-stu-id="9f074-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="9f074-120">**Guardar una imagen generalizada**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="9f074-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="9f074-121">**Guardar una imagen especializada**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="9f074-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="9f074-122">parámetro de Hello OSState es necesario toocreate una imagen de máquina virtual, lo que incluye el disco del sistema operativo de Hola y discos de datos conectados.</span><span class="sxs-lookup"><span data-stu-id="9f074-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="9f074-123">Si no utiliza el parámetro hello, Hola cmdlet crea una imagen de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="9f074-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="9f074-124">valor de Hola de parámetro hello indica si generalizada o especializada Hola imagen, en función de si se ha preparado el disco del sistema operativo Hola para su reutilización.</span><span class="sxs-lookup"><span data-stu-id="9f074-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="9f074-125">**Eliminar una imagen**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="9f074-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f074-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f074-126">Next Steps</span></span>
<span data-ttu-id="9f074-127">También puede [crear una máquina Windows con el portal de Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9f074-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
