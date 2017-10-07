---
title: plantillas de aaaDevelop para la pila de Azure | Documentos de Microsoft
description: "Información sobre las prácticas recomendadas de plantillas de Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="6ab75-103">Consideraciones de la plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6ab75-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="6ab75-104">Al desarrollar la aplicación, es importante tooensure portabilidad de plantilla entre Azure y la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab75-104">As you develop your application, it is important tooensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="6ab75-105">Este tema proporciona consideraciones para el desarrollo de Azure Resource Manager [plantillas](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), por lo que puede prototipo de la implementación de aplicación y prueba en Azure sin el entorno de acceso tooan pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab75-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access tooan Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="6ab75-106">Espacios de nombres públicos</span><span class="sxs-lookup"><span data-stu-id="6ab75-106">Public namespaces</span></span>
<span data-ttu-id="6ab75-107">Como la pila de Azure se hospeda en el centro de datos, tiene espacios de nombres de punto de conexión de servicio diferente que Hola nube pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ab75-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than hello Azure public cloud.</span></span> <span data-ttu-id="6ab75-108">Como resultado, codificado de forma rígida los extremos públicos en las plantillas de administrador de recursos producirá un error cuando intente toodeploy les tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="6ab75-108">As a result, hardcoded public endpoints in Resource Manager templates fail when you try toodeploy them tooAzure Stack.</span></span> <span data-ttu-id="6ab75-109">En su lugar, puede usar hello *referencia* y *concatenar* función toodynamically crear extremo de servicio de hello en función de los valores recuperados de proveedor de recursos de Hola durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="6ab75-109">Instead, you can use hello *reference* and *concatenate* function toodynamically build hello service endpoint based on values retrieved from hello resource provider during deployment.</span></span> <span data-ttu-id="6ab75-110">Por ejemplo, en lugar de especificar *blob.core.windows.net* en la plantilla, recuperar hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically establecer hello *osDisk.URI* punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="6ab75-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically set hello *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="6ab75-111">Control de versiones de la API</span><span class="sxs-lookup"><span data-stu-id="6ab75-111">API versioning</span></span>
<span data-ttu-id="6ab75-112">Las versiones de los servicios de Azure pueden diferir entre Azure y Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6ab75-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="6ab75-113">Cada recurso requiere el atributo de valor apiVersion de hello, que define las capacidades de hello ofrecidas.</span><span class="sxs-lookup"><span data-stu-id="6ab75-113">Each resource requires hello apiVersion attribute, which defines hello capabilities offered.</span></span> <span data-ttu-id="6ab75-114">compatibilidad de versiones de tooensure API en la pila de Azure, Hola después son versiones de API válidas para cada proveedor de recursos:</span><span class="sxs-lookup"><span data-stu-id="6ab75-114">tooensure API version compatibility in Azure Stack, hello following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="6ab75-115">Proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="6ab75-115">Resource Provider</span></span> | <span data-ttu-id="6ab75-116">apiVersion</span><span class="sxs-lookup"><span data-stu-id="6ab75-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="6ab75-117">Proceso</span><span class="sxs-lookup"><span data-stu-id="6ab75-117">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="6ab75-118">Red</span><span class="sxs-lookup"><span data-stu-id="6ab75-118">Network</span></span> |<span data-ttu-id="6ab75-119">`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="6ab75-119">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="6ab75-120">Storage</span><span class="sxs-lookup"><span data-stu-id="6ab75-120">Storage</span></span> |<span data-ttu-id="6ab75-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="6ab75-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="6ab75-122">KeyVault</span><span class="sxs-lookup"><span data-stu-id="6ab75-122">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="6ab75-123">App Service</span><span class="sxs-lookup"><span data-stu-id="6ab75-123">App Service</span></span> |`'2015-08-01'` |
| <span data-ttu-id="6ab75-124">MySQL</span><span class="sxs-lookup"><span data-stu-id="6ab75-124">MySQL</span></span> |`'2015-09-01'` |
| <span data-ttu-id="6ab75-125">SQL</span><span class="sxs-lookup"><span data-stu-id="6ab75-125">SQL</span></span> |`'2014-04-01-preview'` |

## <a name="template-functions"></a><span data-ttu-id="6ab75-126">Funciones de plantillas</span><span class="sxs-lookup"><span data-stu-id="6ab75-126">Template functions</span></span>
<span data-ttu-id="6ab75-127">El Administrador de recursos [funciones](../azure-resource-manager/resource-group-template-functions.md) proporcionan capacidades necesarios toobuild plantillas dinámicas.</span><span class="sxs-lookup"><span data-stu-id="6ab75-127">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required toobuild dynamic templates.</span></span> <span data-ttu-id="6ab75-128">Por ejemplo, puede utilizar funciones para tareas como las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6ab75-128">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="6ab75-129">Concatenar o recortar cadenas</span><span class="sxs-lookup"><span data-stu-id="6ab75-129">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="6ab75-130">Valores de referencia de otros recursos</span><span class="sxs-lookup"><span data-stu-id="6ab75-130">Reference values from other resources</span></span>
* <span data-ttu-id="6ab75-131">Iterar en recursos toodeploy varias instancias</span><span class="sxs-lookup"><span data-stu-id="6ab75-131">Iterating on resources toodeploy multiple instances</span></span> 

<span data-ttu-id="6ab75-132">Al compilar las plantillas, algunas funciones no están disponibles en el kit de desarrollo de Azure Stack y no deben usarse.</span><span class="sxs-lookup"><span data-stu-id="6ab75-132">As you build your templates, some functions are not available in Azure Stack Development Kit, and should not be used.</span></span> <span data-ttu-id="6ab75-133">Estas funciones son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="6ab75-133">These functions are:</span></span>

* <span data-ttu-id="6ab75-134">Skip</span><span class="sxs-lookup"><span data-stu-id="6ab75-134">Skip</span></span>
* <span data-ttu-id="6ab75-135">Take</span><span class="sxs-lookup"><span data-stu-id="6ab75-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="6ab75-136">Ubicación del recurso</span><span class="sxs-lookup"><span data-stu-id="6ab75-136">Resource location</span></span>
<span data-ttu-id="6ab75-137">Plantillas de administrador de recursos usan una recursos tooplace de atributo de ubicación durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="6ab75-137">Resource Manager templates use a location attribute tooplace resources during deployment.</span></span> <span data-ttu-id="6ab75-138">En Azure, ubicaciones consulte región tooa como oeste de Estados Unidos o Sudamérica.</span><span class="sxs-lookup"><span data-stu-id="6ab75-138">In Azure, locations refer tooa region like West US or South America.</span></span> <span data-ttu-id="6ab75-139">En Azure Stack, las ubicaciones son diferentes porque Azure Stack está en el centro de datos.</span><span class="sxs-lookup"><span data-stu-id="6ab75-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="6ab75-140">plantillas de tooensure son transferibles entre Azure y la pila de Azure, debe hacer referencia a ubicación del grupo de recursos de hello como implementar recursos individuales.</span><span class="sxs-lookup"><span data-stu-id="6ab75-140">tooensure templates are transferrable between Azure and Azure Stack, you should reference hello resource group location as you deploy individual resources.</span></span> <span data-ttu-id="6ab75-141">Puede hacerlo mediante `[resourceGroup().Location]` tooensure heredan todos los recursos Hola ubicación del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6ab75-141">You can do this using `[resourceGroup().Location]` tooensure all resources inherit hello resource group location.</span></span>  <span data-ttu-id="6ab75-142">Hello siguiente extracto de la plantilla de administrador de recursos es un ejemplo del uso de esta función durante la implementación de una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="6ab75-142">hello following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a><span data-ttu-id="6ab75-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ab75-143">Next steps</span></span>
* [<span data-ttu-id="6ab75-144">Implementación de plantillas con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ab75-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="6ab75-145">Implementación de plantillas con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6ab75-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="6ab75-146">Implementación de plantillas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ab75-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

