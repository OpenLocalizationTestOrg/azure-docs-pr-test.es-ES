---
title: "aaaCall, desencadenador o anidar flujos de trabajo con puntos de conexión HTTP - Azure Logic Apps | Documentos de Microsoft"
description: "Configurar toocall de extremos HTTP, desencadenador o flujos de trabajo de anidamiento para las aplicaciones lógicas de Azure"
services: logic-apps
keywords: "flujos de trabajo, puntos de conexión HTTP"
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="64e42-104">Llamada, desencadenamiento o anidamiento de flujos de trabajo con puntos de conexión HTTP en aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="64e42-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="64e42-105">Puede exponer de manera nativa puntos de conexión HTTP sincrónicos como desencadenadores en aplicaciones lógicas, de manera que pueda desencadenar las aplicaciones lógicas o llamarlas a través de una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="64e42-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="64e42-106">También puede anidar flujos de trabajo en las aplicaciones lógicas mediante el uso de un patrón de puntos de conexión invocables.</span><span class="sxs-lookup"><span data-stu-id="64e42-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="64e42-107">toocreate puntos de conexión HTTP, puede agregar estos desencadenadores para que las aplicaciones lógicas puedan recibir las solicitudes entrantes:</span><span class="sxs-lookup"><span data-stu-id="64e42-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="64e42-108">Solicitud</span><span class="sxs-lookup"><span data-stu-id="64e42-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="64e42-109">Webhook de conexión de API</span><span class="sxs-lookup"><span data-stu-id="64e42-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="64e42-110">Webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="64e42-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="64e42-111">Aunque nuestros ejemplos utilizan hello **solicitar** desencadenador, puede usar cualquiera de hello aparece desencadenadores HTTP, y todos los principios aplican exactamente igual toohello otros tipos de desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="64e42-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="64e42-112">Configuración de un punto de conexión HTTP para la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="64e42-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="64e42-113">toocreate un extremo HTTP, agregue un desencadenador que puede recibir las solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="64e42-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="64e42-114">Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="64e42-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="64e42-115">Vaya tooyour lógica aplicación y abra el Diseñador de lógica de aplicación.</span><span class="sxs-lookup"><span data-stu-id="64e42-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="64e42-116">Agregue un desencadenador que permita a la aplicación lógica recibir solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="64e42-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="64e42-117">Por ejemplo, agregar hello **solicitar** aplicación lógica de desencadenador tooyour.</span><span class="sxs-lookup"><span data-stu-id="64e42-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="64e42-118">En **esquema de JSON de cuerpo de solicitud**, opcionalmente, puede escribir un esquema JSON para carga hello (datos) que espera Hola desencadenador tooreceive.</span><span class="sxs-lookup"><span data-stu-id="64e42-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="64e42-119">Diseñador de Hello utiliza este esquema para generar tokens que puede usar la aplicación lógica tooconsume, análisis y pasar datos del desencadenador de Hola a través de su flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="64e42-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="64e42-120">Obtenga más información sobre [tokens generados a partir de esquemas JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="64e42-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="64e42-121">En este ejemplo, escriba esquema Hola que se muestra en el Diseñador de hello:</span><span class="sxs-lookup"><span data-stu-id="64e42-121">For this example, enter hello schema shown in hello designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Agregar acción de solicitud de Hola][1]

    > [!TIP]
    > 
    > <span data-ttu-id="64e42-123">Puede generar un esquema para una carga JSON de ejemplo desde una herramienta como [jsonschema.net](http://jsonschema.net/), o en hello **solicitar** desencadenador eligiendo **esquema de uso ejemplo carga toogenerate**.</span><span class="sxs-lookup"><span data-stu-id="64e42-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="64e42-124">Escriba la carga de ejemplo y elija **Listo**.</span><span class="sxs-lookup"><span data-stu-id="64e42-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="64e42-125">Por ejemplo, esta carga de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64e42-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="64e42-126">genera este esquema:</span><span class="sxs-lookup"><span data-stu-id="64e42-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="64e42-127">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e42-127">Save your logic app.</span></span> <span data-ttu-id="64e42-128">En **dirección URL de HTTP POST toothis**, ahora debería encontrar una dirección URL de devolución de llamada generado, al igual que en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64e42-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Dirección URL de devolución de llamadas generada para el punto de conexión](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="64e42-130">Esta dirección URL contiene una clave de firma de acceso compartido (SAS) en los parámetros de consulta de Hola que se usan para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="64e42-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="64e42-131">También puede obtener dirección URL del extremo HTTP de saludo de la introducción de aplicación lógica Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="64e42-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="64e42-132">En **Historial de desencadenadores**, seleccione el desencadenador:</span><span class="sxs-lookup"><span data-stu-id="64e42-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obtención de la dirección URL del punto de conexión HTTP en Azure Portal][2]

    <span data-ttu-id="64e42-134">O bien, puede obtener dirección URL de hello mediante esta llamada:</span><span class="sxs-lookup"><span data-stu-id="64e42-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="64e42-135">Cambiar el método HTTP de hello para el desencadenador</span><span class="sxs-lookup"><span data-stu-id="64e42-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="64e42-136">De forma predeterminada, Hola **solicitud** desencadenador espera una solicitud POST de HTTP, pero puede usar un método HTTP diferente.</span><span class="sxs-lookup"><span data-stu-id="64e42-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="64e42-137">Puede especificar solo un tipo de método.</span><span class="sxs-lookup"><span data-stu-id="64e42-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="64e42-138">En el desencadenador **Request**, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="64e42-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="64e42-139">Abra hello **método** lista.</span><span class="sxs-lookup"><span data-stu-id="64e42-139">Open hello **Method** list.</span></span> <span data-ttu-id="64e42-140">En este ejemplo, seleccione **GET** para que pueda probar la dirección URL del punto de conexión HTTP más adelante.</span><span class="sxs-lookup"><span data-stu-id="64e42-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="64e42-141">Puede seleccionar cualquier otro método HTTP, o bien especificar un método personalizado para su propia aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e42-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Cambio del método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="64e42-143">Aceptación de parámetros a través de la dirección URL del punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="64e42-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="64e42-144">Si desea que los parámetros de tooaccept de dirección URL de extremo HTTP, personalizar la ruta de acceso relativa del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="64e42-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="64e42-145">En el desencadenador **Request**, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="64e42-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="64e42-146">En **método**, especificar método hello HTTP que desea que su toouse de solicitud.</span><span class="sxs-lookup"><span data-stu-id="64e42-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="64e42-147">En este ejemplo, seleccione hello **obtener** método, si no lo ha hecho ya, para que pueda probar la dirección URL de su extremo HTTP.</span><span class="sxs-lookup"><span data-stu-id="64e42-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="64e42-148">Cuando se especifica una ruta de acceso relativa para el desencadenador, también debe especificar explícitamente un método HTTP para el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="64e42-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="64e42-149">En **ruta_relativa**, especifique la ruta de acceso relativa de hello para el parámetro hello que debe aceptar la dirección URL, por ejemplo, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="64e42-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Especifique el método HTTP de hello y ruta de acceso relativa para el parámetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="64e42-151">toouse Hola parámetro, agregue un **respuesta** aplicación lógica de acción tooyour.</span><span class="sxs-lookup"><span data-stu-id="64e42-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="64e42-152">(En el desencadenador, elija **Nuevo paso** > **Agregar una acción** > **Respuesta**).</span><span class="sxs-lookup"><span data-stu-id="64e42-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="64e42-153">En su respuesta **cuerpo**, incluye el token de hello para el parámetro hello que especificó en la ruta de acceso relativa del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="64e42-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="64e42-154">Por ejemplo, tooreturn `Hello {customerID}`, la respuesta de actualización de **cuerpo** con `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="64e42-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="64e42-155">lista de contenido dinámico de Hello debe aparecer y mostrar hello `customerID` tooselect, símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="64e42-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Agregar parámetro tooresponse cuerpo](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="64e42-157">El **cuerpo** debería presentar un aspecto similar al de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64e42-157">Your **Body** should look like this example:</span></span>

    ![Cuerpo de respuesta con el parámetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="64e42-159">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e42-159">Save your logic app.</span></span> 

    <span data-ttu-id="64e42-160">La dirección URL del extremo HTTP ahora incluye ruta de acceso relativa de hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64e42-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="64e42-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="64e42-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="64e42-162">tootest su extremo HTTP, copiar y pegar Hola [URL actualizada en otra ventana del explorador, pero reemplacen `{customerID}` con `123456`, y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="64e42-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="64e42-163">El explorador debe mostrar este texto:</span><span class="sxs-lookup"><span data-stu-id="64e42-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="64e42-164">Tokens generados a partir de esquemas JSON para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="64e42-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="64e42-165">Cuando se proporciona un esquema JSON en su **solicitar** desencadenar, hello lógica de aplicación diseñador genera tokens para las propiedades de dicho esquema.</span><span class="sxs-lookup"><span data-stu-id="64e42-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="64e42-166">Después puede usar esos tokens para pasar datos a través del flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e42-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="64e42-167">En este ejemplo, si agrega hello `title` y `name` esquema de propiedades tooyour JSON, sus tokens están ahora disponible toouse en pasos posteriores de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="64e42-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="64e42-168">Este es el esquema JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="64e42-168">Here is hello complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="64e42-169">Creación de flujos de trabajo anidados para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="64e42-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="64e42-170">Puede anidar los flujos de trabajo en la aplicación lógica mediante la adición de otras aplicaciones de lógica que pueden recibir solicitudes.</span><span class="sxs-lookup"><span data-stu-id="64e42-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="64e42-171">tooinclude estas aplicaciones lógicas, agregar hello **Azure Logic Apps - elegir un flujo de trabajo de las aplicaciones lógicas** desencadenador tooyour de acción.</span><span class="sxs-lookup"><span data-stu-id="64e42-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="64e42-172">A continuación, puede seleccionar desde las aplicaciones lógicas elegibles.</span><span class="sxs-lookup"><span data-stu-id="64e42-172">You can then select from eligible logic apps.</span></span>

![Adición de otra aplicación lógica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="64e42-174">Llamada o desencadenamiento de aplicaciones lógicas a través de puntos de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="64e42-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="64e42-175">Después de crear el punto de conexión HTTP, puede desencadenar la aplicación lógica a través de un `POST` dirección URL completa del método toohello.</span><span class="sxs-lookup"><span data-stu-id="64e42-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="64e42-176">Las aplicaciones lógicas tienen compatibilidad integrada para los puntos de conexión de acceso directo.</span><span class="sxs-lookup"><span data-stu-id="64e42-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="64e42-177">Referencia al contenido de una solicitud entrante</span><span class="sxs-lookup"><span data-stu-id="64e42-177">Reference content from an incoming request</span></span>

<span data-ttu-id="64e42-178">Si Hola contenido del tipo es `application/json`, puede hacer referencia a propiedades de solicitud entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e42-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="64e42-179">En caso contrario, contenido se trata como una sola unidad binaria que se puede pasar tooother API.</span><span class="sxs-lookup"><span data-stu-id="64e42-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="64e42-180">tooreference este contenido dentro de flujo de trabajo de hello, debe convertir el contenido.</span><span class="sxs-lookup"><span data-stu-id="64e42-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="64e42-181">Por ejemplo, si se pasa `application/xml` contenido, puede usar `@xpath()` para una extracción de XPath, o `@json()` para convertir XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="64e42-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="64e42-182">Obtenga información sobre cómo [trabajar con tipos de contenido](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="64e42-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="64e42-183">Hola tooget de salida de una solicitud entrante, puede usar hello `@triggerOutputs()` función.</span><span class="sxs-lookup"><span data-stu-id="64e42-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="64e42-184">salida de Hello podría ser similar a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64e42-184">hello output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="64e42-185">Hola tooaccess `body` propiedad concreto, puede usar hello `@triggerBody()` acceso directo.</span><span class="sxs-lookup"><span data-stu-id="64e42-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="64e42-186">Responder toorequests</span><span class="sxs-lookup"><span data-stu-id="64e42-186">Respond toorequests</span></span>

<span data-ttu-id="64e42-187">Puede ser conveniente toorespond toocertain solicitudes que iniciar una aplicación lógica mediante la devolución de llamada toohello contenido.</span><span class="sxs-lookup"><span data-stu-id="64e42-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="64e42-188">código de estado de hello tooconstruct, encabezado y cuerpo de la respuesta, puede usar hello **respuesta** acción.</span><span class="sxs-lookup"><span data-stu-id="64e42-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="64e42-189">Esta acción puede aparecer en cualquier lugar en la aplicación lógica, no solo al final de hello del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="64e42-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="64e42-190">Si no incluye la aplicación lógica un **respuesta**, punto de conexión de hello HTTP responde *inmediatamente* con un **202 Accepted** estado.</span><span class="sxs-lookup"><span data-stu-id="64e42-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="64e42-191">Además, para hello original tooget Hola solicitud-respuesta, todos los pasos necesarios para la respuesta de hello deben finalizar en hello [límite de tiempo de espera de solicitud](./logic-apps-limits-and-config.md) a menos que se llama a flujo de trabajo de hello como una aplicación de lógica anidados.</span><span class="sxs-lookup"><span data-stu-id="64e42-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="64e42-192">Si se produce ninguna respuesta dentro de este límite, solicitud entrante de hello tiempo de espera y recibe la respuesta HTTP de hello **408 tiempo de espera de cliente**.</span><span class="sxs-lookup"><span data-stu-id="64e42-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="64e42-193">Para las aplicaciones lógicas anidadas, aplicación de lógica de hello primario continúa toowait una respuesta hasta que se complete, independientemente de cuánto tiempo se necesita.</span><span class="sxs-lookup"><span data-stu-id="64e42-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="64e42-194">Respuesta de Hola de construcción</span><span class="sxs-lookup"><span data-stu-id="64e42-194">Construct hello response</span></span>

<span data-ttu-id="64e42-195">Puede incluir más de un encabezado y cualquier tipo de contenido en el cuerpo de la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e42-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="64e42-196">En la respuesta de ejemplo, el encabezado de hello especifica que respuesta hello tiene tipo de contenido `application/json`.</span><span class="sxs-lookup"><span data-stu-id="64e42-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="64e42-197">y contiene el cuerpo de hello `title` y `name`, según el esquema JSON de hello actualizada previamente para hello **solicitar** desencadenador.</span><span class="sxs-lookup"><span data-stu-id="64e42-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Acción de respuesta HTTP][3]

<span data-ttu-id="64e42-199">Las respuestas tienen estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="64e42-199">Responses have these properties:</span></span>

| <span data-ttu-id="64e42-200">Propiedad</span><span class="sxs-lookup"><span data-stu-id="64e42-200">Property</span></span> | <span data-ttu-id="64e42-201">Description</span><span class="sxs-lookup"><span data-stu-id="64e42-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64e42-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="64e42-202">statusCode</span></span> |<span data-ttu-id="64e42-203">Especifica el código de estado de hello HTTP para la solicitud entrante de toohello responde.</span><span class="sxs-lookup"><span data-stu-id="64e42-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="64e42-204">Este código puede ser cualquier código de estado válido que comience con 2xx, 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="64e42-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="64e42-205">En cambio, no se permiten códigos de estado 3xx.</span><span class="sxs-lookup"><span data-stu-id="64e42-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="64e42-206">encabezados</span><span class="sxs-lookup"><span data-stu-id="64e42-206">headers</span></span> |<span data-ttu-id="64e42-207">Define cualquier número de tooinclude de encabezados de respuesta Hola.</span><span class="sxs-lookup"><span data-stu-id="64e42-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="64e42-208">body</span><span class="sxs-lookup"><span data-stu-id="64e42-208">body</span></span> |<span data-ttu-id="64e42-209">Especifica un objeto de cuerpo que puede ser una cadena, un objeto JSON o incluso contenido binario al que se hace referencia desde un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="64e42-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="64e42-210">Aquí es lo que parece que ahora para Hola Hola el esquema JSON **respuesta** acción:</span><span class="sxs-lookup"><span data-stu-id="64e42-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="64e42-211">definición JSON tooview Hola completa para la aplicación lógica, en hello Diseñador de la lógica de aplicaciones, elija **vista código**.</span><span class="sxs-lookup"><span data-stu-id="64e42-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="64e42-212">Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="64e42-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="64e42-213">P: ¿¿Qué se puede decir sobre la seguridad de las direcciones URL?</span><span class="sxs-lookup"><span data-stu-id="64e42-213">Q: What about URL security?</span></span>

<span data-ttu-id="64e42-214">R: Azure genera direcciones URL de devolución de llamada de la aplicación lógica de manera segura con una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="64e42-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="64e42-215">Esta firma pasa como un parámetro de consulta y debe validarse antes de que se pueda activar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e42-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="64e42-216">Azure genera la firma de hello mediante una combinación única de una clave secreta por aplicación lógica, el nombre de desencadenador de Hola y operación de Hola que se lleva a cabo.</span><span class="sxs-lookup"><span data-stu-id="64e42-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="64e42-217">Por lo que, a menos que alguien tiene acceso toohello lógica secreto de aplicación clave, no pueden generar una firma válida.</span><span class="sxs-lookup"><span data-stu-id="64e42-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="64e42-218">Para producción y los sistemas seguros, se recomienda llamar a la aplicación lógica directamente desde el Explorador de hello porque:</span><span class="sxs-lookup"><span data-stu-id="64e42-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="64e42-219">clave de acceso compartido de Hello aparece en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="64e42-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="64e42-220">No se puede administrar directivas de contenido seguras debido tooshared dominios entre los clientes de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="64e42-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="64e42-221">P: ¿Puedo configurar más puntos de conexión HTTP?</span><span class="sxs-lookup"><span data-stu-id="64e42-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="64e42-222">R: Sí, los puntos de conexión HTTP admiten una configuración más avanzada a través de [**API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="64e42-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="64e42-223">Este servicio también ofrece la capacidad de Hola para tooconsistently administre todas las API, incluidas las aplicaciones de lógica, configure los nombres de dominio personalizado, usar varios métodos de autenticación etc., por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="64e42-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="64e42-224">Método de solicitud de cambio Hola</span><span class="sxs-lookup"><span data-stu-id="64e42-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="64e42-225">Cambie los segmentos de dirección URL de saludo de solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="64e42-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="64e42-226">Configurar los dominios de administración de API en hello [portal de Azure](https://portal.azure.com/ "portal de Azure")</span><span class="sxs-lookup"><span data-stu-id="64e42-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="64e42-227">Configurar la directiva toocheck para la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="64e42-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="64e42-228">P: ¿qué cambió cuando migra esquema Hola de vista previa de 1 de diciembre de 2014 de hello?</span><span class="sxs-lookup"><span data-stu-id="64e42-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="64e42-229">R: Este es un resumen sobre estos cambios:</span><span class="sxs-lookup"><span data-stu-id="64e42-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="64e42-230">Versión preliminar de 1 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="64e42-230">December 1, 2014 preview</span></span> | <span data-ttu-id="64e42-231">1 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="64e42-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="64e42-232">Haga clic en la aplicación de API **Agente de escucha HTTP**.</span><span class="sxs-lookup"><span data-stu-id="64e42-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="64e42-233">Haga clic en **Desencadenador manual** (no se necesita ninguna aplicación de API).</span><span class="sxs-lookup"><span data-stu-id="64e42-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="64e42-234">Configuración del Agente de escucha HTTP "*Enviar respuesta automáticamente*"</span><span class="sxs-lookup"><span data-stu-id="64e42-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="64e42-235">Tanto si incluye una **respuesta** acción o no en la definición de flujo de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="64e42-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="64e42-236">Configuración de la autenticación básica o OAuth</span><span class="sxs-lookup"><span data-stu-id="64e42-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="64e42-237">mediante API Management</span><span class="sxs-lookup"><span data-stu-id="64e42-237">via API Management</span></span> |
| <span data-ttu-id="64e42-238">Configuración del método HTTP</span><span class="sxs-lookup"><span data-stu-id="64e42-238">Configure HTTP method</span></span> |<span data-ttu-id="64e42-239">En **Mostrar opciones avanzadas**, elija un método HTTP</span><span class="sxs-lookup"><span data-stu-id="64e42-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="64e42-240">Configuración de la ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="64e42-240">Configure relative path</span></span> |<span data-ttu-id="64e42-241">En **Mostrar opciones avanzadas**, agregue una ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="64e42-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="64e42-242">Cuerpo de entrada de Hola de referencia a través de`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="64e42-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="64e42-243">Referencia a través de `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="64e42-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="64e42-244">**Enviar respuesta HTTP** acción en hello escucha HTTP</span><span class="sxs-lookup"><span data-stu-id="64e42-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="64e42-245">Haga clic en **responden tooHTTP solicitud** (se requiere ninguna API App)</span><span class="sxs-lookup"><span data-stu-id="64e42-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="64e42-246">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="64e42-246">Get help</span></span>

<span data-ttu-id="64e42-247">tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="64e42-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="64e42-248">toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="64e42-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="64e42-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64e42-249">Next steps</span></span>

* [<span data-ttu-id="64e42-250">Creación de definiciones de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="64e42-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="64e42-251">Control de errores y excepciones</span><span class="sxs-lookup"><span data-stu-id="64e42-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
