---
title: aaaUpload VHD archivo laboratorios de desarrollo y pruebas de tooAzure mediante PowerShell | Documentos de Microsoft
description: Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual con PowerShell
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="1c624-103">Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c624-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="1c624-104">En los laboratorios de desarrollo y pruebas de Azure, archivos de disco duro virtual pueden ser toocreate usa imágenes personalizadas, que son máquinas virtuales de tooprovision usado.</span><span class="sxs-lookup"><span data-stu-id="1c624-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="1c624-105">Hello pasos siguientes le guían a través mediante PowerShell tooupload cuenta de almacenamiento del laboratorio tooa de archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="1c624-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="1c624-106">Una vez que haya cargado el archivo VHD, Hola [pasos siguientes sección](#next-steps) enumera algunos artículos que ilustran cómo toocreate una imagen personalizada de hello carga archivo de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="1c624-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="1c624-107">Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).</span><span class="sxs-lookup"><span data-stu-id="1c624-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="1c624-108">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="1c624-108">Step-by-step instructions</span></span>

<span data-ttu-id="1c624-109">Hola siguientes pasos le indican recorrido a través de la carga de un disco duro virtual archivo laboratorios de desarrollo y pruebas de tooAzure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c624-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="1c624-110">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1c624-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="1c624-111">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c624-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="1c624-112">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="1c624-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="1c624-113">En la hoja del laboratorio de hello, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="1c624-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="1c624-114">En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="1c624-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="1c624-115">En hello **imágenes personalizadas** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="1c624-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="1c624-116">En hello **imagen personalizada** hoja, seleccione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="1c624-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="1c624-117">En hello **VHD** hoja, seleccione **cargar un VHD con PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1c624-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Carga del VHD mediante PowerShell](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="1c624-119">En hello **cargar una imagen con PowerShell** hoja, editor de texto de tooa de secuencia de comandos PowerShell de hello generado de copia.</span><span class="sxs-lookup"><span data-stu-id="1c624-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="1c624-120">Modificar hello **LocalFilePath** parámetro de hello **Add-AzureVhd** cmdlet toopoint toohello ubicación del archivo de disco duro virtual que desee tooupload Hola.</span><span class="sxs-lookup"><span data-stu-id="1c624-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="1c624-121">En un símbolo del sistema de PowerShell, ejecute hello **Add-AzureVhd** cmdlet (con hello modificado **LocalFilePath** parámetro).</span><span class="sxs-lookup"><span data-stu-id="1c624-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="1c624-122">proceso de Hola de cargar un archivo de disco duro virtual puede ser larga según el tamaño de hello del archivo de disco duro virtual de hello y la velocidad de conexión.</span><span class="sxs-lookup"><span data-stu-id="1c624-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c624-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c624-123">Next steps</span></span>

- [<span data-ttu-id="1c624-124">Crear una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1c624-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="1c624-125">Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c624-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
