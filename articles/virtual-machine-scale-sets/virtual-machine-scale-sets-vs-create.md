---
title: "Implementación de un conjunto de escalado de máquinas virtuales mediante Visual Studio | Microsoft Docs"
description: "Implementación de un conjunto de escalado de máquinas virtuales mediante Visual Studio y una plantilla de Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="7cf6c-103">Procedimiento para crear un conjunto de escalado de máquinas virtuales con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7cf6c-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="7cf6c-104">En este artículo se muestra cómo implementar un conjunto de escalado de máquinas virtuales de Azure mediante la utilización de una implementación de grupo de recursos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="7cf6c-105">Los [conjuntos de escalado de máquinas virtuales de Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) son un recurso de Azure Compute para implementar y administrar un conjunto de máquinas virtuales similares con equilibrio de carga y escalado automático.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="7cf6c-106">Puede aprovisionar e implementar conjuntos de escalado de máquinas virtuales mediante [plantillas de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="7cf6c-107">Las plantillas de Azure Resource Manager se pueden implementar mediante la CLI de Azure, PowerShell, REST y también directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="7cf6c-108">Visual Studio proporciona un conjunto de plantillas que se pueden implementar como parte de un proyecto de implementación de grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="7cf6c-109">Las implementaciones de grupo de recursos de Azure son una forma de agrupar y publicar un conjunto de recursos de Azure relacionados en una única operación de implementación.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="7cf6c-110">Puede obtener más información aquí: [Creación e implementación de grupos de recursos de Azure mediante Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="7cf6c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7cf6c-111">Pre-requisites</span></span>
<span data-ttu-id="7cf6c-112">Para empezar a implementar conjuntos de escalado de máquinas virtuales en Visual Studio, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7cf6c-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="7cf6c-113">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="7cf6c-114">Azure SDK 2.7, 2.8 o 2.9</span><span class="sxs-lookup"><span data-stu-id="7cf6c-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="7cf6c-115">En estas instrucciones se asume que usa Visual Studio con el [SDK de Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="7cf6c-116">Creación de un proyecto</span><span class="sxs-lookup"><span data-stu-id="7cf6c-116">Creating a Project</span></span>
1. <span data-ttu-id="7cf6c-117">Cree un proyecto nuevo en Visual Studio; para ello, seleccione **Archivo | Nuevo | Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Archivo nuevo][file_new]

2. <span data-ttu-id="7cf6c-119">En **Visual C# | Nube**, elija **Azure Resource Manager** para crear un proyecto para implementar una plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Crear proyecto][create_project]

3. <span data-ttu-id="7cf6c-121">En la lista de plantillas, seleccione la plantilla del conjunto de escalado de máquinas virtuales de Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Seleccionar plantilla][select_Template]

4. <span data-ttu-id="7cf6c-123">Una vez creado el proyecto, verá los scripts de implementación de PowerShell, una plantilla de Azure Resource Manager y un archivo de parámetros para el conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Explorador de soluciones][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="7cf6c-125">Personalización del proyecto</span><span class="sxs-lookup"><span data-stu-id="7cf6c-125">Customize your project</span></span>
<span data-ttu-id="7cf6c-126">Ahora puede editar la plantilla para personalizarla en función de las necesidades de su aplicación, como agregar propiedades de extensión de máquinas virtuales o editar reglas de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="7cf6c-127">De forma predeterminada, las plantillas de conjunto de escalado de máquinas virtuales se configuran para implementar la extensión AzureDiagnostics que facilita la operación de agregar reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="7cf6c-128">También implementa un equilibrador de carga con una dirección IP pública, configurado con reglas NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="7cf6c-129">El equilibrador de carga le permite conectarse a las instancias de VM con SSH (Linux) o RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="7cf6c-130">El intervalo de puertos de front-end comienza en 50000.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="7cf6c-131">Para Linux, esto significa que si usa SSH en el puerto 50000, se le enrutará al puerto 22 de la primera VM en el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="7cf6c-132">La conexión al puerto 50001 se enruta al puerto 22 de la segunda VM, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="7cf6c-133">Una buena forma de editar las plantillas con Visual Studio es utilizar el esquema JSON para organizar los parámetros, las variables y los recursos.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="7cf6c-134">Para comprender el esquema, Visual Studio puede señalar errores en la plantilla antes de implementarla.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Explorador de JSON][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="7cf6c-136">Implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="7cf6c-136">Deploy the project</span></span>
1. <span data-ttu-id="7cf6c-137">Implemente la plantilla de Azure Resource Manager para crear el recurso de conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="7cf6c-138">Haga clic con el botón derecho en el nodo de proyecto y elija **Implementar | Nueva implementación**.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Implementar plantilla][5deploy_Template]
    
2. <span data-ttu-id="7cf6c-140">Seleccione la suscripción en el cuadro de diálogo "Implementar en grupo de recursos".</span><span class="sxs-lookup"><span data-stu-id="7cf6c-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Implementar plantilla][6deploy_Template]

3. <span data-ttu-id="7cf6c-142">Desde aquí, puede crear un grupo de recursos de Azure donde implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![Nuevo grupo de recursos][new_resource]

4. <span data-ttu-id="7cf6c-144">A continuación, haga clic en **Editar parámetros** para escribir los parámetros que se pasan a la plantilla.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="7cf6c-145">Proporcione el nombre de usuario y la contraseña del SO que se necesitan para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="7cf6c-146">Si no tiene instaladas las herramientas de PowerShell para Visual Studio, se recomienda activar la casilla **Guardar contraseñas** para evitar que se oculte un símbolo de la línea de comandos de PowerShell, o bien usar la [compatibilidad con Key Vault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Editar parámetros][edit_parameters]

5. <span data-ttu-id="7cf6c-148">Ahora haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-148">Now click **Deploy**.</span></span> <span data-ttu-id="7cf6c-149">En la ventana **Salida** se muestra el progreso de la implementación.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="7cf6c-150">Tenga en cuenta que la acción ejecuta el script **Deploy-AzureResourceGroup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Ventana de salida][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="7cf6c-152">Exploración del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7cf6c-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="7cf6c-153">Una vez finalizada la implementación, puede ver el nuevo conjunto de escalado de máquinas virtuales en Visual Studio **Cloud Explorer** (actualice la lista).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="7cf6c-154">Cloud Explorer le permite administrar recursos de Azure en Visual Studio mientras se desarrollan aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="7cf6c-155">También puede ver el conjunto de escalado de máquinas virtuales en [Azure Portal](https://portal.azure.com) y en el [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7cf6c-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="7cf6c-157">El portal es la mejor opción para administrar visualmente la infraestructura de Azure con un explorador web, mientras que Azure Resource Explorer ofrece una forma sencilla de explorar y depurar los recursos de Azure al proporcionar una ventana en la "vista de instancias" y mostrar también los comandos de PowerShell para los recursos que está mirando.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cf6c-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7cf6c-158">Next steps</span></span>
<span data-ttu-id="7cf6c-159">Después de implementar satisfactoriamente los conjuntos de escalado de máquinas virtuales en Visual Studio, puede personalizar aún más el proyecto para satisfacer las necesidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="7cf6c-160">Por ejemplo, configurar el escalado automático agregando un recurso de **Insights**, agregar infraestructura a la plantilla (como máquinas virtuales independientes) o implementar aplicaciones con la extensión del script personalizado.</span><span class="sxs-lookup"><span data-stu-id="7cf6c-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="7cf6c-161">Se puede encontrar una buena serie de plantillas de ejemplo en el repositorio de GitHub de [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) (busque "vmss").</span><span class="sxs-lookup"><span data-stu-id="7cf6c-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
