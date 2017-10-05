---
title: "Creación de una imagen de Azure RemoteApp basada en una máquina virtual de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo crear una imagen para Azure RemoteApp comenzando con una máquina virtual de Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="51d8f-103">Creación de una imagen de Azure RemoteApp basada en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="51d8f-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="51d8f-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="51d8f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="51d8f-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="51d8f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="51d8f-106">Puede crear imágenes de Azure RemoteApp (que incluyan las aplicaciones que comparte en la colección) desde una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="51d8f-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="51d8f-107">También puede elegir usar una imagen de máquina virtual que agregamos a la galería de imágenes de máquina virtual de Azure que cumple todos los requisitos de imagen de Azure RemoteApp, y usarla como punto de partida para su propia máquina virtual, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="51d8f-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="51d8f-108">Solo busque la imagen "Host de sesión de Escritorio remoto de Windows Server" en la biblioteca.</span><span class="sxs-lookup"><span data-stu-id="51d8f-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="51d8f-109">Existen dos pasos para crear su propia imagen basada en una máquina virtual de Azure: crear la imagen y luego cargarla desde la biblioteca de máquinas virtuales de Azure en Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="51d8f-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="51d8f-110">Creación de una imagen personalizada basada en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="51d8f-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="51d8f-111">Utilice estos pasos para crear una imagen basada en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="51d8f-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="51d8f-112">Cree una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="51d8f-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="51d8f-113">Puede usar la imagen "Host de sesión de Escritorio remoto de Windows Server" o "Host de sesión de Escritorio remoto de Windows Server con Microsoft Office 365 ProPlus" de la galería de imágenes de máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="51d8f-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="51d8f-114">Esta imagen cumple con todos los requisitos de imagen de plantilla de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="51d8f-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="51d8f-115">Para obtener información detallada, vea [Creación de una máquina virtual que ejecuta Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51d8f-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="51d8f-116">Conéctese a la máquina virtual e instale y configure las aplicaciones que desea compartir a través de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="51d8f-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="51d8f-117">Asegúrese de realizar cualquier configuración adicional de Windows que requieran sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="51d8f-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="51d8f-118">Para obtener información detallada, consulte [Cómo iniciar sesión en una máquina virtual que ejecuta Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51d8f-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="51d8f-119">Si usa una de las imágenes de Host de sesión de Escritorio remoto de Windows Server, hay incluido un script de validación que garantizará que la máquina virtual cumple los requisitos previos de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="51d8f-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="51d8f-120">Para ejecutar el script, haga doble clic en **ValidateRemoteAppImage** en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="51d8f-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="51d8f-121">Asegúrese de que todos los errores que el script informó estén corregidos antes de continuar al paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="51d8f-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="51d8f-122">SYSPREP generalice y capture la imagen.</span><span class="sxs-lookup"><span data-stu-id="51d8f-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="51d8f-123">Vea [Cómo capturar una máquina virtual Windows para usarla como plantilla#](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="51d8f-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="51d8f-124">Importación de la imagen en la biblioteca de imágenes de Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="51d8f-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="51d8f-125">Use estos pasos para importar la imagen nueva en Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="51d8f-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="51d8f-126">En la pestaña **Imágenes de plantilla** :</span><span class="sxs-lookup"><span data-stu-id="51d8f-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="51d8f-127">Si no dispone de imágenes existentes, haga clic en **Carga o importación de una imagen de plantilla**.</span><span class="sxs-lookup"><span data-stu-id="51d8f-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="51d8f-128">Si ya tiene al menos una imagen, haga clic en **+** para agregar otra imagen.</span><span class="sxs-lookup"><span data-stu-id="51d8f-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="51d8f-129">Seleccione **Importar una imagen de la biblioteca de máquinas virtuales** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="51d8f-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="51d8f-130">En la página siguiente, seleccione la imagen personalizada de la lista y confirme que siguió los pasos enumerados al momento de crear la imagen.</span><span class="sxs-lookup"><span data-stu-id="51d8f-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="51d8f-131">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="51d8f-131">Click **Next**.</span></span>
4. <span data-ttu-id="51d8f-132">Escriba un nombre para la imagen nueva de RemoteApp y elija la ubicación; a continuación, haga clic en la marca de verificación para comenzar el proceso de importación.</span><span class="sxs-lookup"><span data-stu-id="51d8f-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="51d8f-133">Puede importar imágenes desde cualquier ubicación de Azure compatible con máquinas virtuales de Azure a cualquier ubicación de Azure compatible con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="51d8f-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="51d8f-134">La importación puede demorar hasta 25 minutos, dependiendo de las ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="51d8f-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="51d8f-135">Ahora está listo para crear su colección, ya sea una colección [en la nube](remoteapp-create-cloud-deployment.md) o una colección [híbrida](remoteapp-create-hybrid-deployment.md), según sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="51d8f-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

