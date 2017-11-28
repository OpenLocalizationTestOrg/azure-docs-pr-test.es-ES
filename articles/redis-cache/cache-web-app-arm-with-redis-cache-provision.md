---
title: "aaaProvision aplicación Web con caché en Redis"
description: "Use la aplicación web de Azure Resource Manager plantilla toodeploy con caché en Redis."
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="af7f6-103">Creación de una aplicación web y Caché en Redis mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="af7f6-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="af7f6-104">En este tema, aprenderá cómo toocreate una plantilla de Azure Resource Manager que se puede implementar una aplicación Web de Azure con caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="af7f6-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="af7f6-105">Obtendrá información sobre cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="af7f6-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="af7f6-106">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="af7f6-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="af7f6-107">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="af7f6-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="af7f6-108">Para la plantilla de hello completa, consulte [aplicación Web con la plantilla de caché en Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="af7f6-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="af7f6-109">Lo que implementará</span><span class="sxs-lookup"><span data-stu-id="af7f6-109">What you will deploy</span></span>
<span data-ttu-id="af7f6-110">En esta plantilla, implementará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="af7f6-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="af7f6-111">Aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="af7f6-111">Azure Web App</span></span>
* <span data-ttu-id="af7f6-112">Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="af7f6-112">Azure Redis Cache.</span></span>

<span data-ttu-id="af7f6-113">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="af7f6-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="af7f6-114">[![Implementar tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="af7f6-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="af7f6-115">Parámetros toospecify</span><span class="sxs-lookup"><span data-stu-id="af7f6-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="af7f6-116">Variables de nombres</span><span class="sxs-lookup"><span data-stu-id="af7f6-116">Variables for names</span></span>
<span data-ttu-id="af7f6-117">Esta plantilla utiliza nombres de tooconstruct de variables para los recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af7f6-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="af7f6-118">Usa hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) función tooconstruct un valor basado en el identificador de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="af7f6-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="af7f6-119">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="af7f6-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="af7f6-120">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="af7f6-120">Redis Cache</span></span>
<span data-ttu-id="af7f6-121">Crea Hola caché Redis de Azure que se usa con la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="af7f6-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="af7f6-122">se especifica el nombre de Hola de caché de Hola Hola **cacheName** variable.</span><span class="sxs-lookup"><span data-stu-id="af7f6-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="af7f6-123">plantilla de Hello crea caché Hola Hola misma ubicación que el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af7f6-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="af7f6-124">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="af7f6-124">Web app</span></span>
<span data-ttu-id="af7f6-125">Crea la aplicación web de hello con nombre especificado en hello **webSiteName** variable.</span><span class="sxs-lookup"><span data-stu-id="af7f6-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="af7f6-126">Tenga en cuenta que dicha aplicación Hola se configura con aplicación establecer las propiedades que permiten su toowork con hello caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="af7f6-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="af7f6-127">Esta configuración de la aplicación se crea dinámicamente de acuerdo con los valores proporcionados durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="af7f6-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="af7f6-128">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="af7f6-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="af7f6-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af7f6-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="af7f6-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="af7f6-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
