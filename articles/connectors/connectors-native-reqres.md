---
title: Uso de acciones de solicitud y respuesta | Microsoft Docs
description: "Información general del desencadenador y la acción de solicitud y respuesta en una aplicación lógica de Azure"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 566924a4-0988-4d86-9ecd-ad22507858c0
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e45b07d709927af64cfba28dfb0d8ee9cb8893b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-request-and-response-components"></a><span data-ttu-id="de798-103">Introducción a los componentes de solicitud y respuesta</span><span class="sxs-lookup"><span data-stu-id="de798-103">Get started with the request and response components</span></span>
<span data-ttu-id="de798-104">Con los componentes de solicitud y respuesta de una aplicación lógica, puede responder en tiempo real a eventos.</span><span class="sxs-lookup"><span data-stu-id="de798-104">With the request and response components in a logic app, you can respond in real time to events.</span></span>

<span data-ttu-id="de798-105">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="de798-105">For example, you can:</span></span>

* <span data-ttu-id="de798-106">Responder a una solicitud HTTP con datos de una base de datos local a través de una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="de798-106">Respond to an HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="de798-107">Desencadenar una aplicación lógica desde un evento webhook externo.</span><span class="sxs-lookup"><span data-stu-id="de798-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="de798-108">Llamar a una aplicación lógica con una acción de solicitud y respuesta desde otra aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="de798-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="de798-109">Para empezar a usar las acciones de solicitud y respuesta en una aplicación lógica, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="de798-109">To get started using the request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-request-trigger"></a><span data-ttu-id="de798-110">Uso del desencadenador de solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="de798-110">Use the HTTP Request trigger</span></span>
<span data-ttu-id="de798-111">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="de798-111">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="de798-112">[Más información sobre los desencadenadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de798-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="de798-113">Esta es una secuencia de ejemplo de cómo configurar una solicitud HTTP en el diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="de798-113">Here’s an example sequence of how to set up an HTTP request in the Logic App Designer.</span></span>

1. <span data-ttu-id="de798-114">Agregue el desencadenador **Request - When an HTTP request is received** (Solicitar: cuando se reciba una solicitud HTTP) a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="de798-114">Add the trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="de798-115">También puede proporcionar un esquema JSON (mediante una herramienta como [JSONSchema.net](http://jsonschema.net)) para el cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="de798-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for the request body.</span></span> <span data-ttu-id="de798-116">Esto permite al diseñador generar tokens para las propiedades de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="de798-116">This allows the designer to generate tokens for properties in the HTTP request.</span></span>
2. <span data-ttu-id="de798-117">Agregue otra acción para que pueda guardar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="de798-117">Add another action so that you can save the logic app.</span></span>
3. <span data-ttu-id="de798-118">Después de guardarla, puede obtener la dirección URL de la solicitud HTTP de la tarjeta de solicitud.</span><span class="sxs-lookup"><span data-stu-id="de798-118">After saving the logic app, you can get the HTTP request URL from the request card.</span></span>
4. <span data-ttu-id="de798-119">Una solicitud HTTP POST (puede utilizar una herramienta como [Postman](https://www.getpostman.com/)) a la dirección URL activará la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="de798-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) to the URL triggers the logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="de798-120">Si no define una acción de respuesta, se devolverá una respuesta `202 ACCEPTED` inmediatamente al llamador.</span><span class="sxs-lookup"><span data-stu-id="de798-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span> <span data-ttu-id="de798-121">Puede utilizar la acción de respuesta para personalizar una respuesta.</span><span class="sxs-lookup"><span data-stu-id="de798-121">You can use the response action to customize a response.</span></span>
> 
> 

![Desencadenador de respuesta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-the-http-response-action"></a><span data-ttu-id="de798-123">Uso de la acción de respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="de798-123">Use the HTTP Response action</span></span>
<span data-ttu-id="de798-124">La acción de respuesta HTTP solo es válida cuando se usa en un flujo de trabajo desencadenado por una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="de798-124">The HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="de798-125">Si no define una acción de respuesta, se devolverá una respuesta `202 ACCEPTED` inmediatamente al llamador.</span><span class="sxs-lookup"><span data-stu-id="de798-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned to the caller.</span></span>  <span data-ttu-id="de798-126">Se puede agregar una acción de respuesta en cualquier paso del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="de798-126">You can add a response action at any step within the workflow.</span></span> <span data-ttu-id="de798-127">La aplicación lógica solo mantiene la solicitud entrante abierta durante un minuto para una respuesta.</span><span class="sxs-lookup"><span data-stu-id="de798-127">The logic app only keeps the incoming request open for one minute for a response.</span></span>  <span data-ttu-id="de798-128">Después de un minuto, si no se envía respuesta desde el flujo de trabajo (y existe una acción de respuesta en la definición), se devuelve una respuesta `504 GATEWAY TIMEOUT` al llamador.</span><span class="sxs-lookup"><span data-stu-id="de798-128">After one minute, if no response was sent from the workflow (and a response action exists in the definition), a `504 GATEWAY TIMEOUT` is returned to the caller.</span></span>

<span data-ttu-id="de798-129">A continuación se explica cómo agregar una acción de respuesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="de798-129">Here's how to add an HTTP Response action:</span></span>

1. <span data-ttu-id="de798-130">Seleccione el botón **Nuevo paso** .</span><span class="sxs-lookup"><span data-stu-id="de798-130">Select the **New Step** button.</span></span>
2. <span data-ttu-id="de798-131">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="de798-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="de798-132">En el cuadro de búsqueda de acciones, escriba **Response** para mostrar la acción de respuesta.</span><span class="sxs-lookup"><span data-stu-id="de798-132">In the action search box, type **response** to list the Response action.</span></span>
   
    ![Seleccionar la acción de respuesta](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="de798-134">Agregue cualquier parámetro necesario para el mensaje de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="de798-134">Add in any parameters that are required for the HTTP response message.</span></span>
   
    ![Completar la acción de respuesta](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="de798-136">Haga clic en la esquina superior izquierda de la barra de herramientas para guardarla; la aplicación lógica se guardará y se publicará (activará).</span><span class="sxs-lookup"><span data-stu-id="de798-136">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="de798-137">Desencadenador de solicitud</span><span class="sxs-lookup"><span data-stu-id="de798-137">Request trigger</span></span>
<span data-ttu-id="de798-138">Aquí se muestran los detalles del desencadenador que admite este conector.</span><span class="sxs-lookup"><span data-stu-id="de798-138">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="de798-139">Solo existe un único desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="de798-139">There is a single request trigger.</span></span>

| <span data-ttu-id="de798-140">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="de798-140">Trigger</span></span> | <span data-ttu-id="de798-141">Description</span><span class="sxs-lookup"><span data-stu-id="de798-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de798-142">Solicitud</span><span class="sxs-lookup"><span data-stu-id="de798-142">Request</span></span> |<span data-ttu-id="de798-143">Se produce cuando se recibe una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="de798-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="de798-144">Acción de respuesta</span><span class="sxs-lookup"><span data-stu-id="de798-144">Response action</span></span>
<span data-ttu-id="de798-145">Aquí se muestran los detalles de la acción que admite este conector.</span><span class="sxs-lookup"><span data-stu-id="de798-145">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="de798-146">Hay una única de acción de respuesta que solo puede usarse acompañada de un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="de798-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="de798-147">Acción</span><span class="sxs-lookup"><span data-stu-id="de798-147">Action</span></span> | <span data-ttu-id="de798-148">Description</span><span class="sxs-lookup"><span data-stu-id="de798-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de798-149">Response</span><span class="sxs-lookup"><span data-stu-id="de798-149">Response</span></span> |<span data-ttu-id="de798-150">Devuelve una respuesta a la solicitud HTTP correlacionada.</span><span class="sxs-lookup"><span data-stu-id="de798-150">Returns a response to the correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="de798-151">Detalles de los desencadenadores y las acciones</span><span class="sxs-lookup"><span data-stu-id="de798-151">Trigger and action details</span></span>
<span data-ttu-id="de798-152">En las tablas siguientes se describen los campos de entrada para el desencadenador y la acción, así como los detalles de salida correspondientes.</span><span class="sxs-lookup"><span data-stu-id="de798-152">The following tables describe the input fields for the trigger and action, and the corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="de798-153">Desencadenador de solicitud</span><span class="sxs-lookup"><span data-stu-id="de798-153">Request trigger</span></span>
<span data-ttu-id="de798-154">El siguiente es un campo de entrada para el desencadenador de una solicitud HTTP entrante.</span><span class="sxs-lookup"><span data-stu-id="de798-154">The following is an input field for the trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="de798-155">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="de798-155">Display name</span></span> | <span data-ttu-id="de798-156">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="de798-156">Property name</span></span> | <span data-ttu-id="de798-157">Description</span><span class="sxs-lookup"><span data-stu-id="de798-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de798-158">Esquema JSON</span><span class="sxs-lookup"><span data-stu-id="de798-158">JSON Schema</span></span> |<span data-ttu-id="de798-159">schema</span><span class="sxs-lookup"><span data-stu-id="de798-159">schema</span></span> |<span data-ttu-id="de798-160">Esquema JSON del cuerpo de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="de798-160">The JSON schema of the HTTP request body</span></span> |

<br>

<span data-ttu-id="de798-161">**Detalles de salida**</span><span class="sxs-lookup"><span data-stu-id="de798-161">**Output details**</span></span>

<span data-ttu-id="de798-162">Los detalles del resultado de la solicitud son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="de798-162">The following are output details for the request.</span></span>

| <span data-ttu-id="de798-163">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="de798-163">Property name</span></span> | <span data-ttu-id="de798-164">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="de798-164">Data type</span></span> | <span data-ttu-id="de798-165">Description</span><span class="sxs-lookup"><span data-stu-id="de798-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de798-166">encabezados</span><span class="sxs-lookup"><span data-stu-id="de798-166">Headers</span></span> |<span data-ttu-id="de798-167">objeto</span><span class="sxs-lookup"><span data-stu-id="de798-167">object</span></span> |<span data-ttu-id="de798-168">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="de798-168">Request headers</span></span> |
| <span data-ttu-id="de798-169">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="de798-169">Body</span></span> |<span data-ttu-id="de798-170">objeto</span><span class="sxs-lookup"><span data-stu-id="de798-170">object</span></span> |<span data-ttu-id="de798-171">Objeto de solicitud</span><span class="sxs-lookup"><span data-stu-id="de798-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="de798-172">Acción de respuesta</span><span class="sxs-lookup"><span data-stu-id="de798-172">Response action</span></span>
<span data-ttu-id="de798-173">A continuación se muestran los campos de entrada para la acción de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="de798-173">The following are input fields for the HTTP Response action.</span></span> <span data-ttu-id="de798-174">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="de798-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="de798-175">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="de798-175">Display name</span></span> | <span data-ttu-id="de798-176">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="de798-176">Property name</span></span> | <span data-ttu-id="de798-177">Description</span><span class="sxs-lookup"><span data-stu-id="de798-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="de798-178">Código de estado*</span><span class="sxs-lookup"><span data-stu-id="de798-178">Status Code*</span></span> |<span data-ttu-id="de798-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="de798-179">statusCode</span></span> |<span data-ttu-id="de798-180">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="de798-180">The HTTP status code</span></span> |
| <span data-ttu-id="de798-181">Encabezados</span><span class="sxs-lookup"><span data-stu-id="de798-181">Headers</span></span> |<span data-ttu-id="de798-182">Encabezados</span><span class="sxs-lookup"><span data-stu-id="de798-182">headers</span></span> |<span data-ttu-id="de798-183">Objeto JSON de cualquier encabezado de respuesta que incluir</span><span class="sxs-lookup"><span data-stu-id="de798-183">A JSON object of any response headers to include</span></span> |
| <span data-ttu-id="de798-184">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="de798-184">Body</span></span> |<span data-ttu-id="de798-185">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="de798-185">body</span></span> |<span data-ttu-id="de798-186">Cuerpo de la respuesta</span><span class="sxs-lookup"><span data-stu-id="de798-186">The response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de798-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de798-187">Next steps</span></span>
<span data-ttu-id="de798-188">Ahora, pruebe la plataforma y [cree una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="de798-188">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="de798-189">Puede explorar los demás conectores disponibles en aplicaciones lógicas consultando nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="de798-189">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

