---
title: aaaUpload VHD archivo laboratorios de desarrollo y pruebas de tooAzure con AzCopy | Documentos de Microsoft
description: Cargar la cuenta de almacenamiento del disco duro virtual archivo toolab con AzCopy
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="7be21-103">Cargar la cuenta de almacenamiento del disco duro virtual archivo toolab con AzCopy</span><span class="sxs-lookup"><span data-stu-id="7be21-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="7be21-104">En los laboratorios de desarrollo y pruebas de Azure, archivos de disco duro virtual pueden ser toocreate usa imágenes personalizadas, que son máquinas virtuales de tooprovision usado.</span><span class="sxs-lookup"><span data-stu-id="7be21-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="7be21-105">Hola pasos orientará sobre el uso de tooupload de utilidad de línea de comandos de AzCopy Hola la cuenta de almacenamiento del laboratorio tooa de archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="7be21-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="7be21-106">Una vez que haya cargado el archivo VHD, Hola [pasos siguientes sección](#next-steps) enumera algunos artículos que ilustran cómo toocreate una imagen personalizada de hello carga archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="7be21-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="7be21-107">Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="7be21-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="7be21-108">AzCopy es una utilidad de línea de comandos solo de Windows.</span><span class="sxs-lookup"><span data-stu-id="7be21-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="7be21-109">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="7be21-109">Step-by-step instructions</span></span>

<span data-ttu-id="7be21-110">Hola después de recorrido de pasos a través de la carga de un disco duro virtual archivo laboratorios de desarrollo y pruebas de tooAzure con [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="7be21-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="7be21-111">Obtener nombre de Hola de cuenta de almacenamiento del laboratorio de hello mediante Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="7be21-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="7be21-112">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="7be21-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="7be21-113">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="7be21-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="7be21-114">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="7be21-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="7be21-115">En la hoja del laboratorio de hello, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="7be21-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="7be21-116">En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="7be21-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="7be21-117">En hello **imágenes personalizadas** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="7be21-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="7be21-118">En hello **imagen personalizada** hoja, seleccione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="7be21-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="7be21-119">En hello **VHD** hoja, seleccione **cargar un VHD con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7be21-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carga del VHD mediante PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="7be21-121">Hola **cargar una imagen con PowerShell** hoja muestra una llamada toohello **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7be21-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="7be21-122">Hola primer parámetro (*destino*) contiene Hola URI para un contenedor de blobs (*carga*) Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="7be21-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="7be21-123">Tome nota de hello completa de URI como se utiliza en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="7be21-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="7be21-124">Cargar archivo de disco duro virtual de hello mediante AzCopy:</span><span class="sxs-lookup"><span data-stu-id="7be21-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="7be21-125">[Descargue e instale la versión más reciente de Hola de AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="7be21-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="7be21-126">Abra una ventana de comandos y desplácese toohello directorio de instalación de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="7be21-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="7be21-127">Si lo desea, puede agregar hello AzCopy tooyour sistema ruta de instalación.</span><span class="sxs-lookup"><span data-stu-id="7be21-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="7be21-128">De forma predeterminada, AzCopy está instalado toohello siguiente directorio:</span><span class="sxs-lookup"><span data-stu-id="7be21-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="7be21-129">Ejecute hello siguiente comando en el símbolo del sistema de hello con hello cuenta clave y el blob en contenedor de almacenamiento de URI.</span><span class="sxs-lookup"><span data-stu-id="7be21-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="7be21-130">Hola *vhdFileName* valor necesita toobe entre comillas.</span><span class="sxs-lookup"><span data-stu-id="7be21-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="7be21-131">proceso de Hola de cargar un archivo de disco duro virtual puede ser larga según el tamaño de hello del archivo de disco duro virtual de hello y la velocidad de conexión.</span><span class="sxs-lookup"><span data-stu-id="7be21-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="7be21-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7be21-132">Next steps</span></span>

- [<span data-ttu-id="7be21-133">Crear una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7be21-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="7be21-134">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7be21-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)