---
title: Carga de archivos VHD en Azure DevTest Labs mediante AzCopy | Microsoft Docs
description: Carga de archivos VHD en la cuenta de almacenamiento del laboratorio mediante AzCopy
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="e9882-103">Carga de archivos VHD en la cuenta de almacenamiento del laboratorio mediante AzCopy</span><span class="sxs-lookup"><span data-stu-id="e9882-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="e9882-104">En Azure DevTest Labs, se pueden usar archivos VHD para crear imágenes personalizadas, que se usan para aprovisionar máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e9882-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="e9882-105">Los siguientes pasos le guían en el uso de la utilidad de línea de comandos AzCopy para cargar un archivo VHD en una cuenta de almacenamiento del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="e9882-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="e9882-106">Cuando haya cargado el archivo VHD, en la sección de [pasos siguientes](#next-steps) se muestran algunos artículos que ilustran cómo crear una imagen personalizada a partir del archivo VHD cargado.</span><span class="sxs-lookup"><span data-stu-id="e9882-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="e9882-107">Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="e9882-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="e9882-108">AzCopy es una utilidad de línea de comandos solo de Windows.</span><span class="sxs-lookup"><span data-stu-id="e9882-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="e9882-109">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="e9882-109">Step-by-step instructions</span></span>

<span data-ttu-id="e9882-110">Los siguientes pasos le guían en la carga de un archivo VHD en Azure DevTest Labs mediante [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="e9882-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="e9882-111">Obtenga el nombre de la cuenta de almacenamiento del laboratorio mediante el portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="e9882-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="e9882-112">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e9882-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="e9882-113">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="e9882-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="e9882-114">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="e9882-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="e9882-115">En la hoja del laboratorio, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="e9882-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="e9882-116">En la hoja **Configuración** del laboratorio, seleccione **Custom images (VHDs)** (Imágenes personalizadas [VHD]).</span><span class="sxs-lookup"><span data-stu-id="e9882-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="e9882-117">En la hoja **Custom images** (Imágenes personalizadas), seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e9882-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="e9882-118">En la hoja **Custom images** (Imágenes personalizadas), seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e9882-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="e9882-119">En la hoja **VHD**, seleccione **Upload a VHD using PowerShell** (Cargar un VHD mediante PowerShell).</span><span class="sxs-lookup"><span data-stu-id="e9882-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carga del VHD mediante PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="e9882-121">La hoja **Upload an image using PowerShell** (Cargar una imagen mediante PowerShell) muestra una llamada al cmdlet **Add-AzureVhd**.</span><span class="sxs-lookup"><span data-stu-id="e9882-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="e9882-122">El primer parámetro (*Destination*) contiene el URI de un contenedor de blobs (*uploads*) en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="e9882-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="e9882-123">Anote el URI completo tal como se usa en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="e9882-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="e9882-124">Carga del archivo VHD mediante AzCopy:</span><span class="sxs-lookup"><span data-stu-id="e9882-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="e9882-125">[Descargue e instale la versión más reciente de AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="e9882-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="e9882-126">Abra una ventana de comandos y vaya al directorio de instalación de AzCopy.</span><span class="sxs-lookup"><span data-stu-id="e9882-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="e9882-127">Opcionalmente, puede agregar la ubicación de instalación de AzCopy a la ruta de acceso del sistema.</span><span class="sxs-lookup"><span data-stu-id="e9882-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="e9882-128">De forma predeterminada, AzCopy se instala en el directorio siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9882-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="e9882-129">Mediante la clave de la cuenta de almacenamiento y el URI del contenedor de blobs, ejecute el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="e9882-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="e9882-130">El valor *vhdFileName* debe incluirse entre comillas.</span><span class="sxs-lookup"><span data-stu-id="e9882-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="e9882-131">El proceso de cargar un archivo VHD puede ser largo en función de su tamaño y de la velocidad de conexión.</span><span class="sxs-lookup"><span data-stu-id="e9882-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="e9882-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9882-132">Next steps</span></span>

- [<span data-ttu-id="e9882-133">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e9882-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="e9882-134">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9882-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)