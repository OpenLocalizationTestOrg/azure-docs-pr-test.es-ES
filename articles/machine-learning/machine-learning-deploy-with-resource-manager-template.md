---
title: "Implementación de un área de trabajo de Machine Learning mediante Azure Resource Manager | Microsoft Docs"
description: "Cómo implementar un área de trabajo de Machine Learning de Azure mediante la plantilla de Azure Resource Manager"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="2993d-103">Implementación del área de trabajo de Machine Learning mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2993d-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="2993d-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="2993d-104">Introduction</span></span>
<span data-ttu-id="2993d-105">El uso de una plantilla de implementación de Azure Resource Manager le permite ahorrar tiempo proporcionándole una manera escalable de implementar componentes interconectados con un mecanismo de validación y reintento.</span><span class="sxs-lookup"><span data-stu-id="2993d-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="2993d-106">Para configurar áreas de trabajo de Azure Machine Learning, por ejemplo, debe configurar primero una cuenta de Almacenamiento de Azure y, a continuación, implementar el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2993d-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="2993d-107">Imagine que tiene que hacer esto manualmente para cientos de áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2993d-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="2993d-108">Una alternativa más sencilla es utilizar una plantilla de Azure Resource Manager para implementar un área de trabajo de Azure Machine Learning y todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="2993d-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="2993d-109">Este artículo le guiará por este proceso paso a paso.</span><span class="sxs-lookup"><span data-stu-id="2993d-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="2993d-110">Para ver una introducción excelente sobre Azure Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2993d-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="2993d-111">Paso a paso: Creación de un área de trabajo de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2993d-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="2993d-112">Crearemos un grupo de recursos de Azure e implementaremos una nueva cuenta de Almacenamiento de Azure y una nueva área de trabajo de Azure Machine Learning mediante una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2993d-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="2993d-113">Una vez completada la implementación, se imprimirá información importante acerca de las áreas de trabajo que se crearon (la clave principal, el identificador y la dirección URL del área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="2993d-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="2993d-114">Creación de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2993d-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="2993d-115">Un área de trabajo de Machine Learning requiere una cuenta de almacenamiento de Azure para almacenar el conjunto de datos vinculado a ella.</span><span class="sxs-lookup"><span data-stu-id="2993d-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="2993d-116">La siguiente plantilla usa el nombre del grupo de recursos para generar el nombre de la cuenta de almacenamiento y el nombre del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2993d-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="2993d-117">También utiliza el nombre de la cuenta de almacenamiento como una propiedad al crear el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2993d-117">It also uses the storage account name as a property when creating the workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="2993d-118">Guarde esta plantilla como archivo mlworkspace.json en c:\temp.</span><span class="sxs-lookup"><span data-stu-id="2993d-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="2993d-119">Implementación del grupo de recursos basado en la plantilla</span><span class="sxs-lookup"><span data-stu-id="2993d-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="2993d-120">Abra PowerShell</span><span class="sxs-lookup"><span data-stu-id="2993d-120">Open PowerShell</span></span>
* <span data-ttu-id="2993d-121">Instale los módulos de Azure Resource Manager y Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="2993d-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="2993d-122">Estos pasos permiten descargar e instalar los módulos necesarios para completar los pasos restantes.</span><span class="sxs-lookup"><span data-stu-id="2993d-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="2993d-123">Esto solo debe realizarse una vez en el entorno donde se ejecutan los comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2993d-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="2993d-124">Autentíquese en Azure</span><span class="sxs-lookup"><span data-stu-id="2993d-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="2993d-125">Este paso debe repetirse para cada sesión.</span><span class="sxs-lookup"><span data-stu-id="2993d-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="2993d-126">Una vez autenticado, aparecerá la información de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2993d-126">Once authenticated, your subscription information should be displayed.</span></span>

![Cuenta de Azure][1]

<span data-ttu-id="2993d-128">Ahora que tenemos acceso a Azure, podemos crear el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2993d-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="2993d-129">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2993d-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="2993d-130">Compruebe que se ha aprovisionado correctamente el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2993d-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="2993d-131">**ProvisioningState** debe ser "Succeeded" (Correcto).</span><span class="sxs-lookup"><span data-stu-id="2993d-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="2993d-132">La plantilla utiliza el nombre del grupo de recursos para generar el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2993d-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="2993d-133">El nombre de la cuenta de almacenamiento debe tener entre 3 y 24 caracteres, y usar solo números y letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2993d-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![El grupos de recursos][2]

* <span data-ttu-id="2993d-135">Mediante la implementación del grupo de recursos, implemente una nueva área de trabajo de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2993d-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="2993d-136">Una vez completada la implementación, resulta sencillo tener acceso a las propiedades del área de trabajo que implementó.</span><span class="sxs-lookup"><span data-stu-id="2993d-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="2993d-137">Por ejemplo, puede tener acceso al token de clave principal.</span><span class="sxs-lookup"><span data-stu-id="2993d-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="2993d-138">Otra manera de recuperar los tokens del área de trabajo existente es usar el comando Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="2993d-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="2993d-139">Por ejemplo, puede enumerar los tokens principales y secundarios de todas las áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="2993d-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="2993d-140">Una vez aprovisionada el área de trabajo, también puede automatizar muchas tareas de Estudio de aprendizaje automático de Microsoft Azure mediante el [módulo de PowerShell para Aprendizaje automático de Azure](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="2993d-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2993d-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2993d-141">Next Steps</span></span>
* <span data-ttu-id="2993d-142">Obtenga más información sobre la [creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2993d-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="2993d-143">Eche un vistazo al [repositorio de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="2993d-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="2993d-144">Vea este vídeo acerca de [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="2993d-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
