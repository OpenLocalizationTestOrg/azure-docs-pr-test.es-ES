---
title: "aaaDeploy conjunto de escala de máquinas virtuales con Visual Studio | Documentos de Microsoft"
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
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="4944c-103">¿Cómo toocreate configuración de escalas de máquina Virtual con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4944c-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="4944c-104">Este artículo muestra cómo toodeploy en que una escala de máquinas virtuales de Azure establecido de mediante una implementación de grupo de recursos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4944c-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="4944c-105">[Conjuntos de escalas de máquina Virtual de Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) es un toodeploy de recursos de proceso de Azure y administrar una colección de máquinas virtuales similares con escala automática y el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="4944c-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="4944c-106">Puede aprovisionar e implementar conjuntos de escalado de máquinas virtuales mediante [plantillas de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="4944c-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="4944c-107">Las plantillas de Azure Resource Manager se pueden implementar mediante la CLI de Azure, PowerShell, REST y también directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4944c-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="4944c-108">Visual Studio proporciona un conjunto de plantillas que se pueden implementar como parte de un proyecto de implementación de grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4944c-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="4944c-109">Las implementaciones de grupo de recursos de Azure son una manera toogroup y publican un conjunto de recursos de Azure relacionados en una única operación de implementación.</span><span class="sxs-lookup"><span data-stu-id="4944c-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="4944c-110">Puede obtener más información aquí: [Creación e implementación de grupos de recursos de Azure mediante Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4944c-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="4944c-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4944c-111">Pre-requisites</span></span>
<span data-ttu-id="4944c-112">tooget introducción sobre cómo implementar conjuntos de escalas de máquina Virtual en Visual Studio, necesita siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="4944c-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="4944c-113">Visual Studio 2013 o posterior.</span><span class="sxs-lookup"><span data-stu-id="4944c-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="4944c-114">Azure SDK 2.7, 2.8 o 2.9</span><span class="sxs-lookup"><span data-stu-id="4944c-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="4944c-115">En estas instrucciones se asume que usa Visual Studio con el [SDK de Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="4944c-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="4944c-116">Creación de un proyecto</span><span class="sxs-lookup"><span data-stu-id="4944c-116">Creating a Project</span></span>
1. <span data-ttu-id="4944c-117">Cree un proyecto nuevo en Visual Studio; para ello, seleccione **Archivo | Nuevo | Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="4944c-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Archivo nuevo][file_new]

2. <span data-ttu-id="4944c-119">En **Visual C# | En la nube**, elija **Azure Resource Manager** toocreate un proyecto para la implementación de una plantilla de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4944c-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Crear proyecto][create_project]

3. <span data-ttu-id="4944c-121">En lista de Hola de plantillas, seleccione Hola Linux o plantilla de conjunto de escala de máquina Virtual de Windows.</span><span class="sxs-lookup"><span data-stu-id="4944c-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Seleccionar plantilla][select_Template]

4. <span data-ttu-id="4944c-123">Una vez creado el proyecto verá scripts de implementación de PowerShell, una plantilla de administrador de recursos de Azure y un archivo de parámetros para hello conjunto de escala de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4944c-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Explorador de soluciones][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="4944c-125">Personalización del proyecto</span><span class="sxs-lookup"><span data-stu-id="4944c-125">Customize your project</span></span>
<span data-ttu-id="4944c-126">Ahora puede editar Hola plantilla toocustomize para las necesidades de su aplicación, como agregar propiedades de extensión de máquina virtual o de edición cargar reglas del equilibrio.</span><span class="sxs-lookup"><span data-stu-id="4944c-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="4944c-127">De forma predeterminada plantillas de conjunto de escala de máquina Virtual de hello son toodeploy configurado hello AzureDiagnostics extensión, lo cual resulta fácil tooadd reglas de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="4944c-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="4944c-128">También implementa un equilibrador de carga con una dirección IP pública, configurado con reglas NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="4944c-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="4944c-129">equilibrador de carga de Hello le permite conectarse toohello instancias de máquina virtual con SSH (Linux) o RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="4944c-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="4944c-130">intervalo de puertos front-end de Hello comienza en 50000.</span><span class="sxs-lookup"><span data-stu-id="4944c-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="4944c-131">Para linux, esto significa que si se SSH tooport 50000, está enrutado tooport 22 de Hola primera VM Hola conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="4944c-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="4944c-132">Conexión tooport 50001 es enrutado tooport 22 de hello segunda máquina virtual y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="4944c-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="4944c-133">Una buena manera tooedit las plantillas de Visual Studio es toouse Hola esquema JSON tooorganize Hola parámetros, variables y recursos.</span><span class="sxs-lookup"><span data-stu-id="4944c-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="4944c-134">Con una comprensión de hello esquema Visual Studio puede señalar errores en la plantilla antes de implementarlo.</span><span class="sxs-lookup"><span data-stu-id="4944c-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Explorador de JSON][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="4944c-136">Implementar proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="4944c-136">Deploy hello project</span></span>
1. <span data-ttu-id="4944c-137">Implementar el recurso de conjunto de escala de máquinas virtuales de hello plantilla del Administrador de recursos de Azure toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="4944c-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="4944c-138">Haga doble clic en el nodo del proyecto de Hola y elija **implementar | Nueva implementación**.</span><span class="sxs-lookup"><span data-stu-id="4944c-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Implementar plantilla][5deploy_Template]
    
2. <span data-ttu-id="4944c-140">Seleccione la suscripción en el cuadro de diálogo de Hola "Implementar tooResource grupo".</span><span class="sxs-lookup"><span data-stu-id="4944c-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Implementar plantilla][6deploy_Template]

3. <span data-ttu-id="4944c-142">Desde aquí, puede crear la plantilla para un toodeploy de grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4944c-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Nuevo grupo de recursos][new_resource]

4. <span data-ttu-id="4944c-144">A continuación, haga clic en **editar parámetros** tooenter parámetros que se pasan tooyour plantilla.</span><span class="sxs-lookup"><span data-stu-id="4944c-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="4944c-145">Proporcionar Hola username y password para hello OS, que es la implementación de hello toocreate necesarios.</span><span class="sxs-lookup"><span data-stu-id="4944c-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="4944c-146">Si no tiene las herramientas de PowerShell para Visual Studio instalado, se recomienda toocheck **guardar contraseñas** tooavoid un línea de comandos de PowerShell oculto solicitar o usar [keyvault compatibilidad](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="4944c-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Editar parámetros][edit_parameters]

5. <span data-ttu-id="4944c-148">Ahora haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="4944c-148">Now click **Deploy**.</span></span> <span data-ttu-id="4944c-149">Hola **salida** ventana muestra el progreso de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4944c-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="4944c-150">Tenga en cuenta que la acción de Hola se está ejecutando hello **Deploy-AzureResourceGroup.ps1** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="4944c-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Ventana de salida][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="4944c-152">Exploración del conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="4944c-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="4944c-153">Una vez que se haya completado la implementación de hello, puede ver Hola conjunto escala de máquinas virtuales nuevas en Visual Studio hello **nube explorador** (lista de Hola de actualización).</span><span class="sxs-lookup"><span data-stu-id="4944c-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="4944c-154">Cloud Explorer le permite administrar recursos de Azure en Visual Studio mientras se desarrollan aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4944c-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="4944c-155">También puede ver el conjunto de escala de máquinas virtuales en hello [portal de Azure](https://portal.azure.com) y [Explorador de recursos de Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4944c-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="4944c-157">portal de Hello proporciona la mejor manera de hello toovisually administrar su infraestructura de Azure con un explorador web, mientras que el Explorador de recursos de Azure proporciona una manera sencilla de tooexplore y depurar recursos de Azure, lo que proporciona una ventana en Hola "instancia ver" y muestra PowerShell comandos para los recursos de Hola que está mirando.</span><span class="sxs-lookup"><span data-stu-id="4944c-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4944c-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4944c-158">Next steps</span></span>
<span data-ttu-id="4944c-159">Una vez que haya implementado correctamente conjuntos de escalas de máquina Virtual a través de Visual Studio, se pueden personalizar aún más su proyecto toosuit requisitos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4944c-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="4944c-160">Por ejemplo, configurar la escala automática mediante la adición de un **visión** recursos, agregar tooyour plantilla de infraestructura (por ejemplo, VM independientes), o implementar las aplicaciones que usan la extensión de script personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="4944c-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="4944c-161">Plantillas de buen ejemplo pueden encontrarse en hello [plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) repositorio de GitHub (busque "vmss").</span><span class="sxs-lookup"><span data-stu-id="4944c-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
