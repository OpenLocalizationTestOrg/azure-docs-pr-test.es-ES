---
title: "Creación de una imagen personalizada de Azure DevTest Labs a partir de una máquina virtual | Microsoft Azure"
description: "Aprenda a crear una imagen personalizada en Azure DevTest Labs a partir de una máquina virtual aprovisionada mediante el portal de Azure."
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
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="cc589-103">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="cc589-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="cc589-104">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="cc589-104">Step-by-step instructions</span></span>

<span data-ttu-id="cc589-105">Puede crear una imagen personalizada a partir de una máquina virtual aprovisionada y luego usar esa imagen personalizada para crear máquinas virtuales idénticas.</span><span class="sxs-lookup"><span data-stu-id="cc589-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="cc589-106">Los siguientes pasos muestran cómo crear una imagen personalizada desde una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="cc589-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="cc589-107">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="cc589-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="cc589-108">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="cc589-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="cc589-109">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="cc589-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="cc589-110">En la hoja del laboratorio, seleccione **Mis máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="cc589-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="cc589-111">En la hoja **Mis máquinas virtuales** , seleccione la máquina virtual desde la que quiere crear la imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="cc589-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="cc589-112">En la hoja de la máquina virtual, seleccione **Create custom image (VHD)**(Crear imagen personalizada [VHD]).</span><span class="sxs-lookup"><span data-stu-id="cc589-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Crear elemento de menú de imagen personalizada](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="cc589-114">En la hoja **Create image** (Crear imagen), escriba un nombre y una descripción para la imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="cc589-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="cc589-115">Esta información se muestra en la lista de bases cuando se crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc589-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Crear imagen personalizada](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="cc589-117">Seleccione si sysprep se ha ejecutado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc589-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="cc589-118">Si no se ha ejecutado sysprep en la máquina virtual, especifique si quiere ejecutar sysprep cuando se cree una máquina virtual a partir de esta imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="cc589-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="cc589-119">Cuando termine de crear la imagen personalizada, seleccione **Aceptar** .</span><span class="sxs-lookup"><span data-stu-id="cc589-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="cc589-120">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="cc589-120">Related blog posts</span></span>

- [<span data-ttu-id="cc589-121">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="cc589-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="cc589-122">Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="cc589-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="cc589-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc589-123">Next steps</span></span>

- [<span data-ttu-id="cc589-124">Agregar una máquina virtual al laboratorio</span><span class="sxs-lookup"><span data-stu-id="cc589-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
