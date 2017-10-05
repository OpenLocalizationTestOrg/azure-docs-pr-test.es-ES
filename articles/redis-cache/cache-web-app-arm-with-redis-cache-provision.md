---
title: "Aprovisionamiento de aplicación web con Caché de Redis"
description: "Use una plantilla de Administrador de recursos de Azure para implementar una aplicación web con Caché en Redis."
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
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="50c18-103">Creación de una aplicación web y Caché en Redis mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="50c18-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="50c18-104">En este tema, aprenderá a crear una plantilla de Administrador de recursos de Azure que implementa una aplicación web de Azure con Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="50c18-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="50c18-105">Aprenderá a definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="50c18-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="50c18-106">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="50c18-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="50c18-107">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="50c18-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="50c18-108">Para ver la plantilla completa, consulte [Plantilla Aplicación web con Caché en Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="50c18-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="50c18-109">Lo que implementará</span><span class="sxs-lookup"><span data-stu-id="50c18-109">What you will deploy</span></span>
<span data-ttu-id="50c18-110">En esta plantilla, implementará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="50c18-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="50c18-111">Aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="50c18-111">Azure Web App</span></span>
* <span data-ttu-id="50c18-112">Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="50c18-112">Azure Redis Cache.</span></span>

<span data-ttu-id="50c18-113">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="50c18-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="50c18-114">[![Implementación en Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="50c18-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="50c18-115">Parámetros para especificar</span><span class="sxs-lookup"><span data-stu-id="50c18-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="50c18-116">Variables de nombres</span><span class="sxs-lookup"><span data-stu-id="50c18-116">Variables for names</span></span>
<span data-ttu-id="50c18-117">Esta plantilla usa variables para construir los nombres de los recursos.</span><span class="sxs-lookup"><span data-stu-id="50c18-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="50c18-118">Usa la función [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) para construir un valor basado en el identificador del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="50c18-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="50c18-119">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="50c18-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="50c18-120">Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="50c18-120">Redis Cache</span></span>
<span data-ttu-id="50c18-121">Crea Caché en Redis de Azure que se usa con la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="50c18-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="50c18-122">El nombre de la memoria caché se especifica en la variable **cacheName** .</span><span class="sxs-lookup"><span data-stu-id="50c18-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="50c18-123">La plantilla crea la memoria caché en la misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="50c18-123">The template creates the cache in the same location as the resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="50c18-124">Aplicación web</span><span class="sxs-lookup"><span data-stu-id="50c18-124">Web app</span></span>
<span data-ttu-id="50c18-125">Crea la aplicación web con el nombre especificado en la variable **webSiteName** .</span><span class="sxs-lookup"><span data-stu-id="50c18-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="50c18-126">Observe que la aplicación web está configurada con las propiedades de configuración de la aplicación que permiten trabajar con Caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="50c18-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="50c18-127">Esta configuración de la aplicación se crea dinámicamente de acuerdo con los valores proporcionados durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="50c18-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="50c18-128">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="50c18-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="50c18-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50c18-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="50c18-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="50c18-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
