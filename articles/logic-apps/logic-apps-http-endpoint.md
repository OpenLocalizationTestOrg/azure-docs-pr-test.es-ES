---
title: "Llamada, desencadenamiento o anidamiento de flujos de trabajo con puntos de conexión HTTP: Azure Logic Apps | Microsoft Docs"
description: "Configuración de puntos de conexión HTTP para llamadas, desencadenamientos o anidamiento de flujos de trabajo para Azure Logic Apps"
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
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="a5cfc-104">Llamada, desencadenamiento o anidamiento de flujos de trabajo con puntos de conexión HTTP en aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="a5cfc-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="a5cfc-105">Puede exponer de manera nativa puntos de conexión HTTP sincrónicos como desencadenadores en aplicaciones lógicas, de manera que pueda desencadenar las aplicaciones lógicas o llamarlas a través de una dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="a5cfc-106">También puede anidar flujos de trabajo en las aplicaciones lógicas mediante el uso de un patrón de puntos de conexión invocables.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="a5cfc-107">Para crear puntos de conexión HTTP, puede agregar estos desencadenadores para que las aplicaciones lógicas puedan recibir solicitudes entrantes:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="a5cfc-108">Solicitud</span><span class="sxs-lookup"><span data-stu-id="a5cfc-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="a5cfc-109">Webhook de conexión de API</span><span class="sxs-lookup"><span data-stu-id="a5cfc-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="a5cfc-110">Webhook HTTP</span><span class="sxs-lookup"><span data-stu-id="a5cfc-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="a5cfc-111">Aunque en los ejemplos se usa el desencadenador **Request**, puede usar cualquiera de los desencadenadores HTTP indicados, y todos los principios se aplican exactamente igual a los otros tipos de desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="a5cfc-112">Configuración de un punto de conexión HTTP para la aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="a5cfc-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="a5cfc-113">Para crear un punto de conexión HTTP, agregue un desencadenador que pueda recibir solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="a5cfc-114">Inicie sesión en [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="a5cfc-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="a5cfc-115">Vaya a la aplicación lógica y abra el Diseñador de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="a5cfc-116">Agregue un desencadenador que permita a la aplicación lógica recibir solicitudes entrantes.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="a5cfc-117">Por ejemplo, agregue el desencadenador de tipo **Solicitud** a su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="a5cfc-118">En **Esquema JSON de cuerpo de solicitud**, tiene la opción de escribir un esquema JSON para la carga (datos) que espera que desencadenador reciba.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="a5cfc-119">El diseñador usa este esquema para generar tokens que la aplicación lógica puede usar para consumir, analizar y pasar datos del desencadenador a través del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="a5cfc-120">Obtenga más información sobre [tokens generados a partir de esquemas JSON](#generated-tokens).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="a5cfc-121">En este ejemplo, escriba el esquema que se muestra en el diseñador:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-121">For this example, enter the schema shown in the designer:</span></span>

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

    ![Agregar la acción de solicitud][1]

    > [!TIP]
    > 
    > <span data-ttu-id="a5cfc-123">Puede generar un esquema para una carga JSON de ejemplo desde una herramienta como [jsonschema.net](http://jsonschema.net/), o bien en el desencadenador **Request** con la selección de **Usar una carga de ejemplo para generar el esquema**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="a5cfc-124">Escriba la carga de ejemplo y elija **Listo**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="a5cfc-125">Por ejemplo, esta carga de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="a5cfc-126">genera este esquema:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="a5cfc-127">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-127">Save your logic app.</span></span> <span data-ttu-id="a5cfc-128">En **HTTP POST a esta dirección URL**, ahora debería encontrar una dirección URL de devolución de llamadas generada, al igual que en este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![Dirección URL de devolución de llamadas generada para el punto de conexión](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="a5cfc-130">Esta dirección URL contiene una clave SAS (Firma de acceso compartido) en los parámetros de consulta usados para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="a5cfc-131">También puede obtener la dirección URL del punto de conexión HTTP en la información general sobre la aplicación lógica en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="a5cfc-132">En **Historial de desencadenadores**, seleccione el desencadenador:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obtención de la dirección URL del punto de conexión HTTP en Azure Portal][2]

    <span data-ttu-id="a5cfc-134">También puede obtener la dirección URL mediante la realización de esta llamada:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="a5cfc-135">Cambiar el método HTTP para el desencadenador</span><span class="sxs-lookup"><span data-stu-id="a5cfc-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="a5cfc-136">De forma predeterminada, el desencadenaador **Request** espera una solicitud POST de HTTP, pero puede usar un método HTTP diferente.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="a5cfc-137">Puede especificar solo un tipo de método.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="a5cfc-138">En el desencadenador **Request**, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="a5cfc-139">Abra la lista **Método**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-139">Open the **Method** list.</span></span> <span data-ttu-id="a5cfc-140">En este ejemplo, seleccione **GET** para que pueda probar la dirección URL del punto de conexión HTTP más adelante.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a5cfc-141">Puede seleccionar cualquier otro método HTTP, o bien especificar un método personalizado para su propia aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Cambio del método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="a5cfc-143">Aceptación de parámetros a través de la dirección URL del punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="a5cfc-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="a5cfc-144">Si desea que la dirección URL del punto de conexión HTTP acepte parámetros, personalice la ruta de acceso relativa del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="a5cfc-145">En el desencadenador **Request**, elija **Mostrar opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="a5cfc-146">En **Método**, especifique el método HTTP que desea que la solicitud use.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="a5cfc-147">En este ejemplo, seleccione el método **GET**, si no lo ha hecho ya, para que pueda probar la dirección URL del punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="a5cfc-148">Cuando se especifica una ruta de acceso relativa para el desencadenador, también debe especificar explícitamente un método HTTP para el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="a5cfc-149">En **Ruta de acceso relativa**, especifique la ruta de acceso relativa del parámetro que la dirección URL debe aceptar, por ejemplo, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Definición del método HTTP y de la ruta de acceso relativa del parámetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="a5cfc-151">Para usar el parámetro, agregue una acción **Respuesta** a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="a5cfc-152">(En el desencadenador, elija **Nuevo paso** > **Agregar una acción** > **Respuesta**).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="a5cfc-153">En el **Cuerpo** de la respuesta, incluya el token para el parámetro especificado en la ruta de acceso relativa del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="a5cfc-154">Por ejemplo, para devolver `Hello {customerID}`, actualice el **cuerpo** de la respuesta con `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="a5cfc-155">Debe aparecer la lista de contenido dinámica y se muestran los `customerID` token para que pueda seleccionar.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Adición del parámetro al cuerpo de respuesta](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="a5cfc-157">El **cuerpo** debería presentar un aspecto similar al de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-157">Your **Body** should look like this example:</span></span>

    ![Cuerpo de respuesta con el parámetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="a5cfc-159">Guarde la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-159">Save your logic app.</span></span> 

    <span data-ttu-id="a5cfc-160">La dirección URL del punto de conexión HTTP ahora incluye la ruta de acceso relativa, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="a5cfc-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="a5cfc-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="a5cfc-162">Para probar el punto de conexión HTTP, copie y pegue la dirección URL actualizada en otra ventana del explorador, pero reemplace `{customerID}` con `123456`, y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="a5cfc-163">El explorador debe mostrar este texto:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="a5cfc-164">Tokens generados a partir de esquemas JSON para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="a5cfc-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="a5cfc-165">Cuando se proporciona un esquema JSON en el desencadenador **Request**, el Diseñador de aplicación lógica genera tokens para las propiedades de dicho esquema.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="a5cfc-166">Después puede usar esos tokens para pasar datos a través del flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="a5cfc-167">En este ejemplo, si agrega las propiedades `title` y `name` al esquema JSON, sus tokens ahora están disponibles para usarlos en pasos posteriores del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="a5cfc-168">Este es el esquema JSON completo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-168">Here is the complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="a5cfc-169">Creación de flujos de trabajo anidados para aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="a5cfc-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="a5cfc-170">Puede anidar los flujos de trabajo en la aplicación lógica mediante la adición de otras aplicaciones de lógica que pueden recibir solicitudes.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="a5cfc-171">Para incluir estas aplicaciones lógicas, agregue la acción **Azure Logic Apps - Elegir un flujo de trabajo de Logic Apps** al desencadenador.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="a5cfc-172">A continuación, puede seleccionar desde las aplicaciones lógicas elegibles.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-172">You can then select from eligible logic apps.</span></span>

![Adición de otra aplicación lógica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="a5cfc-174">Llamada o desencadenamiento de aplicaciones lógicas a través de puntos de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="a5cfc-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="a5cfc-175">Una vez que haya creado el punto de conexión HTTP, puede desencadenar la aplicación lógica mediante un método `POST` a la dirección URL completa.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="a5cfc-176">Las aplicaciones lógicas tienen compatibilidad integrada para los puntos de conexión de acceso directo.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="a5cfc-177">Referencia al contenido de una solicitud entrante</span><span class="sxs-lookup"><span data-stu-id="a5cfc-177">Reference content from an incoming request</span></span>

<span data-ttu-id="a5cfc-178">Si el tipo de contenido es `application/json`, puede hacer referencia a las propiedades desde la solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="a5cfc-179">En caso contrario, el contenido se trata como una sola unidad binaria que se puede pasar a otras API.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="a5cfc-180">Para hacer referencia a este contenido dentro del flujo de trabajo, debe convertir ese contenido.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="a5cfc-181">Por ejemplo, si pasa contenido de `application/xml`, puede usar `@xpath()` para una extracción de XPath, o bien `@json()` para convertir de XML a JSON.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="a5cfc-182">Obtenga información sobre cómo [trabajar con tipos de contenido](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="a5cfc-183">Para obtener la salida de una solicitud entrante, puede usar la función `@triggerOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="a5cfc-184">La salida podría parecerse a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-184">The output might look like this example:</span></span>

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

<span data-ttu-id="a5cfc-185">Para tener acceso a la propiedad `body` de manera específica, puede usar el acceso directo `@triggerBody()`.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="a5cfc-186">Respuesta a solicitudes</span><span class="sxs-lookup"><span data-stu-id="a5cfc-186">Respond to requests</span></span>

<span data-ttu-id="a5cfc-187">Es posible que quiera responder a determinadas solicitudes que inician una aplicación lógica mediante la devolución de contenido al autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="a5cfc-188">Para construir el código de estado, el encabezado y el cuerpo de la respuesta, puede usar la acción **Respuesta**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="a5cfc-189">Esta acción puede aparecer en cualquier lugar de la aplicación lógica, no solo al final del flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="a5cfc-190">Si la aplicación lógica no incluye una **Respuesta**, el punto de conexión HTTP responde *inmediatamente* con un estado **202 - Aceptado**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="a5cfc-191">Además, para que la solicitud original obtenga la respuesta, todos los pasos necesarios para la respuesta deben terminar dentro del [límite del tiempo de espera de la solicitud](./logic-apps-limits-and-config.md), a menos que llame al flujo de trabajo como una aplicación lógica anidada.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="a5cfc-192">Si no se obtiene ninguna respuesta dentro de este límite, la solicitud entrante agota el tiempo de espera y recibe una respuesta HTTP **408 - Tiempo de espera del cliente agotado**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="a5cfc-193">En cuanto a las aplicaciones lógicas anidadas, la aplicación lógica principal seguirá esperando una respuesta hasta que finalice, independientemente del tiempo que se necesite.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="a5cfc-194">Construcción de la respuesta</span><span class="sxs-lookup"><span data-stu-id="a5cfc-194">Construct the response</span></span>

<span data-ttu-id="a5cfc-195">Puede incluir más de un encabezado y cualquier tipo de contenido en el cuerpo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="a5cfc-196">En la respuesta de ejemplo, el encabezado especifica que la respuesta tiene el tipo de contenido `application/json`.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="a5cfc-197">y el cuerpo contiene `title` y `name`, según el esquema JSON actualizado anteriormente para el desencadenador **Request**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![Acción de respuesta HTTP][3]

<span data-ttu-id="a5cfc-199">Las respuestas tienen estas propiedades:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-199">Responses have these properties:</span></span>

| <span data-ttu-id="a5cfc-200">Propiedad</span><span class="sxs-lookup"><span data-stu-id="a5cfc-200">Property</span></span> | <span data-ttu-id="a5cfc-201">Description</span><span class="sxs-lookup"><span data-stu-id="a5cfc-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5cfc-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="a5cfc-202">statusCode</span></span> |<span data-ttu-id="a5cfc-203">Especifica el código de estado HTTP para responder a la solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="a5cfc-204">Este código puede ser cualquier código de estado válido que comience con 2xx, 4xx o 5xx.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="a5cfc-205">En cambio, no se permiten códigos de estado 3xx.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="a5cfc-206">encabezados</span><span class="sxs-lookup"><span data-stu-id="a5cfc-206">headers</span></span> |<span data-ttu-id="a5cfc-207">Define cualquier número de encabezados para incluirse en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="a5cfc-208">body</span><span class="sxs-lookup"><span data-stu-id="a5cfc-208">body</span></span> |<span data-ttu-id="a5cfc-209">Especifica un objeto de cuerpo que puede ser una cadena, un objeto JSON o incluso contenido binario al que se hace referencia desde un paso anterior.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="a5cfc-210">A continuación se presenta el aspecto del esquema JSON ahora para la acción **Response**:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

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
> <span data-ttu-id="a5cfc-211">Para ver la definición de JSON completa de la aplicación lógica, en el Diseñador de aplicación lógica, elija **Vista Código**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="a5cfc-212">Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="a5cfc-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="a5cfc-213">P: ¿¿Qué se puede decir sobre la seguridad de las direcciones URL?</span><span class="sxs-lookup"><span data-stu-id="a5cfc-213">Q: What about URL security?</span></span>

<span data-ttu-id="a5cfc-214">R: Azure genera direcciones URL de devolución de llamada de la aplicación lógica de manera segura con una firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="a5cfc-215">Esta firma pasa como un parámetro de consulta y debe validarse antes de que se pueda activar la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="a5cfc-216">Azure genera la firma mediante una combinación única de una clave secreta por aplicación lógica, el nombre del desencadenador y la operación que se realiza.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="a5cfc-217">Por tanto, a menos que alguien tenga acceso a la clave de aplicación lógica secreta, no se puede generar una firma válida.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a5cfc-218">Para sistemas seguros y de producción, no se recomienda que llame a su aplicación lógica directamente desde el explorador por los siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="a5cfc-219">La clave de acceso compartido aparece en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="a5cfc-220">No puede administrar las directivas de contenido seguro debido a los dominios compartidos entre los clientes de Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="a5cfc-221">P: ¿Puedo configurar más puntos de conexión HTTP?</span><span class="sxs-lookup"><span data-stu-id="a5cfc-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="a5cfc-222">R: Sí, los puntos de conexión HTTP admiten una configuración más avanzada a través de [**API Management**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="a5cfc-223">Este servicio también ofrece la funcionalidad de administrar de forma coherente todas las API, incluidas las aplicaciones lógicas, configurar nombres de dominio personalizados, usar varios métodos de autenticación y muchas más, como, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="a5cfc-224">Cambio del método de solicitud</span><span class="sxs-lookup"><span data-stu-id="a5cfc-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="a5cfc-225">Cambio de los segmentos de dirección URL de la solicitud</span><span class="sxs-lookup"><span data-stu-id="a5cfc-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="a5cfc-226">Configuración de los dominios de API Management en [Azure Portal](https://portal.azure.com/ "Azure Portal")</span><span class="sxs-lookup"><span data-stu-id="a5cfc-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="a5cfc-227">Configuración de la directiva para comprobar la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="a5cfc-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="a5cfc-228">P: ¿Qué ha cambiado cuando se migró el esquema desde la versión preliminar de 1 de diciembre de 2014?</span><span class="sxs-lookup"><span data-stu-id="a5cfc-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="a5cfc-229">R: Este es un resumen sobre estos cambios:</span><span class="sxs-lookup"><span data-stu-id="a5cfc-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="a5cfc-230">Versión preliminar de 1 de diciembre de 2014</span><span class="sxs-lookup"><span data-stu-id="a5cfc-230">December 1, 2014 preview</span></span> | <span data-ttu-id="a5cfc-231">1 de junio de 2016</span><span class="sxs-lookup"><span data-stu-id="a5cfc-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="a5cfc-232">Haga clic en la aplicación de API **Agente de escucha HTTP**.</span><span class="sxs-lookup"><span data-stu-id="a5cfc-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="a5cfc-233">Haga clic en **Desencadenador manual** (no se necesita ninguna aplicación de API).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="a5cfc-234">Configuración del Agente de escucha HTTP "*Enviar respuesta automáticamente*"</span><span class="sxs-lookup"><span data-stu-id="a5cfc-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="a5cfc-235">Tanto si incluye una acción de **Respuesta** en la definición del flujo de trabajo como si no</span><span class="sxs-lookup"><span data-stu-id="a5cfc-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="a5cfc-236">Configuración de la autenticación básica o OAuth</span><span class="sxs-lookup"><span data-stu-id="a5cfc-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="a5cfc-237">mediante API Management</span><span class="sxs-lookup"><span data-stu-id="a5cfc-237">via API Management</span></span> |
| <span data-ttu-id="a5cfc-238">Configuración del método HTTP</span><span class="sxs-lookup"><span data-stu-id="a5cfc-238">Configure HTTP method</span></span> |<span data-ttu-id="a5cfc-239">En **Mostrar opciones avanzadas**, elija un método HTTP</span><span class="sxs-lookup"><span data-stu-id="a5cfc-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="a5cfc-240">Configuración de la ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="a5cfc-240">Configure relative path</span></span> |<span data-ttu-id="a5cfc-241">En **Mostrar opciones avanzadas**, agregue una ruta de acceso relativa</span><span class="sxs-lookup"><span data-stu-id="a5cfc-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="a5cfc-242">Referencia al cuerpo entrante mediante `@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="a5cfc-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="a5cfc-243">Referencia a través de `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="a5cfc-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="a5cfc-244">**Enviar respuesta HTTP** del Agente de escucha HTTP</span><span class="sxs-lookup"><span data-stu-id="a5cfc-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="a5cfc-245">Haga clic en **Responder a la solicitud HTTP** (no se necesita ninguna aplicación de API)</span><span class="sxs-lookup"><span data-stu-id="a5cfc-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="a5cfc-246">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="a5cfc-246">Get help</span></span>

<span data-ttu-id="a5cfc-247">Para formular preguntas, o responderlas, y saber lo que hacen otros usuarios de Azure Logic Apps, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="a5cfc-248">Para ayudar a mejorar Azure Logic Apps y los conectores, vote o envíe ideas en el [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a5cfc-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5cfc-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5cfc-249">Next steps</span></span>

* [<span data-ttu-id="a5cfc-250">Creación de definiciones de aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="a5cfc-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="a5cfc-251">Control de errores y excepciones</span><span class="sxs-lookup"><span data-stu-id="a5cfc-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
