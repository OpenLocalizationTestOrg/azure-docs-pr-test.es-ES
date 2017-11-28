---
title: "aaaCreate la primera VM en un laboratorio de prácticas de desarrollo y pruebas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate la primera máquina virtual en un laboratorio de prácticas de desarrollo y pruebas de Azure"
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
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="a1f66-103">Create your first VM in a lab in Azure DevTest Labs (Creación de su primera máquina virtual en un laboratorio en Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="a1f66-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="a1f66-104">Cuando inicialmente tener acceso a los laboratorios de desarrollo y pruebas y desea toocreate la primera máquina virtual, es probable que lo hará con cargado previamente [imagen de marketplace base](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="a1f66-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="a1f66-105">Más adelante podrá también pueden toochoose desde una [imagen personalizada y una fórmula](devtest-lab-add-vm.md) al crear más máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a1f66-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="a1f66-106">Este tutorial le guiará a través de hello tooadd portal Azure su primera práctica tooa VM en los laboratorios de desarrollo y pruebas.</span><span class="sxs-lookup"><span data-stu-id="a1f66-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="a1f66-107">Los pasos tooadd su primera práctica tooa VM en los laboratorios de desarrollo y pruebas de Azure</span><span class="sxs-lookup"><span data-stu-id="a1f66-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="a1f66-108">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a1f66-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="a1f66-109">Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f66-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="a1f66-110">En lista de Hola de laboratorios, seleccione laboratorio hello en el que desea toocreate Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a1f66-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="a1f66-111">En el laboratorio de hello **Introducción** hoja, seleccione **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="a1f66-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Botón Agregar VM](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="a1f66-113">En hello **elegir una base de** hoja, seleccione la imagen de un mercado para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a1f66-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="a1f66-114">En hello **Máquina Virtual** hoja, escriba un nombre para la nueva máquina virtual de Hola Hola **nombre de máquina Virtual** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="a1f66-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Hoja de la máquina virtual de laboratorio](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="a1f66-116">Escriba un **nombre de usuario** que se conceden privilegios de administrador en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f66-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="a1f66-117">Especifique una contraseña en el campo de texto hello texto **escriba un valor**.</span><span class="sxs-lookup"><span data-stu-id="a1f66-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="a1f66-118">Hola **tipo de disco de máquina Virtual** determina qué tipo de disco de almacenamiento está permitida para las máquinas virtuales de hello en laboratorio Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f66-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="a1f66-119">Seleccione **tamaño de máquina Virtual** y seleccione una de hello predefinidos elementos que especifiquen los núcleos de procesador de hello, el tamaño de RAM y tamaño de unidad de disco duro de Hola de hello toocreate de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a1f66-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="a1f66-120">Seleccione **artefactos** y - Hola seleccione en lista de artefactos - y configurar los artefactos de Hola que desea que la imagen base de tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="a1f66-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="a1f66-121">**Nota:** si nuevos laboratorios de tooDevTest o configuración de artefactos, consulte toohello [agregar un tooa artefacto existente VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) sección y, a continuación, regrese aquí cuando termine.</span><span class="sxs-lookup"><span data-stu-id="a1f66-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="a1f66-122">Seleccione **crear** tooadd Hola especificado laboratorio toohello de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a1f66-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="a1f66-123">hoja de laboratorio Hello muestra el estado de Hola de creación de la máquina virtual de hello - primero como **crear**, a continuación, como **ejecutando** después de hello máquina virtual se ha iniciado.</span><span class="sxs-lookup"><span data-stu-id="a1f66-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1f66-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1f66-124">Next steps</span></span>
* <span data-ttu-id="a1f66-125">Una vez Hola se ha creado la máquina virtual, puede conectarse toohello VM seleccionando **conectar** en la hoja de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1f66-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="a1f66-126">Extraer del repositorio [agregar un laboratorio VM tooa](devtest-lab-add-vm.md) para obtener información más completa acerca de cómo agregar máquinas virtuales posteriores en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="a1f66-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="a1f66-127">Explorar hello [Galería de plantillas de desarrollo y pruebas laboratorios Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="a1f66-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
