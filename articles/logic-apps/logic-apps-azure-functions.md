---
title: "Código personalizado para Azure Logic Apps con Azure Functions | Microsoft Docs"
description: "Cree y ejecute código personalizado para Azure Logic Apps con Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="481ac-103">Adición y ejecución de código personalizado para aplicaciones lógicas con Azure Functions</span><span class="sxs-lookup"><span data-stu-id="481ac-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="481ac-104">Para ejecutar fragmentos de código personalizados de C# o node.js en aplicaciones lógicas, puede crear funciones personalizadas a través de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="481ac-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="481ac-105">[Azure Functions](../azure-functions/functions-overview.md) ofrece una computación sin servidor en Microsoft Azure y es útil para realizar estas tareas:</span><span class="sxs-lookup"><span data-stu-id="481ac-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="481ac-106">Formato o proceso avanzados de los campos de Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="481ac-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="481ac-107">Realización de cálculos en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="481ac-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="481ac-108">Extensión de la funcionalidad de las aplicaciones lógicas con funciones que se admiten en C# o node.js.</span><span class="sxs-lookup"><span data-stu-id="481ac-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="481ac-109">Creación de funciones personalizadas para las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="481ac-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="481ac-110">Se recomienda crear una función en el portal de Azure Functions mediante las plantillas **Generic Webhook - Node** o **Generic Webhook - C#**.</span><span class="sxs-lookup"><span data-stu-id="481ac-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="481ac-111">El resultado crea una plantilla que se rellena automáticamente que acepta `application/json` de una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="481ac-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="481ac-112">Las funciones que se crean con estas plantillas se detectan automáticamente y aparecen en el Diseñador de aplicaciones lógicas en **Azure Functions in my region** (Azure Functions en mi región).</span><span class="sxs-lookup"><span data-stu-id="481ac-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="481ac-113">En Azure Portal, en el panel **Integrar** de una función, la plantilla debe mostrar que en **Modo** está seleccionado **Webhook** y en **Tipo de webhook** está seleccionado **JSON genérico**.</span><span class="sxs-lookup"><span data-stu-id="481ac-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="481ac-114">Las funciones de Webhook aceptan una solicitud y las pasan al método mediante una variable `data` .</span><span class="sxs-lookup"><span data-stu-id="481ac-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="481ac-115">Puede acceder a las propiedades de la carga mediante una notación de puntos, como `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="481ac-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="481ac-116">Por ejemplo, una función de JavaScript simple que convierte un valor de DateTime en una cadena de fecha es similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="481ac-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="481ac-117">Llamada a Azure Functions desde Logic Apps</span><span class="sxs-lookup"><span data-stu-id="481ac-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="481ac-118">Para enumerar los contenedores de una suscripción y seleccionar la función a la que se desea llamado, en el Diseñador de aplicaciones lógicas, haga clic en el menú **Actions** (Acciones) y selecciónelos en **Azure Functions in my Region** (Azure Functions en mi región).</span><span class="sxs-lookup"><span data-stu-id="481ac-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="481ac-119">Después de seleccionar la función, se le solicita que especifique un objeto de carga de entrada.</span><span class="sxs-lookup"><span data-stu-id="481ac-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="481ac-120">Este objeto es el mensaje que la aplicación lógica envía a la función y debe ser un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="481ac-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="481ac-121">Por ejemplo, si desea pasar la fecha de última modificación, **Last Modified Date**, de un desencadenador de Salesforce, la carga de la función podría ser similar a la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="481ac-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Fecha de última modificación][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="481ac-123">Desencadenamiento de aplicaciones lógicas desde una función</span><span class="sxs-lookup"><span data-stu-id="481ac-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="481ac-124">Una aplicación lógica se puede desencadenar desde dentro de una función.</span><span class="sxs-lookup"><span data-stu-id="481ac-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="481ac-125">Consulte [Aplicaciones lógicas como puntos de conexión invocables](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="481ac-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="481ac-126">Cree una aplicación lógica que tenga un desencadenador manual y, después, desde la función, genere una solicitud HTTP POST a la dirección URL del desencadenador manual con la carga que desee que se envíe a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="481ac-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="481ac-127">Creación de una función en el Diseñador de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="481ac-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="481ac-128">Una función de webhook de node.js también se puede crear desde el diseñador.</span><span class="sxs-lookup"><span data-stu-id="481ac-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="481ac-129">En primer lugar, seleccione **Azure Functions in my region** (Funciones de Azure en mi región) y elija un contenedor para la función.</span><span class="sxs-lookup"><span data-stu-id="481ac-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="481ac-130">Si todavía no dispone de ningún contenedor, tendrá que crearlo en el [portal de Funciones de Azure](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="481ac-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="481ac-131">Seleccione **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="481ac-131">Then select **Create New**.</span></span>  

<span data-ttu-id="481ac-132">Para generar una plantilla basada en los datos que desea procesar, especifique el objeto de contexto que piensa pasar a una función,</span><span class="sxs-lookup"><span data-stu-id="481ac-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="481ac-133">que debe ser un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="481ac-133">This object must be a JSON object.</span></span> <span data-ttu-id="481ac-134">Por ejemplo, si pasa el contenido del archivo de una acción de FTP, la carga del contexto será similar a la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="481ac-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Carga de contexto][2]

> [!NOTE]
> <span data-ttu-id="481ac-136">Puesto que este objeto no se transmitió como una cadena, el contenido se agrega directamente a la carga de JSON.</span><span class="sxs-lookup"><span data-stu-id="481ac-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="481ac-137">Sin embargo, si el objeto no es un token JSON (es decir, una cadena o un objeto o matriz JSON), se produce un error.</span><span class="sxs-lookup"><span data-stu-id="481ac-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="481ac-138">Para trasmitir el objeto como una cadena, agregue comillas como se muestra en la primera ilustración de este artículo.</span><span class="sxs-lookup"><span data-stu-id="481ac-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="481ac-139">A continuación, el diseñador genera una plantilla de función que puede crear en línea.</span><span class="sxs-lookup"><span data-stu-id="481ac-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="481ac-140">Las variables se crean previamente de acuerdo con el contexto que se va a pasar a la función.</span><span class="sxs-lookup"><span data-stu-id="481ac-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
