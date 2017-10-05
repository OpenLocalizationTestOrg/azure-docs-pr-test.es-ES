---
title: "Automatización de la implementación de recursos para una aplicación de función en Azure Functions | Microsoft Docs"
description: "Obtenga información sobre cómo crear una plantilla de Azure Resource Manager que implemente su aplicación de función."
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
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="92980-104">Automatización de la implementación de recursos para una aplicación de función en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="92980-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="92980-105">Puede usar una plantilla de Azure Resource Manager para implementar una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="92980-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="92980-106">En este artículo se describen los recursos y los parámetros necesarios para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="92980-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="92980-107">Es posible que tenga que implementar recursos adicionales, dependiendo de los [desencadenadores y enlaces](functions-triggers-bindings.md) de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="92980-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="92980-108">Para más información sobre la creación de plantillas, consulte [Creación de plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="92980-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="92980-109">Para obtener las plantillas de ejemplo, vea:</span><span class="sxs-lookup"><span data-stu-id="92980-109">For sample templates, see:</span></span>
- <span data-ttu-id="92980-110">[Aplicación de función en el plan de consumo]</span><span class="sxs-lookup"><span data-stu-id="92980-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="92980-111">[Aplicación de función en el plan de App Service]</span><span class="sxs-lookup"><span data-stu-id="92980-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="92980-112">Recursos necesarios</span><span class="sxs-lookup"><span data-stu-id="92980-112">Required resources</span></span>

<span data-ttu-id="92980-113">Una aplicación de función requiere estos recursos:</span><span class="sxs-lookup"><span data-stu-id="92980-113">A function app requires these resources:</span></span>

* <span data-ttu-id="92980-114">Una cuenta de [Azure Storage](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="92980-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="92980-115">Un plan de hospedaje (plan de consumo o plan de App Service).</span><span class="sxs-lookup"><span data-stu-id="92980-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="92980-116">Una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="92980-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="92980-117">Cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="92980-117">Storage account</span></span>

<span data-ttu-id="92980-118">Se necesita una cuenta de Azure Storage para una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="92980-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="92980-119">Se necesita una cuenta de uso general que admita blobs, tablas, colas y archivos.</span><span class="sxs-lookup"><span data-stu-id="92980-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="92980-120">Para más información, vea [Requisitos de la cuenta de almacenamiento de Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="92980-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="92980-121">Además, las propiedades `AzureWebJobsStorage` y `AzureWebJobsDashboard` deben especificarse como valores de la aplicación en la configuración del sitio.</span><span class="sxs-lookup"><span data-stu-id="92980-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="92980-122">El tiempo de ejecución de Azure Functions usa la cadena de conexión `AzureWebJobsStorage` para crear colas internas.</span><span class="sxs-lookup"><span data-stu-id="92980-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="92980-123">La cadena de conexión `AzureWebJobsDashboard` se usa para registrar en el almacenamiento de tablas de Azure y alimentar la pestaña **Monitor** en el portal.</span><span class="sxs-lookup"><span data-stu-id="92980-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="92980-124">Estas propiedades se especifican en la colección `appSettings` del objeto `siteConfig`:</span><span class="sxs-lookup"><span data-stu-id="92980-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="92980-125">Plan de hospedaje</span><span class="sxs-lookup"><span data-stu-id="92980-125">Hosting plan</span></span>

<span data-ttu-id="92980-126">La definición del plan de hospedaje varía, dependiendo de si se usa un plan de consumo o un plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="92980-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="92980-127">Vea [Implementar una aplicación de función en el plan de consumo](#consumption) e [Implementar una aplicación de función en el plan de App Service](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="92980-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="92980-128">Aplicación de función</span><span class="sxs-lookup"><span data-stu-id="92980-128">Function app</span></span>

<span data-ttu-id="92980-129">El recurso de aplicación de función se define mediante un recurso de tipo **Microsoft.Web/Site** y tipo **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="92980-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="92980-130">Implementar una aplicación de función en el plan de consumo</span><span class="sxs-lookup"><span data-stu-id="92980-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="92980-131">Puede ejecutar una aplicación de función en dos modos diferentes: el plan de consumo y el plan de App Service.</span><span class="sxs-lookup"><span data-stu-id="92980-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="92980-132">El plan de consumo asigna automáticamente capacidad de proceso cuando se ejecuta el código, se amplía horizontalmente cuando es necesario para gestionar la carga y se reduce horizontalmente cuando no se ejecuta código.</span><span class="sxs-lookup"><span data-stu-id="92980-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="92980-133">Por tanto, no tiene que pagar por máquinas virtuales inactivas y no tiene que reservar capacidad de antemano.</span><span class="sxs-lookup"><span data-stu-id="92980-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="92980-134">Para obtener más información sobre planes de hospedaje, vea [Plan de consumo y plan de App Service de Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="92980-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="92980-135">Para obtener una plantilla de Azure Resource Manager de ejemplo, vea [Aplicación de función en el plan de consumo].</span><span class="sxs-lookup"><span data-stu-id="92980-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="92980-136">Crear un plan de consumo</span><span class="sxs-lookup"><span data-stu-id="92980-136">Create a Consumption plan</span></span>

<span data-ttu-id="92980-137">Un plan de consumo es un tipo especial de recurso de "granja de servidores".</span><span class="sxs-lookup"><span data-stu-id="92980-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="92980-138">Se especifica mediante el valor `Dynamic` para las propiedades `computeMode` y `sku`:</span><span class="sxs-lookup"><span data-stu-id="92980-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="92980-139">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="92980-139">Create a function app</span></span>

<span data-ttu-id="92980-140">Además, un plan de consumo requiere dos configuraciones adicionales en la configuración del sitio: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` y `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="92980-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="92980-141">Estas propiedades configuran la cuenta de almacenamiento y la ruta de acceso del archivo donde se almacenan el código y la configuración de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="92980-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="92980-142">Implementar una aplicación de función en el plan de App Service</span><span class="sxs-lookup"><span data-stu-id="92980-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="92980-143">En el plan de App Service, la aplicación de función se ejecuta en máquinas virtuales dedicadas en las SKU de los niveles Básico, Estándar y Premium, de un modo similar a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="92980-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="92980-144">Para más información acerca del funcionamiento del plan de App Service, consulte [Introducción detallada sobre los planes de Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92980-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="92980-145">Para obtener una plantilla de Azure Resource Manager de ejemplo, vea [Aplicación de función en el plan de App Service].</span><span class="sxs-lookup"><span data-stu-id="92980-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="92980-146">Creación de un plan del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="92980-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="92980-147">Creación de una aplicación de función</span><span class="sxs-lookup"><span data-stu-id="92980-147">Create a function app</span></span> 

<span data-ttu-id="92980-148">Después de seleccionar una opción de escalado, cree una aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="92980-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="92980-149">La aplicación es el contenedor que contiene todas las funciones.</span><span class="sxs-lookup"><span data-stu-id="92980-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="92980-150">Una aplicación de función tiene muchos recursos secundarios que puede usar en la implementación, incluidas la configuración de la aplicación y las opciones de control del código fuente.</span><span class="sxs-lookup"><span data-stu-id="92980-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="92980-151">Es posible que también elija quitar el recurso secundario **sourcecontrols** y usar otra [opción de implementación](functions-continuous-deployment.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="92980-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92980-152">Para implementar la aplicación de forma correcta mediante Azure Resource Manager, es importante comprender cómo se implementan los recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="92980-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="92980-153">En el siguiente ejemplo, se aplican configuraciones de nivel superior mediante **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="92980-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="92980-154">Es importante establecer estas configuraciones en un nivel superior porque transmiten información al motor de implementación y en tiempo de ejecución de Functions.</span><span class="sxs-lookup"><span data-stu-id="92980-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="92980-155">Se necesita información de nivel superior antes de aplicar el recurso secundario **sourcecontrols/web**.</span><span class="sxs-lookup"><span data-stu-id="92980-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="92980-156">Aunque es posible configurar estas opciones en el recurso de nivel secundario **config/appSettings**, en algunos casos debe implementar la aplicación de función *antes de* que se aplique **config/appSettings**.</span><span class="sxs-lookup"><span data-stu-id="92980-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="92980-157">Por ejemplo, cuando se usan funciones con [Logic Apps](../logic-apps/index.md), las funciones son una dependencia de otro recurso.</span><span class="sxs-lookup"><span data-stu-id="92980-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="92980-158">En esta plantilla se usa el valor de configuración de aplicación [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file), que establece el directorio base en el que el motor de implementación de Functions (Kudu) busca código que se pueda implementar.</span><span class="sxs-lookup"><span data-stu-id="92980-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="92980-159">En nuestro repositorio, nuestras funciones están en una subcarpeta de la carpeta **src**.</span><span class="sxs-lookup"><span data-stu-id="92980-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="92980-160">Por tanto, en el ejemplo anterior, se establece el valor de configuración de la aplicación en `src`.</span><span class="sxs-lookup"><span data-stu-id="92980-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="92980-161">Si las funciones se encuentran en la raíz del repositorio, o si no va a implementar desde el control de código fuente, puede quitar este valor de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="92980-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="92980-162">Implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="92980-162">Deploy your template</span></span>

<span data-ttu-id="92980-163">Puede usar cualquiera de los siguientes métodos para implementar la plantilla:</span><span class="sxs-lookup"><span data-stu-id="92980-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="92980-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92980-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="92980-165">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="92980-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="92980-166">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="92980-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="92980-167">API DE REST</span><span class="sxs-lookup"><span data-stu-id="92980-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="92980-168">Botón Implementación en Azure</span><span class="sxs-lookup"><span data-stu-id="92980-168">Deploy to Azure button</span></span>

<span data-ttu-id="92980-169">Reemplace ```<url-encoded-path-to-azuredeploy-json>``` por una versión [codificada de la URL](https://www.bing.com/search?q=url+encode) de la ruta de acceso sin formato del archivo `azuredeploy.json` en GitHub.</span><span class="sxs-lookup"><span data-stu-id="92980-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="92980-170">A continuación se muestra un ejemplo que usa Markdown:</span><span class="sxs-lookup"><span data-stu-id="92980-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="92980-171">A continuación se muestra un ejemplo que usa HTML:</span><span class="sxs-lookup"><span data-stu-id="92980-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="92980-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92980-172">Next steps</span></span>

<span data-ttu-id="92980-173">Aprenda a desarrollar y configurar Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="92980-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="92980-174">Referencia para desarrolladores de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="92980-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="92980-175">Configuración de aplicaciones de función de Azure</span><span class="sxs-lookup"><span data-stu-id="92980-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="92980-176">Creación de su primera función de Azure</span><span class="sxs-lookup"><span data-stu-id="92980-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Aplicación de función en el plan de consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Aplicación de función en el plan de App Service]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
