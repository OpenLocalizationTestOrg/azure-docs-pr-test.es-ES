---
title: "Configuración de imágenes de Azure Marketplace en Azure DevTest Labs | Microsoft Docs"
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
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="b910c-103">Configuración de imágenes de Azure Marketplace en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b910c-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="b910c-104">DevTest Labs admite la creación de máquinas virtuales basadas en imágenes de Azure Marketplace, en función de cómo se hayan configurado las imágenes de Azure Marketplace para usarlas en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="b910c-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="b910c-105">En este artículo se muestra cómo especificar qué imágenes de Azure Marketplace se pueden utilizar al crear máquinas virtuales en un laboratorio, si se puede usar alguna.</span><span class="sxs-lookup"><span data-stu-id="b910c-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="b910c-106">Esto garantiza que el equipo solo tiene acceso a las imágenes de Marketplace que necesitan.</span><span class="sxs-lookup"><span data-stu-id="b910c-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="b910c-107">Elección de las imágenes de Azure Marketplace que se permiten al crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="b910c-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="b910c-108">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b910c-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="b910c-109">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="b910c-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="b910c-110">En la lista de laboratorios, seleccione el laboratorio que desee.</span><span class="sxs-lookup"><span data-stu-id="b910c-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="b910c-111">En la hoja del laboratorio, seleccione **Directivas y configuración**.</span><span class="sxs-lookup"><span data-stu-id="b910c-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="b910c-112">En la hoja **Configuration and policies** (Directivas y configuración) de **Virtual Machine Bases** (Bases de datos de las máquinas virtuales), seleccione **Marketplace images** (Imágenes de Marketplace).</span><span class="sxs-lookup"><span data-stu-id="b910c-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="b910c-113">Especifique si desea que todas las imágenes cualificadas de Azure Marketplace estén disponibles para su uso como base de una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b910c-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="b910c-114">Si selecciona **Sí**, se permitirán en el laboratorio todas las imágenes de Azure Marketplace que cumplan los criterios siguientes:</span><span class="sxs-lookup"><span data-stu-id="b910c-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="b910c-115">La imagen crea una única máquina virtual **y**</span><span class="sxs-lookup"><span data-stu-id="b910c-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="b910c-116">La imagen utiliza Azure Resource Manager para aprovisionar máquinas virtuales **y**</span><span class="sxs-lookup"><span data-stu-id="b910c-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="b910c-117">La imagen no requiere la compra de un plan de licencias adicional.</span><span class="sxs-lookup"><span data-stu-id="b910c-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="b910c-118">Si desea que no se permitan imágenes o desea especificar las imágenes que se pueden utilizar, seleccione **No**.</span><span class="sxs-lookup"><span data-stu-id="b910c-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![Opción para permitir que todas las imágenes de Marketplace se usen como imágenes base para las máquinas virtuales](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="b910c-120">Si ha seleccionado **No** en el paso anterior, se habilita la casilla **Allowed images/Select all** (Imágenes permitidas/seleccionar todas).</span><span class="sxs-lookup"><span data-stu-id="b910c-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="b910c-121">Puede utilizar esta opción junto con el cuadro de búsqueda para seleccionar o anular la selección de todos los elementos que se muestran en la lista rápidamente.</span><span class="sxs-lookup"><span data-stu-id="b910c-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="b910c-122">Seleccione individualmente las imágenes de Azure Marketplace que desea permitir para la creación de máquinas virtuales. Para ello, active la casilla correspondiente a cada imagen.</span><span class="sxs-lookup"><span data-stu-id="b910c-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="b910c-123">No seleccione nada en la lista si no desea permitir que las imágenes de Azure Marketplace se usen en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="b910c-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![Puede especificar qué imágenes de Azure Marketplace se pueden usar como imágenes base para las máquinas virtuales](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="b910c-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b910c-125">Next steps</span></span>
<span data-ttu-id="b910c-126">Una vez que haya configurado cómo se permiten las imágenes de Azure Marketplace al crear una máquina virtual, el siguiente paso es [agregar una máquina virtual al laboratorio](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="b910c-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

