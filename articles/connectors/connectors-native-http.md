---
title: "aaaCommunicate con cualquier punto de conexión a través de HTTP - Azure Logic Apps | Documentos de Microsoft"
description: "Creación de aplicaciones lógicas que se comuniquen con cualquier punto de conexión a través de HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="4c92e-103">Empezar a trabajar con hello acción HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="4c92e-104">Con hello acción HTTP, puede ampliar los flujos de trabajo para su organización y punto de conexión de tooany se comunican a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c92e-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="4c92e-105">Puede:</span><span class="sxs-lookup"><span data-stu-id="4c92e-105">You can:</span></span>

* <span data-ttu-id="4c92e-106">Cree flujos de trabajo de aplicaciones lógicas que se activen (desencadenador) cuando un sitio web que administre deje de funcionar.</span><span class="sxs-lookup"><span data-stu-id="4c92e-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="4c92e-107">Comunicarse el punto de conexión de tooany en otros servicios a través de HTTP tooextend los flujos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4c92e-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="4c92e-108">tooget se hayan iniciado mediante la acción de hello HTTP en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c92e-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="4c92e-109">Utilice el desencadenador de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="4c92e-110">Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="4c92e-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="4c92e-111">[Más información sobre los desencadenadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c92e-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="4c92e-112">Aquí es una secuencia de ejemplo de cómo desencadenar tooset seguridad Hola HTTP Hola diseñador la lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4c92e-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="4c92e-113">Agregar desencadenador HTTP de hello en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="4c92e-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="4c92e-114">Completar parámetros de Hola de punto de conexión de hello HTTP que desea toopoll.</span><span class="sxs-lookup"><span data-stu-id="4c92e-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="4c92e-115">Modificar el intervalo de periodicidad de hello en la frecuencia con debería realizar el sondeo.</span><span class="sxs-lookup"><span data-stu-id="4c92e-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="4c92e-116">aplicación de la lógica de Hello ahora se desencadena con cualquier contenido que se devuelve durante cada comprobación.</span><span class="sxs-lookup"><span data-stu-id="4c92e-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Desencadenador HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="4c92e-118">Cómo funciona el desencadenador de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="4c92e-119">desencadenador de Hello HTTP envía un punto de conexión de llamada tooHTTP en un intervalo periódico.</span><span class="sxs-lookup"><span data-stu-id="4c92e-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="4c92e-120">De forma predeterminada, cualquier código de respuesta HTTP que es inferior a 300 hace un toorun de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="4c92e-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="4c92e-121">toospecify si debería desencadenar la aplicación de la lógica de hello, puede editar aplicación de lógica de hello en la vista de código y agregar una condición que se evalúa como después de hello llamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c92e-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="4c92e-122">Este es un ejemplo de un desencadenador HTTP que se desencadena cuando Hola devolvió el código de estado es mayor o igual a demasiado`400`.</span><span class="sxs-lookup"><span data-stu-id="4c92e-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="4c92e-123">Encuentran los detalles completos acerca de los parámetros de desencadenador de hello HTTP en [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="4c92e-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="4c92e-124">Use la acción Hola HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-124">Use hello HTTP action</span></span>

<span data-ttu-id="4c92e-125">Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="4c92e-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="4c92e-126">[Más información acerca de las acciones](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c92e-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="4c92e-127">Elija **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="4c92e-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="4c92e-128">En el cuadro de búsqueda de la acción de hello, escriba **http** acciones de hello HTTP toolist.</span><span class="sxs-lookup"><span data-stu-id="4c92e-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Seleccione la acción de hello HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="4c92e-130">Agregue los parámetros necesarios para la llamada de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c92e-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Hola completa acción HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="4c92e-132">En la barra de herramientas del diseñador hello, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="4c92e-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="4c92e-133">La aplicación lógica se guardó y publicó (activada) en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="4c92e-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="4c92e-134">Desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-134">HTTP trigger</span></span>
<span data-ttu-id="4c92e-135">A continuación encontrará los detalles de Hola de desencadenador de hello admitido por este conector.</span><span class="sxs-lookup"><span data-stu-id="4c92e-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="4c92e-136">conector HTTP de Hello tiene un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="4c92e-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="4c92e-137">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="4c92e-137">Trigger</span></span> | <span data-ttu-id="4c92e-138">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4c92e-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-139">HTTP</span></span> |<span data-ttu-id="4c92e-140">Realiza una llamada HTTP y devuelve el contenido de la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c92e-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="4c92e-141">Acción HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-141">HTTP action</span></span>
<span data-ttu-id="4c92e-142">A continuación encontrará los detalles de hello para la acción de hello admitido por este conector.</span><span class="sxs-lookup"><span data-stu-id="4c92e-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="4c92e-143">Conector de Hello HTTP tiene una acción posible.</span><span class="sxs-lookup"><span data-stu-id="4c92e-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="4c92e-144">Acción</span><span class="sxs-lookup"><span data-stu-id="4c92e-144">Action</span></span> | <span data-ttu-id="4c92e-145">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4c92e-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-146">HTTP</span></span> |<span data-ttu-id="4c92e-147">Realiza una llamada HTTP y devuelve el contenido de la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c92e-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="4c92e-148">Detalles HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-148">HTTP details</span></span>
<span data-ttu-id="4c92e-149">Hello en las tablas siguientes se describen Hola necesarios y campos de entrada opcionales para acción de Hola y detalles salida correspondientes Hola que están asociados con el uso de la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c92e-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="4c92e-150">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-150">HTTP request</span></span>
<span data-ttu-id="4c92e-151">los siguientes Hola son campos de entrada para la acción de hello, que realiza una solicitud de salida HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c92e-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="4c92e-152">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="4c92e-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="4c92e-153">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="4c92e-153">Display name</span></span> | <span data-ttu-id="4c92e-154">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="4c92e-154">Property name</span></span> | <span data-ttu-id="4c92e-155">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c92e-156">Método*</span><span class="sxs-lookup"><span data-stu-id="4c92e-156">Method*</span></span> |<span data-ttu-id="4c92e-157">estático</span><span class="sxs-lookup"><span data-stu-id="4c92e-157">method</span></span> |<span data-ttu-id="4c92e-158">Hola HTTP verbo toouse</span><span class="sxs-lookup"><span data-stu-id="4c92e-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="4c92e-159">URI*</span><span class="sxs-lookup"><span data-stu-id="4c92e-159">URI*</span></span> |<span data-ttu-id="4c92e-160">uri</span><span class="sxs-lookup"><span data-stu-id="4c92e-160">uri</span></span> |<span data-ttu-id="4c92e-161">Hola URI de solicitud de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="4c92e-162">Encabezados</span><span class="sxs-lookup"><span data-stu-id="4c92e-162">Headers</span></span> |<span data-ttu-id="4c92e-163">encabezados</span><span class="sxs-lookup"><span data-stu-id="4c92e-163">headers</span></span> |<span data-ttu-id="4c92e-164">Un objeto JSON de tooinclude de encabezados HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="4c92e-165">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="4c92e-165">Body</span></span> |<span data-ttu-id="4c92e-166">body</span><span class="sxs-lookup"><span data-stu-id="4c92e-166">body</span></span> |<span data-ttu-id="4c92e-167">Hola cuerpo de solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-167">hello HTTP request body</span></span> |
| <span data-ttu-id="4c92e-168">Autenticación</span><span class="sxs-lookup"><span data-stu-id="4c92e-168">Authentication</span></span> |<span data-ttu-id="4c92e-169">Autenticación</span><span class="sxs-lookup"><span data-stu-id="4c92e-169">authentication</span></span> |<span data-ttu-id="4c92e-170">Detalles de hello [autenticación](#authentication) sección</span><span class="sxs-lookup"><span data-stu-id="4c92e-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="4c92e-171">Detalles de salida</span><span class="sxs-lookup"><span data-stu-id="4c92e-171">Output details</span></span>
<span data-ttu-id="4c92e-172">siguiente Hola es detalles de salida de respuesta HTTP Hola.</span><span class="sxs-lookup"><span data-stu-id="4c92e-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="4c92e-173">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="4c92e-173">Property name</span></span> | <span data-ttu-id="4c92e-174">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="4c92e-174">Data type</span></span> | <span data-ttu-id="4c92e-175">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c92e-176">encabezados</span><span class="sxs-lookup"><span data-stu-id="4c92e-176">Headers</span></span> |<span data-ttu-id="4c92e-177">objeto</span><span class="sxs-lookup"><span data-stu-id="4c92e-177">object</span></span> |<span data-ttu-id="4c92e-178">Encabezados de respuesta</span><span class="sxs-lookup"><span data-stu-id="4c92e-178">Response headers</span></span> |
| <span data-ttu-id="4c92e-179">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="4c92e-179">Body</span></span> |<span data-ttu-id="4c92e-180">objeto</span><span class="sxs-lookup"><span data-stu-id="4c92e-180">object</span></span> |<span data-ttu-id="4c92e-181">Objeto de respuesta</span><span class="sxs-lookup"><span data-stu-id="4c92e-181">Response object</span></span> |
| <span data-ttu-id="4c92e-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="4c92e-182">Status Code</span></span> |<span data-ttu-id="4c92e-183">int</span><span class="sxs-lookup"><span data-stu-id="4c92e-183">int</span></span> |<span data-ttu-id="4c92e-184">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="4c92e-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="4c92e-185">Autenticación</span><span class="sxs-lookup"><span data-stu-id="4c92e-185">Authentication</span></span>
<span data-ttu-id="4c92e-186">característica de las aplicaciones lógicas de Hello permite a toouse diferentes tipos de autenticación en los extremos HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c92e-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="4c92e-187">Puede usar este procedimiento de autenticación con hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, y  **[HTTP Webhook](connectors-native-webhook.md)**  conectores.</span><span class="sxs-lookup"><span data-stu-id="4c92e-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="4c92e-188">Hola siguientes tipos de autenticación es configurable:</span><span class="sxs-lookup"><span data-stu-id="4c92e-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="4c92e-189">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="4c92e-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="4c92e-190">Autenticación de certificados de clientes</span><span class="sxs-lookup"><span data-stu-id="4c92e-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="4c92e-191">Autenticación de OAuth de Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="4c92e-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="4c92e-192">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="4c92e-192">Basic authentication</span></span>

<span data-ttu-id="4c92e-193">Hola después el objeto de autenticación es necesario para la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="4c92e-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="4c92e-194">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="4c92e-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="4c92e-195">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="4c92e-195">Property name</span></span> | <span data-ttu-id="4c92e-196">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="4c92e-196">Data type</span></span> | <span data-ttu-id="4c92e-197">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c92e-198">Type*</span><span class="sxs-lookup"><span data-stu-id="4c92e-198">Type*</span></span> |<span data-ttu-id="4c92e-199">type</span><span class="sxs-lookup"><span data-stu-id="4c92e-199">type</span></span> |<span data-ttu-id="4c92e-200">Tipo de autenticación (debe ser `Basic` para la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="4c92e-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="4c92e-201">Username*</span><span class="sxs-lookup"><span data-stu-id="4c92e-201">Username*</span></span> |<span data-ttu-id="4c92e-202">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="4c92e-202">username</span></span> |<span data-ttu-id="4c92e-203">Tooauthenticate de nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="4c92e-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="4c92e-204">Password*</span><span class="sxs-lookup"><span data-stu-id="4c92e-204">Password*</span></span> |<span data-ttu-id="4c92e-205">Contraseña</span><span class="sxs-lookup"><span data-stu-id="4c92e-205">password</span></span> |<span data-ttu-id="4c92e-206">Contraseña tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="4c92e-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="4c92e-207">Si desea toouse una contraseña que no se puede recuperar de la definición de hello, use un `securestring` hello y parámetro `@parameters()`  
>  [función de la definición de flujo de trabajo](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="4c92e-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="4c92e-208">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4c92e-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="4c92e-209">Autenticación de certificados de clientes</span><span class="sxs-lookup"><span data-stu-id="4c92e-209">Client certificate authentication</span></span>

<span data-ttu-id="4c92e-210">Hello es necesario siguiente objeto de autenticación para la autenticación de certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="4c92e-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="4c92e-211">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="4c92e-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="4c92e-212">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="4c92e-212">Property name</span></span> | <span data-ttu-id="4c92e-213">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="4c92e-213">Data type</span></span> | <span data-ttu-id="4c92e-214">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c92e-215">Type*</span><span class="sxs-lookup"><span data-stu-id="4c92e-215">Type*</span></span> |<span data-ttu-id="4c92e-216">type</span><span class="sxs-lookup"><span data-stu-id="4c92e-216">type</span></span> |<span data-ttu-id="4c92e-217">tipo de autenticación de Hola (debe ser `ClientCertificate` para los certificados de cliente SSL)</span><span class="sxs-lookup"><span data-stu-id="4c92e-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="4c92e-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="4c92e-218">PFX*</span></span> |<span data-ttu-id="4c92e-219">pfx</span><span class="sxs-lookup"><span data-stu-id="4c92e-219">pfx</span></span> |<span data-ttu-id="4c92e-220">contenido de Hello con codificación Base64 del archivo de intercambio de información Personal (PFX) Hola</span><span class="sxs-lookup"><span data-stu-id="4c92e-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="4c92e-221">Password*</span><span class="sxs-lookup"><span data-stu-id="4c92e-221">Password*</span></span> |<span data-ttu-id="4c92e-222">Contraseña</span><span class="sxs-lookup"><span data-stu-id="4c92e-222">password</span></span> |<span data-ttu-id="4c92e-223">Hola contraseña tooaccess Hola archivo PFX</span><span class="sxs-lookup"><span data-stu-id="4c92e-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="4c92e-224">toouse un parámetro que no se puede leer en la definición de hello después de guardar la aplicación de la lógica de hello, puede usar un `securestring` hello y parámetro `@parameters()`  
>  [función de la definición de flujo de trabajo](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="4c92e-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="4c92e-225">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4c92e-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="4c92e-226">Autenticación de OAuth de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c92e-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="4c92e-227">Hola después el objeto de autenticación es necesario para la autenticación de OAuth de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c92e-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="4c92e-228">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="4c92e-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="4c92e-229">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="4c92e-229">Property name</span></span> | <span data-ttu-id="4c92e-230">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="4c92e-230">Data type</span></span> | <span data-ttu-id="4c92e-231">Description</span><span class="sxs-lookup"><span data-stu-id="4c92e-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c92e-232">Type*</span><span class="sxs-lookup"><span data-stu-id="4c92e-232">Type*</span></span> |<span data-ttu-id="4c92e-233">type</span><span class="sxs-lookup"><span data-stu-id="4c92e-233">type</span></span> |<span data-ttu-id="4c92e-234">tipo de autenticación de Hola (debe ser `ActiveDirectoryOAuth` para Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="4c92e-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="4c92e-235">Tenant*</span><span class="sxs-lookup"><span data-stu-id="4c92e-235">Tenant*</span></span> |<span data-ttu-id="4c92e-236">tenant</span><span class="sxs-lookup"><span data-stu-id="4c92e-236">tenant</span></span> |<span data-ttu-id="4c92e-237">identificador del inquilino Hello para el inquilino de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c92e-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="4c92e-238">Audience*</span><span class="sxs-lookup"><span data-stu-id="4c92e-238">Audience*</span></span> |<span data-ttu-id="4c92e-239">audience</span><span class="sxs-lookup"><span data-stu-id="4c92e-239">audience</span></span> |<span data-ttu-id="4c92e-240">recurso de Hola que está solicitando toouse de autorización.</span><span class="sxs-lookup"><span data-stu-id="4c92e-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="4c92e-241">Por ejemplo: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="4c92e-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="4c92e-242">Client ID*</span><span class="sxs-lookup"><span data-stu-id="4c92e-242">Client ID*</span></span> |<span data-ttu-id="4c92e-243">clientId</span><span class="sxs-lookup"><span data-stu-id="4c92e-243">clientId</span></span> |<span data-ttu-id="4c92e-244">Hola identificador de cliente de la aplicación hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c92e-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="4c92e-245">Secret*</span><span class="sxs-lookup"><span data-stu-id="4c92e-245">Secret*</span></span> |<span data-ttu-id="4c92e-246">secret</span><span class="sxs-lookup"><span data-stu-id="4c92e-246">secret</span></span> |<span data-ttu-id="4c92e-247">secreto de Hola Hola del cliente de que solicita el token de Hola</span><span class="sxs-lookup"><span data-stu-id="4c92e-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="4c92e-248">Puede usar un `securestring` hello y parámetro `@parameters()` [función de la definición de flujo de trabajo](http://aka.ms/logicappdocs) toouse un parámetro que no se puede leer en la definición de hello después de guardar.</span><span class="sxs-lookup"><span data-stu-id="4c92e-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="4c92e-249">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4c92e-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="4c92e-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c92e-250">Next steps</span></span>
<span data-ttu-id="4c92e-251">Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c92e-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4c92e-252">Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4c92e-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

