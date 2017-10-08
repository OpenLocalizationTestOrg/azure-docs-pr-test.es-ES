---
title: "aaaDeploy una aplicación web que está vinculado el repositorio de GitHub de tooa | Documentos de Microsoft"
description: "Utilice un toodeploy de plantilla de Azure Resource Manager una aplicación web que contiene un proyecto desde un repositorio de GitHub."
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
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="d7c24-103">Implementar un repositorio de GitHub de web app vinculado tooa</span><span class="sxs-lookup"><span data-stu-id="d7c24-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="d7c24-104">En este tema, obtendrá información sobre cómo toocreate una plantilla de Azure Resource Manager que se puede implementar una aplicación web que está había vinculado tooa proyecto en un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7c24-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="d7c24-105">Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7c24-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="d7c24-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="d7c24-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="d7c24-107">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d7c24-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d7c24-108">Para la plantilla de hello completa, consulte [Web App vinculado plantilla tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="d7c24-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="d7c24-109">Lo que implementará</span><span class="sxs-lookup"><span data-stu-id="d7c24-109">What you will deploy</span></span>
<span data-ttu-id="d7c24-110">Con esta plantilla, se implementará una aplicación web que contiene el código de hello desde un proyecto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7c24-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="d7c24-111">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="d7c24-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="d7c24-112">[![Implementar tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d7c24-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d7c24-113">parameters</span><span class="sxs-lookup"><span data-stu-id="d7c24-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="d7c24-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="d7c24-114">repoURL</span></span>
<span data-ttu-id="d7c24-115">dirección URL de Hello para el repositorio de GitHub que contiene Hola proyecto toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d7c24-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="d7c24-116">Este parámetro contiene un valor predeterminado, pero este valor es solo previsto tooshow también cómo tooprovide Hola dirección URL para el repositorio.</span><span class="sxs-lookup"><span data-stu-id="d7c24-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="d7c24-117">Puede usar este valor pruebas plantilla Hola pero resulta conveniente tooprovide Hola URL su propio repositorio cuando se trabaja con plantilla Hola.</span><span class="sxs-lookup"><span data-stu-id="d7c24-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="d7c24-118">branch</span><span class="sxs-lookup"><span data-stu-id="d7c24-118">branch</span></span>
<span data-ttu-id="d7c24-119">rama de Hola de hello repositorio toouse al implementar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d7c24-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="d7c24-120">valor predeterminado de Hello es principal, pero puede proporcionar nombre Hola de alguna de las bifurcaciones en el repositorio de Hola que desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d7c24-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="d7c24-121">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="d7c24-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="d7c24-122">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="d7c24-122">Web app</span></span>
<span data-ttu-id="d7c24-123">Crea la aplicación web de hello que está vinculado toohello proyecto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7c24-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="d7c24-124">Especificar nombre de Hola de aplicación web de hello a través de hello **siteName** parámetro y la ubicación de Hola de aplicación web de hello a través de hello **siteLocation** parámetro.</span><span class="sxs-lookup"><span data-stu-id="d7c24-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="d7c24-125">Hola **dependsOn** elemento, plantilla de Hola define aplicación web de hello como dependiente de plan de hospedaje de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d7c24-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="d7c24-126">Dado que es dependiente de hello plan de hospedaje, aplicación web de hello no se crea hasta Hola plan de hospedaje ha terminado de crear.</span><span class="sxs-lookup"><span data-stu-id="d7c24-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="d7c24-127">Hola **dependsOn** elemento es solo el orden de implementación toospecify usado.</span><span class="sxs-lookup"><span data-stu-id="d7c24-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="d7c24-128">Si no marca la aplicación web de hello como dependiente de plan de hospedaje de Hola, Azure Resource Manager intentará toocreate los recursos en hello mismo tiempo y puede que aparezca un error si se crea la aplicación web de hello antes de hello plan de hospedaje.</span><span class="sxs-lookup"><span data-stu-id="d7c24-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="d7c24-129">aplicación web de Hello también tiene un recurso secundario que se define en **recursos** sección más adelante.</span><span class="sxs-lookup"><span data-stu-id="d7c24-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="d7c24-130">Este recurso secundario define el control de código fuente para proyecto de hello implementado con la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="d7c24-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="d7c24-131">En esta plantilla, control de código fuente de hello es vinculado tooa repositorio de GitHub determinado.</span><span class="sxs-lookup"><span data-stu-id="d7c24-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="d7c24-132">repositorio de GitHub de Hola se define con código de hello **"Dirección URL del repositorio": "https://github.com/davidebbo-test/Mvc52Application.git"** podría URL del repositorio de codificar de forma rígida hello cuando desee toocreate una plantilla que implementa varias veces una proyecto solo requieren un mínimo de parámetros Hola.</span><span class="sxs-lookup"><span data-stu-id="d7c24-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="d7c24-133">En lugar de codificar de forma rígida Hola dirección URL del repositorio, puede agregar un parámetro de dirección URL de repositorio de Hola y usar ese valor para hello **dirección URL del repositorio** propiedad.</span><span class="sxs-lookup"><span data-stu-id="d7c24-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="d7c24-134">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="d7c24-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="d7c24-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7c24-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="d7c24-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d7c24-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="d7c24-137">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="d7c24-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="d7c24-138">Para el contenido del archivo JSON de parámetros de hello, consulte [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="d7c24-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

