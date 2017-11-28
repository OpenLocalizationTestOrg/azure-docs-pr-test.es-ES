---
title: "Creación de una imagen personalizada de Azure DevTest Labs a partir de un archivo VHD | Microsoft Azure"
description: Aprenda a crear una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante el portal de Azure.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="0483a-103">Crear una imagen personalizada a partir de un archivo VHD</span><span class="sxs-lookup"><span data-stu-id="0483a-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="0483a-104">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="0483a-104">Step-by-step instructions</span></span>

<span data-ttu-id="0483a-105">Los siguientes pasos le guían en la creación de una imagen personalizada a partir de un archivo VHD mediante el portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="0483a-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="0483a-106">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="0483a-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="0483a-107">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="0483a-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="0483a-108">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="0483a-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="0483a-109">En la hoja del laboratorio, seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0483a-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="0483a-110">En la hoja **Configuración** del laboratorio, seleccione **Custom images (VHDs)** (Imágenes personalizadas [VHD]).</span><span class="sxs-lookup"><span data-stu-id="0483a-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="0483a-111">En la hoja **Custom images** (Imágenes personalizadas), seleccione **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="0483a-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Adición de imágenes personalizadas](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="0483a-113">Escriba el nombre de la imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="0483a-113">Enter the name of the custom image.</span></span> <span data-ttu-id="0483a-114">Este nombre se muestra en la lista de imágenes base al crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0483a-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="0483a-115">Escriba la descripción de la imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="0483a-115">Enter the description of the custom image.</span></span> <span data-ttu-id="0483a-116">Esta descripción se muestra en la lista de imágenes base al crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0483a-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="0483a-117">Seleccione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="0483a-117">Select **VHD**.</span></span>

1. <span data-ttu-id="0483a-118">En la hoja **VHD**, seleccione el archivo VHD deseado.</span><span class="sxs-lookup"><span data-stu-id="0483a-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="0483a-119">Seleccione **Aceptar** para cerrar la hoja **VHD**.</span><span class="sxs-lookup"><span data-stu-id="0483a-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="0483a-120">Seleccione la **configuración del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="0483a-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="0483a-121">En la pestaña **Configuración de SO**, seleccione **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="0483a-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="0483a-122">Si se selecciona **Windows** , especifique mediante la casilla si se ha ejecutado *Sysprep* en la máquina.</span><span class="sxs-lookup"><span data-stu-id="0483a-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="0483a-123">Seleccione **Aceptar** para cerrar la hoja **Configuración de SO**.</span><span class="sxs-lookup"><span data-stu-id="0483a-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="0483a-124">Seleccione **Aceptar** para crear la imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="0483a-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="0483a-125">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="0483a-125">Related blog posts</span></span>

- [<span data-ttu-id="0483a-126">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="0483a-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="0483a-127">Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="0483a-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="0483a-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0483a-128">Next steps</span></span>

- [<span data-ttu-id="0483a-129">Agregar una máquina virtual al laboratorio</span><span class="sxs-lookup"><span data-stu-id="0483a-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
