---
title: acciones de solicitud y respuesta aaaUse | Documentos de Microsoft
description: "Información general de desencadenador de solicitud y respuesta de Hola y de acción en una aplicación de lógica de Azure"
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
ms.openlocfilehash: 24c378cc12d5f3f65116d5e59278236186a99662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-request-and-response-components"></a><span data-ttu-id="3dc5c-103">Empezar a trabajar con componentes de solicitud y respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="3dc5c-103">Get started with hello request and response components</span></span>
<span data-ttu-id="3dc5c-104">Con hello solicitud y respuesta componentes en una aplicación de lógica, puede responder en tiempo real tooevents.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-104">With hello request and response components in a logic app, you can respond in real time tooevents.</span></span>

<span data-ttu-id="3dc5c-105">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="3dc5c-105">For example, you can:</span></span>

* <span data-ttu-id="3dc5c-106">Responder tooan solicitud HTTP con los datos desde una base de datos local a través de una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-106">Respond tooan HTTP request with data from an on-premises database through a logic app.</span></span>
* <span data-ttu-id="3dc5c-107">Desencadenar una aplicación lógica desde un evento webhook externo.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-107">Trigger a logic app from an external webhook event.</span></span>
* <span data-ttu-id="3dc5c-108">Llamar a una aplicación lógica con una acción de solicitud y respuesta desde otra aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-108">Call a logic app with a request and response action from within another logic app.</span></span>

<span data-ttu-id="3dc5c-109">tooget a usar acciones de solicitud y respuesta de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3dc5c-109">tooget started using hello request and response actions in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-request-trigger"></a><span data-ttu-id="3dc5c-110">Usar hello desencadenador de solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="3dc5c-110">Use hello HTTP Request trigger</span></span>
<span data-ttu-id="3dc5c-111">Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-111">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="3dc5c-112">[Más información sobre los desencadenadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3dc5c-112">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="3dc5c-113">Aquí es una secuencia de ejemplo de cómo solicitar tooset seguridad HTTP Hola diseñador la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-113">Here’s an example sequence of how tooset up an HTTP request in hello Logic App Designer.</span></span>

1. <span data-ttu-id="3dc5c-114">Agregar desencadenador de hello **solicitar - se recibe la solicitud HTTP de un cuando** en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-114">Add hello trigger **Request - When an HTTP request is received** in your logic app.</span></span> <span data-ttu-id="3dc5c-115">También puede proporcionar un esquema JSON (mediante el uso de una herramienta como [JSONSchema.net](http://jsonschema.net)) para el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-115">You can optionally provide a JSON schema (by using a tool like [JSONSchema.net](http://jsonschema.net)) for hello request body.</span></span> <span data-ttu-id="3dc5c-116">Esto permite hello toogenerate diseñador símbolos (tokens) para las propiedades de solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-116">This allows hello designer toogenerate tokens for properties in hello HTTP request.</span></span>
2. <span data-ttu-id="3dc5c-117">Agregar otra acción para que pueda guardar aplicación lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-117">Add another action so that you can save hello logic app.</span></span>
3. <span data-ttu-id="3dc5c-118">Después de guardar la aplicación de la lógica de hello, puede obtener la dirección URL de solicitud de hello HTTP de tarjeta de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-118">After saving hello logic app, you can get hello HTTP request URL from hello request card.</span></span>
4. <span data-ttu-id="3dc5c-119">Una solicitud HTTP POST (puede utilizar una herramienta como [Postman](https://www.getpostman.com/)) desencadenadores de la dirección URL de toohello Hola aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-119">An HTTP POST (you can use a tool like [Postman](https://www.getpostman.com/)) toohello URL triggers hello logic app.</span></span>

> [!NOTE]
> <span data-ttu-id="3dc5c-120">Si no define una acción de respuesta, un `202 ACCEPTED` respuesta se devuelve inmediatamente toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-120">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span> <span data-ttu-id="3dc5c-121">Puede usar toocustomize de acción de respuesta de hello una respuesta.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-121">You can use hello response action toocustomize a response.</span></span>
> 
> 

![Desencadenador de respuesta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a><span data-ttu-id="3dc5c-123">Usar hello acción de respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="3dc5c-123">Use hello HTTP Response action</span></span>
<span data-ttu-id="3dc5c-124">Hola acción de respuesta HTTP solo es válido cuando se usa en un flujo de trabajo activado por una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-124">hello HTTP Response action is only valid when you use it in a workflow that is triggered by an HTTP request.</span></span> <span data-ttu-id="3dc5c-125">Si no define una acción de respuesta, un `202 ACCEPTED` respuesta se devuelve inmediatamente toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-125">If you don't define a response action, a `202 ACCEPTED` response is immediately returned toohello caller.</span></span>  <span data-ttu-id="3dc5c-126">Puede agregar una acción de respuesta en cualquier paso en el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-126">You can add a response action at any step within hello workflow.</span></span> <span data-ttu-id="3dc5c-127">aplicación de la lógica de Hello solo mantiene solicitud entrante de hello abierto durante un minuto para una respuesta.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-127">hello logic app only keeps hello incoming request open for one minute for a response.</span></span>  <span data-ttu-id="3dc5c-128">Después de un minuto, si no hay respuesta fue enviada desde el flujo de trabajo de hello (y existe una acción de respuesta en la definición de hello), un `504 GATEWAY TIMEOUT` se devuelve toohello autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-128">After one minute, if no response was sent from hello workflow (and a response action exists in hello definition), a `504 GATEWAY TIMEOUT` is returned toohello caller.</span></span>

<span data-ttu-id="3dc5c-129">Le mostramos cómo tooadd una acción de respuesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="3dc5c-129">Here's how tooadd an HTTP Response action:</span></span>

1. <span data-ttu-id="3dc5c-130">Seleccione hello **nuevo paso** botón.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-130">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="3dc5c-131">Elija **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="3dc5c-131">Choose **Add an action**.</span></span>
3. <span data-ttu-id="3dc5c-132">En el cuadro de búsqueda de la acción de hello, escriba **respuesta** hello toolist acción de respuesta.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-132">In hello action search box, type **response** toolist hello Response action.</span></span>
   
    ![Seleccione la acción de respuesta de Hola](./media/connectors-native-reqres/using-action-1.png)
4. <span data-ttu-id="3dc5c-134">Agregue todos los parámetros que son necesarios para el mensaje de respuesta HTTP de saludo.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-134">Add in any parameters that are required for hello HTTP response message.</span></span>
   
    ![Acción de respuesta de hello completa](./media/connectors-native-reqres/using-action-2.png)
5. <span data-ttu-id="3dc5c-136">Haga clic en la esquina superior izquierda de Hola de hello toosave de barra de herramientas y la lógica aplicación guardará ambos y publicar (activar).</span><span class="sxs-lookup"><span data-stu-id="3dc5c-136">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="request-trigger"></a><span data-ttu-id="3dc5c-137">Desencadenador de solicitud</span><span class="sxs-lookup"><span data-stu-id="3dc5c-137">Request trigger</span></span>
<span data-ttu-id="3dc5c-138">A continuación encontrará los detalles de Hola de desencadenador de hello admitido por este conector.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-138">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="3dc5c-139">Solo existe un único desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-139">There is a single request trigger.</span></span>

| <span data-ttu-id="3dc5c-140">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="3dc5c-140">Trigger</span></span> | <span data-ttu-id="3dc5c-141">Description</span><span class="sxs-lookup"><span data-stu-id="3dc5c-141">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3dc5c-142">Solicitud</span><span class="sxs-lookup"><span data-stu-id="3dc5c-142">Request</span></span> |<span data-ttu-id="3dc5c-143">Se produce cuando se recibe una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-143">Occurs when an HTTP request is received</span></span> |

## <a name="response-action"></a><span data-ttu-id="3dc5c-144">Acción de respuesta</span><span class="sxs-lookup"><span data-stu-id="3dc5c-144">Response action</span></span>
<span data-ttu-id="3dc5c-145">A continuación encontrará los detalles de hello para la acción de hello admitido por este conector.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-145">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="3dc5c-146">Hay una única de acción de respuesta que solo puede usarse acompañada de un desencadenador de solicitud.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-146">There is a single response action that can only be used when it is accompanied by a request trigger.</span></span>

| <span data-ttu-id="3dc5c-147">Acción</span><span class="sxs-lookup"><span data-stu-id="3dc5c-147">Action</span></span> | <span data-ttu-id="3dc5c-148">Description</span><span class="sxs-lookup"><span data-stu-id="3dc5c-148">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3dc5c-149">Response</span><span class="sxs-lookup"><span data-stu-id="3dc5c-149">Response</span></span> |<span data-ttu-id="3dc5c-150">Devuelve que una respuesta toohello correlacionado solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="3dc5c-150">Returns a response toohello correlated HTTP request</span></span> |

### <a name="trigger-and-action-details"></a><span data-ttu-id="3dc5c-151">Detalles de los desencadenadores y las acciones</span><span class="sxs-lookup"><span data-stu-id="3dc5c-151">Trigger and action details</span></span>
<span data-ttu-id="3dc5c-152">Hello en las tablas siguientes se describen los campos de entrada de hello para el desencadenador de Hola y acción y Hola detalles de salida correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-152">hello following tables describe hello input fields for hello trigger and action, and hello corresponding output details.</span></span>

#### <a name="request-trigger"></a><span data-ttu-id="3dc5c-153">Desencadenador de solicitud</span><span class="sxs-lookup"><span data-stu-id="3dc5c-153">Request trigger</span></span>
<span data-ttu-id="3dc5c-154">Hola aquí te mostramos un campo de entrada de desencadenador de Hola de una solicitud HTTP entrante.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-154">hello following is an input field for hello trigger from an incoming HTTP request.</span></span>

| <span data-ttu-id="3dc5c-155">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="3dc5c-155">Display name</span></span> | <span data-ttu-id="3dc5c-156">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="3dc5c-156">Property name</span></span> | <span data-ttu-id="3dc5c-157">Description</span><span class="sxs-lookup"><span data-stu-id="3dc5c-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3dc5c-158">Esquema JSON</span><span class="sxs-lookup"><span data-stu-id="3dc5c-158">JSON Schema</span></span> |<span data-ttu-id="3dc5c-159">schema</span><span class="sxs-lookup"><span data-stu-id="3dc5c-159">schema</span></span> |<span data-ttu-id="3dc5c-160">esquema JSON de Hola Hola HTTP del cuerpo de solicitud</span><span class="sxs-lookup"><span data-stu-id="3dc5c-160">hello JSON schema of hello HTTP request body</span></span> |

<br>

<span data-ttu-id="3dc5c-161">**Detalles de salida**</span><span class="sxs-lookup"><span data-stu-id="3dc5c-161">**Output details**</span></span>

<span data-ttu-id="3dc5c-162">siguiente Hola es detalles de salida de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-162">hello following are output details for hello request.</span></span>

| <span data-ttu-id="3dc5c-163">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="3dc5c-163">Property name</span></span> | <span data-ttu-id="3dc5c-164">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="3dc5c-164">Data type</span></span> | <span data-ttu-id="3dc5c-165">Description</span><span class="sxs-lookup"><span data-stu-id="3dc5c-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3dc5c-166">encabezados</span><span class="sxs-lookup"><span data-stu-id="3dc5c-166">Headers</span></span> |<span data-ttu-id="3dc5c-167">objeto</span><span class="sxs-lookup"><span data-stu-id="3dc5c-167">object</span></span> |<span data-ttu-id="3dc5c-168">Encabezados de solicitud</span><span class="sxs-lookup"><span data-stu-id="3dc5c-168">Request headers</span></span> |
| <span data-ttu-id="3dc5c-169">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="3dc5c-169">Body</span></span> |<span data-ttu-id="3dc5c-170">objeto</span><span class="sxs-lookup"><span data-stu-id="3dc5c-170">object</span></span> |<span data-ttu-id="3dc5c-171">Objeto de solicitud</span><span class="sxs-lookup"><span data-stu-id="3dc5c-171">Request object</span></span> |

#### <a name="response-action"></a><span data-ttu-id="3dc5c-172">Acción de respuesta</span><span class="sxs-lookup"><span data-stu-id="3dc5c-172">Response action</span></span>
<span data-ttu-id="3dc5c-173">los siguientes Hola son campos de entrada para hello acción de respuesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-173">hello following are input fields for hello HTTP Response action.</span></span> <span data-ttu-id="3dc5c-174">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="3dc5c-174">A * means that it is a required field.</span></span>

| <span data-ttu-id="3dc5c-175">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="3dc5c-175">Display name</span></span> | <span data-ttu-id="3dc5c-176">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="3dc5c-176">Property name</span></span> | <span data-ttu-id="3dc5c-177">Description</span><span class="sxs-lookup"><span data-stu-id="3dc5c-177">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3dc5c-178">Código de estado*</span><span class="sxs-lookup"><span data-stu-id="3dc5c-178">Status Code*</span></span> |<span data-ttu-id="3dc5c-179">statusCode</span><span class="sxs-lookup"><span data-stu-id="3dc5c-179">statusCode</span></span> |<span data-ttu-id="3dc5c-180">Hola código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="3dc5c-180">hello HTTP status code</span></span> |
| <span data-ttu-id="3dc5c-181">Encabezados</span><span class="sxs-lookup"><span data-stu-id="3dc5c-181">Headers</span></span> |<span data-ttu-id="3dc5c-182">encabezados</span><span class="sxs-lookup"><span data-stu-id="3dc5c-182">headers</span></span> |<span data-ttu-id="3dc5c-183">Un objeto JSON de cualquier tooinclude de encabezados de respuesta</span><span class="sxs-lookup"><span data-stu-id="3dc5c-183">A JSON object of any response headers tooinclude</span></span> |
| <span data-ttu-id="3dc5c-184">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="3dc5c-184">Body</span></span> |<span data-ttu-id="3dc5c-185">body</span><span class="sxs-lookup"><span data-stu-id="3dc5c-185">body</span></span> |<span data-ttu-id="3dc5c-186">cuerpo de respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="3dc5c-186">hello response body</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3dc5c-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3dc5c-187">Next steps</span></span>
<span data-ttu-id="3dc5c-188">Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3dc5c-188">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3dc5c-189">Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3dc5c-189">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

