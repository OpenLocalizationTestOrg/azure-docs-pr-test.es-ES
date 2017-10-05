---
title: "Creación, compilación e implementación de aplicaciones lógicas en Visual Studio: Azure Logic Apps | Microsoft Docs"
description: "Cree proyectos de Visual Studio para diseñar, compilar e implementar Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: e7f5cf483d22e4c60dedbe5176ceb0bc8b2b6e66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="1ba5b-103">Diseño, compilación e implementación de Azure Logic Apps en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba5b-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="1ba5b-104">Aunque [Azure Portal](https://portal.azure.com/) es un medio excelente de crear y administrar Azure Logic Apps, puede usar Visual Studio para diseñar, compilar e implementar sus aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="1ba5b-105">Visual Studio proporciona herramientas muy completas, como Diseñador de aplicación lógica, para crear aplicaciones lógicas, configurar las plantillas de implementación y automatización e implementarlas en cualquier entorno.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="1ba5b-106">Para empezar a trabajar con Azure Logic Apps, aprenda a [crear su primera aplicación lógica en Azure Portal](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ba5b-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="1ba5b-107">Pasos de instalación</span><span class="sxs-lookup"><span data-stu-id="1ba5b-107">Installation steps</span></span>

<span data-ttu-id="1ba5b-108">Para instalar y configurar las herramientas de Visual Studio para Azure Logic Apps siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1ba5b-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1ba5b-109">Prerequisites</span></span>

* <span data-ttu-id="1ba5b-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="1ba5b-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="1ba5b-111">[SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)</span><span class="sxs-lookup"><span data-stu-id="1ba5b-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="1ba5b-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ba5b-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="1ba5b-113">Acceso a la web para usar el diseñador incrustado</span><span class="sxs-lookup"><span data-stu-id="1ba5b-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="1ba5b-114">Instalación de herramientas de Visual Studio para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1ba5b-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="1ba5b-115">Una vez cumplidos los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="1ba5b-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="1ba5b-116">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-116">Open Visual Studio.</span></span> <span data-ttu-id="1ba5b-117">En el menú **Herramientas**, seleccione **Extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="1ba5b-118">Expanda la categoría **En línea** para poder buscar en línea.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="1ba5b-119">Busque **Logic Apps** hasta que encuentre las **herramientas de Azure Logic Apps para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="1ba5b-120">Para descargar e instalar la extensión, haga clic en el botón **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="1ba5b-121">Reinicie Visual Studio después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba5b-122">También puede descargar las [herramientas de Azure Logic Apps para Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) y las [herramientas de Azure Logic Apps para Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directamente desde Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="1ba5b-123">Una vez finalizada la instalación, podrá usar el proyecto Grupo de recursos de Azure con el Diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="1ba5b-124">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="1ba5b-124">Create your project</span></span>

1. <span data-ttu-id="1ba5b-125">En el menú **Archivo**, vaya a **Nuevo** y seleccione **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="1ba5b-126">O para agregar el proyecto a una solución existente, vaya a **Agregar** y seleccione **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![Menú Archivo](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="1ba5b-128">En la ventana **Nuevo proyecto**, busque **Nube** y seleccione **Grupo de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="1ba5b-129">Asigne un nombre al proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-129">Name your project, and click **OK**.</span></span>

    ![Incorporación de proyecto nuevo](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="1ba5b-131">Seleccione la plantilla de la **aplicación lógica** para crear una plantilla de implementación de una aplicación lógica en blanco para poder usarla.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="1ba5b-132">Cuando la haya seleccionado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-132">After you select your template, click **OK**.</span></span>

    ![Selección de la plantilla de aplicación lógica](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="1ba5b-134">Ahora habrá agregado el proyecto de aplicación lógica a la solución.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="1ba5b-135">En el Explorador de soluciones debería aparecer el archivo de implementación.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![Archivo de implementación](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="1ba5b-137">Creación de la aplicación lógica en Diseñador de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="1ba5b-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="1ba5b-138">Cuando tenga un proyecto Grupo de recursos de Azure con una aplicación lógica, podrá abrir el Diseñador de aplicaciones lógicas en Visual Studio para crear el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="1ba5b-139">El diseñador requiere una conexión a internet a los conectores de consulta de datos y propiedades disponibles.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="1ba5b-140">Por ejemplo, si usa el conector de Dynamics CRM Online, el diseñador consulta a la instancia de CRM para que muestre las propiedades personalizadas disponibles y las predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="1ba5b-141">Haga clic con el botón derecho en el archivo `<template>.json` y seleccione **Open with Logic App Designer** (Abrir con diseñador de aplicación lógica).</span><span class="sxs-lookup"><span data-stu-id="1ba5b-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="1ba5b-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="1ba5b-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="1ba5b-143">Elija la suscripción de Azure, el grupo de recursos y la ubicación para la plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba5b-144">El diseño de una aplicación lógica creará recursos de una conexión de API para consultar las propiedades durante el diseño.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="1ba5b-145">Visual Studio usa el grupo de recursos seleccionado para crear las conexiones durante el diseño.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="1ba5b-146">Para consultar o modificar las conexiones de API, vaya a Azure Portal y busque **Conexiones de API**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![Selector de suscripción](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="1ba5b-148">El diseñador utiliza la definición del archivo `<template>.json` para la representación.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="1ba5b-149">Cree y diseñe la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-149">Create and design your logic app.</span></span> <span data-ttu-id="1ba5b-150">La plantilla de implementación se actualiza con los cambios.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-150">Your deployment template is updated with your changes.</span></span>

    ![Diseñador de aplicaciones lógicas en Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="1ba5b-152">Visual Studio agrega recursos `Microsoft.Web/connections` al archivo de recursos para cualquier conexión que necesite la aplicación lógica para funcionar.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="1ba5b-153">Estas propiedades de conexión pueden establecerse durante la implementación y administrarse después de implementar **Conexiones de API** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="1ba5b-154">Cambio a la vista de código JSON</span><span class="sxs-lookup"><span data-stu-id="1ba5b-154">Switch to JSON code view</span></span>

<span data-ttu-id="1ba5b-155">Para mostrar la representación JSON de la aplicación lógica, seleccione la pestaña **Vista Código** de la parte inferior del diseñador.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="1ba5b-156">Para volver al JSON de todos los recursos, haga clic con el botón derecho en el archivo `<template>.json` y seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="1ba5b-157">Incorporación de referencias a los recursos dependientes a las plantillas de implementación de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba5b-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="1ba5b-158">Si desea que la aplicación lógica haga referencia a los recursos dependientes, puede usar las [funciones de plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions), como los parámetros, de la plantilla de implementación de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="1ba5b-159">Por ejemplo, si quiere que la aplicación lógica haga referencia a una función de Azure o cuenta de integración que desee implementar junto con la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="1ba5b-160">Siga estas instrucciones sobre cómo usar parámetros en la plantilla de implementación para que el Diseñador de aplicaciones lógicas represente correctamente.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="1ba5b-161">Puede usar parámetros de aplicación lógica en estos tipos de desencadenadores y acciones:</span><span class="sxs-lookup"><span data-stu-id="1ba5b-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="1ba5b-162">Flujo de trabajo secundario</span><span class="sxs-lookup"><span data-stu-id="1ba5b-162">Child workflow</span></span>
*   <span data-ttu-id="1ba5b-163">Aplicación de función</span><span class="sxs-lookup"><span data-stu-id="1ba5b-163">Function app</span></span>
*   <span data-ttu-id="1ba5b-164">Llamada APIM</span><span class="sxs-lookup"><span data-stu-id="1ba5b-164">APIM call</span></span>
*   <span data-ttu-id="1ba5b-165">Dirección URL en tiempo de ejecución de conexión de API</span><span class="sxs-lookup"><span data-stu-id="1ba5b-165">API connection runtime URL</span></span>
*   <span data-ttu-id="1ba5b-166">Ruta de conexión de API</span><span class="sxs-lookup"><span data-stu-id="1ba5b-166">API connection path</span></span>

<span data-ttu-id="1ba5b-167">Y puede utilizar funciones de plantilla como, por ejemplo, parámetros, variables, resourceId, concat, etc. Por ejemplo, aquí verá cómo se puede reemplazar el identificador de recurso de función de Azure:</span><span class="sxs-lookup"><span data-stu-id="1ba5b-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="1ba5b-168">Y dónde usaría parámetros:</span><span class="sxs-lookup"><span data-stu-id="1ba5b-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="1ba5b-169">En otro ejemplo puede parametrizar la operación send message de Service Bus:</span><span class="sxs-lookup"><span data-stu-id="1ba5b-169">As another example you can parameterize the Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="1ba5b-170">host.runtimeUrl es opcional y se puede quitar de la plantilla si está presente.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="1ba5b-171">Para que el Diseñador de aplicaciones lógicas funcione con parámetros, debe proporcionar valores predeterminados, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1ba5b-171">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="1ba5b-172">Guardado de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="1ba5b-172">Save your logic app</span></span>

<span data-ttu-id="1ba5b-173">Para guardar la aplicación lógica en cualquier momento, vaya a **Archivo** > **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-173">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="1ba5b-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="1ba5b-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="1ba5b-175">Si la aplicación lógica tiene errores al guardarla, se muestran en la ventana **Resultados** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-175">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="1ba5b-176">Implementación de la aplicación lógica desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba5b-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="1ba5b-177">Después de configurar la aplicación, puede realizar la implementación directamente desde Visual Studio en solo un par de pasos.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="1ba5b-178">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y vaya a **Implementar** > **Nueva implementación...**</span><span class="sxs-lookup"><span data-stu-id="1ba5b-178">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![Nueva implementación](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="1ba5b-180">Cuando se le solicite, inicie sesión en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-180">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="1ba5b-181">Ahora debe seleccionar los detalles para el grupo de recursos donde desea implementar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-181">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="1ba5b-182">Cuando haya terminado, haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1ba5b-183">Asegúrese de seleccionar el archivo de plantilla y de parámetros correcto para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-183">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="1ba5b-184">Por ejemplo, si desea implementar en un entorno de producción, elija el archivo de parámetros de producción.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-184">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![Implementación en el grupo de recursos](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="1ba5b-186">El estado de la implementación aparece en la ventana **Resultados**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-186">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="1ba5b-187">Es posible que deba seleccionar **Aprovisionamiento de Azure** en la lista **Mostrar salida de**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-187">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![Salida del estado de la implementación](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="1ba5b-189">En el futuro, puede modificar la aplicación lógica en el control de código fuente y usar Visual Studio para implementar versiones nuevas.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-189">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="1ba5b-190">Si modifica directamente la definición en Azure Portal, la próxima vez que realice una implementación desde Visual Studio estos cambios se sobrescriben.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-190">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="1ba5b-191">Incorporación de la aplicación lógica a un proyecto de grupo de recursos existente</span><span class="sxs-lookup"><span data-stu-id="1ba5b-191">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="1ba5b-192">Si tiene un proyecto de grupo de recursos existente, puede agregar la aplicación lógica desde la ventana Esquema JSON.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-192">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="1ba5b-193">También puede agregar otra aplicación lógica junto con la que creara anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-193">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="1ba5b-194">Abra el archivo `<template>.json` .</span><span class="sxs-lookup"><span data-stu-id="1ba5b-194">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="1ba5b-195">La ventana Esquema JSON, vaya a en **Ver** > **Otras ventanas** > **Esquema JSON**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-195">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="1ba5b-196">Para agregar un recurso al archivo de plantilla, haga clic en **Agregar recurso** en la parte superior de la ventana Esquema de JSON.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-196">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="1ba5b-197">O, en la ventana Esquema de JSON, haga clic en **recursos** y seleccione **Agregar nuevo recurso**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-197">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Ventana Esquema JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="1ba5b-199">En el cuadro de diálogo **Agregar recurso**, busque y seleccione **Aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-199">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="1ba5b-200">Asigne un nombre a la aplicación lógica y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1ba5b-200">Name your logic app, and choose **Add**.</span></span>

    ![Agregar recurso](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="1ba5b-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ba5b-202">Next Steps</span></span>

* [<span data-ttu-id="1ba5b-203">Administración de aplicaciones lógicas con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="1ba5b-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="1ba5b-204">Ejemplos de aplicaciones lógicas y escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="1ba5b-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="1ba5b-205">Aprenda a automatizar procesos empresariales con Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1ba5b-205">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="1ba5b-206">Aprenda a integrar sus sistemas con Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1ba5b-206">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
