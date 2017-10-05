---
title: Aprovisionamiento de Redis Cache mediante Azure Resource Manager | Microsoft Docs
description: "Use una plantilla del Administrador de recursos de Azure para implementar Caché en Redis de Azure."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="82c8c-103">Creación de una Caché en Redis mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="82c8c-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="82c8c-104">En este tema, aprenderá a crear una plantilla de Azure Resource Manager que implementa Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="82c8c-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="82c8c-105">La memoria caché se puede usar con una cuenta de almacenamiento existente para mantener los datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="82c8c-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="82c8c-106">Aprenderá a definir los recursos que se implementan y los parámetros que se especifican cuando se ejecuta la implementación.</span><span class="sxs-lookup"><span data-stu-id="82c8c-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="82c8c-107">Puede usar esta plantilla para sus propias implementaciones o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="82c8c-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="82c8c-108">Actualmente, se comparten los ajustes de configuración de diagnóstico para todas las cachés de la misma región para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="82c8c-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="82c8c-109">Actualizar una caché en la región afectará a todas las demás cachés de la región.</span><span class="sxs-lookup"><span data-stu-id="82c8c-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="82c8c-110">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="82c8c-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="82c8c-111">Para ver la plantilla completa, consulte [Plantilla Caché en Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="82c8c-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="82c8c-112">Las plantillas de Resource Manager para el nuevo [nivel Premium](cache-premium-tier-intro.md) están disponibles.</span><span class="sxs-lookup"><span data-stu-id="82c8c-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="82c8c-113">Crear una caché en Redis Premium con agrupación en clústeres</span><span class="sxs-lookup"><span data-stu-id="82c8c-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="82c8c-114">Crear una caché en Redis Premium con persistencia de datos</span><span class="sxs-lookup"><span data-stu-id="82c8c-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="82c8c-115">Crear una caché en Redis Premium con una red virtual y agrupación en clústeres opcional</span><span class="sxs-lookup"><span data-stu-id="82c8c-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="82c8c-116">Para buscar las últimas plantillas, diríjase a [Plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) y busque `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="82c8c-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="82c8c-117">Lo que implementará</span><span class="sxs-lookup"><span data-stu-id="82c8c-117">What you will deploy</span></span>
<span data-ttu-id="82c8c-118">En esta plantilla, implementará una caché en Redis de Azure que utiliza una cuenta de almacenamiento de datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="82c8c-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="82c8c-119">Para ejecutar automáticamente la implementación, haga clic en el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="82c8c-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="82c8c-120">[![Implementación en Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="82c8c-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="82c8c-121">Parámetros</span><span class="sxs-lookup"><span data-stu-id="82c8c-121">Parameters</span></span>
<span data-ttu-id="82c8c-122">Con el Administrador de recursos de Azure, se definen los parámetros de los valores que desea especificar al implementar la plantilla.</span><span class="sxs-lookup"><span data-stu-id="82c8c-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="82c8c-123">La plantilla incluye una sección denominada Parámetros que contiene todos los valores de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="82c8c-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="82c8c-124">Debe definir un parámetro para esos valores que variarán según el proyecto que vaya a implementar o según el entorno en el que vaya a realizar la implementación.</span><span class="sxs-lookup"><span data-stu-id="82c8c-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="82c8c-125">No defina parámetros para valores que siempre permanezcan igual.</span><span class="sxs-lookup"><span data-stu-id="82c8c-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="82c8c-126">Cada valor de parámetro se usa en la plantilla para definir los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="82c8c-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="82c8c-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="82c8c-127">redisCacheLocation</span></span>
<span data-ttu-id="82c8c-128">La ubicación de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="82c8c-128">The location of the Redis Cache.</span></span> <span data-ttu-id="82c8c-129">Para un mejor rendimiento, utilice la misma ubicación que la aplicación que se usará con la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="82c8c-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="82c8c-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="82c8c-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="82c8c-131">Nombre de la cuenta de almacenamiento existente que desea usar para el diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="82c8c-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="82c8c-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="82c8c-132">enableNonSslPort</span></span>
<span data-ttu-id="82c8c-133">Valor booleano que indica si se debe permitir el acceso a través de puertos no SSL.</span><span class="sxs-lookup"><span data-stu-id="82c8c-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="82c8c-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="82c8c-134">diagnosticsStatus</span></span>
<span data-ttu-id="82c8c-135">Un valor que indica si están activados los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="82c8c-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="82c8c-136">Utilice ON (activados) u OFF (desactivados).</span><span class="sxs-lookup"><span data-stu-id="82c8c-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="82c8c-137">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="82c8c-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="82c8c-138">Caché en Redis</span><span class="sxs-lookup"><span data-stu-id="82c8c-138">Redis Cache</span></span>
<span data-ttu-id="82c8c-139">Crea Caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="82c8c-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="82c8c-140">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="82c8c-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="82c8c-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82c8c-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="82c8c-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="82c8c-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


