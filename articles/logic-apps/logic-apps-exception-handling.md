---
title: "aaaError & control de excepciones: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="3ac4d-103">Control de errores y excepciones en Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3ac4d-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="3ac4d-104">Aplicaciones lógicas de Azure proporciona completas herramientas y toohelp de patrones Asegúrese de que sus integraciones son sólido y flexible frente a errores.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="3ac4d-105">Cualquier arquitectura de integración supone Hola desafío de hacer que el tiempo de inactividad del identificador de tooappropriately seguro o problemas de sistemas dependientes.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="3ac4d-106">Control de errores de lógica aplicaciones facilita una experiencia de primera clase, lo que le otorga Hola herramientas necesita tooact en excepciones y errores en los flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="3ac4d-107">Directivas de reintentos</span><span class="sxs-lookup"><span data-stu-id="3ac4d-107">Retry policies</span></span>

<span data-ttu-id="3ac4d-108">Una directiva de reintentos es tipo más básico de Hola de excepciones y control de errores.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="3ac4d-109">Si una solicitud inicial agotó el tiempo o no se pudo (cualquier solicitud que da como resultado un 429 o una respuesta 5xx), esta directiva define si debería volver a intentar la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="3ac4d-110">De forma predeterminada, todas las acciones se reintentan 4 veces adicionales durante intervalos de 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="3ac4d-111">Por tanto, si recibe la primera solicitud de hello un `500 Internal Server Error` respuesta, el motor de flujo de trabajo de Hola se detiene durante 20 segundos y los intentos de Hola solicitud de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="3ac4d-112">Si después de todos los reintentos, respuesta de hello sigue siendo una excepción o error, continúa de flujo de trabajo de Hola y Hola de marcas de estado de la acción como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="3ac4d-113">Puede configurar directivas de reintento de hello **entradas** para una acción concreta.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="3ac4d-114">Por ejemplo, puede configurar una tootry de directiva de reintento hasta 4 veces en intervalos de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="3ac4d-115">Para ver detalles completos sobre las propiedades de entrada, consulte [Workflow Actions and Triggers][retryPolicyMSDN] (Acciones y desencadenadores de flujo de trabajo).</span><span class="sxs-lookup"><span data-stu-id="3ac4d-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="3ac4d-116">Si deseara su tooretry de acción HTTP 4 veces y espere 10 minutos entre cada intento, usaría Hola siguiente definición:</span><span class="sxs-lookup"><span data-stu-id="3ac4d-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

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

<span data-ttu-id="3ac4d-117">Para obtener más información sobre la sintaxis admitida, vea hello [sección Directiva de reintentos en desencadenadores y acciones de flujo de trabajo][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="3ac4d-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="3ac4d-118">Detectar errores con hello RunAfter propiedad</span><span class="sxs-lookup"><span data-stu-id="3ac4d-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="3ac4d-119">Cada acción de aplicación lógica declara qué acciones deben finalizar antes de que empiece de acción de hello, como clasificación pasos hello en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="3ac4d-120">En la definición de la acción de hello, esta clasificación se denomina hello `runAfter` propiedad.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="3ac4d-121">Esta propiedad es un objeto que describe qué acciones y Estados de acción ejecutan la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="3ac4d-122">De forma predeterminada, todas las acciones agregadas a través de hello diseñador la lógica de aplicación se establecen demasiado`runAfter` paso anterior de hello si hello paso anterior `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="3ac4d-123">Sin embargo, puede personalizar esta acciones de toofire valor cuando las acciones anteriores tienen `Failed`, `Skipped`, o un conjunto posibles de estos valores.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="3ac4d-124">Si deseara tooadd un tooa elemento designado tema de Bus de servicio después de una acción específica `Insert_Row` se produce un error, podría utilizar Hola después `runAfter` configuración:</span><span class="sxs-lookup"><span data-stu-id="3ac4d-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

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

<span data-ttu-id="3ac4d-125">Hola aviso `runAfter` propiedad se establece toofire si hello `Insert_Row` acción es `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="3ac4d-126">acción de hello toorun si es el estado de la acción de hello `Succeeded`, `Failed`, o `Skipped`, use esta sintaxis:</span><span class="sxs-lookup"><span data-stu-id="3ac4d-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="3ac4d-127">Las acciones que se ejecutan y completan correctamente después de que una acción anterior haya producido error se marcan como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="3ac4d-128">Este comportamiento significa que si se correctamente catch todos los errores en un flujo de trabajo, Hola ejecutarse está marcada como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="3ac4d-129">Acciones de tooevaluate ámbitos y resultados</span><span class="sxs-lookup"><span data-stu-id="3ac4d-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="3ac4d-130">Toohow similar puede ejecutar después de acciones individuales, también puede agrupar acciones entre sí dentro de un [ámbito](../logic-apps/logic-apps-loops-and-scopes.md), que actúan como una agrupación lógica de acciones.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="3ac4d-131">Los ámbitos son útiles para organizar las acciones de aplicación lógica y para realizar evaluaciones agregadas en estado de Hola de un ámbito.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="3ac4d-132">ámbito de Hello propia recibe un estado una vez han terminado todas las acciones en un ámbito.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="3ac4d-133">el estado del ámbito de Hola se determina con hello mismos criterios como una ejecución.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="3ac4d-134">Si Hola acción final en una bifurcación de la ejecución es `Failed` o `Aborted`, estado de hello es `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="3ac4d-135">toofire acciones específicas para los errores que se produjeron en el ámbito de hello, puede usar `runAfter` con un ámbito que está marcado como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="3ac4d-136">Si *cualquier* producirá un error en las acciones en el ámbito de hello, ejecutándose después de que se produce un error en un ámbito permite crear una sola acción toocatch errores.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="3ac4d-137">Introducción al contexto de Hola de errores con resultados</span><span class="sxs-lookup"><span data-stu-id="3ac4d-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="3ac4d-138">Aunque es útil detectar errores de un ámbito, puede que le interese toohelp contexto que entender exactamente qué acciones de error, y los errores o los códigos de estado que se devolvieron.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="3ac4d-139">Hola `@result()` función de flujo de trabajo proporciona contexto sobre el resultado de hello de todas las acciones en un ámbito.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="3ac4d-140">`@result()`toma un único parámetro, el nombre de ámbito y devuelve una matriz de todos los resultados de acción de Hola desde dentro de ese ámbito.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="3ac4d-141">Estos objetos de acción incluyen hello mismo atributos como hello `@actions()` genera el objeto, incluidos la hora de inicio de la acción, hora de finalización de la acción, estado de la acción, entradas de la acción, identificador de correlación de acción y acción.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="3ac4d-142">contexto de toosend de todas las acciones que no se pudo dentro de un ámbito, puede emparejar fácilmente un `@result()` funcionando con un `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="3ac4d-143">tooexecute una acción *para cada* acción en un ámbito que `Failed`, matriz de Hola de filtro de resultados tooactions que han resultado erróneas, puede emparejar `@result()` con un  **[filtro matriz](../connectors/connectors-native-query.md)**  acción y un  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  bucle.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="3ac4d-144">Puede tomar la matriz de resultados filtrado hello y realizar una acción para cada error mediante hello **ForEach** bucle.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="3ac4d-145">Este es un ejemplo, seguido por una explicación detallada, que envía una solicitud HTTP POST con el cuerpo de respuesta de Hola de todas las acciones que no se pudo ámbito hello `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

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

<span data-ttu-id="3ac4d-146">Este es un toodescribe un tutorial detallado, lo que sucede:</span><span class="sxs-lookup"><span data-stu-id="3ac4d-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="3ac4d-147">resultado de hello tooget de todas las acciones de `My_Scope`, hello **filtro matriz** filtros de acción `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="3ac4d-148">Hola condición para **filtro matriz** es cualquier `@result()` elemento que tiene el estado igual demasiado`Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="3ac4d-149">Esta condición filtra la matriz de Hola a todos los resultados de acción de `My_Scope` tooan matriz solamente con resultados de la acción de error.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="3ac4d-150">Realizar una **For Each** acción en hello **filtra matriz** genera.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="3ac4d-151">En este paso se realiza una acción *para cada* acción resultante en error que se filtrara antes.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="3ac4d-152">Si se produce un error en una sola acción en el ámbito de hello, Hola acciones en hello `foreach` ejecutar solo una vez.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="3ac4d-153">Muchas acciones con error causan una acción por cada error.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="3ac4d-154">Enviar una solicitud HTTP POST en hello `foreach` elemento cuerpo de respuesta, o `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="3ac4d-155">Hola `@result()` forma Elem Hola igual como hello `@actions()` forma y se puede analizar Hola igual manera.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="3ac4d-156">Incluye dos encabezados personalizados con nombre de la acción error de hello `@item()['name']` y ejecución cliente Id. de seguimiento de error de hello `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="3ac4d-157">Como referencia, este es un ejemplo de una sola `@result()` elemento, que muestra hello `name`, `body`, y `clientTrackingId` propiedades que se analizan en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="3ac4d-158">Fuera de un elemento `foreach`, `@result()` devuelve una matriz de estos objetos.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="3ac4d-159">patrones de control de excepciones diferentes tooperform, puede usar expresiones de Hola que se ha mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="3ac4d-160">Puede elegir una única acción fuera de ámbito de Hola que acepta Hola toda filtrados matriz de errores de control de excepciones de tooexecute y quitar hello `foreach`.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="3ac4d-161">También puede incluir otras propiedades útiles de hello `@result()` respuesta se ha mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="3ac4d-162">Diagnósticos de Azure y datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="3ac4d-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="3ac4d-163">Hello modelos anteriores son errores de manera estupenda toohandle y excepciones dentro de una ejecución, pero también puede identificar y responder tooerrors independiente del programa Hola a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="3ac4d-164">[Diagnósticos de Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) proporciona una manera sencilla de toosend todas las cuenta de almacenamiento de Azure de tooan de eventos (incluidos todos los Estados de ejecución y acción) de flujo de trabajo o un concentrador de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="3ac4d-165">tooevaluate ejecutar Estados, puede supervisar los registros de Hola y métricas o publicarlos en cualquier herramienta de supervisión que prefiera.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="3ac4d-166">Una opción posible es toostream todos los eventos de Hola a través del concentrador de eventos de Azure en [análisis de transmisiones](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3ac4d-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="3ac4d-167">En el análisis de transmisiones, puede escribir las consultas actuales de las anomalías, medias o errores de hello registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="3ac4d-168">Análisis de transmisiones puede generar fácilmente orígenes de datos de tooother como colas, temas, SQL, base de datos de Azure Cosmos y Power BI.</span><span class="sxs-lookup"><span data-stu-id="3ac4d-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac4d-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ac4d-169">Next Steps</span></span>

* [<span data-ttu-id="3ac4d-170">Vea cómo un cliente crea el control de errores con Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3ac4d-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="3ac4d-171">Encuentre más escenarios y ejemplos de Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3ac4d-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="3ac4d-172">Obtenga información acerca de cómo toocreate automatizar las implementaciones para las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="3ac4d-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="3ac4d-173">Creación e implementación de aplicaciones lógicas con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ac4d-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
