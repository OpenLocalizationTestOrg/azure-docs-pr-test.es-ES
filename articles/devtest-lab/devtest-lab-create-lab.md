---
title: "Creación de un laboratorio en Azure DevTest Labs | Microsoft Docs"
description: "Creación de un laboratorio en Azure DevTest Labs para máquinas virtuales"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 265a968f902f53c7561c8c7e937f8eacfdb37167
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="285d5-103">Creación de un laboratorio con Laboratorios de desarrollo y pruebas de Azure</span><span class="sxs-lookup"><span data-stu-id="285d5-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="285d5-104">En Azure DevTest Labs, un laboratorio es la infraestructura que abarca un grupo de recursos, como máquinas virtuales (VM), que permite una mejor administración de dichos recursos mediante la especificación de límites y cuotas.</span><span class="sxs-lookup"><span data-stu-id="285d5-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="285d5-105">Este artículo le guiará a través del proceso de creación de un laboratorio mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="285d5-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="285d5-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="285d5-106">Prerequisites</span></span>
<span data-ttu-id="285d5-107">Para crear un laboratorio necesitará:</span><span class="sxs-lookup"><span data-stu-id="285d5-107">To create a lab, you need:</span></span>

* <span data-ttu-id="285d5-108">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="285d5-108">An Azure subscription.</span></span> <span data-ttu-id="285d5-109">Para información sobre las opciones de compra de Azure, consulte [Instrucciones para contratar Azure](https://azure.microsoft.com/pricing/purchase-options/) o [Evaluación gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="285d5-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="285d5-110">Debe ser el propietario de la suscripción para crear el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="285d5-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="285d5-111">Pasos para crear un laboratorio con Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="285d5-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="285d5-112">Los pasos siguientes muestran cómo usar Azure Portal para crear un laboratorio en Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="285d5-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="285d5-113">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="285d5-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="285d5-114">En el menú principal de la izquierda, seleccione **Más servicios** (en la parte inferior de la lista).</span><span class="sxs-lookup"><span data-stu-id="285d5-114">From the main menu on the left side, select **More Services** (at the bottom of the list).</span></span>

    ![Opción del menú Más servicios](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="285d5-116">En la lista de servicios disponibles, **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="285d5-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="285d5-117">En la hoja **DevTest Labs**, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="285d5-117">On the **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Incorporación de un laboratorio](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="285d5-119">En la hoja **Crear un laboratorio de desarrollo y pruebas** :</span><span class="sxs-lookup"><span data-stu-id="285d5-119">On the **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="285d5-120">Escriba un **Nombre de laboratorio** para el nuevo laboratorio.</span><span class="sxs-lookup"><span data-stu-id="285d5-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="285d5-121">Seleccione una **suscripción** para asociar al laboratorio.</span><span class="sxs-lookup"><span data-stu-id="285d5-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="285d5-122">Seleccione una **Ubicación** en la que se va a almacenar el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="285d5-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="285d5-123">Seleccione **Apagado automático** para especificar si desea habilitar y definir los parámetros para el cierre automático de todas las máquinas virtuales del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="285d5-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="285d5-124">La característica de apagado automático es principalmente una característica de ahorro de costos por la que puede especificar cuándo desea que la máquina virtual se apague automáticamente.</span><span class="sxs-lookup"><span data-stu-id="285d5-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="285d5-125">Para cambiar la configuración del apagado automático después de crear el laboratorio, siga los pasos que se describen en el artículo [Administración de todas las directivas para un laboratorio de Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="285d5-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="285d5-126">Seleccione **Anclar al panel** si desea que un acceso directo al laboratorio aparezca en el panel del portal.</span><span class="sxs-lookup"><span data-stu-id="285d5-126">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="285d5-127">Seleccione **Opciones de automatización** para obtener plantillas de Azure Resource Manager para la automatización de la configuración.</span><span class="sxs-lookup"><span data-stu-id="285d5-127">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="285d5-128">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="285d5-128">Select **Create**.</span></span> <span data-ttu-id="285d5-129">Después de seleccionar **Crear**, se muestra la hoja **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="285d5-129">After selecting **Create**, the **DevTest Labs** blade displays.</span></span> <span data-ttu-id="285d5-130">Para supervisar el estado del proceso de creación de un laboratorio, inspeccione el área **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="285d5-130">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="285d5-131">Una vez completado, actualice la página para ver el laboratorio recién creado en la lista de laboratorios.</span><span class="sxs-lookup"><span data-stu-id="285d5-131">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![Creación de una hoja de laboratorio](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="285d5-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="285d5-133">Next steps</span></span>
<span data-ttu-id="285d5-134">Una vez creado el laboratorio, le presentamos algunos pasos que se deben tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="285d5-134">Once you've created your lab, here are some next steps to consider:</span></span>

* <span data-ttu-id="285d5-135">[Acceso seguro a un laboratorio](devtest-lab-add-devtest-user.md)</span><span class="sxs-lookup"><span data-stu-id="285d5-135">[Secure access to a lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="285d5-136">[Definición de directivas de laboratorio](devtest-lab-set-lab-policy.md)</span><span class="sxs-lookup"><span data-stu-id="285d5-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="285d5-137">[Creación de una plantilla de laboratorio](devtest-lab-create-template.md)</span><span class="sxs-lookup"><span data-stu-id="285d5-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="285d5-138">[Creación de artefactos personalizados para máquinas virtuales](devtest-lab-artifact-author.md)</span><span class="sxs-lookup"><span data-stu-id="285d5-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="285d5-139">[Incorporación de una máquina virtual con artefactos a un laboratorio](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/)</span><span class="sxs-lookup"><span data-stu-id="285d5-139">[Add a VM with artifacts to a lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

