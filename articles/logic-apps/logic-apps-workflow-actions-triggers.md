---
title: "aaaWorkflow acciones y desencadenadores: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="526c6-102">Acciones y desencadenadores de flujo de trabajo para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="526c6-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="526c6-103">Las aplicaciones lógicas constan de desencadenadores y acciones.</span><span class="sxs-lookup"><span data-stu-id="526c6-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="526c6-104">Existen seis tipos de desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="526c6-104">There are six types of triggers.</span></span> <span data-ttu-id="526c6-105">Cada tipo tiene una interfaz y un comportamiento diferentes.</span><span class="sxs-lookup"><span data-stu-id="526c6-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="526c6-106">También puede aprender sobre otros detalles examinando detalles Hola de hello [lenguaje de definición de flujo de trabajo](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="526c6-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="526c6-107">Siga leyendo toolearn más información acerca de los desencadenadores, acciones y cómo puede usarlos toobuild lógica aplicaciones tooimprove los procesos empresariales y flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="526c6-108">Desencadenadores</span><span class="sxs-lookup"><span data-stu-id="526c6-108">Triggers</span></span>  

<span data-ttu-id="526c6-109">Un desencadenador especifica llamadas de Hola que pueden iniciar una ejecución de su flujo de trabajo de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="526c6-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="526c6-110">Estas son dos maneras diferentes de hello tooinitiate una ejecución del flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="526c6-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="526c6-111">Un desencadenador de sondeo</span><span class="sxs-lookup"><span data-stu-id="526c6-111">A polling trigger</span></span>  

-   <span data-ttu-id="526c6-112">Un desencadenador de inserción: por llamada hello [API de REST de servicios de flujo de trabajo](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="526c6-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="526c6-113">Todos los desencadenadores contienen estos elementos de nivel superior:</span><span class="sxs-lookup"><span data-stu-id="526c6-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="526c6-114">Tipos de desencadenadores y sus entradas</span><span class="sxs-lookup"><span data-stu-id="526c6-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="526c6-115">Puede usar estos tipos de desencadenadores:</span><span class="sxs-lookup"><span data-stu-id="526c6-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="526c6-116">**Solicitar** \- hace un extremo para toocall de aplicación lógica de hello</span><span class="sxs-lookup"><span data-stu-id="526c6-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="526c6-117">**Periodicidad**: se desencadena en función de una programación definida.</span><span class="sxs-lookup"><span data-stu-id="526c6-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="526c6-118">**HTTP**: sondea un punto de conexión web HTTP.</span><span class="sxs-lookup"><span data-stu-id="526c6-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="526c6-119">punto de conexión de Hello HTTP debe ajustarse contrato de activación específico tooa \- mediante un 202\-patrón asincrónico, o devolviendo una matriz</span><span class="sxs-lookup"><span data-stu-id="526c6-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="526c6-120">**ApiConnection** \- desencadenan sondeos como Hola HTTP, sin embargo, aprovecha las ventajas de hello [API administrada por Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="526c6-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="526c6-121">**HTTPWebhook** \- abre un extremo, similar toohello Manual desencadenador, sin embargo, llama también a tooa especifica la dirección URL tooregister y anular el registro</span><span class="sxs-lookup"><span data-stu-id="526c6-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="526c6-122">**ApiConnectionWebhook** \- funciona como Hola HTTPWebhook desencadenador aprovechando las ventajas de hello API administrada por Microsoft</span><span class="sxs-lookup"><span data-stu-id="526c6-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="526c6-123">Cada tipo de desencadenador tiene un conjunto de **entradas** diferente que define su comportamiento.</span><span class="sxs-lookup"><span data-stu-id="526c6-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="526c6-124">Desencadenador de solicitud</span><span class="sxs-lookup"><span data-stu-id="526c6-124">Request trigger</span></span>  

<span data-ttu-id="526c6-125">Este desencadenador actúa como un punto de conexión que se llama a través de una solicitud HTTP tooinvoke la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="526c6-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="526c6-126">Un desencadenador de solicitud es similar a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="526c6-127">También hay una propiedad opcional denominada **schema**:</span><span class="sxs-lookup"><span data-stu-id="526c6-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="526c6-128">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-128">Element name</span></span>|<span data-ttu-id="526c6-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-129">Required</span></span>|<span data-ttu-id="526c6-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="526c6-131">schema</span><span class="sxs-lookup"><span data-stu-id="526c6-131">schema</span></span>|<span data-ttu-id="526c6-132">No</span><span class="sxs-lookup"><span data-stu-id="526c6-132">No</span></span>|<span data-ttu-id="526c6-133">Un esquema JSON que valida la solicitud entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="526c6-134">Resulta útil para ayudar a los pasos de flujo de trabajo posterior a saber qué tooreference de propiedades.</span><span class="sxs-lookup"><span data-stu-id="526c6-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="526c6-135">tooinvoke este extremo, necesita hello toocall *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="526c6-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="526c6-136">Consulte [API de REST de servicio de flujo de trabajo](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="526c6-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="526c6-137">Desencadenador de periodicidad</span><span class="sxs-lookup"><span data-stu-id="526c6-137">Recurrence trigger</span></span>  

<span data-ttu-id="526c6-138">Un desencadenador de periodicidad es aquel que se ejecuta según una programación definida.</span><span class="sxs-lookup"><span data-stu-id="526c6-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="526c6-139">Ese tipo de desencadenador podría parecerse a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="526c6-140">Como puede ver, es un toorun de manera sencilla un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="526c6-141">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-141">Element name</span></span>|<span data-ttu-id="526c6-142">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-142">Required</span></span>|<span data-ttu-id="526c6-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="526c6-144">frequency</span><span class="sxs-lookup"><span data-stu-id="526c6-144">frequency</span></span>|<span data-ttu-id="526c6-145">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-145">Yes</span></span>|<span data-ttu-id="526c6-146">¿Con qué frecuencia hello desencadenador se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="526c6-146">How often hello trigger executes.</span></span> <span data-ttu-id="526c6-147">Use solo uno de estos valores posibles: segundo, minuto, hora, día, semana, mes o año.</span><span class="sxs-lookup"><span data-stu-id="526c6-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="526c6-148">interval</span><span class="sxs-lookup"><span data-stu-id="526c6-148">interval</span></span>|<span data-ttu-id="526c6-149">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-149">Yes</span></span>|<span data-ttu-id="526c6-150">Intervalo de hello dada la frecuencia de repetición de Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="526c6-151">startTime</span><span class="sxs-lookup"><span data-stu-id="526c6-151">startTime</span></span>|<span data-ttu-id="526c6-152">No</span><span class="sxs-lookup"><span data-stu-id="526c6-152">No</span></span>|<span data-ttu-id="526c6-153">Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria.</span><span class="sxs-lookup"><span data-stu-id="526c6-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="526c6-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="526c6-154">timeZone</span></span>|<span data-ttu-id="526c6-155">no</span><span class="sxs-lookup"><span data-stu-id="526c6-155">no</span></span>|<span data-ttu-id="526c6-156">Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria.</span><span class="sxs-lookup"><span data-stu-id="526c6-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="526c6-157">También puede programar un desencadenador que se toostart ejecute en algún momento futuro Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="526c6-158">Por ejemplo, si desea que toostart semanales notificar todos los lunes puede programar toostart de aplicación lógica de hello todos los lunes mediante la creación de hello después desencadenador:</span><span class="sxs-lookup"><span data-stu-id="526c6-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="526c6-159">Desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="526c6-159">HTTP trigger</span></span>  

<span data-ttu-id="526c6-160">Desencadenadores HTTP sondean un extremo especificado y comprobación Hola respuesta toodetermine si se debe ejecutar el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="526c6-161">objeto de entradas de Hello toma conjunto Hola de parámetros necesarios tooconstruct una llamada HTTP:</span><span class="sxs-lookup"><span data-stu-id="526c6-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="526c6-162">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-162">Element name</span></span>|<span data-ttu-id="526c6-163">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-163">Required</span></span>|<span data-ttu-id="526c6-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-164">Description</span></span>|<span data-ttu-id="526c6-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="526c6-166">estático</span><span class="sxs-lookup"><span data-stu-id="526c6-166">method</span></span>|<span data-ttu-id="526c6-167">yes</span><span class="sxs-lookup"><span data-stu-id="526c6-167">yes</span></span>|<span data-ttu-id="526c6-168">Puede ser uno de hello siguiendo métodos HTTP: GET, POST, PUT, HEAD, PATCH o DELETE</span><span class="sxs-lookup"><span data-stu-id="526c6-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="526c6-169">String</span><span class="sxs-lookup"><span data-stu-id="526c6-169">String</span></span>|  
|<span data-ttu-id="526c6-170">uri</span><span class="sxs-lookup"><span data-stu-id="526c6-170">uri</span></span>|<span data-ttu-id="526c6-171">yes</span><span class="sxs-lookup"><span data-stu-id="526c6-171">yes</span></span>|<span data-ttu-id="526c6-172">Hola extremo http o https que se llama.</span><span class="sxs-lookup"><span data-stu-id="526c6-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="526c6-173">2 kilobytes como máximo.</span><span class="sxs-lookup"><span data-stu-id="526c6-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="526c6-174">String</span><span class="sxs-lookup"><span data-stu-id="526c6-174">String</span></span>|  
|<span data-ttu-id="526c6-175">Consultas</span><span class="sxs-lookup"><span data-stu-id="526c6-175">queries</span></span>|<span data-ttu-id="526c6-176">No</span><span class="sxs-lookup"><span data-stu-id="526c6-176">No</span></span>|<span data-ttu-id="526c6-177">Objeto que representa la dirección de URL de hello consulta parámetros tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="526c6-178">Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="526c6-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="526c6-179">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-179">Object</span></span>|  
|<span data-ttu-id="526c6-180">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-180">headers</span></span>|<span data-ttu-id="526c6-181">No</span><span class="sxs-lookup"><span data-stu-id="526c6-181">No</span></span>|<span data-ttu-id="526c6-182">Objeto que representa cada uno de los encabezados de Hola que se envía la solicitud de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="526c6-183">Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="526c6-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="526c6-184">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-184">Object</span></span>|  
|<span data-ttu-id="526c6-185">body</span><span class="sxs-lookup"><span data-stu-id="526c6-185">body</span></span>|<span data-ttu-id="526c6-186">No</span><span class="sxs-lookup"><span data-stu-id="526c6-186">No</span></span>|<span data-ttu-id="526c6-187">Objeto que representa la carga de Hola que se envía el punto de conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="526c6-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-188">Object</span></span>|  
|<span data-ttu-id="526c6-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="526c6-189">retryPolicy</span></span>|<span data-ttu-id="526c6-190">No</span><span class="sxs-lookup"><span data-stu-id="526c6-190">No</span></span>|<span data-ttu-id="526c6-191">Un objeto que le permite personalizar el comportamiento de reintento de hello errores de 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="526c6-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="526c6-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-192">Object</span></span>|  
|<span data-ttu-id="526c6-193">authentication</span><span class="sxs-lookup"><span data-stu-id="526c6-193">authentication</span></span>|<span data-ttu-id="526c6-194">No</span><span class="sxs-lookup"><span data-stu-id="526c6-194">No</span></span>|<span data-ttu-id="526c6-195">Método de hello representa que Hola solicitud se debe autenticar.</span><span class="sxs-lookup"><span data-stu-id="526c6-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="526c6-196">Para más información sobre este objeto, consulte [Autenticación saliente de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="526c6-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="526c6-197">Aparte del programador, hay una propiedad más admitida: `authority`. De forma predeterminada, este valor es `https://login.windows.net` cuando no se especifica, pero puede usar una audiencia diferente como `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="526c6-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="526c6-198">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-198">Object</span></span>|  
  
<span data-ttu-id="526c6-199">desencadenador de Hello HTTP requiere Hola API HTTP tooconform con un toowork de modelo específico bien con la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="526c6-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="526c6-200">Requiere Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="526c6-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="526c6-201">Response</span><span class="sxs-lookup"><span data-stu-id="526c6-201">Response</span></span>|<span data-ttu-id="526c6-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="526c6-203">Código de estado</span><span class="sxs-lookup"><span data-stu-id="526c6-203">Status code</span></span>|<span data-ttu-id="526c6-204">Código de estado 200 \(Aceptar\) toocause una ejecución.</span><span class="sxs-lookup"><span data-stu-id="526c6-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="526c6-205">Cualquier otro código de estado no provoca una ejecución.</span><span class="sxs-lookup"><span data-stu-id="526c6-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="526c6-206">Encabezado Retry\-after</span><span class="sxs-lookup"><span data-stu-id="526c6-206">Retry\-after header</span></span>|<span data-ttu-id="526c6-207">Número de segundos hasta que la aplicación de la lógica de hello sondea extremo Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="526c6-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="526c6-208">Encabezado Location</span><span class="sxs-lookup"><span data-stu-id="526c6-208">Location header</span></span>|<span data-ttu-id="526c6-209">Hola toocall de dirección URL en el siguiente intervalo de sondeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="526c6-210">Si no se especifica, se utiliza la dirección URL original de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="526c6-211">Estos son algunos ejemplos de diferentes comportamientos para diferentes tipos de solicitudes:</span><span class="sxs-lookup"><span data-stu-id="526c6-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="526c6-212">Response code</span><span class="sxs-lookup"><span data-stu-id="526c6-212">Response code</span></span>|<span data-ttu-id="526c6-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="526c6-213">Retry\-After</span></span>|<span data-ttu-id="526c6-214">Comportamiento</span><span class="sxs-lookup"><span data-stu-id="526c6-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="526c6-215">200</span><span class="sxs-lookup"><span data-stu-id="526c6-215">200</span></span>|<span data-ttu-id="526c6-216">\(Ninguna\)</span><span class="sxs-lookup"><span data-stu-id="526c6-216">\(none\)</span></span>|<span data-ttu-id="526c6-217">No es un desencadenador válido, reintento\-After es motor Hola necesario; de lo contrario nunca sondea la siguiente solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="526c6-218">202</span><span class="sxs-lookup"><span data-stu-id="526c6-218">202</span></span>|<span data-ttu-id="526c6-219">60</span><span class="sxs-lookup"><span data-stu-id="526c6-219">60</span></span>|<span data-ttu-id="526c6-220">No se desencadenará el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="526c6-221">próximo intento de Hola se realiza en un minuto.</span><span class="sxs-lookup"><span data-stu-id="526c6-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="526c6-222">200</span><span class="sxs-lookup"><span data-stu-id="526c6-222">200</span></span>|<span data-ttu-id="526c6-223">10</span><span class="sxs-lookup"><span data-stu-id="526c6-223">10</span></span>|<span data-ttu-id="526c6-224">Ejecutar el flujo de trabajo de Hola y comprobar de nuevo para el contenido de más de 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="526c6-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="526c6-225">400</span><span class="sxs-lookup"><span data-stu-id="526c6-225">400</span></span>|<span data-ttu-id="526c6-226">\(Ninguna\)</span><span class="sxs-lookup"><span data-stu-id="526c6-226">\(none\)</span></span>|<span data-ttu-id="526c6-227">No se ejecutan el flujo de trabajo de hello, si la solicitud es incorrecta.</span><span class="sxs-lookup"><span data-stu-id="526c6-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="526c6-228">Si no hay ningún **directiva de reintentos** definido, a continuación, se utiliza la directiva predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="526c6-229">Una vez alcanzado el número de Hola de reintentos, el desencadenador de hello ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="526c6-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="526c6-230">500</span><span class="sxs-lookup"><span data-stu-id="526c6-230">500</span></span>|<span data-ttu-id="526c6-231">\(Ninguna\)</span><span class="sxs-lookup"><span data-stu-id="526c6-231">\(none\)</span></span>|<span data-ttu-id="526c6-232">Error del servidor, no se ejecutan el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="526c6-233">Si no hay ningún **directiva de reintentos** definido, a continuación, se utiliza la directiva predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="526c6-234">Una vez alcanzado el número de Hola de reintentos, el desencadenador de hello ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="526c6-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="526c6-235">salidas de Hola de un desencadenador HTTP ser similar a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="526c6-236">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-236">Element name</span></span>|<span data-ttu-id="526c6-237">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-237">Description</span></span>|<span data-ttu-id="526c6-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="526c6-239">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-239">headers</span></span>|<span data-ttu-id="526c6-240">encabezados de Hola de respuesta de http de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-240">hello headers of hello http response.</span></span>|<span data-ttu-id="526c6-241">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-241">Object</span></span>|  
|<span data-ttu-id="526c6-242">body</span><span class="sxs-lookup"><span data-stu-id="526c6-242">body</span></span>|<span data-ttu-id="526c6-243">cuerpo de Hola de respuesta de http de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-243">hello body of hello http response.</span></span>|<span data-ttu-id="526c6-244">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="526c6-245">Desencadenador de conexión de API</span><span class="sxs-lookup"><span data-stu-id="526c6-245">API Connection trigger</span></span>  

<span data-ttu-id="526c6-246">Hola API conexión desencadenador es similar toohello HTTP en su funcionalidad básica.</span><span class="sxs-lookup"><span data-stu-id="526c6-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="526c6-247">Sin embargo, los parámetros de Hola para identificar la acción de hello son diferentes.</span><span class="sxs-lookup"><span data-stu-id="526c6-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="526c6-248">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="526c6-249">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-249">Element name</span></span>|<span data-ttu-id="526c6-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-250">Required</span></span>|<span data-ttu-id="526c6-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-251">Type</span></span>|<span data-ttu-id="526c6-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="526c6-253">host</span><span class="sxs-lookup"><span data-stu-id="526c6-253">host</span></span>|<span data-ttu-id="526c6-254">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-254">Yes</span></span>||<span data-ttu-id="526c6-255">Hola ApiApp había hospedado puerta de enlace y el identificador.</span><span class="sxs-lookup"><span data-stu-id="526c6-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="526c6-256">estático</span><span class="sxs-lookup"><span data-stu-id="526c6-256">method</span></span>|<span data-ttu-id="526c6-257">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-257">Yes</span></span>|<span data-ttu-id="526c6-258">String</span><span class="sxs-lookup"><span data-stu-id="526c6-258">String</span></span>|<span data-ttu-id="526c6-259">Puede ser uno de hello siguiendo métodos HTTP: **obtener**, **POST**, **colocar**, **eliminar**, **PATCH**, o  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="526c6-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="526c6-260">Consultas</span><span class="sxs-lookup"><span data-stu-id="526c6-260">queries</span></span>|<span data-ttu-id="526c6-261">No</span><span class="sxs-lookup"><span data-stu-id="526c6-261">No</span></span>|<span data-ttu-id="526c6-262">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-262">Object</span></span>|<span data-ttu-id="526c6-263">Toobe de parámetros de consulta de hello representa agrega dirección URL de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="526c6-264">Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="526c6-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="526c6-265">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-265">headers</span></span>|<span data-ttu-id="526c6-266">No</span><span class="sxs-lookup"><span data-stu-id="526c6-266">No</span></span>|<span data-ttu-id="526c6-267">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-267">Object</span></span>|<span data-ttu-id="526c6-268">Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="526c6-269">Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="526c6-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="526c6-270">body</span><span class="sxs-lookup"><span data-stu-id="526c6-270">body</span></span>|<span data-ttu-id="526c6-271">No</span><span class="sxs-lookup"><span data-stu-id="526c6-271">No</span></span>|<span data-ttu-id="526c6-272">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-272">Object</span></span>|<span data-ttu-id="526c6-273">Representa la carga de Hola que se envía el punto de conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="526c6-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="526c6-274">retryPolicy</span></span>|<span data-ttu-id="526c6-275">No</span><span class="sxs-lookup"><span data-stu-id="526c6-275">No</span></span>|<span data-ttu-id="526c6-276">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-276">Object</span></span>|<span data-ttu-id="526c6-277">Permite el comportamiento para reintentar hello toocustomize errores de 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="526c6-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="526c6-278">Autenticación</span><span class="sxs-lookup"><span data-stu-id="526c6-278">authentication</span></span>|<span data-ttu-id="526c6-279">No</span><span class="sxs-lookup"><span data-stu-id="526c6-279">No</span></span>|<span data-ttu-id="526c6-280">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-280">Object</span></span>|<span data-ttu-id="526c6-281">Método de hello representa que Hola solicitud se debe autenticar.</span><span class="sxs-lookup"><span data-stu-id="526c6-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="526c6-282">Para más información sobre este objeto, consulte [Autenticación saliente de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="526c6-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="526c6-283">propiedades de Hola para host son:</span><span class="sxs-lookup"><span data-stu-id="526c6-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="526c6-284">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-284">Element name</span></span>|<span data-ttu-id="526c6-285">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-285">Required</span></span>|<span data-ttu-id="526c6-286">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="526c6-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="526c6-287">api runtimeUrl</span></span>|<span data-ttu-id="526c6-288">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-288">Yes</span></span>|<span data-ttu-id="526c6-289">punto de conexión de Hola de hello API administrada.</span><span class="sxs-lookup"><span data-stu-id="526c6-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="526c6-290">connection name</span><span class="sxs-lookup"><span data-stu-id="526c6-290">connection name</span></span>||<span data-ttu-id="526c6-291">Debe ser un parámetro de referencia tooa llamado `$connection` y es el nombre de Hola de conexión de API de hello administrado que Hola usos de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="526c6-292">salidas de Hola de un desencadenador de conexión de API son:</span><span class="sxs-lookup"><span data-stu-id="526c6-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="526c6-293">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-293">Element name</span></span>|<span data-ttu-id="526c6-294">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-294">Type</span></span>|<span data-ttu-id="526c6-295">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="526c6-296">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-296">headers</span></span>|<span data-ttu-id="526c6-297">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-297">Object</span></span>|<span data-ttu-id="526c6-298">encabezados de Hola de respuesta de http de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="526c6-299">body</span><span class="sxs-lookup"><span data-stu-id="526c6-299">body</span></span>|<span data-ttu-id="526c6-300">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-300">Object</span></span>|<span data-ttu-id="526c6-301">cuerpo de Hola de respuesta de http de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="526c6-302">Desencadenador HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="526c6-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="526c6-303">Aperturas de desencadenador de Hello HTTPWebhook un punto de conexión, desencadenador manual de toohello similares, pero hello HTTPWebhook desencadenador también llama a tooa especifica la dirección URL tooregister y anular el registro.</span><span class="sxs-lookup"><span data-stu-id="526c6-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="526c6-304">Este es un ejemplo del aspecto que podría tener un desencadenador HTTPWebhook:</span><span class="sxs-lookup"><span data-stu-id="526c6-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="526c6-305">Muchas de estas secciones son opcionales y comportamiento de Hola de hello Webhook depende de qué secciones se proporciona o se omite.</span><span class="sxs-lookup"><span data-stu-id="526c6-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="526c6-306">propiedades de Hola de un Webhook son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="526c6-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="526c6-307">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-307">Element name</span></span>|<span data-ttu-id="526c6-308">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-308">Required</span></span>|<span data-ttu-id="526c6-309">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="526c6-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="526c6-310">subscribe</span></span>|<span data-ttu-id="526c6-311">No</span><span class="sxs-lookup"><span data-stu-id="526c6-311">No</span></span>|<span data-ttu-id="526c6-312">Hola solicitud que se llama al desencadenador de Hola se crea y realiza el registro inicial del Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="526c6-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="526c6-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="526c6-313">unsubscribe</span></span>|<span data-ttu-id="526c6-314">No</span><span class="sxs-lookup"><span data-stu-id="526c6-314">No</span></span>|<span data-ttu-id="526c6-315">Hola solicitud de salida cuando se elimina el desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="526c6-316">**Suscribirse** Hola salida llamada que ha realizado toostart escucha tooevents.</span><span class="sxs-lookup"><span data-stu-id="526c6-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="526c6-317">Esta llamada se inicia con hello es el mismo conjunto de parámetros que Hola acciones HTTP normales.</span><span class="sxs-lookup"><span data-stu-id="526c6-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="526c6-318">Esta llamada saliente se realiza cualquier Hola tiempo cambios de flujo de trabajo de cualquier manera, por ejemplo, siempre que las credenciales de Hola se revierten y el cambio de parámetros de entrada del desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="526c6-319">toosupport esta llamada, hay una nueva función: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="526c6-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="526c6-320">Esta función devuelve una dirección URL única para este desencadenador específico en este flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="526c6-321">Que representa el identificador único de Hola para los extremos de Hola que utilizan Hola REST de servicio.</span><span class="sxs-lookup"><span data-stu-id="526c6-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="526c6-322">**Unsubscribe** se llama cuando una operación representa este desencadenador como no válido, lo que incluye:</span><span class="sxs-lookup"><span data-stu-id="526c6-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="526c6-323">Eliminar o deshabilitar el desencadenador de Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="526c6-324">Eliminación o deshabilitación de flujo de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="526c6-325">Eliminar o deshabilitar la suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="526c6-326">aplicación de la lógica de Hello llama automáticamente a Hola acción Cancelar la suscripción.</span><span class="sxs-lookup"><span data-stu-id="526c6-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="526c6-327">Hola parámetros de función toothis Hola igual como desencadenador de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="526c6-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="526c6-328">Hello salidas de desencadenador de hello HTTPWebhook son contenido de saludo de solicitud entrante de hello:</span><span class="sxs-lookup"><span data-stu-id="526c6-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="526c6-329">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-329">Element name</span></span>|<span data-ttu-id="526c6-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-330">Type</span></span>|<span data-ttu-id="526c6-331">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="526c6-332">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-332">headers</span></span>|<span data-ttu-id="526c6-333">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-333">Object</span></span>|<span data-ttu-id="526c6-334">encabezados de saludo de solicitud de http de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="526c6-335">body</span><span class="sxs-lookup"><span data-stu-id="526c6-335">body</span></span>|<span data-ttu-id="526c6-336">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-336">Object</span></span>|<span data-ttu-id="526c6-337">cuerpo de saludo de solicitud de http de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="526c6-338">Se pueden especificar límites en una acción de webhook en hello misma manera que [HTTP asincrónica límites](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="526c6-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="526c6-339">Condiciones</span><span class="sxs-lookup"><span data-stu-id="526c6-339">Conditions</span></span>  

<span data-ttu-id="526c6-340">Para cualquier desencadenador, puede usar uno o más toodetermine condiciones si debe ejecutar el flujo de trabajo de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="526c6-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="526c6-341">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="526c6-342">En este caso, Hola desencadenadores solo de informe del flujo de trabajo de hello `sendReports` parámetro se establece tootrue.</span><span class="sxs-lookup"><span data-stu-id="526c6-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="526c6-343">Por último, las condiciones pueden hacer referencia a código de estado de Hola de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="526c6-344">Por ejemplo, podría iniciar un flujo de trabajo solo cuando su sitio web devuelva un código de estado 500, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="526c6-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="526c6-345">Cuando hace referencia a cualquier expresión de código de estado de Hola de desencadenador de hello \(de ninguna manera\), Hola comportamiento predeterminado \(desencadenador solo en 200 \(Aceptar\) \) se reemplaza.</span><span class="sxs-lookup"><span data-stu-id="526c6-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="526c6-346">Por ejemplo, si desea tootrigger de código de estado 200 y el código de estado 201, tendrá que tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` como la condición.</span><span class="sxs-lookup"><span data-stu-id="526c6-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="526c6-347">Inicio de varias ejecuciones para una solicitud</span><span class="sxs-lookup"><span data-stu-id="526c6-347">Start multiple runs for a request</span></span>

<span data-ttu-id="526c6-348">tookick desactivar varias ejecuciones para una única solicitud `splitOn` es útil, por ejemplo, cuando se desea toopoll un punto de conexión que puede tener varios elementos nuevos entre los intervalos de sondeo.</span><span class="sxs-lookup"><span data-stu-id="526c6-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="526c6-349">Con `splitOn`, especificar propiedad Hola dentro de la carga de respuesta de Hola que contiene la matriz de Hola de elementos, cada uno de los cuales desea toouse toostart una ejecución del desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="526c6-350">Por ejemplo, imagine que tiene una API que devuelve Hola después de respuesta:</span><span class="sxs-lookup"><span data-stu-id="526c6-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="526c6-351">La lógica de aplicación solo necesita contenido de filas de hello, por lo que puede crear el desencadenador como en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="526c6-352">A continuación, en la definición de flujo de trabajo de hello `@triggerBody().name` devuelve `mycoolrow` para hello ejecuta por primera vez, y `another row` para la segunda ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="526c6-353">Hola desencadenador salidas aspecto mostrado en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="526c6-354">Por tanto, si usas `SplitOn`, no se puede obtener propiedades de Hola que están fuera de la matriz de hello, en este caso, hello `Status` campo.</span><span class="sxs-lookup"><span data-stu-id="526c6-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="526c6-355">En este ejemplo, utilizamos hello `?` tooavoid capaz de operador toobe un error si hello `Rows` propiedad no está presente.</span><span class="sxs-lookup"><span data-stu-id="526c6-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="526c6-356">Instancia de ejecución única</span><span class="sxs-lookup"><span data-stu-id="526c6-356">Single run instance</span></span>

<span data-ttu-id="526c6-357">Puede configurar desencadenadores que tengan un incendio de periodicidad propiedad tooonly si han completado todas las ejecuciones activas.</span><span class="sxs-lookup"><span data-stu-id="526c6-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="526c6-358">Si se produce una periodicidad programada mientras hay una ejecución en curso, el desencadenador de hello omite y espera hasta Hola siguiente repetición programada intervalo toocheck nuevo.</span><span class="sxs-lookup"><span data-stu-id="526c6-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="526c6-359">Puede configurar a través de opciones de la operación de hello:</span><span class="sxs-lookup"><span data-stu-id="526c6-359">You can configure this setting through hello operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="526c6-360">Tipos y entradas</span><span class="sxs-lookup"><span data-stu-id="526c6-360">Types and inputs</span></span>  

<span data-ttu-id="526c6-361">Hay muchos tipos de acciones, cada una con un comportamiento único.</span><span class="sxs-lookup"><span data-stu-id="526c6-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="526c6-362">Las acciones de colección pueden contener muchas otras acciones dentro de sí mismas.</span><span class="sxs-lookup"><span data-stu-id="526c6-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="526c6-363">Acciones estándar</span><span class="sxs-lookup"><span data-stu-id="526c6-363">Standard actions</span></span>  

-   <span data-ttu-id="526c6-364">**HTTP**: esta acción llama a un punto de conexión web HTTP.</span><span class="sxs-lookup"><span data-stu-id="526c6-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="526c6-365">**ApiConnection** \- esta acción se comporta como Hola acción HTTP, pero usa Hola API administrada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="526c6-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="526c6-366">**ApiConnectionWebhook** \- como HTTPWebhook, pero utiliza Hola API administrada por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="526c6-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="526c6-367">**Response**: esta acción define una respuesta para una llamada entrante.</span><span class="sxs-lookup"><span data-stu-id="526c6-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="526c6-368">**Wait**: esta acción simple espera una cantidad fija de tiempo o hasta una hora específica.</span><span class="sxs-lookup"><span data-stu-id="526c6-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="526c6-369">**Workflow**: esta acción representa un flujo de trabajo anidado.</span><span class="sxs-lookup"><span data-stu-id="526c6-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="526c6-370">**Función**: esta acción representa una función de Azure.</span><span class="sxs-lookup"><span data-stu-id="526c6-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="526c6-371">Acciones de colección</span><span class="sxs-lookup"><span data-stu-id="526c6-371">Collection actions</span></span>

-   <span data-ttu-id="526c6-372">**Scope**: esta acción es una agrupación lógica de otras acciones.</span><span class="sxs-lookup"><span data-stu-id="526c6-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="526c6-373">**Condición** \- esta acción evalúa una expresión y ejecuta la bifurcación de resultado de hello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="526c6-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="526c6-374">**ForEach**\-: esta acción de bucle recorre en iteración una matriz y realiza acciones internas para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="526c6-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="526c6-375">**Hasta que** \- esta acción bucle ejecuta acciones internas hasta que una condición da como resultado tootrue.</span><span class="sxs-lookup"><span data-stu-id="526c6-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="526c6-376">Cada tipo de acción tiene un conjunto diferente de **entradas** que definen el comportamiento de la acción.</span><span class="sxs-lookup"><span data-stu-id="526c6-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="526c6-377">Acción HTTP</span><span class="sxs-lookup"><span data-stu-id="526c6-377">HTTP action</span></span>  

<span data-ttu-id="526c6-378">Acciones HTTP llamar a un punto de conexión especificada y comprobación Hola respuesta toodetermine si se debe ejecutar el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="526c6-379">Hola **entradas** objeto toma conjunto Hola de parámetros necesarios tooconstruct Hola HTTP llamada:</span><span class="sxs-lookup"><span data-stu-id="526c6-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="526c6-380">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-380">Element name</span></span>|<span data-ttu-id="526c6-381">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-381">Required</span></span>|<span data-ttu-id="526c6-382">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-382">Type</span></span>|<span data-ttu-id="526c6-383">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="526c6-384">estático</span><span class="sxs-lookup"><span data-stu-id="526c6-384">method</span></span>|<span data-ttu-id="526c6-385">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-385">Yes</span></span>|<span data-ttu-id="526c6-386">String</span><span class="sxs-lookup"><span data-stu-id="526c6-386">String</span></span>|<span data-ttu-id="526c6-387">Puede ser uno de hello siguiendo métodos HTTP: **obtener**, **POST**, **colocar**, **eliminar**, **PATCH**, o  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="526c6-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="526c6-388">uri</span><span class="sxs-lookup"><span data-stu-id="526c6-388">uri</span></span>|<span data-ttu-id="526c6-389">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-389">Yes</span></span>|<span data-ttu-id="526c6-390">String</span><span class="sxs-lookup"><span data-stu-id="526c6-390">String</span></span>|<span data-ttu-id="526c6-391">Hola extremo http o https que se llama.</span><span class="sxs-lookup"><span data-stu-id="526c6-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="526c6-392">La longitud máxima es de 2 kilobytes.</span><span class="sxs-lookup"><span data-stu-id="526c6-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="526c6-393">Consultas</span><span class="sxs-lookup"><span data-stu-id="526c6-393">queries</span></span>|<span data-ttu-id="526c6-394">No</span><span class="sxs-lookup"><span data-stu-id="526c6-394">No</span></span>|<span data-ttu-id="526c6-395">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-395">Object</span></span>|<span data-ttu-id="526c6-396">Representa la URL de hello consulta parámetros tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="526c6-397">Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="526c6-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="526c6-398">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-398">headers</span></span>|<span data-ttu-id="526c6-399">No</span><span class="sxs-lookup"><span data-stu-id="526c6-399">No</span></span>|<span data-ttu-id="526c6-400">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-400">Object</span></span>|<span data-ttu-id="526c6-401">Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="526c6-402">Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="526c6-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="526c6-403">body</span><span class="sxs-lookup"><span data-stu-id="526c6-403">body</span></span>|<span data-ttu-id="526c6-404">No</span><span class="sxs-lookup"><span data-stu-id="526c6-404">No</span></span>|<span data-ttu-id="526c6-405">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-405">Object</span></span>|<span data-ttu-id="526c6-406">Representa la carga de Hola que se envía el punto de conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="526c6-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="526c6-407">retryPolicy</span></span>|<span data-ttu-id="526c6-408">No</span><span class="sxs-lookup"><span data-stu-id="526c6-408">No</span></span>|<span data-ttu-id="526c6-409">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-409">Object</span></span>|<span data-ttu-id="526c6-410">Le permite personalizar el comportamiento de reintento de hello errores de 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="526c6-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="526c6-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="526c6-411">operationsOptions</span></span>|<span data-ttu-id="526c6-412">No</span><span class="sxs-lookup"><span data-stu-id="526c6-412">No</span></span>|<span data-ttu-id="526c6-413">String</span><span class="sxs-lookup"><span data-stu-id="526c6-413">String</span></span>|<span data-ttu-id="526c6-414">Define el conjunto de Hola de toooverride comportamientos especiales.</span><span class="sxs-lookup"><span data-stu-id="526c6-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="526c6-415">Autenticación</span><span class="sxs-lookup"><span data-stu-id="526c6-415">authentication</span></span>|<span data-ttu-id="526c6-416">No</span><span class="sxs-lookup"><span data-stu-id="526c6-416">No</span></span>|<span data-ttu-id="526c6-417">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-417">Object</span></span>|<span data-ttu-id="526c6-418">Método de hello representa que Hola solicitud se debe autenticar.</span><span class="sxs-lookup"><span data-stu-id="526c6-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="526c6-419">Para más información sobre este objeto, consulte [Autenticación saliente de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="526c6-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="526c6-420">Aparte de scheduler, hay una propiedad más que se admite: `authority`.</span><span class="sxs-lookup"><span data-stu-id="526c6-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="526c6-421">De forma predeterminada, es `https://login.windows.net` cuando no se especifica, pero se puede usar una audiencia diferente como `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="526c6-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="526c6-422">Las acciones HTTP \(y las acciones de conexión de API\) admiten directivas de reintentos.</span><span class="sxs-lookup"><span data-stu-id="526c6-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="526c6-423">Una directiva de reintentos aplica a los errores toointermittent, caracterizados como código de estado HTTP 408 y 429, 5xx, excepciones de conectividad de tooany de suma de los códigos.</span><span class="sxs-lookup"><span data-stu-id="526c6-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="526c6-424">Esta directiva se describe mediante hello *retryPolicy* objeto definido como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="526c6-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="526c6-425">intervalo de reintento de saludo se especifica en formato ISO 8601 Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="526c6-426">Este intervalo tiene un valor predeterminado y el valor mínimo de 20 segundos, mientras el valor máximo de hello es una hora.</span><span class="sxs-lookup"><span data-stu-id="526c6-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="526c6-427">Hola predeterminado y máximo de reintentos son cuatro horas.</span><span class="sxs-lookup"><span data-stu-id="526c6-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="526c6-428">Si no se especificó la definición de directiva de reintento de hello, un `fixed` estrategia se usa con valores de recuento y el intervalo de reintento predeterminados.</span><span class="sxs-lookup"><span data-stu-id="526c6-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="526c6-429">Directiva de reintentos de hello toodisable, establezca su tipo demasiado`None`.</span><span class="sxs-lookup"><span data-stu-id="526c6-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="526c6-430">Por ejemplo, hello acción siguiente vuelve obteniendo noticias más recientes de hello dos veces, si hay errores intermitentes, para un total de tres ejecuciones, con un retraso de 30 segundos entre cada intento de:</span><span class="sxs-lookup"><span data-stu-id="526c6-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="526c6-431">Patrones asincrónicos</span><span class="sxs-lookup"><span data-stu-id="526c6-431">Asynchronous patterns</span></span>

<span data-ttu-id="526c6-432">De forma predeterminada, todas las acciones basadas en HTTP admiten el patrón estándar de operación asincrónica de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="526c6-433">Por lo que si el servidor remoto de Hola indica que la solicitud hello es aceptado para su procesamiento con un 202 \(aceptado\) respuesta, motor de Logic Apps Hola mantiene sondeo URL Hola especificada en el encabezado de ubicación de la respuesta de hello hasta alcanzar un terminal estado \(un no\-respuesta 202\).</span><span class="sxs-lookup"><span data-stu-id="526c6-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="526c6-434">comportamiento asincrónico de hello toodisable previamente descrito, establezca un `DisableAsyncPattern` opción en entradas de la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="526c6-435">En este caso, la salida de hello de acción de Hola se basa en hello inicial 202 respuesta Hola servidor.</span><span class="sxs-lookup"><span data-stu-id="526c6-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="526c6-436">Límites asincrónicos</span><span class="sxs-lookup"><span data-stu-id="526c6-436">Asynchronous Limits</span></span>

<span data-ttu-id="526c6-437">Un patrón asincrónico puede estar limitado en su intervalo de tiempo específico de tooa de duración.</span><span class="sxs-lookup"><span data-stu-id="526c6-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="526c6-438">Si el intervalo de tiempo de hello transcurre sin que se alcance un estado terminal, se marcarán estado Hola de acción de hello `Cancelled` con el código `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="526c6-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="526c6-439">tiempo de espera de Hello límite se especifica en formato ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="526c6-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="526c6-440">Límites se pueden especificar con la sintaxis de hello:</span><span class="sxs-lookup"><span data-stu-id="526c6-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="526c6-441">API Connection</span><span class="sxs-lookup"><span data-stu-id="526c6-441">API Connection</span></span>  

<span data-ttu-id="526c6-442">API Connection es una acción que hace referencia a un conector administrado por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="526c6-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="526c6-443">Esta acción requiere una conexión válida de tooa de referencia y obtener información sobre la API de Hola y los parámetros requeridos.</span><span class="sxs-lookup"><span data-stu-id="526c6-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="526c6-444">Nombre del elemento</span><span class="sxs-lookup"><span data-stu-id="526c6-444">Element name</span></span>|<span data-ttu-id="526c6-445">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-445">Required</span></span>|<span data-ttu-id="526c6-446">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-446">Type</span></span>|<span data-ttu-id="526c6-447">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="526c6-448">host</span><span class="sxs-lookup"><span data-stu-id="526c6-448">host</span></span>|<span data-ttu-id="526c6-449">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-449">Yes</span></span>|<span data-ttu-id="526c6-450">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-450">Object</span></span>|<span data-ttu-id="526c6-451">Representa la información de conector de hello como objeto de conexión de toohello de referencia y runtimeUrl Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="526c6-452">estático</span><span class="sxs-lookup"><span data-stu-id="526c6-452">method</span></span>|<span data-ttu-id="526c6-453">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-453">Yes</span></span>|<span data-ttu-id="526c6-454">String</span><span class="sxs-lookup"><span data-stu-id="526c6-454">String</span></span>|<span data-ttu-id="526c6-455">Puede ser uno de hello siguiendo métodos HTTP: **obtener**, **POST**, **colocar**, **eliminar**, **PATCH**, o  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="526c6-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="526c6-456">path</span><span class="sxs-lookup"><span data-stu-id="526c6-456">path</span></span>|<span data-ttu-id="526c6-457">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-457">Yes</span></span>|<span data-ttu-id="526c6-458">String</span><span class="sxs-lookup"><span data-stu-id="526c6-458">String</span></span>|<span data-ttu-id="526c6-459">ruta de acceso de Hola de operación de hello API.</span><span class="sxs-lookup"><span data-stu-id="526c6-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="526c6-460">Consultas</span><span class="sxs-lookup"><span data-stu-id="526c6-460">queries</span></span>|<span data-ttu-id="526c6-461">No</span><span class="sxs-lookup"><span data-stu-id="526c6-461">No</span></span>|<span data-ttu-id="526c6-462">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-462">Object</span></span>|<span data-ttu-id="526c6-463">Representa la URL de hello consulta parámetros tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="526c6-464">Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="526c6-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="526c6-465">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-465">headers</span></span>|<span data-ttu-id="526c6-466">No</span><span class="sxs-lookup"><span data-stu-id="526c6-466">No</span></span>|<span data-ttu-id="526c6-467">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-467">Object</span></span>|<span data-ttu-id="526c6-468">Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="526c6-469">Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="526c6-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="526c6-470">body</span><span class="sxs-lookup"><span data-stu-id="526c6-470">body</span></span>|<span data-ttu-id="526c6-471">No</span><span class="sxs-lookup"><span data-stu-id="526c6-471">No</span></span>|<span data-ttu-id="526c6-472">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-472">Object</span></span>|<span data-ttu-id="526c6-473">Representa la carga de Hola que se envía el punto de conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="526c6-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="526c6-474">retryPolicy</span></span>|<span data-ttu-id="526c6-475">No</span><span class="sxs-lookup"><span data-stu-id="526c6-475">No</span></span>|<span data-ttu-id="526c6-476">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-476">Object</span></span>|<span data-ttu-id="526c6-477">Le permite personalizar el comportamiento de reintento de hello errores de 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="526c6-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="526c6-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="526c6-478">operationsOptions</span></span>|<span data-ttu-id="526c6-479">No</span><span class="sxs-lookup"><span data-stu-id="526c6-479">No</span></span>|<span data-ttu-id="526c6-480">String</span><span class="sxs-lookup"><span data-stu-id="526c6-480">String</span></span>|<span data-ttu-id="526c6-481">Define el conjunto de Hola de toooverride comportamientos especiales.</span><span class="sxs-lookup"><span data-stu-id="526c6-481">Defines hello set of special behaviors toooverride.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="526c6-482">Acción Webhook de API Connection</span><span class="sxs-lookup"><span data-stu-id="526c6-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="526c6-483">Se pueden especificar límites en una acción de webhook en hello misma manera que [HTTP asincrónica límites](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="526c6-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="526c6-484">Acción de respuesta</span><span class="sxs-lookup"><span data-stu-id="526c6-484">Response action</span></span>  

<span data-ttu-id="526c6-485">Este tipo de acción contiene la carga de respuesta completo Hola de una solicitud HTTP e incluye un statusCode, cuerpo y encabezados:</span><span class="sxs-lookup"><span data-stu-id="526c6-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="526c6-486">acción de respuesta de Hello tiene restricciones especiales que no son aplicables a las acciones de tooother.</span><span class="sxs-lookup"><span data-stu-id="526c6-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="526c6-487">Concretamente:</span><span class="sxs-lookup"><span data-stu-id="526c6-487">Specifically:</span></span>  
  
-   <span data-ttu-id="526c6-488">Las acciones de respuesta no pueden ser paralelas en una definición de porque es necesaria una solicitud entrante de toohello de respuesta determinista.</span><span class="sxs-lookup"><span data-stu-id="526c6-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="526c6-489">Si se alcanza una acción de respuesta después de solicitud entrante de hello ha recibido una respuesta, la acción de Hola se considera no se pudo \(conflicto\), y como resultado, es Hola ejecutar `Failed`.</span><span class="sxs-lookup"><span data-stu-id="526c6-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="526c6-490">Un flujo de trabajo con acciones de respuesta no puede tener `splitOn` en su desencadenador porque una llamada provoca muchas ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="526c6-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="526c6-491">Como resultado, esto se debe validar al flujo de hello es PUT y causa una solicitud incorrecta.</span><span class="sxs-lookup"><span data-stu-id="526c6-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="526c6-492">Acción Wait</span><span class="sxs-lookup"><span data-stu-id="526c6-492">Wait action</span></span>  

<span data-ttu-id="526c6-493">Hola `wait` acción suspende la ejecución de flujo de trabajo para el intervalo especificado de saludo.</span><span class="sxs-lookup"><span data-stu-id="526c6-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="526c6-494">Por ejemplo, toowait 15 minutos, puede usar este fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="526c6-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="526c6-495">O bien, toowait hasta un momento específico en el tiempo, puede utilizar este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="526c6-496">duración de la espera de Hello puede especificarse ya sea mediante hello **intervalo** objeto o hello **hasta** objeto, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="526c6-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="526c6-497">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-497">Name</span></span>|<span data-ttu-id="526c6-498">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-498">Required</span></span>|<span data-ttu-id="526c6-499">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-499">Type</span></span>|<span data-ttu-id="526c6-500">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-501">interval</span><span class="sxs-lookup"><span data-stu-id="526c6-501">interval</span></span>|<span data-ttu-id="526c6-502">No</span><span class="sxs-lookup"><span data-stu-id="526c6-502">No</span></span>|<span data-ttu-id="526c6-503">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-503">Object</span></span>|<span data-ttu-id="526c6-504">duración en función de la cantidad de tiempo de espera de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="526c6-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="526c6-505">interval unit</span></span>|<span data-ttu-id="526c6-506">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-506">Yes</span></span>|<span data-ttu-id="526c6-507">string</span><span class="sxs-lookup"><span data-stu-id="526c6-507">String</span></span>|<span data-ttu-id="526c6-508">Uno de estos intervalos: segundo, minuto, hora, día, semana, mes o año.</span><span class="sxs-lookup"><span data-stu-id="526c6-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="526c6-509">interval count</span><span class="sxs-lookup"><span data-stu-id="526c6-509">interval count</span></span>|<span data-ttu-id="526c6-510">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-510">Yes</span></span>|<span data-ttu-id="526c6-511">String</span><span class="sxs-lookup"><span data-stu-id="526c6-511">String</span></span>|<span data-ttu-id="526c6-512">Duración en función de hello unidad interna proporcionada.</span><span class="sxs-lookup"><span data-stu-id="526c6-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="526c6-513">until</span><span class="sxs-lookup"><span data-stu-id="526c6-513">until</span></span>|<span data-ttu-id="526c6-514">No</span><span class="sxs-lookup"><span data-stu-id="526c6-514">No</span></span>|<span data-ttu-id="526c6-515">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-515">Object</span></span>|<span data-ttu-id="526c6-516">duración en función de un punto en el tiempo de espera de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="526c6-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="526c6-517">until timestamp</span></span>|<span data-ttu-id="526c6-518">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-518">Yes</span></span>|<span data-ttu-id="526c6-519">String</span><span class="sxs-lookup"><span data-stu-id="526c6-519">String</span></span>|<span data-ttu-id="526c6-520">Cadena &#124; Hola punto en el tiempo en UTC cuando Hola espera expira.</span><span class="sxs-lookup"><span data-stu-id="526c6-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="526c6-521">Acción de consulta</span><span class="sxs-lookup"><span data-stu-id="526c6-521">Query action</span></span>

<span data-ttu-id="526c6-522">Hola `query` acción le permite filtrar una matriz basada en una condición.</span><span class="sxs-lookup"><span data-stu-id="526c6-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="526c6-523">Por ejemplo, tooselect un número superior a 2, puede usar:</span><span class="sxs-lookup"><span data-stu-id="526c6-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="526c6-524">Hola salida de hello `query` acción es una matriz que tiene elementos de matriz de entrada de Hola que satisfacen la condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="526c6-525">Si no hay valores satisfacen hello `where` condición, hello resultado es una matriz vacía.</span><span class="sxs-lookup"><span data-stu-id="526c6-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="526c6-526">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-526">Name</span></span>|<span data-ttu-id="526c6-527">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-527">Required</span></span>|<span data-ttu-id="526c6-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-528">Type</span></span>|<span data-ttu-id="526c6-529">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="526c6-530">De</span><span class="sxs-lookup"><span data-stu-id="526c6-530">from</span></span>|<span data-ttu-id="526c6-531">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-531">Yes</span></span>|<span data-ttu-id="526c6-532">Matriz</span><span class="sxs-lookup"><span data-stu-id="526c6-532">Array</span></span>|<span data-ttu-id="526c6-533">matriz de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-533">hello source array.</span></span>|
|<span data-ttu-id="526c6-534">donde</span><span class="sxs-lookup"><span data-stu-id="526c6-534">where</span></span>|<span data-ttu-id="526c6-535">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-535">Yes</span></span>|<span data-ttu-id="526c6-536">String</span><span class="sxs-lookup"><span data-stu-id="526c6-536">String</span></span>|<span data-ttu-id="526c6-537">Hola condition tooapply tooeach, elemento de matriz de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="526c6-538">Acción Select</span><span class="sxs-lookup"><span data-stu-id="526c6-538">Select action</span></span>

<span data-ttu-id="526c6-539">Hola `select` acción permite proyectar cada elemento de una matriz con un nuevo valor.</span><span class="sxs-lookup"><span data-stu-id="526c6-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="526c6-540">Por ejemplo, tooconvert una matriz de números en una matriz de objetos, puede usar:</span><span class="sxs-lookup"><span data-stu-id="526c6-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="526c6-541">Hola salida de hello `select` acción es una matriz cuya Hola misma cardinalidad Hola matriz de entrada, con cada elemento transformada según lo definido por hello `select` propiedad.</span><span class="sxs-lookup"><span data-stu-id="526c6-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="526c6-542">Si la entrada de hello es una matriz vacía, salida de hello también es una matriz vacía.</span><span class="sxs-lookup"><span data-stu-id="526c6-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="526c6-543">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-543">Name</span></span>|<span data-ttu-id="526c6-544">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-544">Required</span></span>|<span data-ttu-id="526c6-545">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-545">Type</span></span>|<span data-ttu-id="526c6-546">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="526c6-547">De</span><span class="sxs-lookup"><span data-stu-id="526c6-547">from</span></span>|<span data-ttu-id="526c6-548">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-548">Yes</span></span>|<span data-ttu-id="526c6-549">Matriz</span><span class="sxs-lookup"><span data-stu-id="526c6-549">Array</span></span>|<span data-ttu-id="526c6-550">matriz de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-550">hello source array.</span></span>|
|<span data-ttu-id="526c6-551">select</span><span class="sxs-lookup"><span data-stu-id="526c6-551">select</span></span>|<span data-ttu-id="526c6-552">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-552">Yes</span></span>|<span data-ttu-id="526c6-553">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="526c6-553">Any</span></span>|<span data-ttu-id="526c6-554">elemento de Hello proyección tooapply tooeach de matriz de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="526c6-555">Acción Terminate</span><span class="sxs-lookup"><span data-stu-id="526c6-555">Terminate action</span></span>

<span data-ttu-id="526c6-556">Hola acción terminar detiene la ejecución de Hola y flujo de trabajo ejecutar, anular cualquier acción en curso, omitiendo las acciones restantes.</span><span class="sxs-lookup"><span data-stu-id="526c6-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="526c6-557">Por ejemplo, tooterminate una ejecución con el estado **error**, puede usar Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="526c6-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="526c6-558">Hola no afecta a las acciones que ya ha completado terminar la acción.</span><span class="sxs-lookup"><span data-stu-id="526c6-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="526c6-559">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-559">Name</span></span>|<span data-ttu-id="526c6-560">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-560">Required</span></span>|<span data-ttu-id="526c6-561">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-561">Type</span></span>|<span data-ttu-id="526c6-562">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="526c6-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="526c6-563">runStatus</span></span>|<span data-ttu-id="526c6-564">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-564">Yes</span></span>|<span data-ttu-id="526c6-565">String</span><span class="sxs-lookup"><span data-stu-id="526c6-565">String</span></span>|<span data-ttu-id="526c6-566">destino de Hello estado de ejecución.</span><span class="sxs-lookup"><span data-stu-id="526c6-566">hello target run status.</span></span> <span data-ttu-id="526c6-567">**Failed** o **Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="526c6-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="526c6-568">runError</span><span class="sxs-lookup"><span data-stu-id="526c6-568">runError</span></span>|<span data-ttu-id="526c6-569">No</span><span class="sxs-lookup"><span data-stu-id="526c6-569">No</span></span>|<span data-ttu-id="526c6-570">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-570">Object</span></span>|<span data-ttu-id="526c6-571">Detalles del error Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-571">hello error details.</span></span> <span data-ttu-id="526c6-572">Solo es compatible cuando **runStatus** se establece demasiado**error**.</span><span class="sxs-lookup"><span data-stu-id="526c6-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="526c6-573">runError code</span><span class="sxs-lookup"><span data-stu-id="526c6-573">runError code</span></span>|<span data-ttu-id="526c6-574">No</span><span class="sxs-lookup"><span data-stu-id="526c6-574">No</span></span>|<span data-ttu-id="526c6-575">String</span><span class="sxs-lookup"><span data-stu-id="526c6-575">String</span></span>|<span data-ttu-id="526c6-576">Hola ejecutar código de error.</span><span class="sxs-lookup"><span data-stu-id="526c6-576">hello run error code.</span></span>|
|<span data-ttu-id="526c6-577">runError message</span><span class="sxs-lookup"><span data-stu-id="526c6-577">runError message</span></span>|<span data-ttu-id="526c6-578">No</span><span class="sxs-lookup"><span data-stu-id="526c6-578">No</span></span>|<span data-ttu-id="526c6-579">String</span><span class="sxs-lookup"><span data-stu-id="526c6-579">String</span></span>|<span data-ttu-id="526c6-580">Hola ejecutar el mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="526c6-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="526c6-581">Acción Compose</span><span class="sxs-lookup"><span data-stu-id="526c6-581">Compose action</span></span>

<span data-ttu-id="526c6-582">Hola redactar acción le permite construir un objeto arbitrario.</span><span class="sxs-lookup"><span data-stu-id="526c6-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="526c6-583">salida de Hello de hello redactar acción es resultado de hello de evaluar sus entradas.</span><span class="sxs-lookup"><span data-stu-id="526c6-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="526c6-584">Por ejemplo, puede usar hello crear salidas de toomerge de acción de varias acciones:</span><span class="sxs-lookup"><span data-stu-id="526c6-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="526c6-585">Hola **redactar** acción puede ser usado tooconstruct ningún resultado, incluidos objetos, matrices y cualquier otro tipo de lógica de aplicaciones como XML y binario lo admitidos de forma nativa.</span><span class="sxs-lookup"><span data-stu-id="526c6-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="526c6-586">Acción Table</span><span class="sxs-lookup"><span data-stu-id="526c6-586">Table action</span></span>

<span data-ttu-id="526c6-587">Hola `table` permite tooconvert una matriz de elementos en una **CSV** o **HTML** tabla.</span><span class="sxs-lookup"><span data-stu-id="526c6-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="526c6-588">Si @triggerBody() es</span><span class="sxs-lookup"><span data-stu-id="526c6-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="526c6-589">Y deje que la acción de Hola se define como</span><span class="sxs-lookup"><span data-stu-id="526c6-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="526c6-590">Hola anterior generaría</span><span class="sxs-lookup"><span data-stu-id="526c6-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="526c6-591">id</span><span class="sxs-lookup"><span data-stu-id="526c6-591">id</span></span></th><th><span data-ttu-id="526c6-592">name</span><span class="sxs-lookup"><span data-stu-id="526c6-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="526c6-593">0</span><span class="sxs-lookup"><span data-stu-id="526c6-593">0</span></span></td><td><span data-ttu-id="526c6-594">apples</span><span class="sxs-lookup"><span data-stu-id="526c6-594">apples</span></span></td></tr><tr><td><span data-ttu-id="526c6-595">1</span><span class="sxs-lookup"><span data-stu-id="526c6-595">1</span></span></td><td><span data-ttu-id="526c6-596">oranges</span><span class="sxs-lookup"><span data-stu-id="526c6-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="526c6-597">"</span><span class="sxs-lookup"><span data-stu-id="526c6-597">"</span></span>

<span data-ttu-id="526c6-598">En la tabla de orden toocustomize hello, puede especificar las columnas de hello explícitamente.</span><span class="sxs-lookup"><span data-stu-id="526c6-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="526c6-599">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="526c6-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="526c6-600">Hola anterior generaría</span><span class="sxs-lookup"><span data-stu-id="526c6-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="526c6-601">produce id</span><span class="sxs-lookup"><span data-stu-id="526c6-601">produce id</span></span></th><th><span data-ttu-id="526c6-602">Description</span><span class="sxs-lookup"><span data-stu-id="526c6-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="526c6-603">0</span><span class="sxs-lookup"><span data-stu-id="526c6-603">0</span></span></td><td><span data-ttu-id="526c6-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="526c6-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="526c6-605">1</span><span class="sxs-lookup"><span data-stu-id="526c6-605">1</span></span></td><td><span data-ttu-id="526c6-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="526c6-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="526c6-607">"</span><span class="sxs-lookup"><span data-stu-id="526c6-607">"</span></span>

<span data-ttu-id="526c6-608">Si hello `from` valor de la propiedad es una matriz vacía, la salida de hello es una tabla vacía.</span><span class="sxs-lookup"><span data-stu-id="526c6-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="526c6-609">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-609">Name</span></span>|<span data-ttu-id="526c6-610">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-610">Required</span></span>|<span data-ttu-id="526c6-611">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-611">Type</span></span>|<span data-ttu-id="526c6-612">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="526c6-613">De</span><span class="sxs-lookup"><span data-stu-id="526c6-613">from</span></span>|<span data-ttu-id="526c6-614">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-614">Yes</span></span>|<span data-ttu-id="526c6-615">Matriz</span><span class="sxs-lookup"><span data-stu-id="526c6-615">Array</span></span>|<span data-ttu-id="526c6-616">matriz de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-616">hello source array.</span></span>|
|<span data-ttu-id="526c6-617">formato</span><span class="sxs-lookup"><span data-stu-id="526c6-617">format</span></span>|<span data-ttu-id="526c6-618">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-618">Yes</span></span>|<span data-ttu-id="526c6-619">String</span><span class="sxs-lookup"><span data-stu-id="526c6-619">String</span></span>|<span data-ttu-id="526c6-620">Hola formato, ya sea **CSV** o **HTML**.</span><span class="sxs-lookup"><span data-stu-id="526c6-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="526c6-621">columnas</span><span class="sxs-lookup"><span data-stu-id="526c6-621">columns</span></span>|<span data-ttu-id="526c6-622">No</span><span class="sxs-lookup"><span data-stu-id="526c6-622">No</span></span>|<span data-ttu-id="526c6-623">Matriz</span><span class="sxs-lookup"><span data-stu-id="526c6-623">Array</span></span>|<span data-ttu-id="526c6-624">columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-624">hello columns.</span></span> <span data-ttu-id="526c6-625">Permite la forma de toooverride Hola predeterminada de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="526c6-626">column header</span><span class="sxs-lookup"><span data-stu-id="526c6-626">column header</span></span>|<span data-ttu-id="526c6-627">No</span><span class="sxs-lookup"><span data-stu-id="526c6-627">No</span></span>|<span data-ttu-id="526c6-628">String</span><span class="sxs-lookup"><span data-stu-id="526c6-628">String</span></span>|<span data-ttu-id="526c6-629">encabezado de Hola de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-629">hello header of hello column.</span></span>|
|<span data-ttu-id="526c6-630">column value</span><span class="sxs-lookup"><span data-stu-id="526c6-630">column value</span></span>|<span data-ttu-id="526c6-631">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-631">Yes</span></span>|<span data-ttu-id="526c6-632">String</span><span class="sxs-lookup"><span data-stu-id="526c6-632">String</span></span>|<span data-ttu-id="526c6-633">valor de Hola de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="526c6-634">Acción Workflow</span><span class="sxs-lookup"><span data-stu-id="526c6-634">Workflow action</span></span>   

|<span data-ttu-id="526c6-635">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-635">Name</span></span>|<span data-ttu-id="526c6-636">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-636">Required</span></span>|<span data-ttu-id="526c6-637">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-637">Type</span></span>|<span data-ttu-id="526c6-638">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-639">host id</span><span class="sxs-lookup"><span data-stu-id="526c6-639">host id</span></span>|<span data-ttu-id="526c6-640">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-640">Yes</span></span>|<span data-ttu-id="526c6-641">String</span><span class="sxs-lookup"><span data-stu-id="526c6-641">String</span></span>|<span data-ttu-id="526c6-642">Identificador de recurso de Hola de flujo de trabajo de Hola que quieres toocall.</span><span class="sxs-lookup"><span data-stu-id="526c6-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="526c6-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="526c6-643">host triggerName</span></span>|<span data-ttu-id="526c6-644">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-644">Yes</span></span>|<span data-ttu-id="526c6-645">String</span><span class="sxs-lookup"><span data-stu-id="526c6-645">String</span></span>|<span data-ttu-id="526c6-646">nombre de Hola de desencadenador de Hola que desea tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="526c6-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="526c6-647">Consultas</span><span class="sxs-lookup"><span data-stu-id="526c6-647">queries</span></span>|<span data-ttu-id="526c6-648">No</span><span class="sxs-lookup"><span data-stu-id="526c6-648">No</span></span>|<span data-ttu-id="526c6-649">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-649">Object</span></span>|<span data-ttu-id="526c6-650">Representa la URL de hello consulta parámetros tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="526c6-651">Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="526c6-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="526c6-652">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-652">headers</span></span>|<span data-ttu-id="526c6-653">No</span><span class="sxs-lookup"><span data-stu-id="526c6-653">No</span></span>|<span data-ttu-id="526c6-654">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-654">Object</span></span>|<span data-ttu-id="526c6-655">Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="526c6-656">Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="526c6-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="526c6-657">body</span><span class="sxs-lookup"><span data-stu-id="526c6-657">body</span></span>|<span data-ttu-id="526c6-658">No</span><span class="sxs-lookup"><span data-stu-id="526c6-658">No</span></span>|<span data-ttu-id="526c6-659">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-659">Object</span></span>|<span data-ttu-id="526c6-660">Representa la carga de hello enviado toohello extremo.</span><span class="sxs-lookup"><span data-stu-id="526c6-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="526c6-661">Se realiza una comprobación de acceso en el flujo de trabajo de hello \(más específicamente, desencadenador de hello\), lo que significa que necesita tener acceso a toohello flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="526c6-662">Hola salidas de hello `workflow` acción se basan en la que define en hello `response` acción en el flujo de trabajo de hello secundario.</span><span class="sxs-lookup"><span data-stu-id="526c6-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="526c6-663">Si no ha definido alguno `response` acción y, a continuación, salidas de hello están vacíos.</span><span class="sxs-lookup"><span data-stu-id="526c6-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="526c6-664">Acción de la función</span><span class="sxs-lookup"><span data-stu-id="526c6-664">Function action</span></span>   

|<span data-ttu-id="526c6-665">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-665">Name</span></span>|<span data-ttu-id="526c6-666">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-666">Required</span></span>|<span data-ttu-id="526c6-667">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-667">Type</span></span>|<span data-ttu-id="526c6-668">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-669">function id</span><span class="sxs-lookup"><span data-stu-id="526c6-669">function id</span></span>|<span data-ttu-id="526c6-670">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-670">Yes</span></span>|<span data-ttu-id="526c6-671">String</span><span class="sxs-lookup"><span data-stu-id="526c6-671">String</span></span>|<span data-ttu-id="526c6-672">Hola Id. de recurso de función hello que desea tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="526c6-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="526c6-673">estático</span><span class="sxs-lookup"><span data-stu-id="526c6-673">method</span></span>|<span data-ttu-id="526c6-674">No</span><span class="sxs-lookup"><span data-stu-id="526c6-674">No</span></span>|<span data-ttu-id="526c6-675">String</span><span class="sxs-lookup"><span data-stu-id="526c6-675">String</span></span>|<span data-ttu-id="526c6-676">Hola método HTTP utiliza la función de hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="526c6-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="526c6-677">De forma predeterminada, es `POST` cuando no se especifica.</span><span class="sxs-lookup"><span data-stu-id="526c6-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="526c6-678">Consultas</span><span class="sxs-lookup"><span data-stu-id="526c6-678">queries</span></span>|<span data-ttu-id="526c6-679">No</span><span class="sxs-lookup"><span data-stu-id="526c6-679">No</span></span>|<span data-ttu-id="526c6-680">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-680">Object</span></span>|<span data-ttu-id="526c6-681">Representa la URL de hello consulta parámetros tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="526c6-682">Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="526c6-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="526c6-683">encabezados</span><span class="sxs-lookup"><span data-stu-id="526c6-683">headers</span></span>|<span data-ttu-id="526c6-684">No</span><span class="sxs-lookup"><span data-stu-id="526c6-684">No</span></span>|<span data-ttu-id="526c6-685">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-685">Object</span></span>|<span data-ttu-id="526c6-686">Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello.</span><span class="sxs-lookup"><span data-stu-id="526c6-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="526c6-687">Por ejemplo, el idioma de hello tooset y el tipo en una solicitud: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="526c6-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="526c6-688">body</span><span class="sxs-lookup"><span data-stu-id="526c6-688">body</span></span>|<span data-ttu-id="526c6-689">No</span><span class="sxs-lookup"><span data-stu-id="526c6-689">No</span></span>|<span data-ttu-id="526c6-690">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-690">Object</span></span>|<span data-ttu-id="526c6-691">Representa la carga de hello enviado toohello extremo.</span><span class="sxs-lookup"><span data-stu-id="526c6-691">Represents hello payload sent toohello endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="526c6-692">Cuando se guarda la aplicación de la lógica de hello, realizamos algunas comprobaciones de la función hello al que hace referencia:</span><span class="sxs-lookup"><span data-stu-id="526c6-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="526c6-693">Se necesita la función de toohello de acceso de toohave.</span><span class="sxs-lookup"><span data-stu-id="526c6-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="526c6-694">Solo se permite el desencadenador HTTP estándar o webhook JSON genérico.</span><span class="sxs-lookup"><span data-stu-id="526c6-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="526c6-695">No debe tener ninguna ruta definida.</span><span class="sxs-lookup"><span data-stu-id="526c6-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="526c6-696">Solo se permite el nivel de autorización "function" y "anonymous".</span><span class="sxs-lookup"><span data-stu-id="526c6-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="526c6-697">dirección URL de desencadenador de Hello recuperan, almacenado en memoria caché y utiliza en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="526c6-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="526c6-698">Por lo que si cualquier operación invalida la dirección URL de hello en caché, se produce un error en la acción de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="526c6-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="526c6-699">toowork evitar este problema, guarde Hola aplicación lógica de nuevo, lo que provocará tooretrieve de aplicación lógica y almacenar en caché URL de desencadenador de hello nuevo.</span><span class="sxs-lookup"><span data-stu-id="526c6-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="526c6-700">Acciones de colección (ámbitos y bucles)</span><span class="sxs-lookup"><span data-stu-id="526c6-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="526c6-701">Algunos tipos de acciones pueden contener acciones dentro de sí mismas.</span><span class="sxs-lookup"><span data-stu-id="526c6-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="526c6-702">Pueden hacer referencia a acciones de referencia dentro de una colección directamente fuera de la colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="526c6-703">Si ha definido `http` en un ámbito, `@body('http')` sigue siendo válido en cualquier parte de un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="526c6-704">Las acciones dentro de una colección pueden `runAfter` solo otras acciones en Hola misma colección.</span><span class="sxs-lookup"><span data-stu-id="526c6-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="526c6-705">Acción Scope</span><span class="sxs-lookup"><span data-stu-id="526c6-705">Scope action</span></span>

<span data-ttu-id="526c6-706">Hola `scope` acción permite lógicamente agrupar acciones en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="526c6-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="526c6-707">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-707">Name</span></span>|<span data-ttu-id="526c6-708">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-708">Required</span></span>|<span data-ttu-id="526c6-709">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-709">Type</span></span>|<span data-ttu-id="526c6-710">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-711">actions</span><span class="sxs-lookup"><span data-stu-id="526c6-711">actions</span></span>|<span data-ttu-id="526c6-712">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-712">Yes</span></span>|<span data-ttu-id="526c6-713">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-713">Object</span></span>|<span data-ttu-id="526c6-714">Acciones interna tooexecute ámbito Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-714">Inner actions tooexecute within hello scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="526c6-715">Acción ForEach</span><span class="sxs-lookup"><span data-stu-id="526c6-715">ForEach action</span></span>

<span data-ttu-id="526c6-716">Esta acción de bucle recorre en iteración una matriz y realiza acciones internas para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="526c6-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="526c6-717">De forma predeterminada, bucle foreach de Hola se ejecuta en paralelo (20 ejecuciones en paralelo a la vez).</span><span class="sxs-lookup"><span data-stu-id="526c6-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="526c6-718">Puede establecer reglas de ejecución con hello `operationOptions` parámetro.</span><span class="sxs-lookup"><span data-stu-id="526c6-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="526c6-719">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-719">Name</span></span>|<span data-ttu-id="526c6-720">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-720">Required</span></span>|<span data-ttu-id="526c6-721">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-721">Type</span></span>|<span data-ttu-id="526c6-722">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-723">actions</span><span class="sxs-lookup"><span data-stu-id="526c6-723">actions</span></span>|<span data-ttu-id="526c6-724">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-724">Yes</span></span>|<span data-ttu-id="526c6-725">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-725">Object</span></span>|<span data-ttu-id="526c6-726">Tooexecute acciones interna en el bucle de Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="526c6-727">foreach</span><span class="sxs-lookup"><span data-stu-id="526c6-727">foreach</span></span>|<span data-ttu-id="526c6-728">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-728">Yes</span></span>|<span data-ttu-id="526c6-729">cadena</span><span class="sxs-lookup"><span data-stu-id="526c6-729">string</span></span>|<span data-ttu-id="526c6-730">Hola matriz tooiterate sobre</span><span class="sxs-lookup"><span data-stu-id="526c6-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="526c6-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="526c6-731">operationOptions</span></span>|<span data-ttu-id="526c6-732">no</span><span class="sxs-lookup"><span data-stu-id="526c6-732">no</span></span>|<span data-ttu-id="526c6-733">string</span><span class="sxs-lookup"><span data-stu-id="526c6-733">string</span></span>|<span data-ttu-id="526c6-734">Las opciones de comportamiento de la operación.</span><span class="sxs-lookup"><span data-stu-id="526c6-734">Any operation options for behavior.</span></span> <span data-ttu-id="526c6-735">Actualmente sólo admite `sequential` tooexecute iteraciones secuencialmente (comportamiento predeterminado es paralelo)</span><span class="sxs-lookup"><span data-stu-id="526c6-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="526c6-736">Acción Until</span><span class="sxs-lookup"><span data-stu-id="526c6-736">Until action</span></span>

<span data-ttu-id="526c6-737">Esta acción bucle ejecuta acciones internas hasta que una condición da como resultado tootrue.</span><span class="sxs-lookup"><span data-stu-id="526c6-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="526c6-738">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-738">Name</span></span>|<span data-ttu-id="526c6-739">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-739">Required</span></span>|<span data-ttu-id="526c6-740">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-740">Type</span></span>|<span data-ttu-id="526c6-741">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-742">actions</span><span class="sxs-lookup"><span data-stu-id="526c6-742">actions</span></span>|<span data-ttu-id="526c6-743">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-743">Yes</span></span>|<span data-ttu-id="526c6-744">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-744">Object</span></span>|<span data-ttu-id="526c6-745">Tooexecute acciones interna en el bucle de Hola</span><span class="sxs-lookup"><span data-stu-id="526c6-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="526c6-746">expresión</span><span class="sxs-lookup"><span data-stu-id="526c6-746">expression</span></span>|<span data-ttu-id="526c6-747">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-747">Yes</span></span>|<span data-ttu-id="526c6-748">cadena</span><span class="sxs-lookup"><span data-stu-id="526c6-748">string</span></span>|<span data-ttu-id="526c6-749">Hola tooevaluate expresión después de cada iteración</span><span class="sxs-lookup"><span data-stu-id="526c6-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="526c6-750">limit</span><span class="sxs-lookup"><span data-stu-id="526c6-750">limit</span></span>|<span data-ttu-id="526c6-751">yes</span><span class="sxs-lookup"><span data-stu-id="526c6-751">yes</span></span>|<span data-ttu-id="526c6-752">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-752">Object</span></span>|<span data-ttu-id="526c6-753">se deben definir límites de Hola de bucle de hello - al menos un límite</span><span class="sxs-lookup"><span data-stu-id="526c6-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="526c6-754">count</span><span class="sxs-lookup"><span data-stu-id="526c6-754">count</span></span>|<span data-ttu-id="526c6-755">no</span><span class="sxs-lookup"><span data-stu-id="526c6-755">no</span></span>|<span data-ttu-id="526c6-756">int</span><span class="sxs-lookup"><span data-stu-id="526c6-756">int</span></span>|<span data-ttu-id="526c6-757">Hola limitar toohello el número de iteraciones que se pueden realizar</span><span class="sxs-lookup"><span data-stu-id="526c6-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="526c6-758">timeout</span><span class="sxs-lookup"><span data-stu-id="526c6-758">timeout</span></span>|<span data-ttu-id="526c6-759">no</span><span class="sxs-lookup"><span data-stu-id="526c6-759">no</span></span>|<span data-ttu-id="526c6-760">cadena</span><span class="sxs-lookup"><span data-stu-id="526c6-760">string</span></span>|<span data-ttu-id="526c6-761">tiempo de espera de Hola de cuánto tiempo debe entrar en bucle.</span><span class="sxs-lookup"><span data-stu-id="526c6-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="526c6-762">Formato ISO 8601</span><span class="sxs-lookup"><span data-stu-id="526c6-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="526c6-763">Condiciones: acción If</span><span class="sxs-lookup"><span data-stu-id="526c6-763">Conditions - If Action</span></span>

<span data-ttu-id="526c6-764">Hola `If` acción le permite evaluar una condición y ejecutar una rama en función de si la expresión de Hola se evalúa como demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="526c6-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="526c6-765">Nombre</span><span class="sxs-lookup"><span data-stu-id="526c6-765">Name</span></span>|<span data-ttu-id="526c6-766">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="526c6-766">Required</span></span>|<span data-ttu-id="526c6-767">Tipo</span><span class="sxs-lookup"><span data-stu-id="526c6-767">Type</span></span>|<span data-ttu-id="526c6-768">Descripción</span><span class="sxs-lookup"><span data-stu-id="526c6-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="526c6-769">actions</span><span class="sxs-lookup"><span data-stu-id="526c6-769">actions</span></span>|<span data-ttu-id="526c6-770">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-770">Yes</span></span>|<span data-ttu-id="526c6-771">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-771">Object</span></span>|<span data-ttu-id="526c6-772">Acciones interna tooexecute cuando la expresión se evalúa como demasiado`true`</span><span class="sxs-lookup"><span data-stu-id="526c6-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="526c6-773">expresión</span><span class="sxs-lookup"><span data-stu-id="526c6-773">expression</span></span>|<span data-ttu-id="526c6-774">Sí</span><span class="sxs-lookup"><span data-stu-id="526c6-774">Yes</span></span>|<span data-ttu-id="526c6-775">cadena</span><span class="sxs-lookup"><span data-stu-id="526c6-775">string</span></span>|<span data-ttu-id="526c6-776">Hola expresión tooevaluate</span><span class="sxs-lookup"><span data-stu-id="526c6-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="526c6-777">else</span><span class="sxs-lookup"><span data-stu-id="526c6-777">else</span></span>|<span data-ttu-id="526c6-778">no</span><span class="sxs-lookup"><span data-stu-id="526c6-778">no</span></span>|<span data-ttu-id="526c6-779">Objeto</span><span class="sxs-lookup"><span data-stu-id="526c6-779">Object</span></span>|<span data-ttu-id="526c6-780">Acciones interna tooexecute cuando la expresión se evalúa como demasiado`false`</span><span class="sxs-lookup"><span data-stu-id="526c6-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="526c6-781">Hello tabla siguiente muestra ejemplos de cómo condiciones pueden utilizarse expresiones en una acción:</span><span class="sxs-lookup"><span data-stu-id="526c6-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="526c6-782">Valor JSON</span><span class="sxs-lookup"><span data-stu-id="526c6-782">JSON value</span></span>|<span data-ttu-id="526c6-783">Resultado</span><span class="sxs-lookup"><span data-stu-id="526c6-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="526c6-784">Cualquier valor que se evaluaría tootrue hace que esta condición toopass.</span><span class="sxs-lookup"><span data-stu-id="526c6-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="526c6-785">Solo se admiten expresiones de tipo Boolean.</span><span class="sxs-lookup"><span data-stu-id="526c6-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="526c6-786">tooconvert otro tipos tooBoolean, utilizar funciones `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="526c6-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="526c6-787">Se admiten funciones de comparación.</span><span class="sxs-lookup"><span data-stu-id="526c6-787">Comparison functions are supported.</span></span> <span data-ttu-id="526c6-788">Para este ejemplo de Hola, acción de hello solo se ejecuta cuando la salida de hello de act1 es mayor que el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="526c6-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="526c6-789">Las funciones de lógica son también compatible toocreate anidar expresiones booleanas.</span><span class="sxs-lookup"><span data-stu-id="526c6-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="526c6-790">En este caso, acción de Hola se ejecuta cuando la salida de hello de act1 esté por encima del umbral de Hola o por debajo de 100.</span><span class="sxs-lookup"><span data-stu-id="526c6-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="526c6-791">Puede usar toocheck de funciones de matriz si una matriz tiene todos los elementos.</span><span class="sxs-lookup"><span data-stu-id="526c6-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="526c6-792">En este caso, la acción de hello ejecuta cuando Hola errores matriz está vacía.</span><span class="sxs-lookup"><span data-stu-id="526c6-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="526c6-793">Error: no es una condición válida porque se requiere @ para las condiciones.</span><span class="sxs-lookup"><span data-stu-id="526c6-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="526c6-794">Si una condición se evalúa correctamente, la condición de hello está marcada como `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="526c6-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="526c6-795">Las acciones dentro de cualquier hello `actions` o `else` objetos evaluación demasiado`Succeeded` cuando se ejecuta y se realizó correctamente, `Failed` cuando se ejecuta y no se pudo, o `Skipped` cuando no se ejecuta esa rama.</span><span class="sxs-lookup"><span data-stu-id="526c6-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="526c6-796">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="526c6-796">Next steps</span></span>

[<span data-ttu-id="526c6-797">API de REST de Servicio de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="526c6-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
