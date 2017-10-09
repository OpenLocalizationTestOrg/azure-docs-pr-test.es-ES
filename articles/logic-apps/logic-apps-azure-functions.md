---
title: "código de aaaCustom para las aplicaciones de la lógica de Azure con funciones de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="088ee-103">Adición y ejecución de código personalizado para aplicaciones lógicas con Azure Functions</span><span class="sxs-lookup"><span data-stu-id="088ee-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="088ee-104">toorun fragmentos de código personalizado de C# o node.js en las aplicaciones lógicas, puede crear funciones personalizadas a través de funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="088ee-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="088ee-105">[Azure Functions](../azure-functions/functions-overview.md) ofrece una computación sin servidor en Microsoft Azure y es útil para realizar estas tareas:</span><span class="sxs-lookup"><span data-stu-id="088ee-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="088ee-106">Formato o proceso avanzados de los campos de Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="088ee-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="088ee-107">Realización de cálculos en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="088ee-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="088ee-108">Ampliar la funcionalidad de la aplicación hello lógica con funciones que se admiten en C# o node.js</span><span class="sxs-lookup"><span data-stu-id="088ee-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="088ee-109">Creación de funciones personalizadas para las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="088ee-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="088ee-110">Le recomendamos que cree una función en portal de Azure funciones hello, de hello **Webhook genérico - nodo** o **Webhook genérico - C#** plantillas.</span><span class="sxs-lookup"><span data-stu-id="088ee-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="088ee-111">resultado de Hello crea un rellena automáticamente una plantilla que acepta `application/json` desde una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="088ee-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="088ee-112">Las funciones que cree a partir de estas plantillas se detectan automáticamente y aparecen en hello Diseñador de la aplicación lógica en **funciones de Azure en mi región.**</span><span class="sxs-lookup"><span data-stu-id="088ee-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="088ee-113">En el portal de Azure, en Hola Hola **integrar** panel de la función, la plantilla debe mostrar que **modo** establecido demasiado**Webhook** y **Webhook tipo** se establece demasiado**JSON genérico**.</span><span class="sxs-lookup"><span data-stu-id="088ee-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="088ee-114">Funciones de Webhook Aceptar una solicitud y lo pasa en el método de Hola a través de un `data` variable.</span><span class="sxs-lookup"><span data-stu-id="088ee-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="088ee-115">Puede tener acceso a propiedades de saludo de la carga mediante el uso de la notación de puntos como `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="088ee-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="088ee-116">Por ejemplo, una función de JavaScript simple que convierte un valor de fecha y hora en una cadena de fecha aspecto Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="088ee-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="088ee-117">Llamada a Azure Functions desde Logic Apps</span><span class="sxs-lookup"><span data-stu-id="088ee-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="088ee-118">contenedores de hello toolist en su suscripción y la función hello select que desea toocall, en el Diseñador de la aplicación de lógica, haga clic en hello **acciones** menú y seleccione desde **funciones de Azure en mi región**.</span><span class="sxs-lookup"><span data-stu-id="088ee-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="088ee-119">Después de seleccionar la función hello, es más frecuentes toospecify un objeto de carga de la entrada.</span><span class="sxs-lookup"><span data-stu-id="088ee-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="088ee-120">Este objeto es mensaje Hola Hola lógica aplicación envía toohello función y debe ser un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="088ee-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="088ee-121">Por ejemplo, si desea toopass Hola **última modificación** fecha desde un desencadenador de Salesforce, carga de función hello podría ser similar a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="088ee-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Fecha de última modificación][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="088ee-123">Desencadenamiento de aplicaciones lógicas desde una función</span><span class="sxs-lookup"><span data-stu-id="088ee-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="088ee-124">Una aplicación lógica se puede desencadenar desde dentro de una función.</span><span class="sxs-lookup"><span data-stu-id="088ee-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="088ee-125">Consulte [Aplicaciones lógicas como puntos de conexión invocables](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="088ee-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="088ee-126">Crear una aplicación de lógica que tiene un desencadenador manual y, a continuación, desde dentro de la función, generar una dirección URL de desencadenador manual de HTTP POST toohello con una carga de Hola que desee enviar la aplicación de la lógica de toohello.</span><span class="sxs-lookup"><span data-stu-id="088ee-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="088ee-127">Creación de una función en el Diseñador de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="088ee-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="088ee-128">También puede crear una función de webhook de node.js desde el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="088ee-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="088ee-129">En primer lugar, seleccione **Azure Functions in my region** (Funciones de Azure en mi región) y elija un contenedor para la función.</span><span class="sxs-lookup"><span data-stu-id="088ee-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="088ee-130">Si aún no tiene un contenedor, deberá toocreate de hello [portal de Azure funciones](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="088ee-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="088ee-131">Seleccione **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="088ee-131">Then select **Create New**.</span></span>  

<span data-ttu-id="088ee-132">toogenerate una plantilla basada en datos de saludo que desea que toocompute, especifique el objeto de contexto de Hola que planea toopass a una función.</span><span class="sxs-lookup"><span data-stu-id="088ee-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="088ee-133">que debe ser un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="088ee-133">This object must be a JSON object.</span></span> <span data-ttu-id="088ee-134">Por ejemplo, si se pasa el contenido del archivo de Hola desde una acción de FTP, carga de contexto de hello es similar en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="088ee-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Carga de contexto][2]

> [!NOTE]
> <span data-ttu-id="088ee-136">Dado que este objeto no se ha convertido en una cadena, contenido de Hola se agrega directamente toohello carga JSON.</span><span class="sxs-lookup"><span data-stu-id="088ee-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="088ee-137">Sin embargo, se produce un error si el objeto de hello no es un token JSON (es decir, una cadena o una JSON/matriz de objetos).</span><span class="sxs-lookup"><span data-stu-id="088ee-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="088ee-138">objeto de hello toocast como una cadena, agregar comillas tal y como se muestra en la primera ilustración de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="088ee-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="088ee-139">Diseñador de Hello, a continuación, genera una plantilla de función que se puede crear en línea.</span><span class="sxs-lookup"><span data-stu-id="088ee-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="088ee-140">Las variables se crean previamente basándose en el contexto de Hola que planea toopass en función de Hola.</span><span class="sxs-lookup"><span data-stu-id="088ee-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
