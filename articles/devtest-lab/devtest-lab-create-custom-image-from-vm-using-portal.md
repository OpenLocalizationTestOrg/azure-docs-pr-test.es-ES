---
title: "una imagen personalizada de laboratorios de desarrollo y pruebas de Azure desde una máquina virtual aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde una VM aprovisionado con Hola portal de Azure"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="ef71e-103">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ef71e-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="ef71e-104">Instrucciones paso a paso</span><span class="sxs-lookup"><span data-stu-id="ef71e-104">Step-by-step instructions</span></span>

<span data-ttu-id="ef71e-105">Puede crear una imagen personalizada de una máquina virtual con aprovisionamiento y después usar esa imagen personalizada toocreate máquinas virtuales idénticas.</span><span class="sxs-lookup"><span data-stu-id="ef71e-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="ef71e-106">Hola siguientes pasos muestra cómo toocreate personalizado de la imagen de una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="ef71e-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="ef71e-107">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ef71e-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="ef71e-108">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef71e-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="ef71e-109">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="ef71e-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="ef71e-110">En la hoja del laboratorio de hello, seleccione **mis equipos virtuales**.</span><span class="sxs-lookup"><span data-stu-id="ef71e-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="ef71e-111">En hello **mis equipos virtuales** hoja, VM Hola seleccione del que desea que la imagen personalizada de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="ef71e-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="ef71e-112">En la hoja de la máquina virtual de hello, seleccione **crear imagen personalizada (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="ef71e-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Crear elemento de menú de imagen personalizada](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="ef71e-114">En hello **crear imagen** hoja, escriba un nombre y una descripción para la imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="ef71e-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="ef71e-115">Esta información se muestra en la lista de Hola de bases de cuando se crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ef71e-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Crear imagen personalizada](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="ef71e-117">Seleccione si se ejecutó sysprep en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ef71e-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="ef71e-118">Si no se ha ejecutado sysprep hello en hello VM, especifique si desea ejecutar cuando se crea una máquina virtual desde su imagen personalizada de sysprep.</span><span class="sxs-lookup"><span data-stu-id="ef71e-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="ef71e-119">Seleccione **Aceptar** cuando toocreate terminado Hola imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="ef71e-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="ef71e-120">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="ef71e-120">Related blog posts</span></span>

- [<span data-ttu-id="ef71e-121">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="ef71e-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="ef71e-122">Copying Custom Images between Azure DevTest Labs (Copiar imágenes personalizadas entre instancias de Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="ef71e-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="ef71e-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef71e-123">Next steps</span></span>

- [<span data-ttu-id="ef71e-124">Agregar un laboratorio de tooyour VM</span><span class="sxs-lookup"><span data-stu-id="ef71e-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
