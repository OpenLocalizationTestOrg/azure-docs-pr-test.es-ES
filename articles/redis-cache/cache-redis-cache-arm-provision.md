---
title: "aaaProvision una caché en Redis mediante el Administrador de recursos de Azure | Documentos de Microsoft"
description: "Use el Administrador de recursos de Azure plantilla toodeploy una caché en Redis de Azure."
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="63659-103">Creación de una Caché en Redis mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="63659-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="63659-104">En este tema, aprenderá cómo toocreate una plantilla de Azure Resource Manager que implementa una caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="63659-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="63659-105">caché de Hello puede utilizarse con un almacenamiento cuenta tookeep diagnóstico los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="63659-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="63659-106">También aprenderá cómo toodefine qué recursos se implementan y cómo toodefine parámetros que especifican cuando se ejecuta la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="63659-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="63659-107">Puede usar esta plantilla para sus propias implementaciones o personalizarlo toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="63659-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="63659-108">Actualmente, se comparten la configuración de diagnóstico para todas las memorias caché en hello misma región para una suscripción.</span><span class="sxs-lookup"><span data-stu-id="63659-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="63659-109">La actualización de una memoria caché en la región de hello afecta a todas las demás cachés región Hola.</span><span class="sxs-lookup"><span data-stu-id="63659-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="63659-110">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="63659-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="63659-111">Para la plantilla de hello completa, consulte [plantilla caché de Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="63659-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="63659-112">Plantillas de administrador de recursos para hello nueva [nivel Premium](cache-premium-tier-intro.md) están disponibles.</span><span class="sxs-lookup"><span data-stu-id="63659-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="63659-113">Crear una caché en Redis Premium con agrupación en clústeres</span><span class="sxs-lookup"><span data-stu-id="63659-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="63659-114">Crear una caché en Redis Premium con persistencia de datos</span><span class="sxs-lookup"><span data-stu-id="63659-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="63659-115">Crear una caché en Redis Premium con una red virtual y agrupación en clústeres opcional</span><span class="sxs-lookup"><span data-stu-id="63659-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="63659-116">toocheck para las plantillas de hello más recientes, consulte [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/) y busque `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="63659-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="63659-117">Lo que implementará</span><span class="sxs-lookup"><span data-stu-id="63659-117">What you will deploy</span></span>
<span data-ttu-id="63659-118">En esta plantilla, implementará una caché en Redis de Azure que utiliza una cuenta de almacenamiento de datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="63659-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="63659-119">toorun Hola implementación automáticamente, haga clic en hello después de botón:</span><span class="sxs-lookup"><span data-stu-id="63659-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="63659-120">[![Implementar tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="63659-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="63659-121">parameters</span><span class="sxs-lookup"><span data-stu-id="63659-121">Parameters</span></span>
<span data-ttu-id="63659-122">Con el Administrador de recursos de Azure, se definen parámetros para los valores que desee toospecify cuando se implementa Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="63659-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="63659-123">plantilla de Hello incluye una sección denominada parámetros que contiene todos los valores de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="63659-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="63659-124">Debe definir un parámetro para aquellos valores que varían en función de que va a implementar el proyecto de Hola o según va a implementar en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="63659-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="63659-125">No se define parámetros para valores que permanezcan siempre Hola igual.</span><span class="sxs-lookup"><span data-stu-id="63659-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="63659-126">Cada valor de parámetro se usa en hello plantilla toodefine Hola los recursos que se implementan.</span><span class="sxs-lookup"><span data-stu-id="63659-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="63659-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="63659-127">redisCacheLocation</span></span>
<span data-ttu-id="63659-128">ubicación de Hola de hello caché en Redis.</span><span class="sxs-lookup"><span data-stu-id="63659-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="63659-129">Para un rendimiento óptimo, utilice Hola misma ubicación como Hola toobe de aplicación que se usa con la caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="63659-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="63659-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="63659-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="63659-131">nombre de Hola de hello toouse de cuenta de almacenamiento existente para diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="63659-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="63659-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="63659-132">enableNonSslPort</span></span>
<span data-ttu-id="63659-133">Un valor booleano que indica si tooallow acceden a través de puertos no SSL.</span><span class="sxs-lookup"><span data-stu-id="63659-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="63659-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="63659-134">diagnosticsStatus</span></span>
<span data-ttu-id="63659-135">Un valor que indica si están activados los diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="63659-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="63659-136">Utilice ON (activados) u OFF (desactivados).</span><span class="sxs-lookup"><span data-stu-id="63659-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="63659-137">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="63659-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="63659-138">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="63659-138">Redis Cache</span></span>
<span data-ttu-id="63659-139">Crea Hola caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="63659-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="63659-140">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="63659-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="63659-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63659-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="63659-142">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="63659-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


