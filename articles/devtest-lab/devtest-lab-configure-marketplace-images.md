---
title: "configuración de la imagen aaaConfigure Azure Marketplace en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Configuración de las imágenes de Azure Marketplace que se pueden usar al crear una máquina virtual en Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="2af54-103">Configuración de imágenes de Azure Marketplace en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2af54-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="2af54-104">Laboratorios de desarrollo y pruebas admite crear máquinas virtuales basadas en imágenes de Azure Marketplace dependiendo de cómo se haya configurado Azure Marketplace imágenes toobe utilizado en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="2af54-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="2af54-105">Este artículo muestra cómo toospecify que, si lo hay, imágenes de Azure Marketplace se pueden usar al crear máquinas virtuales en un laboratorio.</span><span class="sxs-lookup"><span data-stu-id="2af54-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="2af54-106">Esto garantiza que el equipo sólo tiene imágenes de Marketplace de toohello de acceso que necesitan.</span><span class="sxs-lookup"><span data-stu-id="2af54-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="2af54-107">Elección de las imágenes de Azure Marketplace que se permiten al crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2af54-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="2af54-108">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2af54-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="2af54-109">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="2af54-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="2af54-110">En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.</span><span class="sxs-lookup"><span data-stu-id="2af54-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="2af54-111">En la hoja del laboratorio de hello, seleccione **directivas y configuración**.</span><span class="sxs-lookup"><span data-stu-id="2af54-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="2af54-112">En la hoja **Configuration and policies** (Directivas y configuración) de **Virtual Machine Bases** (Bases de datos de las máquinas virtuales), seleccione **Marketplace images** (Imágenes de Marketplace).</span><span class="sxs-lookup"><span data-stu-id="2af54-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="2af54-113">Especifique si desea que todos los Hola toobe de imágenes de Azure Marketplace completo disponible para su uso como base de una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2af54-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="2af54-114">Si selecciona **Sí**, a continuación, todos los hello Azure Marketplace que cumplan Hola a todos los siguientes criterios se permiten imágenes en laboratorio hello:</span><span class="sxs-lookup"><span data-stu-id="2af54-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="2af54-115">imagen de Hello crea una sola máquina virtual, **y**</span><span class="sxs-lookup"><span data-stu-id="2af54-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="2af54-116">imagen de Hello usa las máquinas virtuales de Azure Resource Manager tooprovision, **y**</span><span class="sxs-lookup"><span data-stu-id="2af54-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="2af54-117">imagen de Hello no requiere la compra de un plan de licencias adicionales</span><span class="sxs-lookup"><span data-stu-id="2af54-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="2af54-118">Si no desea que ningún toobe de imágenes permite, o si desea toospecify qué imágenes se pueden usar, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="2af54-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Opción tooallow toobe de imágenes de Marketplace todos los utiliza como imágenes de base para las máquinas virtuales](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="2af54-120">Si selecciona **No** toohello anterior paso a paso, hello **permitido imágenes o seleccionar todo** casilla de verificación está habilitada.</span><span class="sxs-lookup"><span data-stu-id="2af54-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="2af54-121">Puede usar esta opción junto con el cuadro de búsqueda, hello tooquickly seleccione o anule la selección de todos los elementos de hello aparece en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="2af54-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="2af54-122">Seleccione hello Azure Marketplace imágenes que desee tooallow creación de máquinas virtuales individualmente activando la casilla de verificación correspondiente de la imagen.</span><span class="sxs-lookup"><span data-stu-id="2af54-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="2af54-123">No se selecciona nada en lista de hello si no desea tooallow cualquier toobe de imágenes de Azure Marketplace utilizado en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2af54-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Puede especificar qué imágenes de Azure Marketplace se pueden usar como imágenes base para las máquinas virtuales](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="2af54-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2af54-125">Next steps</span></span>
<span data-ttu-id="2af54-126">Una vez haya configurado el modo en que se permiten imágenes de Azure Marketplace al crear una máquina virtual, paso siguiente hello es demasiado[agregar un laboratorio VM tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="2af54-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

