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
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a>Llamada, desencadenamiento o anidamiento de flujos de trabajo con puntos de conexión HTTP en aplicaciones lógicas

Puede exponer de manera nativa puntos de conexión HTTP sincrónicos como desencadenadores en aplicaciones lógicas, de manera que pueda desencadenar las aplicaciones lógicas o llamarlas a través de una dirección URL. También puede anidar flujos de trabajo en las aplicaciones lógicas mediante el uso de un patrón de puntos de conexión invocables.

toocreate puntos de conexión HTTP, puede agregar estos desencadenadores para que las aplicaciones lógicas puedan recibir las solicitudes entrantes:

* [Solicitud](../connectors/connectors-native-reqres.md)

* [Webhook de conexión de API](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [Webhook HTTP](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > Aunque nuestros ejemplos utilizan hello **solicitar** desencadenador, puede usar cualquiera de hello aparece desencadenadores HTTP, y todos los principios aplican exactamente igual toohello otros tipos de desencadenadores.

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a>Configuración de un punto de conexión HTTP para la aplicación lógica

toocreate un extremo HTTP, agregue un desencadenador que puede recibir las solicitudes entrantes.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure"). Vaya tooyour lógica aplicación y abra el Diseñador de lógica de aplicación.

2. Agregue un desencadenador que permita a la aplicación lógica recibir solicitudes entrantes. Por ejemplo, agregar hello **solicitar** aplicación lógica de desencadenador tooyour.

3.  En **esquema de JSON de cuerpo de solicitud**, opcionalmente, puede escribir un esquema JSON para carga hello (datos) que espera Hola desencadenador tooreceive.

    Diseñador de Hello utiliza este esquema para generar tokens que puede usar la aplicación lógica tooconsume, análisis y pasar datos del desencadenador de Hola a través de su flujo de trabajo. 
    Obtenga más información sobre [tokens generados a partir de esquemas JSON](#generated-tokens).

    En este ejemplo, escriba esquema Hola que se muestra en el Diseñador de hello:

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
    > Puede generar un esquema para una carga JSON de ejemplo desde una herramienta como [jsonschema.net](http://jsonschema.net/), o en hello **solicitar** desencadenador eligiendo **esquema de uso ejemplo carga toogenerate**. 
    > Escriba la carga de ejemplo y elija **Listo**.

    Por ejemplo, esta carga de ejemplo:

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    genera este esquema:

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

4.  Guarde la aplicación lógica. En **dirección URL de HTTP POST toothis**, ahora debería encontrar una dirección URL de devolución de llamada generado, al igual que en este ejemplo:

    ![Dirección URL de devolución de llamadas generada para el punto de conexión](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    Esta dirección URL contiene una clave de firma de acceso compartido (SAS) en los parámetros de consulta de Hola que se usan para la autenticación. 
    También puede obtener dirección URL del extremo HTTP de saludo de la introducción de aplicación lógica Hola portal de Azure. En **Historial de desencadenadores**, seleccione el desencadenador:

    ![Obtención de la dirección URL del punto de conexión HTTP en Azure Portal][2]

    O bien, puede obtener dirección URL de hello mediante esta llamada:

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a>Cambiar el método HTTP de hello para el desencadenador

De forma predeterminada, Hola **solicitud** desencadenador espera una solicitud POST de HTTP, pero puede usar un método HTTP diferente. 

> [!NOTE]
> Puede especificar solo un tipo de método.

1. En el desencadenador **Request**, elija **Mostrar opciones avanzadas**.

2. Abra hello **método** lista. En este ejemplo, seleccione **GET** para que pueda probar la dirección URL del punto de conexión HTTP más adelante.

    > [!NOTE]
    > Puede seleccionar cualquier otro método HTTP, o bien especificar un método personalizado para su propia aplicación lógica.

    ![Cambio del método HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a>Aceptación de parámetros a través de la dirección URL del punto de conexión HTTP

Si desea que los parámetros de tooaccept de dirección URL de extremo HTTP, personalizar la ruta de acceso relativa del desencadenador.

1. En el desencadenador **Request**, elija **Mostrar opciones avanzadas**. 

2. En **método**, especificar método hello HTTP que desea que su toouse de solicitud. En este ejemplo, seleccione hello **obtener** método, si no lo ha hecho ya, para que pueda probar la dirección URL de su extremo HTTP.

      > [!NOTE]
      > Cuando se especifica una ruta de acceso relativa para el desencadenador, también debe especificar explícitamente un método HTTP para el desencadenador.

3. En **ruta_relativa**, especifique la ruta de acceso relativa de hello para el parámetro hello que debe aceptar la dirección URL, por ejemplo, `customers/{customerID}`.

    ![Especifique el método HTTP de hello y ruta de acceso relativa para el parámetro](./media/logic-apps-http-endpoint/relativeurl.png)

4. toouse Hola parámetro, agregue un **respuesta** aplicación lógica de acción tooyour. (En el desencadenador, elija **Nuevo paso** > **Agregar una acción** > **Respuesta**). 

5. En su respuesta **cuerpo**, incluye el token de hello para el parámetro hello que especificó en la ruta de acceso relativa del desencadenador.

    Por ejemplo, tooreturn `Hello {customerID}`, la respuesta de actualización de **cuerpo** con `Hello {customerID token}`. 
    lista de contenido dinámico de Hello debe aparecer y mostrar hello `customerID` tooselect, símbolo (token).

    ![Agregar parámetro tooresponse cuerpo](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    El **cuerpo** debería presentar un aspecto similar al de este ejemplo:

    ![Cuerpo de respuesta con el parámetro](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. Guarde la aplicación lógica. 

    La dirección URL del extremo HTTP ahora incluye ruta de acceso relativa de hello, por ejemplo: 

    https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...

7. tootest su extremo HTTP, copiar y pegar Hola [URL actualizada en otra ventana del explorador, pero reemplacen `{customerID}` con `123456`, y presione ENTRAR.

    El explorador debe mostrar este texto: 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a>Tokens generados a partir de esquemas JSON para aplicaciones lógicas

Cuando se proporciona un esquema JSON en su **solicitar** desencadenar, hello lógica de aplicación diseñador genera tokens para las propiedades de dicho esquema. Después puede usar esos tokens para pasar datos a través del flujo de trabajo de la aplicación lógica.

En este ejemplo, si agrega hello `title` y `name` esquema de propiedades tooyour JSON, sus tokens están ahora disponible toouse en pasos posteriores de flujo de trabajo. 

Este es el esquema JSON completo hello:

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

## <a name="create-nested-workflows-for-logic-apps"></a>Creación de flujos de trabajo anidados para aplicaciones lógicas

Puede anidar los flujos de trabajo en la aplicación lógica mediante la adición de otras aplicaciones de lógica que pueden recibir solicitudes. tooinclude estas aplicaciones lógicas, agregar hello **Azure Logic Apps - elegir un flujo de trabajo de las aplicaciones lógicas** desencadenador tooyour de acción. A continuación, puede seleccionar desde las aplicaciones lógicas elegibles.

![Adición de otra aplicación lógica](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a>Llamada o desencadenamiento de aplicaciones lógicas a través de puntos de conexión HTTP

Después de crear el punto de conexión HTTP, puede desencadenar la aplicación lógica a través de un `POST` dirección URL completa del método toohello. Las aplicaciones lógicas tienen compatibilidad integrada para los puntos de conexión de acceso directo.

## <a name="reference-content-from-an-incoming-request"></a>Referencia al contenido de una solicitud entrante

Si Hola contenido del tipo es `application/json`, puede hacer referencia a propiedades de solicitud entrante de Hola. En caso contrario, contenido se trata como una sola unidad binaria que se puede pasar tooother API. tooreference este contenido dentro de flujo de trabajo de hello, debe convertir el contenido. Por ejemplo, si se pasa `application/xml` contenido, puede usar `@xpath()` para una extracción de XPath, o `@json()` para convertir XML tooJSON. Obtenga información sobre cómo [trabajar con tipos de contenido](../logic-apps/logic-apps-content-type.md).

Hola tooget de salida de una solicitud entrante, puede usar hello `@triggerOutputs()` función. salida de Hello podría ser similar a este ejemplo:

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

Hola tooaccess `body` propiedad concreto, puede usar hello `@triggerBody()` acceso directo. 

## <a name="respond-toorequests"></a>Responder toorequests

Puede ser conveniente toorespond toocertain solicitudes que iniciar una aplicación lógica mediante la devolución de llamada toohello contenido. código de estado de hello tooconstruct, encabezado y cuerpo de la respuesta, puede usar hello **respuesta** acción. Esta acción puede aparecer en cualquier lugar en la aplicación lógica, no solo al final de hello del flujo de trabajo.

> [!NOTE] 
> Si no incluye la aplicación lógica un **respuesta**, punto de conexión de hello HTTP responde *inmediatamente* con un **202 Accepted** estado. Además, para hello original tooget Hola solicitud-respuesta, todos los pasos necesarios para la respuesta de hello deben finalizar en hello [límite de tiempo de espera de solicitud](./logic-apps-limits-and-config.md) a menos que se llama a flujo de trabajo de hello como una aplicación de lógica anidados. Si se produce ninguna respuesta dentro de este límite, solicitud entrante de hello tiempo de espera y recibe la respuesta HTTP de hello **408 tiempo de espera de cliente**. Para las aplicaciones lógicas anidadas, aplicación de lógica de hello primario continúa toowait una respuesta hasta que se complete, independientemente de cuánto tiempo se necesita.

### <a name="construct-hello-response"></a>Respuesta de Hola de construcción

Puede incluir más de un encabezado y cualquier tipo de contenido en el cuerpo de la respuesta de Hola. En la respuesta de ejemplo, el encabezado de hello especifica que respuesta hello tiene tipo de contenido `application/json`. y contiene el cuerpo de hello `title` y `name`, según el esquema JSON de hello actualizada previamente para hello **solicitar** desencadenador.

![Acción de respuesta HTTP][3]

Las respuestas tienen estas propiedades:

| Propiedad | Description |
| --- | --- |
| statusCode |Especifica el código de estado de hello HTTP para la solicitud entrante de toohello responde. Este código puede ser cualquier código de estado válido que comience con 2xx, 4xx o 5xx. En cambio, no se permiten códigos de estado 3xx. |
| encabezados |Define cualquier número de tooinclude de encabezados de respuesta Hola. |
| body |Especifica un objeto de cuerpo que puede ser una cadena, un objeto JSON o incluso contenido binario al que se hace referencia desde un paso anterior. |

Aquí es lo que parece que ahora para Hola Hola el esquema JSON **respuesta** acción:

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
> definición JSON tooview Hola completa para la aplicación lógica, en hello Diseñador de la lógica de aplicaciones, elija **vista código**.

## <a name="q--a"></a>Preguntas y respuestas

#### <a name="q-what-about-url-security"></a>P: ¿¿Qué se puede decir sobre la seguridad de las direcciones URL?

R: Azure genera direcciones URL de devolución de llamada de la aplicación lógica de manera segura con una firma de acceso compartido (SAS). Esta firma pasa como un parámetro de consulta y debe validarse antes de que se pueda activar la aplicación lógica. Azure genera la firma de hello mediante una combinación única de una clave secreta por aplicación lógica, el nombre de desencadenador de Hola y operación de Hola que se lleva a cabo. Por lo que, a menos que alguien tiene acceso toohello lógica secreto de aplicación clave, no pueden generar una firma válida.

   > [!IMPORTANT]
   > Para producción y los sistemas seguros, se recomienda llamar a la aplicación lógica directamente desde el Explorador de hello porque:
   > 
   > * clave de acceso compartido de Hello aparece en la dirección URL de Hola.
   > * No se puede administrar directivas de contenido seguras debido tooshared dominios entre los clientes de aplicación lógica.

#### <a name="q-can-i-configure-http-endpoints-further"></a>P: ¿Puedo configurar más puntos de conexión HTTP?

R: Sí, los puntos de conexión HTTP admiten una configuración más avanzada a través de [**API Management**](../api-management/api-management-key-concepts.md). Este servicio también ofrece la capacidad de Hola para tooconsistently administre todas las API, incluidas las aplicaciones de lógica, configure los nombres de dominio personalizado, usar varios métodos de autenticación etc., por ejemplo:

* [Método de solicitud de cambio Hola](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [Cambie los segmentos de dirección URL de saludo de solicitud de Hola](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* Configurar los dominios de administración de API en hello [portal de Azure](https://portal.azure.com/ "portal de Azure")
* Configurar la directiva toocheck para la autenticación básica

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a>P: ¿qué cambió cuando migra esquema Hola de vista previa de 1 de diciembre de 2014 de hello?

R: Este es un resumen sobre estos cambios:

| Versión preliminar de 1 de diciembre de 2014 | 1 de junio de 2016 |
| --- | --- |
| Haga clic en la aplicación de API **Agente de escucha HTTP**. |Haga clic en **Desencadenador manual** (no se necesita ninguna aplicación de API). |
| Configuración del Agente de escucha HTTP "*Enviar respuesta automáticamente*" |Tanto si incluye una **respuesta** acción o no en la definición de flujo de trabajo de Hola |
| Configuración de la autenticación básica o OAuth |mediante API Management |
| Configuración del método HTTP |En **Mostrar opciones avanzadas**, elija un método HTTP |
| Configuración de la ruta de acceso relativa |En **Mostrar opciones avanzadas**, agregue una ruta de acceso relativa |
| Cuerpo de entrada de Hola de referencia a través de`@triggerOutputs().body.Content` |Referencia a través de `@triggerOutputs().body` |
| **Enviar respuesta HTTP** acción en hello escucha HTTP |Haga clic en **responden tooHTTP solicitud** (se requiere ninguna API App) |

## <a name="get-help"></a>Obtener ayuda

tooask preguntas, responda a preguntas y obtenga información acerca de qué otra lógica de aplicaciones de Azure hacen los usuarios, visite hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar las aplicaciones lógicas de Azure y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

* [Creación de definiciones de aplicación lógica](./logic-apps-author-definitions.md)
* [Control de errores y excepciones](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
