---
title: "Incorporación de una máquina virtual reclamable a un laboratorio de Azure DevTest Labs | Microsoft Docs"
description: "Obtenga información sobre cómo agregar una máquina virtual reclamable a un laboratorio de Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 98950d72e90b0e178bae2fffa7644fd824a25eea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="41e2b-103">Incorporación de una máquina virtual reclamable a un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="41e2b-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="41e2b-104">Una imagen virtual reclamable se agrega a un laboratorio de forma similar a como se [agrega una máquina virtual estándar](devtest-lab-add-vm.md): desde una *base* que es una [imagen personalizada](devtest-lab-create-template.md), [fórmula](devtest-lab-manage-formulas.md), o [imagen de Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="41e2b-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="41e2b-105">Este tutorial le guía por el proceso de utilización de Azure Portal para agregar una máquina virtual reclamable a un laboratorio de DevTest Labs, y muestra el proceso que sigue un usuario para reclamar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e2b-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="41e2b-106">Si implementa máquinas virtuales de laboratorio a través de [plantillas de Azure Resource Manager](devtest-lab-create-environment-from-arm.md), puede crear máquinas virtuales reclamables estableciendo la propiedad **allowClaim** en "true" en la sección de propiedades.</span><span class="sxs-lookup"><span data-stu-id="41e2b-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="41e2b-107">Pasos para agregar una máquina virtual reclamable a un laboratorio de Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="41e2b-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="41e2b-108">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="41e2b-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="41e2b-109">Seleccione **Más servicios** y, luego, **DevTest Labs** en la lista.</span><span class="sxs-lookup"><span data-stu-id="41e2b-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="41e2b-110">En la lista de laboratorios, seleccione aquel en el que desea crear la máquina virtual reclamable.</span><span class="sxs-lookup"><span data-stu-id="41e2b-110">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="41e2b-111">En la hoja **Información general** del laboratorio, seleccione **+ Agregar**.</span><span class="sxs-lookup"><span data-stu-id="41e2b-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botón Agregar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="41e2b-113">En la hoja **Elegir una base** , seleccione una base para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e2b-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="41e2b-114">En la hoja **Máquina virtual**, escriba un nombre para la nueva máquina virtual en el cuadro de texto **Nombre de la máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="41e2b-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Hoja de la máquina virtual de laboratorio](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="41e2b-116">Escriba un **Nombre de usuario** al que se concederán privilegios de administrador en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e2b-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="41e2b-117">Si quiere usar una contraseña almacenada en su [almacén secreto](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), seleccione **Use a saved secret** (Usar un secreto guardado) y especifique un valor de clave que corresponda a su secreto (contraseña).</span><span class="sxs-lookup"><span data-stu-id="41e2b-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="41e2b-118">De lo contrario, escriba una contraseña en el campo de texto **Escriba un valor**.</span><span class="sxs-lookup"><span data-stu-id="41e2b-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="41e2b-119">El valor **Virtual machine disk type** (Tipo de disco de máquina virtual) determina qué tipo de disco de almacenamiento se admite para las máquinas virtuales del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="41e2b-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="41e2b-120">Seleccione **Tamaño de máquina virtual** y seleccione uno de los elementos predefinidos que especifican los núcleos del procesador, el tamaño de RAM y el tamaño de la unidad de disco duro de la máquina virtual que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="41e2b-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="41e2b-121">Seleccione **Artefactos** y, en la lista de artefactos, seleccione y configure los artefactos que desea agregar a la imagen base.</span><span class="sxs-lookup"><span data-stu-id="41e2b-121">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="41e2b-122">Si no está familiarizado con DevTest Labs o la configuración de artefactos, vaya a la sección [Incorporación de un artefacto existente a una máquina virtual](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) y vuelva aquí cuando haya finalizado.</span><span class="sxs-lookup"><span data-stu-id="41e2b-122">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="41e2b-123">Seleccione **Configuración avanzada** para configurar las opciones de expiración y las opciones de red de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e2b-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="41e2b-124">En **Claim options** (Opciones de reclamación), elija **Sí** para que la máquina sea reclamable.</span><span class="sxs-lookup"><span data-stu-id="41e2b-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Elija que la máquina virtual sea reclamable.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="41e2b-126">Si desea ver o copiar la plantilla de Azure Resource Manager, vaya a la sección [Almacenamiento de una plantilla de Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) y vuelva aquí cuando haya finalizado.</span><span class="sxs-lookup"><span data-stu-id="41e2b-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="41e2b-127">Seleccione **Crear** para agregar la máquina virtual especificada al laboratorio.</span><span class="sxs-lookup"><span data-stu-id="41e2b-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="41e2b-128">La hoja del laboratorio muestra el estado de creación de la máquina virtual; primero como **Creating** (En creación) y luego como **Running** (En ejecución), una vez que se haya iniciado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e2b-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="41e2b-129">Uso de una máquina virtual reclamable</span><span class="sxs-lookup"><span data-stu-id="41e2b-129">Using a claimable VM</span></span>

<span data-ttu-id="41e2b-130">Un usuario puede reclamar cualquier máquina virtual de la lista de máquinas virtuales reclamables siguiendo alguno de estos pasos:</span><span class="sxs-lookup"><span data-stu-id="41e2b-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="41e2b-131">En la lista de máquinas virtuales reclamables, en la parte inferior de la hoja de información general del laboratorio, haga doble clic en una de las máquinas virtuales en la lista y elija **Claim machine**  (Reclamar máquina).</span><span class="sxs-lookup"><span data-stu-id="41e2b-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Solicite una máquina virtual reclamable específica.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="41e2b-133">En la parte superior de la hoja **Información general** , elija **Claim any** (Reclamar cualquiera).</span><span class="sxs-lookup"><span data-stu-id="41e2b-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="41e2b-134">Se asigna una máquina virtual aleatoria de la lista de máquinas virtuales reclamables.</span><span class="sxs-lookup"><span data-stu-id="41e2b-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Solicite cualquier máquina virtual reclamable.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="41e2b-136">Una vez que un usuario reclama una máquina virtual, se mueve a su lista de máquinas virtuales y ya no podrá reclamarla otro usuario.</span><span class="sxs-lookup"><span data-stu-id="41e2b-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41e2b-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41e2b-137">Next steps</span></span>
* <span data-ttu-id="41e2b-138">Una vez creada la máquina virtual, puede conectarse a la misma seleccionando **Conectar** en la hoja de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41e2b-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="41e2b-139">Explore la [galería de plantillas de inicio rápido de Azure Resource Manager de DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="41e2b-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
