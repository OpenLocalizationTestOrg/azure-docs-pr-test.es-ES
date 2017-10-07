---
title: "aaaCreate una imagen de Azure RemoteApp se basa en una máquina virtual de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una imagen de Azure RemoteApp a partir de una máquina virtual de Azure."
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
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="bcab0-103">Creación de una imagen de Azure RemoteApp basada en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="bcab0-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bcab0-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="bcab0-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bcab0-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="bcab0-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bcab0-106">Puede crear imágenes de Azure RemoteApp (que contienen aplicaciones de Hola que comparte en la colección) de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcab0-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="bcab0-107">También puede elegir toouse una imagen de máquina virtual que agregamos la Galería de imágenes de máquina virtual de Azure toohello que cumple todos los requisitos de imagen de Azure RemoteApp hello: puede usar esa imagen de máquina virtual como un punto de partida para su propia máquina virtual, si desea.</span><span class="sxs-lookup"><span data-stu-id="bcab0-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="bcab0-108">Busque imágenes de "Windows Server escritorio remoto" hello en la biblioteca de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcab0-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="bcab0-109">Hay dos toocreate pasos según su propia imagen en una máquina virtual de Azure: crear imagen de hello y, a continuación, cargarlo desde hello Azure VM biblioteca tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bcab0-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="bcab0-110">Creación de una imagen personalizada basada en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="bcab0-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="bcab0-111">Use estos toocreate pasos una imagen basada en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcab0-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="bcab0-112">Cree una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcab0-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="bcab0-113">Puede usar Hola "Host a sesión remota de escritorio de Windows Server" o "Windows Server remoto escritorio sesión Host con Microsoft Office 365 ProPlus" imagen de Hola desde galería de imágenes de máquina virtual de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="bcab0-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="bcab0-114">Esta imagen cumple todos los requisitos de imagen de plantilla de RemoteApp de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcab0-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="bcab0-115">Para obtener información detallada, vea [Creación de una máquina virtual que ejecuta Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bcab0-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="bcab0-116">Conectar toohello máquina virtual e instalar y configurar aplicaciones de Hola que desea que tooshare a través de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bcab0-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="bcab0-117">Asegúrese de tooperform seguro de las configuraciones de Windows adicionales requeridas por las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bcab0-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="bcab0-118">Para obtener más información, consulte [cómo tooLog en tooa Máquina Virtual que ejecuta Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bcab0-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="bcab0-119">Si está utilizando uno de imágenes de Host de sesión de escritorio remoto de Windows Server de hello, hay una secuencia de comandos de validación incluye que asegure que la máquina virtual cumple Hola RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="bcab0-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="bcab0-120">secuencia de comandos de toorun, haga doble clic en **ValidateRemoteAppImage** en el escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcab0-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="bcab0-121">Asegúrese de que todos los errores notificados por el script de Hola se corrigen antes del paso siguiente de toohello de continuar.</span><span class="sxs-lookup"><span data-stu-id="bcab0-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="bcab0-122">SYSPREP /generalize y capturar imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="bcab0-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="bcab0-123">Vea [cómo tooCapture una tooUse de máquina Virtual de Windows como una plantilla de](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="bcab0-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="bcab0-124">Importar imagen hello en la biblioteca de imágenes de hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bcab0-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="bcab0-125">Use estos nueva imagen de pasos tooimport hello en Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="bcab0-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="bcab0-126">Hola **imágenes de plantilla** ficha:</span><span class="sxs-lookup"><span data-stu-id="bcab0-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="bcab0-127">Si no dispone de imágenes existentes, haga clic en **Carga o importación de una imagen de plantilla**.</span><span class="sxs-lookup"><span data-stu-id="bcab0-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="bcab0-128">Si ya tiene al menos una imagen, haga clic en  **+**  tooadd una nueva imagen.</span><span class="sxs-lookup"><span data-stu-id="bcab0-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="bcab0-129">Seleccione **Importar una imagen de la biblioteca de máquinas virtuales** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bcab0-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="bcab0-130">En la página siguiente de hello, seleccione la imagen personalizada de lista de Hola y compruebe que ha seguido los pasos de hello aparece cuando se creó la imagen.</span><span class="sxs-lookup"><span data-stu-id="bcab0-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="bcab0-131">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bcab0-131">Click **Next**.</span></span>
4. <span data-ttu-id="bcab0-132">Escriba un nombre para la nueva imagen de RemoteApp hello y Seleccionar ubicación de Hola y luego haga clic en el proceso de importación de hello marca de verificación toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="bcab0-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="bcab0-133">Puede importar imágenes desde cualquier ubicación de Azure compatible con máquinas virtuales de Azure tooany ubicación de Azure compatible con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bcab0-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="bcab0-134">Función ubicaciones Hola importación Hola puede durar too25 minutos.</span><span class="sxs-lookup"><span data-stu-id="bcab0-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="bcab0-135">Ahora está listo toocreate la nueva colección, ya sea un [nube](remoteapp-create-cloud-deployment.md) colección o [híbrida](remoteapp-create-hybrid-deployment.md), en función de sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="bcab0-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

