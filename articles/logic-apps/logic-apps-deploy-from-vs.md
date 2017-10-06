---
title: "aaaCreate, genere e implemente las aplicaciones lógicas en Visual Studio: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="e3be2-103">Diseño, compilación e implementación de Azure Logic Apps en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3be2-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="e3be2-104">Aunque hello [portal de Azure](https://portal.azure.com/) ofrece una excelente manera de que toocreate y administrar las aplicaciones lógicas de Azure, puede usar Visual Studio para diseñar, crear e implementar las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="e3be2-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="e3be2-105">Visual Studio proporciona herramientas enriquecidos como Hola diseñador la lógica de aplicación para toocreate las aplicaciones lógicas, configurar las plantillas de implementación y automatización e implementar tooany entorno.</span><span class="sxs-lookup"><span data-stu-id="e3be2-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="e3be2-106">Obtenga información acerca de tooget a trabajar con las aplicaciones lógicas de Azure, [cómo toocreate su primera aplicación de lógica en el portal de Azure hello](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e3be2-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="e3be2-107">Pasos de instalación</span><span class="sxs-lookup"><span data-stu-id="e3be2-107">Installation steps</span></span>

<span data-ttu-id="e3be2-108">tooinstall y configurar las herramientas de Visual Studio para aplicaciones de la lógica de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="e3be2-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e3be2-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e3be2-109">Prerequisites</span></span>

* <span data-ttu-id="e3be2-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e3be2-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="e3be2-111">[SDK de Azure más reciente](https://azure.microsoft.com/downloads/) (2.9.1 o superior)</span><span class="sxs-lookup"><span data-stu-id="e3be2-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="e3be2-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3be2-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="e3be2-113">Web toohello de acceso al usar el Diseñador de hello incrustado</span><span class="sxs-lookup"><span data-stu-id="e3be2-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="e3be2-114">Instalación de herramientas de Visual Studio para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e3be2-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="e3be2-115">Después de instalar requisitos previos de hello:</span><span class="sxs-lookup"><span data-stu-id="e3be2-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="e3be2-116">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3be2-116">Open Visual Studio.</span></span> <span data-ttu-id="e3be2-117">En hello **herramientas** menú, seleccione **extensiones y actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="e3be2-118">Expanda hello **Online** categoría de forma que pueda buscar en línea.</span><span class="sxs-lookup"><span data-stu-id="e3be2-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="e3be2-119">Busque **Logic Apps** hasta que encuentre las **herramientas de Azure Logic Apps para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="e3be2-120">toodownload y la extensión de Hola de instalación, haga clic en **descargar**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="e3be2-121">Reinicie Visual Studio después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="e3be2-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="e3be2-122">También puede descargar [aplicaciones de lógica de Azure Tools para Visual Studio de 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) hello y [aplicaciones de lógica de Azure Tools para Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directamente desde Visual Studio Marketplace Hola.</span><span class="sxs-lookup"><span data-stu-id="e3be2-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="e3be2-123">Después de finalizar la instalación, puede usar el proyecto del grupo de recursos de Azure de Hola con lógica de aplicación diseñador.</span><span class="sxs-lookup"><span data-stu-id="e3be2-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="e3be2-124">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="e3be2-124">Create your project</span></span>

1. <span data-ttu-id="e3be2-125">En hello **archivo** menú, ir demasiado**New**y seleccione **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="e3be2-126">O tooadd su tooan proyecto existente de solución, vaya demasiado**agregar**y seleccione **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Menú Archivo](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="e3be2-128">Hola **nuevo proyecto** ventana, buscar **nube**y seleccione **grupo de recursos de Azure**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="e3be2-129">Asigne un nombre al proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-129">Name your project, and click **OK**.</span></span>

    ![Incorporación de proyecto nuevo](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="e3be2-131">Seleccione hello **aplicación lógica** plantilla, que crea una plantilla de implementación de aplicación lógica en blanco de toouse.</span><span class="sxs-lookup"><span data-stu-id="e3be2-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="e3be2-132">Cuando la haya seleccionado, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-132">After you select your template, click **OK**.</span></span>

    ![Selección de la plantilla de aplicación lógica](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="e3be2-134">Ahora ha agregado la solución de tooyour de proyecto de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e3be2-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="e3be2-135">En el Explorador de soluciones de hello, debe aparecer el archivo de implementación.</span><span class="sxs-lookup"><span data-stu-id="e3be2-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Archivo de implementación](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="e3be2-137">Creación de la aplicación lógica en Diseñador de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="e3be2-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="e3be2-138">Cuando tenga un proyecto del grupo de recursos de Azure que contiene una aplicación de lógica, puede abrir Hola diseñador la lógica de aplicación en Visual Studio toocreate el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e3be2-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="e3be2-139">Diseñador de Hello requiere una conexión a internet demasiado consultar conectores de datos y propiedades disponibles.</span><span class="sxs-lookup"><span data-stu-id="e3be2-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="e3be2-140">Por ejemplo, si usa el conector de Dynamics CRM Online hello, Diseñador de hello consulta su personalizado disponible de CRM instancia tooshow y propiedades predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="e3be2-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="e3be2-141">Haga clic con el botón derecho en el archivo `<template>.json` y seleccione **Open with Logic App Designer** (Abrir con diseñador de aplicación lógica).</span><span class="sxs-lookup"><span data-stu-id="e3be2-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="e3be2-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="e3be2-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="e3be2-143">Elija la suscripción de Azure, el grupo de recursos y la ubicación para la plantilla de implementación.</span><span class="sxs-lookup"><span data-stu-id="e3be2-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3be2-144">El diseño de una aplicación lógica creará recursos de una conexión de API para consultar las propiedades durante el diseño.</span><span class="sxs-lookup"><span data-stu-id="e3be2-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="e3be2-145">Visual Studio usa el toocreate del grupo de recursos seleccionado esas conexiones en tiempo de diseño.</span><span class="sxs-lookup"><span data-stu-id="e3be2-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="e3be2-146">tooview o cambiar las conexiones de API, vaya toohello portal de Azure y busque **API conexiones**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Selector de suscripción](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="e3be2-148">Diseñador de Hello utiliza la definición de Hola Hola `<template>.json` archivo para la representación.</span><span class="sxs-lookup"><span data-stu-id="e3be2-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="e3be2-149">Cree y diseñe la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e3be2-149">Create and design your logic app.</span></span> <span data-ttu-id="e3be2-150">La plantilla de implementación se actualiza con los cambios.</span><span class="sxs-lookup"><span data-stu-id="e3be2-150">Your deployment template is updated with your changes.</span></span>

    ![Diseñador de aplicaciones lógicas en Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="e3be2-152">Visual Studio agrega `Microsoft.Web/connections` recursos demasiado el archivo de recursos para las conexiones toofunction necesita de la aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="e3be2-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="e3be2-153">Estas propiedades de conexión se pueden establecer cuando se implementa y administra después de implementar en **API conexiones** Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3be2-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="e3be2-154">Cambiar la vista de código tooJSON</span><span class="sxs-lookup"><span data-stu-id="e3be2-154">Switch tooJSON code view</span></span>

<span data-ttu-id="e3be2-155">Hola tooshow representación JSON de la aplicación lógica, seleccione hello **en la vista código** pestaña final Hola de diseñador Hola.</span><span class="sxs-lookup"><span data-stu-id="e3be2-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="e3be2-156">tooswitch atrás toohello completa a recursos JSON, haga clic en hello `<template>.json` de archivos y seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="e3be2-157">Agregar referencias para plantillas de implementación de los recursos dependientes tooVisual Studio</span><span class="sxs-lookup"><span data-stu-id="e3be2-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="e3be2-158">Si desea que los recursos dependientes de la tooreference de aplicación lógica, puede usar [funciones de plantilla de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) en la plantilla de implementación de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e3be2-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="e3be2-159">Por ejemplo, puede que su tooreference de aplicación lógica una cuenta de integración o de función de Azure que desea que toodeploy junto con la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e3be2-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="e3be2-160">Siga estas instrucciones sobre cómo se representa correctamente toouse parámetros en la plantilla de implementación para Hola diseñador la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3be2-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="e3be2-161">Puede usar parámetros de aplicación lógica en estos tipos de desencadenadores y acciones:</span><span class="sxs-lookup"><span data-stu-id="e3be2-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="e3be2-162">Flujo de trabajo secundario</span><span class="sxs-lookup"><span data-stu-id="e3be2-162">Child workflow</span></span>
*   <span data-ttu-id="e3be2-163">Aplicación de función</span><span class="sxs-lookup"><span data-stu-id="e3be2-163">Function app</span></span>
*   <span data-ttu-id="e3be2-164">Llamada APIM</span><span class="sxs-lookup"><span data-stu-id="e3be2-164">APIM call</span></span>
*   <span data-ttu-id="e3be2-165">Dirección URL en tiempo de ejecución de conexión de API</span><span class="sxs-lookup"><span data-stu-id="e3be2-165">API connection runtime URL</span></span>
*   <span data-ttu-id="e3be2-166">Ruta de conexión de API</span><span class="sxs-lookup"><span data-stu-id="e3be2-166">API connection path</span></span>

<span data-ttu-id="e3be2-167">Y puede utilizar funciones de plantilla como, por ejemplo, parámetros, variables, resourceId, concat, etc. Por ejemplo, mostramos cómo puede reemplazar el Id. de recurso de Azure función hello:</span><span class="sxs-lookup"><span data-stu-id="e3be2-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="e3be2-168">Y dónde usaría parámetros:</span><span class="sxs-lookup"><span data-stu-id="e3be2-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="e3be2-169">Otro ejemplo puede parametrizar Hola operación de mensaje de envío de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="e3be2-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

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
> <span data-ttu-id="e3be2-170">host.runtimeUrl es opcional y se puede quitar de la plantilla si está presente.</span><span class="sxs-lookup"><span data-stu-id="e3be2-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="e3be2-171">Para toowork del Diseñador de la aplicación lógica de Hola para utilizar parámetros, debe proporcionar valores predeterminados, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e3be2-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="e3be2-172">Guardado de la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="e3be2-172">Save your logic app</span></span>

<span data-ttu-id="e3be2-173">toosave la aplicación lógica y en cualquier momento, vaya demasiado**archivo** > **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="e3be2-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="e3be2-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="e3be2-175">Si la aplicación lógica tiene errores cuando guarda la aplicación, que aparecen en Visual Studio hello **salidas** ventana.</span><span class="sxs-lookup"><span data-stu-id="e3be2-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="e3be2-176">Implementación de la aplicación lógica desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3be2-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="e3be2-177">Después de configurar la aplicación, puede realizar la implementación directamente desde Visual Studio en solo un par de pasos.</span><span class="sxs-lookup"><span data-stu-id="e3be2-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="e3be2-178">En el Explorador de soluciones, haga clic en el proyecto y vaya demasiado**implementar** > **nueva implementación...**</span><span class="sxs-lookup"><span data-stu-id="e3be2-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Nueva implementación](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="e3be2-180">Cuando se le pida, inicie sesión en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e3be2-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="e3be2-181">Ahora debe seleccionar detalles de Hola Hola para grupo de recursos donde desea toodeploy la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="e3be2-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="e3be2-182">Cuando haya terminado, haga clic en **Implementar**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3be2-183">Asegúrese de que selecciona plantilla correcta de Hola y el archivo de parámetros para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3be2-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="e3be2-184">Por ejemplo, si desea que el entorno de producción de toodeploy tooa, elija el archivo de parámetros de producción de hello.</span><span class="sxs-lookup"><span data-stu-id="e3be2-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Implementar grupo tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="e3be2-186">estado de la implementación de Hello aparece en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="e3be2-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="e3be2-187">Es posible que tenga tooselect **Azure aprovisionamiento** en hello **mostrar resultados desde** lista.</span><span class="sxs-lookup"><span data-stu-id="e3be2-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Salida del estado de la implementación](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="e3be2-189">Hola futuro, puede editar la aplicación lógica de control de código fuente y usa toodeploy nuevas versiones de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3be2-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="e3be2-190">Si cambia la definición de Hola Hola portal de Azure directamente, los cambios se sobrescriben cuando se implementa desde Visual Studio próxima vez.</span><span class="sxs-lookup"><span data-stu-id="e3be2-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="e3be2-191">Agregar el proyecto existente de grupo de recursos de la lógica aplicación tooan</span><span class="sxs-lookup"><span data-stu-id="e3be2-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="e3be2-192">Si tiene un proyecto del grupo de recursos existente, puede agregar el proyecto de toothat de aplicación lógica en la ventana de esquema de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3be2-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="e3be2-193">También puede agregar otra lógica de aplicación, junto con la aplicación hello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3be2-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="e3be2-194">Abra hello `<template>.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="e3be2-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="e3be2-195">Hola tooopen ventana Esquema de JSON, vaya demasiado**vista** > **otras ventanas** > **esquema JSON**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="e3be2-196">Haga clic en un archivo de plantilla de recursos toohello, tooadd **Agregar recurso** en parte superior de Hola de ventana de esquema de JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="e3be2-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="e3be2-197">O en la ventana de esquema de JSON de hello, haga clic en **recursos**y seleccione **Agregar nuevo recurso**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Ventana Esquema JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="e3be2-199">Hola **Agregar recurso** cuadro de diálogo, busque y seleccione **aplicación lógica**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="e3be2-200">Asigne un nombre a la aplicación lógica y elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e3be2-200">Name your logic app, and choose **Add**.</span></span>

    ![Agregar recurso](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="e3be2-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e3be2-202">Next Steps</span></span>

* [<span data-ttu-id="e3be2-203">Administración de aplicaciones lógicas con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="e3be2-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="e3be2-204">Ejemplos de aplicaciones lógicas y escenarios comunes</span><span class="sxs-lookup"><span data-stu-id="e3be2-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="e3be2-205">Obtenga información acerca de cómo los procesos del negocio tooautomate con las aplicaciones lógicas de Azure</span><span class="sxs-lookup"><span data-stu-id="e3be2-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="e3be2-206">Obtenga información acerca de cómo toointegrate los sistemas con las aplicaciones lógicas de Azure</span><span class="sxs-lookup"><span data-stu-id="e3be2-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
