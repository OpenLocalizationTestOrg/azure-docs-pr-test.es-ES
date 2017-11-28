---
title: "aaaCreate una aplicación de lógica mediante una plantilla de Azure | Documentos de Microsoft"
description: "Utilice un toodeploy de plantilla de Azure Resource Manager una aplicación lógica para definir los flujos de trabajo."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="e95e3-103">Creación de una aplicación lógica mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="e95e3-103">Create a Logic App using a template</span></span>
<span data-ttu-id="e95e3-104">Las plantillas proporcionan una forma rápida toouse conectores diferentes dentro de una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="e95e3-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="e95e3-105">Las aplicaciones lógicas incluye plantillas de Azure Resource Manager para toocreate una aplicación de la lógica que puede ser usado toodefine flujos de trabajo empresariales.</span><span class="sxs-lookup"><span data-stu-id="e95e3-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="e95e3-106">Puede definir qué recursos se implementan y cómo toodefine parámetros al implementar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e95e3-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="e95e3-107">Puede usar esta plantilla para sus propios escenarios empresariales, o personalizar toomeet sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="e95e3-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="e95e3-108">Para obtener más detalles sobre las propiedades de la aplicación hello lógica, consulte [API de administración de flujo de trabajo de aplicación lógica](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="e95e3-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="e95e3-109">Para obtener ejemplos de la propia definición de hello, consulte [definiciones de aplicación lógica de autor](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="e95e3-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="e95e3-110">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e95e3-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="e95e3-111">Para la plantilla de hello completa, consulte [plantilla de aplicación lógica](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e95e3-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="e95e3-112">¿Qué se puede implementar?</span><span class="sxs-lookup"><span data-stu-id="e95e3-112">What you deploy</span></span>
<span data-ttu-id="e95e3-113">Con esta plantilla, implementará una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e95e3-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="e95e3-114">implementación de hello toorun automáticamente, seleccione Hola después de botón:</span><span class="sxs-lookup"><span data-stu-id="e95e3-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="e95e3-115">[![Implementar tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e95e3-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="e95e3-116">parameters</span><span class="sxs-lookup"><span data-stu-id="e95e3-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="e95e3-117">testUri</span><span class="sxs-lookup"><span data-stu-id="e95e3-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="e95e3-118">Toodeploy de recursos</span><span class="sxs-lookup"><span data-stu-id="e95e3-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="e95e3-119">Aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="e95e3-119">Logic app</span></span>
<span data-ttu-id="e95e3-120">Crea la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="e95e3-120">Creates hello logic app.</span></span>

<span data-ttu-id="e95e3-121">plantillas de Hello usa un valor de parámetro para el nombre de la aplicación hello lógica.</span><span class="sxs-lookup"><span data-stu-id="e95e3-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="e95e3-122">Establece la ubicación de Hola de toohello de aplicación lógica de hello misma ubicación que el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e95e3-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="e95e3-123">Esta definición en particular ejecuta una vez cada hora y pings Hola ubicación especificada en hello **testUri** parámetro.</span><span class="sxs-lookup"><span data-stu-id="e95e3-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a><span data-ttu-id="e95e3-124">Implementación de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="e95e3-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="e95e3-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e95e3-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="e95e3-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e95e3-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



