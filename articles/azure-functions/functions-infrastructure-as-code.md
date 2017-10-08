---
title: "implementación de recursos de aaaAutomate para una aplicación de la función en funciones de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toobuild una plantilla de Azure Resource Manager que implementa la aplicación de la función."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, arquitectura sin servidor, infraestructura como código, azure resource manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="5cb00-104">Automatización de la implementación de recursos para una aplicación de función en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5cb00-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="5cb00-105">Puede usar un toodeploy de plantilla una aplicación de la función de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb00-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="5cb00-106">En este artículo se describe Hola requerido recursos y parámetros para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="5cb00-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="5cb00-107">Tendrá que toodeploy obtener recursos adicionales, dependiendo de hello [desencadenadores y enlaces](functions-triggers-bindings.md) en la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="5cb00-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="5cb00-108">Para más información sobre la creación de plantillas, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5cb00-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="5cb00-109">Para obtener las plantillas de ejemplo, vea:</span><span class="sxs-lookup"><span data-stu-id="5cb00-109">For sample templates, see:</span></span>
- <span data-ttu-id="5cb00-110">[Aplicación de función en el plan de consumo]</span><span class="sxs-lookup"><span data-stu-id="5cb00-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="5cb00-111">[Aplicación de función en el plan de App Service]</span><span class="sxs-lookup"><span data-stu-id="5cb00-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="5cb00-112">Recursos necesarios</span><span class="sxs-lookup"><span data-stu-id="5cb00-112">Required resources</span></span>

<span data-ttu-id="5cb00-113">Una aplicación de función requiere estos recursos:</span><span class="sxs-lookup"><span data-stu-id="5cb00-113">A function app requires these resources:</span></span>

* <span data-ttu-id="5cb00-114">Una cuenta de [Azure Storage](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="5cb00-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="5cb00-115">Un plan de hospedaje (plan de consumo o plan de App Service).</span><span class="sxs-lookup"><span data-stu-id="5cb00-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="5cb00-116">Una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="5cb00-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="5cb00-117">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="5cb00-117">Storage account</span></span>

<span data-ttu-id="5cb00-118">Se necesita una cuenta de Azure Storage para una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="5cb00-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="5cb00-119">Se necesita una cuenta de uso general que admita blobs, tablas, colas y archivos.</span><span class="sxs-lookup"><span data-stu-id="5cb00-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="5cb00-120">Para más información, vea [Requisitos de la cuenta de almacenamiento de Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="5cb00-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="5cb00-121">Además, Hola propiedades `AzureWebJobsStorage` y `AzureWebJobsDashboard` debe especificarse como configuración de la aplicación en la configuración de sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5cb00-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="5cb00-122">en tiempo de ejecución de funciones de Azure de Hello usa hello `AzureWebJobsStorage` toocreate las colas internas de la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="5cb00-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="5cb00-123">Hola la cadena de conexión `AzureWebJobsDashboard` es toolog usado tooAzure tabla almacenamiento y power hello **Monitor** portal Hola de.</span><span class="sxs-lookup"><span data-stu-id="5cb00-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="5cb00-124">Estas propiedades se especifican en hello `appSettings` colección Hola `siteConfig` objeto:</span><span class="sxs-lookup"><span data-stu-id="5cb00-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="5cb00-125">Plan de hospedaje</span><span class="sxs-lookup"><span data-stu-id="5cb00-125">Hosting plan</span></span>

<span data-ttu-id="5cb00-126">definición de Hola de hello plan de hospedaje varía, dependiendo de si utiliza un plan de consumo o servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5cb00-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="5cb00-127">Vea [implementar una aplicación de la función en el plan de consumo de hello](#consumption) y [implementar una aplicación de función en el plan de servicio de aplicación Hola](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="5cb00-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="5cb00-128">Aplicación de función</span><span class="sxs-lookup"><span data-stu-id="5cb00-128">Function app</span></span>

<span data-ttu-id="5cb00-129">recurso de la función aplicación Hola se define mediante un recurso de tipo **Microsoft.Web/Site** y tipo **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="5cb00-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="5cb00-130">Implementar una aplicación de la función en el plan de consumo de Hola</span><span class="sxs-lookup"><span data-stu-id="5cb00-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="5cb00-131">Puede ejecutar una aplicación de función en dos modos diferentes: Hola hello plan de servicio de aplicaciones y el plan de consumo.</span><span class="sxs-lookup"><span data-stu-id="5cb00-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="5cb00-132">plan de consumo de Hello asigna automáticamente la capacidad de proceso cuando el código se ejecuta, admita la ampliación horizontal como carga de toohandle necesarios y, a continuación, se escala hacia abajo cuando no se está ejecutando el código.</span><span class="sxs-lookup"><span data-stu-id="5cb00-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="5cb00-133">Por lo tanto, no tiene toopay para máquinas virtuales inactivas y no tiene capacidad de tooreserve de antemano.</span><span class="sxs-lookup"><span data-stu-id="5cb00-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="5cb00-134">toolearn más sobre el hospedaje de planes, consulte [planes de servicio de aplicaciones y de consumo de funciones de Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="5cb00-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="5cb00-135">Para obtener una plantilla de Azure Resource Manager de ejemplo, vea [Aplicación de función en el plan de consumo].</span><span class="sxs-lookup"><span data-stu-id="5cb00-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="5cb00-136">Crear un plan de consumo</span><span class="sxs-lookup"><span data-stu-id="5cb00-136">Create a Consumption plan</span></span>

<span data-ttu-id="5cb00-137">Un plan de consumo es un tipo especial de recurso de "granja de servidores".</span><span class="sxs-lookup"><span data-stu-id="5cb00-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="5cb00-138">Se especifica mediante hello `Dynamic` valor de hello `computeMode` y `sku` propiedades:</span><span class="sxs-lookup"><span data-stu-id="5cb00-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="5cb00-139">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="5cb00-139">Create a function app</span></span>

<span data-ttu-id="5cb00-140">Además, un plan de consumo requiere dos configuraciones adicionales en la configuración de sitio de hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` y `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="5cb00-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="5cb00-141">Estas propiedades configuran Hola almacenamiento cuenta y la ruta donde se almacenan el código de aplicación de función de Hola y la configuración.</span><span class="sxs-lookup"><span data-stu-id="5cb00-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="5cb00-142">Implementar una aplicación de la función en hello plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="5cb00-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="5cb00-143">Hola plan de servicio de aplicaciones, la aplicación de la función se ejecuta en máquinas virtuales dedicadas en Basic, Standard y Premium SKU, aplicaciones tooweb similar.</span><span class="sxs-lookup"><span data-stu-id="5cb00-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="5cb00-144">Para obtener más información acerca del funcionamiento de hello plan de servicio de aplicaciones, vea hello [información general detallada de planes de servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cb00-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="5cb00-145">Para obtener una plantilla de Azure Resource Manager de ejemplo, vea [Aplicación de función en el plan de App Service].</span><span class="sxs-lookup"><span data-stu-id="5cb00-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5cb00-146">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="5cb00-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="5cb00-147">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="5cb00-147">Create a function app</span></span> 

<span data-ttu-id="5cb00-148">Después de seleccionar una opción de escalado, cree una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="5cb00-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="5cb00-149">aplicación Hello es contenedor de Hola que contiene todas las funciones.</span><span class="sxs-lookup"><span data-stu-id="5cb00-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="5cb00-150">Una aplicación de función tiene muchos recursos secundarios que puede usar en la implementación, incluidas la configuración de la aplicación y las opciones de control del código fuente.</span><span class="sxs-lookup"><span data-stu-id="5cb00-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="5cb00-151">También puede elegir hello tooremove **sourcecontrols** recurso secundario y use otra [opción de implementación](functions-continuous-deployment.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="5cb00-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cb00-152">toosuccessfully implementar su aplicación mediante el Administrador de recursos de Azure, es importante toounderstand forma en que se implementan los recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb00-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="5cb00-153">En el siguiente ejemplo de Hola, se aplican las configuraciones de nivel superior mediante **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="5cb00-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="5cb00-154">Es importante tooset nivel estas configuraciones en un principio, porque transmite información toohello funciones en tiempo de ejecución e implementación el motor.</span><span class="sxs-lookup"><span data-stu-id="5cb00-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="5cb00-155">Se necesita información de nivel superior antes de secundarios de hello **sourcecontrols/web** se aplica un recurso.</span><span class="sxs-lookup"><span data-stu-id="5cb00-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="5cb00-156">Aunque es posible tooconfigure estos valores en Hola nivel secundario **config/appSettings** recurso, en algunos casos se debe implementar la aplicación de la función *antes de* **config/appSettings**  se aplica.</span><span class="sxs-lookup"><span data-stu-id="5cb00-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="5cb00-157">Por ejemplo, cuando se usan funciones con [Logic Apps](../logic-apps/index.md), las funciones son una dependencia de otro recurso.</span><span class="sxs-lookup"><span data-stu-id="5cb00-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="5cb00-158">Esta plantilla utiliza hello [proyecto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valor de la configuración de aplicación, que establece el directorio base hello en qué Hola motor de implementación de funciones (Kudu) es para código que se pueden implementar.</span><span class="sxs-lookup"><span data-stu-id="5cb00-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="5cb00-159">En nuestro repositorio, nuestro funciones están en una subcarpeta de hello **src** carpeta.</span><span class="sxs-lookup"><span data-stu-id="5cb00-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="5cb00-160">Por lo tanto, en el anterior ejemplo de Hola, establecemos el valor de configuración de aplicación de hello demasiado`src`.</span><span class="sxs-lookup"><span data-stu-id="5cb00-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="5cb00-161">Si las funciones están en la raíz de hello del repositorio, o si no va a implementar desde el control de código fuente, puede quitar este valor de configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="5cb00-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="5cb00-162">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="5cb00-162">Deploy your template</span></span>

<span data-ttu-id="5cb00-163">Puede usar cualquiera de hello después formas toodeploy la plantilla:</span><span class="sxs-lookup"><span data-stu-id="5cb00-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="5cb00-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cb00-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="5cb00-165">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5cb00-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="5cb00-166">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5cb00-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="5cb00-167">API DE REST</span><span class="sxs-lookup"><span data-stu-id="5cb00-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="5cb00-168">Botón tooAzure implementar</span><span class="sxs-lookup"><span data-stu-id="5cb00-168">Deploy tooAzure button</span></span>

<span data-ttu-id="5cb00-169">Reemplace ```<url-encoded-path-to-azuredeploy-json>``` con un [codificados de dirección URL](https://www.bing.com/search?q=url+encode) versión de la ruta de acceso sin procesar de Hola de su `azuredeploy.json` archivo en GitHub.</span><span class="sxs-lookup"><span data-stu-id="5cb00-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="5cb00-170">A continuación se muestra un ejemplo que usa Markdown:</span><span class="sxs-lookup"><span data-stu-id="5cb00-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="5cb00-171">A continuación se muestra un ejemplo que usa HTML:</span><span class="sxs-lookup"><span data-stu-id="5cb00-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="5cb00-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cb00-172">Next steps</span></span>

<span data-ttu-id="5cb00-173">Más información acerca de cómo toodevelop y configurar las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="5cb00-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="5cb00-174">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="5cb00-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="5cb00-175">Funcionamiento de tooconfigure Azure en configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5cb00-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="5cb00-176">Creación de su primera función de Azure</span><span class="sxs-lookup"><span data-stu-id="5cb00-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Aplicación de función en el plan de consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Aplicación de función en el plan de App Service]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
