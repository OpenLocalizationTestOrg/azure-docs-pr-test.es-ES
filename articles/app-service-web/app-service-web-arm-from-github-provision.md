---
title: "Implementación de una aplicación web vinculada a un repositorio de GitHub | Microsoft Docs"
description: "Use una plantilla de Administrador de recursos de Azure para implementar una aplicación web que contenga un proyecto de un repositorio de GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="12c05-103">Implementación de una aplicación web vinculada a un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="12c05-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="12c05-104">En este tema, aprenderá a crear una plantilla de Administrador de recursos de Azure que implementa una aplicación web que está vinculada a un proyecto en un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="12c05-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="12c05-105">Aprenderá a definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="12c05-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="12c05-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="12c05-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="12c05-107">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="12c05-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="12c05-108">Para la plantilla completa, consulte [Aplicación web vinculada a la plantilla de GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="12c05-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="12c05-109">Lo que implementará</span><span class="sxs-lookup"><span data-stu-id="12c05-109">What you will deploy</span></span>
<span data-ttu-id="12c05-110">Con esta plantilla, implementará una aplicación web que contiene el código de un proyecto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="12c05-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="12c05-111">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="12c05-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="12c05-112">[![Implementación en Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="12c05-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="12c05-113">Parámetros</span><span class="sxs-lookup"><span data-stu-id="12c05-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="12c05-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="12c05-114">repoURL</span></span>
<span data-ttu-id="12c05-115">La dirección URL del repositorio GitHub que contiene el proyecto que se va a implementar.</span><span class="sxs-lookup"><span data-stu-id="12c05-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="12c05-116">Este parámetro contiene un valor predeterminado, pero la finalidad de este valor es únicamente mostrarle cómo proporcionar la dirección URL del repositorio.</span><span class="sxs-lookup"><span data-stu-id="12c05-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="12c05-117">Puede usar este valor cuando pruebe la plantilla, pero lo más seguro es que quiera proporcionar la dirección URL de su propio repositorio cuando trabaje con la plantilla.</span><span class="sxs-lookup"><span data-stu-id="12c05-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="12c05-118">branch</span><span class="sxs-lookup"><span data-stu-id="12c05-118">branch</span></span>
<span data-ttu-id="12c05-119">La rama del repositorio que se va a usar al implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12c05-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="12c05-120">El valor predeterminado es maestro, pero puede proporcionar el nombre de cualquier rama del repositorio que desee implementar.</span><span class="sxs-lookup"><span data-stu-id="12c05-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="12c05-121">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="12c05-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="12c05-122">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="12c05-122">Web app</span></span>
<span data-ttu-id="12c05-123">Crea la aplicación web que está vinculada al proyecto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="12c05-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="12c05-124">Especifique el nombre de la aplicación web a través del parámetro **siteName** y la ubicación de la aplicación web a través del parámetro **siteLocation**.</span><span class="sxs-lookup"><span data-stu-id="12c05-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="12c05-125">En el elemento **dependsOn** , la plantilla define la aplicación web como dependiente del plan de hospedaje de servicio.</span><span class="sxs-lookup"><span data-stu-id="12c05-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="12c05-126">Puesto que depende del plan de hospedaje, la aplicación web no se crea hasta que ha terminado de crearse el plan de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="12c05-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="12c05-127">El elemento **dependsOn** solo se usa para especificar el orden de implementación.</span><span class="sxs-lookup"><span data-stu-id="12c05-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="12c05-128">Si no marca la aplicación web como dependientes en el plan de hospedaje, el Administrador de recursos de Azure intentará crear ambos recursos al mismo tiempo y puede recibir un error si la aplicación web se crea antes que el plan de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="12c05-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="12c05-129">La aplicación web también tiene un recurso secundario que se define en la sección sobre **recursos** posterior.</span><span class="sxs-lookup"><span data-stu-id="12c05-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="12c05-130">Este recurso secundario define el control de código fuente para el proyecto implementado con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="12c05-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="12c05-131">En esta plantilla, el control de código fuente está vinculado a un repositorio de GitHub determinado.</span><span class="sxs-lookup"><span data-stu-id="12c05-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="12c05-132">El repositorio de GitHub se define con el código **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** Podría codificar de forma rígida la dirección URL del repositorio cuando desee crear una plantilla que implemente de forma repetida un único proyecto y se requiera el número mínimo de parámetros.</span><span class="sxs-lookup"><span data-stu-id="12c05-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="12c05-133">En lugar de codificar de forma rígida la dirección URL del repositorio, puede agregar un parámetro para ella y usar ese valor para la propiedad **RepoUrl**.</span><span class="sxs-lookup"><span data-stu-id="12c05-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="12c05-134">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="12c05-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="12c05-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12c05-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="12c05-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="12c05-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="12c05-137">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="12c05-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="12c05-138">Para el contenido del archivo JSON de parámetros, consulte [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="12c05-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

