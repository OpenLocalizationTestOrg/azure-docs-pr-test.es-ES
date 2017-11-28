---
title: "Comunicación con cualquier punto de conexión a través de HTTP: Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="ce62b-103">Introducción a la acción HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-103">Get started with the HTTP action</span></span>

<span data-ttu-id="ce62b-104">Con la acción HTTP, puede ampliar los flujos de trabajo de su organización y comunicarse con cualquier punto de conexión a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce62b-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="ce62b-105">Puede:</span><span class="sxs-lookup"><span data-stu-id="ce62b-105">You can:</span></span>

* <span data-ttu-id="ce62b-106">Cree flujos de trabajo de aplicaciones lógicas que se activen (desencadenador) cuando un sitio web que administre deje de funcionar.</span><span class="sxs-lookup"><span data-stu-id="ce62b-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="ce62b-107">Comuníquese con cualquier punto de conexión por HTTP para ampliar los flujos de trabajo a otros servicios.</span><span class="sxs-lookup"><span data-stu-id="ce62b-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="ce62b-108">Para empezar a usar la acción HTTP en una aplicación lógica, consulte [Creación de una nueva aplicación lógica mediante la conexión de servicios de SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ce62b-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="ce62b-109">Uso del desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-109">Use the HTTP trigger</span></span>
<span data-ttu-id="ce62b-110">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ce62b-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="ce62b-111">[Más información sobre los desencadenadores](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce62b-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="ce62b-112">Esta es una secuencia de ejemplo de cómo configurar un desencadenador HTTP en el diseñador de aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="ce62b-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="ce62b-113">Agregue el desencadenador HTTP a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ce62b-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="ce62b-114">Rellene los parámetros para el punto de conexión HTTP que desee sondear.</span><span class="sxs-lookup"><span data-stu-id="ce62b-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="ce62b-115">Modifique el intervalo de periodicidad de la frecuencia con que se debe sondear.</span><span class="sxs-lookup"><span data-stu-id="ce62b-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="ce62b-116">Ahora se activa la aplicación lógica con cualquier contenido que se devuelva durante cada comprobación.</span><span class="sxs-lookup"><span data-stu-id="ce62b-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![Desencadenador HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="ce62b-118">Funcionamiento del desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-118">How the HTTP trigger works</span></span>

<span data-ttu-id="ce62b-119">El desencadenador HTTP realiza una llamada a un punto de conexión HTTP en un intervalo periódico.</span><span class="sxs-lookup"><span data-stu-id="ce62b-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="ce62b-120">De forma predeterminada, cualquier código de respuesta HTTP inferior a 300 hace que se ejecute una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ce62b-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="ce62b-121">Para especificar si se debe activar la aplicación lógica, puede editarla en la vista de código y agregar una condición que se examine después de la llamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce62b-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="ce62b-122">Este es un ejemplo de desencadenador HTTP que se activa cada vez que el código de estado devuelto es mayor o igual que `400`.</span><span class="sxs-lookup"><span data-stu-id="ce62b-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

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

<span data-ttu-id="ce62b-123">Los detalles completos acerca de los parámetros de desencadenador HTTP están disponibles en [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="ce62b-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="ce62b-124">Uso de la acción HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-124">Use the HTTP action</span></span>

<span data-ttu-id="ce62b-125">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="ce62b-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="ce62b-126">[Más información sobre las acciones](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce62b-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="ce62b-127">Elija **Nuevo paso** > **Agregar una acción**.</span><span class="sxs-lookup"><span data-stu-id="ce62b-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="ce62b-128">En el cuadro de búsqueda de acciones, escriba **http** para mostrar las acciones HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce62b-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Selección de la acción de HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="ce62b-130">Agregue los parámetros necesarios para la llamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce62b-130">Add any required parameters for the HTTP call.</span></span>
   
    ![Finalización de la acción de HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="ce62b-132">En la barra de herramientas del diseñador, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ce62b-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="ce62b-133">La aplicación lógica se guarda y publica (activa) al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="ce62b-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="ce62b-134">Desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-134">HTTP trigger</span></span>
<span data-ttu-id="ce62b-135">Aquí se muestran los detalles del desencadenador que admite este conector.</span><span class="sxs-lookup"><span data-stu-id="ce62b-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="ce62b-136">El conector HTTP tiene un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="ce62b-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="ce62b-137">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="ce62b-137">Trigger</span></span> | <span data-ttu-id="ce62b-138">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce62b-139">http</span><span class="sxs-lookup"><span data-stu-id="ce62b-139">HTTP</span></span> |<span data-ttu-id="ce62b-140">Realiza una llamada HTTP y devuelve el contenido de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ce62b-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="ce62b-141">Acción HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-141">HTTP action</span></span>
<span data-ttu-id="ce62b-142">Aquí se muestran los detalles de la acción que admite este conector.</span><span class="sxs-lookup"><span data-stu-id="ce62b-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="ce62b-143">El conector HTTP tiene una acción posible.</span><span class="sxs-lookup"><span data-stu-id="ce62b-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="ce62b-144">Acción</span><span class="sxs-lookup"><span data-stu-id="ce62b-144">Action</span></span> | <span data-ttu-id="ce62b-145">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ce62b-146">http</span><span class="sxs-lookup"><span data-stu-id="ce62b-146">HTTP</span></span> |<span data-ttu-id="ce62b-147">Realiza una llamada HTTP y devuelve el contenido de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="ce62b-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="ce62b-148">Detalles HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-148">HTTP details</span></span>
<span data-ttu-id="ce62b-149">Las tablas siguientes describen los campos de entrada obligatorios y opcionales para la acción y los detalles de salida correspondientes asociados a su uso.</span><span class="sxs-lookup"><span data-stu-id="ce62b-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="ce62b-150">Solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-150">HTTP request</span></span>
<span data-ttu-id="ce62b-151">Los siguientes son los campos de entrada para la acción que realiza una solicitud de salida HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce62b-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="ce62b-152">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="ce62b-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="ce62b-153">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="ce62b-153">Display name</span></span> | <span data-ttu-id="ce62b-154">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="ce62b-154">Property name</span></span> | <span data-ttu-id="ce62b-155">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce62b-156">Método*</span><span class="sxs-lookup"><span data-stu-id="ce62b-156">Method*</span></span> |<span data-ttu-id="ce62b-157">estático</span><span class="sxs-lookup"><span data-stu-id="ce62b-157">method</span></span> |<span data-ttu-id="ce62b-158">El verbo HTTP que se usará</span><span class="sxs-lookup"><span data-stu-id="ce62b-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="ce62b-159">URI*</span><span class="sxs-lookup"><span data-stu-id="ce62b-159">URI*</span></span> |<span data-ttu-id="ce62b-160">uri</span><span class="sxs-lookup"><span data-stu-id="ce62b-160">uri</span></span> |<span data-ttu-id="ce62b-161">El identificador URI de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="ce62b-162">Encabezados</span><span class="sxs-lookup"><span data-stu-id="ce62b-162">Headers</span></span> |<span data-ttu-id="ce62b-163">Encabezados</span><span class="sxs-lookup"><span data-stu-id="ce62b-163">headers</span></span> |<span data-ttu-id="ce62b-164">Objeto JSON de los encabezados HTTP que incluir</span><span class="sxs-lookup"><span data-stu-id="ce62b-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="ce62b-165">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="ce62b-165">Body</span></span> |<span data-ttu-id="ce62b-166">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="ce62b-166">body</span></span> |<span data-ttu-id="ce62b-167">Cuerpo de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-167">The HTTP request body</span></span> |
| <span data-ttu-id="ce62b-168">Autenticación</span><span class="sxs-lookup"><span data-stu-id="ce62b-168">Authentication</span></span> |<span data-ttu-id="ce62b-169">Autenticación</span><span class="sxs-lookup"><span data-stu-id="ce62b-169">authentication</span></span> |<span data-ttu-id="ce62b-170">Detalles en la sección [Autenticación](#authentication)</span><span class="sxs-lookup"><span data-stu-id="ce62b-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="ce62b-171">Detalles de salida</span><span class="sxs-lookup"><span data-stu-id="ce62b-171">Output details</span></span>
<span data-ttu-id="ce62b-172">Los detalles de la salida de la respuesta HTTP son los siguientes.</span><span class="sxs-lookup"><span data-stu-id="ce62b-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="ce62b-173">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="ce62b-173">Property name</span></span> | <span data-ttu-id="ce62b-174">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="ce62b-174">Data type</span></span> | <span data-ttu-id="ce62b-175">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce62b-176">encabezados</span><span class="sxs-lookup"><span data-stu-id="ce62b-176">Headers</span></span> |<span data-ttu-id="ce62b-177">objeto</span><span class="sxs-lookup"><span data-stu-id="ce62b-177">object</span></span> |<span data-ttu-id="ce62b-178">Encabezados de respuesta</span><span class="sxs-lookup"><span data-stu-id="ce62b-178">Response headers</span></span> |
| <span data-ttu-id="ce62b-179">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="ce62b-179">Body</span></span> |<span data-ttu-id="ce62b-180">objeto</span><span class="sxs-lookup"><span data-stu-id="ce62b-180">object</span></span> |<span data-ttu-id="ce62b-181">Objeto de respuesta</span><span class="sxs-lookup"><span data-stu-id="ce62b-181">Response object</span></span> |
| <span data-ttu-id="ce62b-182">Código de estado</span><span class="sxs-lookup"><span data-stu-id="ce62b-182">Status Code</span></span> |<span data-ttu-id="ce62b-183">int</span><span class="sxs-lookup"><span data-stu-id="ce62b-183">int</span></span> |<span data-ttu-id="ce62b-184">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="ce62b-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="ce62b-185">Autenticación</span><span class="sxs-lookup"><span data-stu-id="ce62b-185">Authentication</span></span>
<span data-ttu-id="ce62b-186">Logic Apps permite utilizar diferentes tipos de autenticación en los puntos de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="ce62b-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="ce62b-187">Esta autenticación se puede usar con los conectores **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)** y **[HTTP Webhook](connectors-native-webhook.md)**.</span><span class="sxs-lookup"><span data-stu-id="ce62b-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="ce62b-188">Los siguientes tipos de autenticación pueden configurarse:</span><span class="sxs-lookup"><span data-stu-id="ce62b-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="ce62b-189">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="ce62b-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="ce62b-190">Autenticación de certificados de clientes</span><span class="sxs-lookup"><span data-stu-id="ce62b-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="ce62b-191">Autenticación de OAuth de Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="ce62b-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="ce62b-192">Autenticación básica</span><span class="sxs-lookup"><span data-stu-id="ce62b-192">Basic authentication</span></span>

<span data-ttu-id="ce62b-193">Se requiere el siguiente objeto de autenticación para la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="ce62b-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="ce62b-194">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="ce62b-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="ce62b-195">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="ce62b-195">Property name</span></span> | <span data-ttu-id="ce62b-196">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="ce62b-196">Data type</span></span> | <span data-ttu-id="ce62b-197">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce62b-198">Type*</span><span class="sxs-lookup"><span data-stu-id="ce62b-198">Type*</span></span> |<span data-ttu-id="ce62b-199">type</span><span class="sxs-lookup"><span data-stu-id="ce62b-199">type</span></span> |<span data-ttu-id="ce62b-200">Tipo de autenticación (debe ser `Basic` para la autenticación básica)</span><span class="sxs-lookup"><span data-stu-id="ce62b-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="ce62b-201">Username*</span><span class="sxs-lookup"><span data-stu-id="ce62b-201">Username*</span></span> |<span data-ttu-id="ce62b-202">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="ce62b-202">username</span></span> |<span data-ttu-id="ce62b-203">Nombre de usuario que se va a autenticar</span><span class="sxs-lookup"><span data-stu-id="ce62b-203">User name to authenticate</span></span> |
| <span data-ttu-id="ce62b-204">Password*</span><span class="sxs-lookup"><span data-stu-id="ce62b-204">Password*</span></span> |<span data-ttu-id="ce62b-205">contraseña</span><span class="sxs-lookup"><span data-stu-id="ce62b-205">password</span></span> |<span data-ttu-id="ce62b-206">Contraseña para autenticar.</span><span class="sxs-lookup"><span data-stu-id="ce62b-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="ce62b-207">Si quiere usar una contraseña que no se pueda recuperar de la definición, use un parámetro `securestring` y la  
> [función de definición de flujo de trabajo](http://aka.ms/logicappdocs) `@parameters()`.</span><span class="sxs-lookup"><span data-stu-id="ce62b-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="ce62b-208">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce62b-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="ce62b-209">Autenticación de certificados de clientes</span><span class="sxs-lookup"><span data-stu-id="ce62b-209">Client certificate authentication</span></span>

<span data-ttu-id="ce62b-210">Se requiere el siguiente objeto de autenticación para la autenticación de certificados de clientes.</span><span class="sxs-lookup"><span data-stu-id="ce62b-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="ce62b-211">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="ce62b-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="ce62b-212">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="ce62b-212">Property name</span></span> | <span data-ttu-id="ce62b-213">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="ce62b-213">Data type</span></span> | <span data-ttu-id="ce62b-214">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce62b-215">Type*</span><span class="sxs-lookup"><span data-stu-id="ce62b-215">Type*</span></span> |<span data-ttu-id="ce62b-216">type</span><span class="sxs-lookup"><span data-stu-id="ce62b-216">type</span></span> |<span data-ttu-id="ce62b-217">El tipo de autenticación (debe ser `ClientCertificate` para los certificados de cliente SSL)</span><span class="sxs-lookup"><span data-stu-id="ce62b-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="ce62b-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="ce62b-218">PFX*</span></span> |<span data-ttu-id="ce62b-219">pfx</span><span class="sxs-lookup"><span data-stu-id="ce62b-219">pfx</span></span> |<span data-ttu-id="ce62b-220">El contenido codificado en base 64 del archivo de intercambio de información personal (PFX)</span><span class="sxs-lookup"><span data-stu-id="ce62b-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="ce62b-221">Password*</span><span class="sxs-lookup"><span data-stu-id="ce62b-221">Password*</span></span> |<span data-ttu-id="ce62b-222">contraseña</span><span class="sxs-lookup"><span data-stu-id="ce62b-222">password</span></span> |<span data-ttu-id="ce62b-223">La contraseña para acceder al archivo PFX</span><span class="sxs-lookup"><span data-stu-id="ce62b-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="ce62b-224">Para usar un parámetro que no se pueda leer en la definición después de guardar la aplicación lógica puede usar un parámetro `securestring` y la  
> [función de definición de flujo de trabajo](http://aka.ms/logicappdocs) `@parameters()`.</span><span class="sxs-lookup"><span data-stu-id="ce62b-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="ce62b-225">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce62b-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="ce62b-226">Autenticación de OAuth de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce62b-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="ce62b-227">Se requiere el siguiente objeto de autenticación para la autenticación de OAuth de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce62b-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="ce62b-228">Un * significa que es un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="ce62b-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="ce62b-229">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="ce62b-229">Property name</span></span> | <span data-ttu-id="ce62b-230">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="ce62b-230">Data type</span></span> | <span data-ttu-id="ce62b-231">Description</span><span class="sxs-lookup"><span data-stu-id="ce62b-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce62b-232">Type*</span><span class="sxs-lookup"><span data-stu-id="ce62b-232">Type*</span></span> |<span data-ttu-id="ce62b-233">type</span><span class="sxs-lookup"><span data-stu-id="ce62b-233">type</span></span> |<span data-ttu-id="ce62b-234">El tipo de autenticación (debe ser `ActiveDirectoryOAuth` para la autenticación de OAuth de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="ce62b-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="ce62b-235">Tenant*</span><span class="sxs-lookup"><span data-stu-id="ce62b-235">Tenant*</span></span> |<span data-ttu-id="ce62b-236">tenant</span><span class="sxs-lookup"><span data-stu-id="ce62b-236">tenant</span></span> |<span data-ttu-id="ce62b-237">Identificador del inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce62b-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="ce62b-238">Audience*</span><span class="sxs-lookup"><span data-stu-id="ce62b-238">Audience*</span></span> |<span data-ttu-id="ce62b-239">audience</span><span class="sxs-lookup"><span data-stu-id="ce62b-239">audience</span></span> |<span data-ttu-id="ce62b-240">Recurso para cuyo uso solicita autorización.</span><span class="sxs-lookup"><span data-stu-id="ce62b-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="ce62b-241">Por ejemplo: `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="ce62b-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="ce62b-242">Client ID*</span><span class="sxs-lookup"><span data-stu-id="ce62b-242">Client ID*</span></span> |<span data-ttu-id="ce62b-243">clientId</span><span class="sxs-lookup"><span data-stu-id="ce62b-243">clientId</span></span> |<span data-ttu-id="ce62b-244">Identificador de cliente para la aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce62b-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="ce62b-245">Secret*</span><span class="sxs-lookup"><span data-stu-id="ce62b-245">Secret*</span></span> |<span data-ttu-id="ce62b-246">secret</span><span class="sxs-lookup"><span data-stu-id="ce62b-246">secret</span></span> |<span data-ttu-id="ce62b-247">El secreto del cliente que solicita el token</span><span class="sxs-lookup"><span data-stu-id="ce62b-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="ce62b-248">Puede usar un parámetro `securestring` y la [función de definición de flujo de trabajo](http://aka.ms/logicappdocs) `@parameters()` para usar un parámetro que no se pueda leer en la definición después de guardarse.</span><span class="sxs-lookup"><span data-stu-id="ce62b-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="ce62b-249">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ce62b-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="ce62b-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce62b-250">Next steps</span></span>
<span data-ttu-id="ce62b-251">Ahora, pruebe la plataforma y [cree una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ce62b-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ce62b-252">Puede explorar los demás conectores disponibles en Logic Apps consultando nuestra [lista de API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ce62b-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

