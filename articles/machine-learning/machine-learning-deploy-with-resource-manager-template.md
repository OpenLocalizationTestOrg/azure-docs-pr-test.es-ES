---
title: "aaaDeploy un área de trabajo de aprendizaje automático con el Administrador de recursos de Azure | Documentos de Microsoft"
description: "¿Cómo toodeploy un área de trabajo para el aprendizaje automático de Azure mediante la plantilla del Administrador de recursos de Azure"
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
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="ccb7d-103">Implementación del área de trabajo de Machine Learning mediante Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ccb7d-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="ccb7d-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="ccb7d-104">Introduction</span></span>
<span data-ttu-id="ccb7d-105">Mediante una plantilla de implementación guarda en Azure Resource Manager tiempo proporcionando un toodeploy escalable interconectados componentes mediante un mecanismo de validación y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="ccb7d-106">tooset de áreas de trabajo de aprendizaje de automático de Azure, por ejemplo, necesita toofirst configure una cuenta de almacenamiento de Azure y, a continuación, implementar el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="ccb7d-107">Imagine que tiene que hacer esto manualmente para cientos de áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="ccb7d-108">Una alternativa más sencilla es toouse un toodeploy de plantilla de Azure Resource Manager un área de trabajo de aprendizaje de automático de Azure y todas sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="ccb7d-109">Este artículo le guiará por este proceso paso a paso.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="ccb7d-110">Para ver una introducción excelente sobre Azure Resource Manager, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="ccb7d-111">Paso a paso: Creación de un área de trabajo de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ccb7d-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="ccb7d-112">Crearemos un grupo de recursos de Azure e implementaremos una nueva cuenta de Almacenamiento de Azure y una nueva área de trabajo de Azure Machine Learning mediante una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="ccb7d-113">Una vez completada la implementación de hello, se imprimirá información importante acerca de las áreas de trabajo de hello creados (Hola primary key, workspaceID Hola y el área de trabajo de hello URL toohello).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="ccb7d-114">Creación de una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ccb7d-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="ccb7d-115">Un área de trabajo de aprendizaje automático requiere un tooit de conjunto de datos vinculado de almacenamiento de Azure cuenta toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="ccb7d-116">Hello siguiente plantilla utiliza nombre Hola de nombre de cuenta de almacenamiento de Hola de hello recursos grupo toogenerate y el nombre del área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="ccb7d-117">También utiliza nombre de cuenta de almacenamiento de hello como una propiedad al crear el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

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
<span data-ttu-id="ccb7d-118">Guarde esta plantilla como archivo mlworkspace.json en c:\temp.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="ccb7d-119">Implementar grupo de recursos de hello, en función de plantilla de Hola</span><span class="sxs-lookup"><span data-stu-id="ccb7d-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="ccb7d-120">Abra PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccb7d-120">Open PowerShell</span></span>
* <span data-ttu-id="ccb7d-121">Instale los módulos de Azure Resource Manager y Azure Service Management</span><span class="sxs-lookup"><span data-stu-id="ccb7d-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="ccb7d-122">Estos pasos descargar e instalación pasos restantes del Hola Hola módulos toocomplete necesarios.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="ccb7d-123">Solo es necesario toobe efectuar una vez en entorno de Hola donde se ejecutan los comandos de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="ccb7d-124">Autenticar tooAzure</span><span class="sxs-lookup"><span data-stu-id="ccb7d-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="ccb7d-125">Este paso es necesario toobe repite para cada sesión.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="ccb7d-126">Una vez autenticado, aparecerá la información de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-126">Once authenticated, your subscription information should be displayed.</span></span>

![Cuenta de Azure][1]

<span data-ttu-id="ccb7d-128">Ahora que tenemos acceso tooAzure, podemos crear grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="ccb7d-129">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ccb7d-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="ccb7d-130">Compruebe que ese grupo de recursos de Hola se aprovisionó correctamente.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="ccb7d-131">**ProvisioningState** debe ser "Succeeded" (Correcto).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="ccb7d-132">nombre de grupo de recursos de Hola se usa por nombre de cuenta de almacenamiento de hello plantilla toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="ccb7d-133">nombre de cuenta de almacenamiento de Hello debe tener entre 3 y 24 caracteres de longitud y usar números y letras en minúsculas solo.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![Grupo de recursos][2]

* <span data-ttu-id="ccb7d-135">Con la implementación del grupo de recursos de hello, implemente una nueva área de trabajo de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="ccb7d-136">Una vez completada la implementación de hello, resulta sencillo tooaccess propiedades del área de trabajo de Hola que implementó.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="ccb7d-137">Por ejemplo, puede tener acceso a Hola el Token de clave principal.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="ccb7d-138">Otra manera tooretrieve símbolos (tokens) de área de trabajo existente es toouse Hola comando Invoke-AzureRmResourceAction.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="ccb7d-139">Por ejemplo, puede enumerar Hola principal y secundaria símbolos (tokens) de todas las áreas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="ccb7d-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="ccb7d-140">Después de aprovisiona el área de trabajo de hello, también puede automatizar muchas tareas de estudio de aprendizaje automático de Azure con hello [módulo de PowerShell para el aprendizaje automático de Azure](http://aka.ms/amlps).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccb7d-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccb7d-141">Next Steps</span></span>
* <span data-ttu-id="ccb7d-142">Obtenga más información sobre la [creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="ccb7d-143">Eche un vistazo a hello [repositorio de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="ccb7d-144">Vea este vídeo acerca de [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span><span class="sxs-lookup"><span data-stu-id="ccb7d-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
