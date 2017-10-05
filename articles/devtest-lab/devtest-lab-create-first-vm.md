---
title: "Create your first VM in a lab in Azure DevTest Labs (Creación de su primera máquina virtual en un laboratorio en Azure DevTest Labs) | Microsoft Docs"
description: "Obtenga información sobre cómo crear su primera máquina virtual en un laboratorio de Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="e518a-103">Create your first VM in a lab in Azure DevTest Labs (Creación de su primera máquina virtual en un laboratorio en Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="e518a-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="e518a-104">Cuando tenga acceso inicialmente a DevTest Labs y quiera crear su primera máquina virtual, es probable que lo haga con una [imagen de Marketplace base](devtest-lab-configure-marketplace-images.md) precargada.</span><span class="sxs-lookup"><span data-stu-id="e518a-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="e518a-105">Posteriormente, también podrá elegir entre una [imagen personalizada y una fórmula](devtest-lab-add-vm.md) al crear más máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e518a-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="e518a-106">En este tutorial se explica cómo usar Azure Portal para agregar su primera máquina virtual a un laboratorio de DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="e518a-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="e518a-107">Pasos para agregar su primera máquina virtual a un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="e518a-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="e518a-108">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e518a-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="e518a-109">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="e518a-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="e518a-110">En la lista de laboratorios, seleccione aquel en el que desea crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e518a-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="e518a-111">En la hoja **Información general** del laboratorio, seleccione **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e518a-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botón Agregar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="e518a-113">En la hoja **Elegir una base**, seleccione una imagen de Marketplace para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e518a-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="e518a-114">En la hoja **Máquina virtual**, escriba un nombre para la nueva máquina virtual en el cuadro de texto **Nombre de la máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="e518a-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Hoja de la máquina virtual de laboratorio](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="e518a-116">Escriba un **Nombre de usuario** al que se concederán privilegios de administrador en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e518a-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="e518a-117">Escriba una contraseña en el campo de texto **Escriba un valor**.</span><span class="sxs-lookup"><span data-stu-id="e518a-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="e518a-118">El valor **Virtual machine disk type** (Tipo de disco de máquina virtual) determina qué tipo de disco de almacenamiento se admite para las máquinas virtuales del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="e518a-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="e518a-119">Seleccione **Tamaño de máquina virtual** y seleccione uno de los elementos predefinidos que especifican los núcleos del procesador, el tamaño de RAM y el tamaño de la unidad de disco duro de la máquina virtual que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="e518a-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="e518a-120">Seleccione **Artefactos** y, en la lista de artefactos, seleccione y configure los artefactos que desea agregar a la imagen base.</span><span class="sxs-lookup"><span data-stu-id="e518a-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="e518a-121">**Nota:** Si no está familiarizado con DevTest Labs o la configuración de artefactos, vaya a la sección [Incorporación de un artefacto existente a una máquina virtual](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) y vuelva aquí cuando haya finalizado.</span><span class="sxs-lookup"><span data-stu-id="e518a-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="e518a-122">Seleccione **Crear** para agregar la máquina virtual especificada al laboratorio.</span><span class="sxs-lookup"><span data-stu-id="e518a-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="e518a-123">La hoja del laboratorio muestra el estado de creación de la máquina virtual; primero como **Creating** (En creación) y luego como **Running** (En ejecución), una vez que se haya iniciado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e518a-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e518a-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e518a-124">Next steps</span></span>
* <span data-ttu-id="e518a-125">Una vez creada la máquina virtual, puede conectarse a la misma seleccionando **Conectar** en la hoja de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e518a-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="e518a-126">Consulte [Incorporación de una máquina virtual a un laboratorio](devtest-lab-add-vm.md) para obtener información más completa sobre cómo agregar máquinas virtuales posteriores en su laboratorio.</span><span class="sxs-lookup"><span data-stu-id="e518a-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="e518a-127">Explore la [galería de plantillas de inicio rápido de Azure Resource Manager de DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="e518a-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
