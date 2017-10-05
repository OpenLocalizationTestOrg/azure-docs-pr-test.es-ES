---
title: "Creación de una aplicación lógica a partir de una plantilla en Azure | Microsoft Docs"
description: "Use una plantilla de Azure Resource Manager para implementar una aplicación lógica vacía para definir flujos de trabajo."
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
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="11499-103">Creación de una aplicación lógica mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="11499-103">Create a Logic App using a template</span></span>
<span data-ttu-id="11499-104">Las plantillas proporcionan una forma rápida de utilizar distintos conectores dentro de una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="11499-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="11499-105">Logic Apps incluye plantillas de Azure Resource Manager para crear una aplicación lógica que puede utilizarse para definir flujos de trabajo empresariales.</span><span class="sxs-lookup"><span data-stu-id="11499-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="11499-106">Puede especificar qué recursos se implementan y cómo definir parámetros al implementar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="11499-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="11499-107">Puede usar esta plantilla para sus propios escenarios empresariales o personalizarla para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="11499-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="11499-108">Para obtener más detalles sobre las propiedades de la aplicación lógica, consulte [API de administración de flujos de trabajo de aplicaciones lógicas](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span><span class="sxs-lookup"><span data-stu-id="11499-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="11499-109">Para obtener ejemplos de la propia definición, consulte [Creación de definiciones de aplicaciones lógicas](logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="11499-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="11499-110">Para obtener más información sobre la creación de plantillas, consulte [Creación de plantillas de Administrador de recursos de Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="11499-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="11499-111">Para la plantilla completa, consulte [Plantilla de aplicación lógica](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="11499-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="11499-112">¿Qué se puede implementar?</span><span class="sxs-lookup"><span data-stu-id="11499-112">What you deploy</span></span>
<span data-ttu-id="11499-113">Con esta plantilla, implementará una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="11499-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="11499-114">Para ejecutar automáticamente la implementación, seleccione el botón siguiente:</span><span class="sxs-lookup"><span data-stu-id="11499-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="11499-115">[![Implementación en Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="11499-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="11499-116">Parámetros</span><span class="sxs-lookup"><span data-stu-id="11499-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="11499-117">testUri</span><span class="sxs-lookup"><span data-stu-id="11499-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="11499-118">Recursos para implementar</span><span class="sxs-lookup"><span data-stu-id="11499-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="11499-119">Aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="11499-119">Logic app</span></span>
<span data-ttu-id="11499-120">Crea la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="11499-120">Creates the logic app.</span></span>

<span data-ttu-id="11499-121">Las plantillas utilizan un valor de parámetro para el nombre de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="11499-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="11499-122">Establece la ubicación de la aplicación lógica en la misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="11499-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="11499-123">Esta definición determinada se ejecuta una vez cada hora y hace ping en la ubicación especificada en el parámetro **testUri** .</span><span class="sxs-lookup"><span data-stu-id="11499-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

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


## <a name="commands-to-run-deployment"></a><span data-ttu-id="11499-124">Comandos para ejecutar la implementación</span><span class="sxs-lookup"><span data-stu-id="11499-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="11499-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11499-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="11499-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="11499-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



