---
title: 'Control de errores y excepciones: Azure Logic Apps | Microsoft Docs'
description: Patrones para el control de errores y excepciones en Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="5f8b7-103">Control de errores y excepciones en Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5f8b7-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="5f8b7-104">Azure Logic Apps proporciona completas herramientas y patrones para garantizar la solidez de sus integraciones y su resistencia frente a los errores.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="5f8b7-105">Cualquier arquitectura de integración presenta el reto de asegurarse de controlar correctamente el tiempo de inactividad o los problemas con sistemas dependientes.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="5f8b7-106">Logic Apps convierte el control de errores en una experiencia de primera clase al proporcionarle las herramientas que necesita para actuar ante las excepciones y los errores en los flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="5f8b7-107">Directivas de reintentos</span><span class="sxs-lookup"><span data-stu-id="5f8b7-107">Retry policies</span></span>

<span data-ttu-id="5f8b7-108">Una directiva de reintentos es el tipo más básico de control de errores y excepciones.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="5f8b7-109">Si una solicitud inicial ha agotado el tiempo de espera o ha producido error (toda solicitud que tenga como resultado una respuesta 429 o 5xx), esta directiva define si se debe reintentar la acción.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="5f8b7-110">De forma predeterminada, todas las acciones se reintentan 4 veces adicionales durante intervalos de 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="5f8b7-111">Por lo tanto, si la primera solicitud recibe una respuesta `500 Internal Server Error`, el motor de flujo de trabajo se pausa durante 20 segundos y vuelve a intentar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="5f8b7-112">Si, después de todos los reintentos, la respuesta sigue siendo una excepción o un error, el flujo de trabajo continúa y marca el estado de la acción como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="5f8b7-113">Puede configurar directivas de reintentos en las **entradas** para una acción determinada.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="5f8b7-114">Por ejemplo, puede configurar una directiva de reintentos para que haga hasta 4 intentos en intervalos de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="5f8b7-115">Para ver detalles completos sobre las propiedades de entrada, consulte [Workflow Actions and Triggers][retryPolicyMSDN] (Acciones y desencadenadores de flujo de trabajo).</span><span class="sxs-lookup"><span data-stu-id="5f8b7-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="5f8b7-116">Si desea que la acción HTTP se reintente 4 veces con intervalos de 10 minutos entre cada reintento, se usaría la siguiente definición:</span><span class="sxs-lookup"><span data-stu-id="5f8b7-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

<span data-ttu-id="5f8b7-117">Para más información sobre la sintaxis admitida, consulte la [sección sobre la directiva de reintentos en Workflow Actions and Triggers][retryPolicyMSDN] (Acciones y desencadenadores de flujo de trabajo).</span><span class="sxs-lookup"><span data-stu-id="5f8b7-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="5f8b7-118">Detección de errores con la propiedad RunAfter</span><span class="sxs-lookup"><span data-stu-id="5f8b7-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="5f8b7-119">Cada acción de aplicación lógica declara qué acciones deben finalizar antes de que se inicie la acción, algo parecido a ordenar los pasos del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="5f8b7-120">En la definición de la acción, esta ordenación se conoce como la propiedad `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="5f8b7-121">Esta propiedad es un objeto que describe qué acciones y estados de acciones ejecutan la acción.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="5f8b7-122">De forma predeterminada, todas las acciones que se agregan mediante el Diseñador de aplicación lógica se establecen en `runAfter` respecto al paso anterior, si el paso anterior era `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="5f8b7-123">Sin embargo, este valor se puede personalizar para que active acciones cuando las acciones anteriores sean `Failed`, `Skipped` o un posible conjunto de estos valores.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="5f8b7-124">Si desea agregar un elemento a un tema de Service Bus designado después de que una acción específica `Insert_Row` produzca un error, podría usar la siguiente configuración `runAfter`:</span><span class="sxs-lookup"><span data-stu-id="5f8b7-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

<span data-ttu-id="5f8b7-125">Observe que la propiedad `runAfter` está establecida para desencadenarse si el estado de la acción `Insert_Row` es `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="5f8b7-126">Para ejecutar la acción si el estado de la acción es `Succeeded`, `Failed` o `Skipped`, use esta sintaxis:</span><span class="sxs-lookup"><span data-stu-id="5f8b7-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="5f8b7-127">Las acciones que se ejecutan y completan correctamente después de que una acción anterior haya producido error se marcan como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="5f8b7-128">Este comportamiento significa que, si detecta correctamente todos los errores de un flujo de trabajo, la propia ejecución se marca como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="5f8b7-129">Ámbitos y resultados para evaluar acciones</span><span class="sxs-lookup"><span data-stu-id="5f8b7-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="5f8b7-130">Del mismo modo que puede establecer la propiedad RunAfter para acciones individuales, también puede agrupar acciones dentro de un [ámbito](../logic-apps/logic-apps-loops-and-scopes.md), que actúa como agrupación lógica de acciones.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="5f8b7-131">Los ámbitos son útiles para organizar las acciones de aplicación lógica y para realizar evaluaciones agregadas sobre el estado de un ámbito.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="5f8b7-132">El ámbito en sí recibe un estado una vez que hayan terminado todas las acciones en un ámbito.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="5f8b7-133">El estado del ámbito se determina con los mismos criterios que una ejecución.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="5f8b7-134">Si la acción final en una rama de la ejecución es `Failed` o `Aborted`, el estado es `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="5f8b7-135">Para activar acciones específicas para los errores que se produjeran dentro del ámbito, puede usar `runAfter` con un ámbito que esté marcado como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="5f8b7-136">Si *cualquier* acción en el ámbito produce un error, la ejecución después de que un ámbito produzca un error permite crear una única acción para detectar errores.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="5f8b7-137">Obtención del contexto de errores con resultados</span><span class="sxs-lookup"><span data-stu-id="5f8b7-137">Getting the context of failures with results</span></span>

<span data-ttu-id="5f8b7-138">Aunque la detección de errores desde un ámbito es útil, quizás también necesite el contexto como ayuda para comprender exactamente qué acciones han producido un error y los errores o códigos de estado que se hayan devuelto.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="5f8b7-139">La función del flujo de trabajo `@result()` proporciona contexto sobre el resultado de todas las acciones en un ámbito.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="5f8b7-140">`@result()` toma un único parámetro, un nombre de ámbito, y devuelve una matriz de todos los resultados de acción desde dentro de ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="5f8b7-141">Estos objetos de acción incluyen los mismos atributos que el objeto `@actions()`, como la hora de inicio de la acción, la hora de finalización de la acción, el estado de la acción, las entradas de acción, los id. de correlación de acción y la salidas de acción.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="5f8b7-142">Para enviar el contexto de las acciones que produjeron un error dentro de un ámbito, puede emparejar fácilmente una función `@result()` con una propiedad `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="5f8b7-143">Para ejecutar una acción *para cada una* de las acciones de un ámbito con el estado `Failed`, filtre la matriz de resultados para las acciones que produjeron un error; puede emparejar `@result()` con una acción **[Filtrar matriz](../connectors/connectors-native-query.md)** y un bucle **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="5f8b7-144">Puede tomar la matriz de resultados filtrada y realizar una acción para cada error mediante el bucle **ForEach** .</span><span class="sxs-lookup"><span data-stu-id="5f8b7-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="5f8b7-145">En este ejemplo, seguido de una explicación detallada, se envía una solicitud HTTP POST con el cuerpo de respuesta de todas las acciones que produjeron un error dentro del ámbito `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

<span data-ttu-id="5f8b7-146">Este es un tutorial detallado que describe lo que sucede:</span><span class="sxs-lookup"><span data-stu-id="5f8b7-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="5f8b7-147">Para obtener el resultado de todas las acciones dentro de `My_Scope`, la acción **Filtrar matriz** filtra `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="5f8b7-148">La condición para **Filtrar matriz** es cualquier elemento `@result()` que tenga el estado `Failed`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="5f8b7-149">Esta condición filtra la matriz con los resultados de todas las acciones de `My_Scope` a una matriz con solo los resultados de acción que hayan producido un error.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="5f8b7-150">Realización de una acción **For Each** en las salidas **Filtered Array**.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="5f8b7-151">En este paso se realiza una acción *para cada* acción resultante en error que se filtrara antes.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="5f8b7-152">Si solo hay una acción en el ámbito que produjera error, las acciones en el elemento `foreach` solo se ejecutan una vez.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="5f8b7-153">Muchas acciones con error causan una acción por cada error.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="5f8b7-154">Envío de una solicitud HTTP POST en el cuero de respuesta del elemento `foreach`, o `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="5f8b7-155">La forma del elemento `@result()` es la misma que la forma de `@actions()`, y se puede analizar del mismo modo.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="5f8b7-156">Incluya dos encabezados personalizados con el nombre de la acción con errores `@item()['name']` y el id. de seguimiento de cliente de la ejecución con errores `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="5f8b7-157">Como referencia, este es un ejemplo de un solo elemento `@result()`, que muestra las propiedades `name`, `body` y `clientTrackingId` que se analizan en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="5f8b7-158">Fuera de un elemento `foreach`, `@result()` devuelve una matriz de estos objetos.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

<span data-ttu-id="5f8b7-159">Para poner en práctica diferentes patrones de control de excepciones, puede usar las expresiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="5f8b7-160">Es posible que elija ejecutar una única acción de control de excepciones fuera del ámbito que acepte toda la matriz filtrada de errores y quite el elemento `foreach`.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="5f8b7-161">También puede incluir otras propiedades útiles de la respuesta `@result()` mostrada antes.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="5f8b7-162">Diagnósticos de Azure y datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="5f8b7-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="5f8b7-163">Los patrones anteriores son una manera excelente de controlar errores y excepciones dentro de una ejecución, pero también puede identificar y responder a los errores con independencia de la ejecución en sí.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="5f8b7-164">[Diagnósticos de Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) ofrece un método sencillo de enviar todos los eventos de flujo de trabajo (incluidos todos los estados de ejecución y acción) a una cuenta de almacenamiento de Azure o a un Centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="5f8b7-165">Para evaluar los estados de ejecución, puede supervisar los registros y las métricas, o publicarlos en la herramienta de supervisión que prefiera.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="5f8b7-166">Una posible opción es transmitir todos los eventos mediante el Centro de eventos de Azure a [Análisis de transmisiones](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="5f8b7-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="5f8b7-167">En Stream Analytics, puede escribir consultas en directo partiendo de anomalías, promedios o errores en los registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="5f8b7-168">Con Stream Analytics es fácil enviar resultados a otros orígenes de datos, como colas, temas, SQL, Azure Cosmos DB y Power BI.</span><span class="sxs-lookup"><span data-stu-id="5f8b7-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f8b7-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f8b7-169">Next Steps</span></span>

* [<span data-ttu-id="5f8b7-170">Vea cómo un cliente crea el control de errores con Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5f8b7-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="5f8b7-171">Encuentre más escenarios y ejemplos de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="5f8b7-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="5f8b7-172">Aprenda a crear implementaciones automatizadas para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="5f8b7-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="5f8b7-173">Creación e implementación de aplicaciones lógicas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f8b7-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
