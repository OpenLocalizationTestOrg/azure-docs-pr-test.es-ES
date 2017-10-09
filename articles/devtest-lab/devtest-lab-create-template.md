---
title: aaaCreate una imagen personalizada de laboratorios de desarrollo y pruebas de Azure desde un archivo VHD | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="276bc-103">Crear una imagen personalizada a partir de un archivo VHD</span><span class="sxs-lookup"><span data-stu-id="276bc-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="276bc-104">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="276bc-104">Step-by-step instructions</span></span>

<span data-ttu-id="276bc-105">Hello pasos siguientes le guían por la creación de una imagen personalizada desde un archivo de disco duro virtual mediante Hola portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="276bc-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="276bc-106">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="276bc-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="276bc-107">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="276bc-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="276bc-108">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="276bc-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="276bc-109">En la hoja del laboratorio de hello, seleccione **configuración**.</span><span class="sxs-lookup"><span data-stu-id="276bc-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="276bc-110">En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="276bc-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="276bc-111">En hello **imágenes personalizadas** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="276bc-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Adición de imágenes personalizadas](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="276bc-113">Escriba el nombre de Hola de imagen personalizada de Hola.</span><span class="sxs-lookup"><span data-stu-id="276bc-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="276bc-114">Este nombre se muestra en la lista de Hola de imágenes de base al crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="276bc-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="276bc-115">Escriba la descripción de Hola de imagen personalizada de Hola.</span><span class="sxs-lookup"><span data-stu-id="276bc-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="276bc-116">Esta descripción se muestra en la lista de Hola de imágenes de base al crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="276bc-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="276bc-117">Seleccione **VHD**.</span><span class="sxs-lookup"><span data-stu-id="276bc-117">Select **VHD**.</span></span>

1. <span data-ttu-id="276bc-118">De hello **VHD** hoja, archivo de disco duro virtual de hello seleccione deseado.</span><span class="sxs-lookup"><span data-stu-id="276bc-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="276bc-119">Seleccione **Aceptar** tooclose hello **VHD** hoja.</span><span class="sxs-lookup"><span data-stu-id="276bc-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="276bc-120">Seleccione la **configuración del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="276bc-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="276bc-121">En hello **configuración del sistema operativo** ficha, seleccione **Windows** o **Linux**.</span><span class="sxs-lookup"><span data-stu-id="276bc-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="276bc-122">Si **Windows** está seleccionada, especifique a través de la casilla de verificación de hello si *Sysprep* se ha ejecutado en la máquina de Hola.</span><span class="sxs-lookup"><span data-stu-id="276bc-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="276bc-123">Seleccione **Aceptar** tooclose hello **configuración del sistema operativo** hoja.</span><span class="sxs-lookup"><span data-stu-id="276bc-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="276bc-124">Seleccione **Aceptar** imagen personalizada de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="276bc-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="276bc-125">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="276bc-125">Related blog posts</span></span>

- [<span data-ttu-id="276bc-126">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="276bc-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="276bc-127">Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="276bc-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="276bc-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="276bc-128">Next steps</span></span>

- [<span data-ttu-id="276bc-129">Agregar un laboratorio de tooyour VM</span><span class="sxs-lookup"><span data-stu-id="276bc-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
