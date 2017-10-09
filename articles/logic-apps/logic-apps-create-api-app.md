---
title: aaaCreate web API y las API de REST que los conectores - Azure Logic Apps | Documentos de Microsoft
description: "Crear web API y las API de REST toocall su API, servicios o sistemas en los flujos de trabajo de aplicaciones integradas del sistema con aplicaciones de Azure lógica"
keywords: API web, API de REST, conectores, flujos de trabajo, integraciones de sistemas
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Creación de API personalizadas como conectores para aplicaciones lógicas

Aunque las aplicaciones lógicas de Azure ofrece [100 + conectores integrados](../connectors/apis-list.md) que puede usar en flujos de trabajo de aplicación lógica, puede querer toocall API, sistemas, y servicios que no están disponibles como conectores. Puede crear su propia API personalizadas que proporcionan las acciones y desencadenadores toouse en aplicaciones de la lógica. Estas son otras razones por las que podría toocreate su propia API demasiado usar que los conectores de aplicaciones lógicas:

* Ampliar los flujos de trabajo actuales de integración de datos e integración de sistemas.
* Ayudar a los clientes utilizar sus tareas profesionales o personales del toomanage de servicio.
* Expanda Hola alcance, detectabilidad y el uso de su servicio.

Básicamente, los conectores son API web que usan REST para las interfaces conectables, [formato de metadatos de Swagger](http://swagger.io/specification/) para documentación y JSON como formato de intercambio de datos. Dado que los conectores son API de REST que se comunican a través de puntos de conexión HTTP, puede utilizar cualquier lenguaje para crear conectores, como, por ejemplo, .NET, Java, o Node.js. También puede hospedar las API en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md), un plataforma como-servicio (PaaS) de la oferta que proporciona una de las maneras de mejor, más fáciles y más escalables de hello para la API de hospedaje. 

Para toowork API personalizada a las aplicaciones lógicas, puede proporcionar su API [ *acciones* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) que realizan tareas específicas en flujos de trabajo de aplicación lógica. La API también puede actuar como un [*desencadenador*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) que inicia un flujo de trabajo de aplicación lógica cuando un evento o datos nuevos cumplen una condición especificada. Este tema describen los patrones comunes que puede seguir para crear acciones y desencadenadores en la API basada en hello un comportamiento que desea que su tooprovide de API.

> [!TIP] 
> Aunque puede implementar las API como [aplicaciones web](../app-service-web/app-service-web-overview.md), considere la posibilidad de implementar las API como [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md), que puede facilitar su trabajo al compilar, hospedar y utilizar las API en la nube de Hola y de forma local. No tienes toochange cualquier código en las API, implemente la aplicación de API de código tooan. Obtenga información acerca de cómo demasiado [compilar aplicaciones de API creadas con ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), o [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Para obtener ejemplos de API App compiladas para las aplicaciones lógicas, visite hello [repositorio de GitHub de aplicaciones de Azure lógica](http://github.com/logicappsio) o [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Herramientas útiles

Una API personalizada funciona mejor con las aplicaciones lógicas cuando Hola API también tiene un [Swagger documento](http://swagger.io/specification/) que describe las operaciones y los parámetros de hello de la API.
Al igual que muchas bibliotecas [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), puede generar automáticamente el archivo Swagger de hello para usted. archivo de Swagger de hello tooannotate para nombres para mostrar, tipos de propiedades etc., también puede usar [TRex](https://github.com/nihaue/TRex) para que el archivo Swagger funciona bien con aplicaciones de la lógica.

<a name="actions"></a>

## <a name="action-patterns"></a>Patrones de acción

Para tareas de tooperform de aplicaciones de lógica, debe proporcionar la API personalizada [ *acciones*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Cada operación de la API asigna tooan acción. Una acción básica es un controlador que acepta solicitudes HTTP y devuelve respuestas HTTP. Por ejemplo, una aplicación de lógica envía una aplicación de web de tooyour de solicitud HTTP o una aplicación de API. La aplicación, a continuación, devuelve una respuesta HTTP, junto con el contenido que Hola lógica de aplicación puede procesar.

Para una acción estándar, puede escribir un método de solicitud HTTP en la API y describir ese método en un archivo Swagger. A continuación, puede llamar directamente a su API con una [acción HTTP](../connectors/connectors-native-http.md) o una acción [HTTP + Swagger](../connectors/connectors-native-http-swagger.md). De forma predeterminada, se deben devolver las respuestas en hello [límite de tiempo de espera de solicitud](./logic-apps-limits-and-config.md). 

![Patrón de acción estándar](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake una aplicación lógica Espere mientras su API finalice las tareas de ejecución más larga, la API puede seguir hello [patrón asincrónico de sondeo](#async-pattern) o hello [patrón asincrónico webhook](#webhook-actions) descritos en este tema. Para una analogía que ayudan a visualizar distintos comportamientos de estos patrones, imagine proceso Hola para ordenar una sencilla personalizado desde una pastelería. patrón de sondeo de Hello refleja comportamiento Hola donde se llamó a la pastelería Hola cada toocheck de 20 minutos si pastel Hola está preparado. Hola webhook reflejos Hola comportamiento de la trama donde pastelería Hola se le pedirá su número de teléfono por lo que pueden llamar a cuando pastel Hola está listo.

Para obtener ejemplos, visite hello [repositorio de GitHub de aplicaciones de la lógica](https://github.com/logicappsio). Además, obtenga más información sobre la [medición de uso para acciones](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Realizar tareas de larga duración con hello patrón de acción de sondeo

toohave su API realizar tareas que pudieron ejecutar más hello [límite de tiempo de espera de solicitud](./logic-apps-limits-and-config.md), puede usar el patrón asincrónico de sondeo de Hola. Este patrón tiene su realice API funcionan en un subproceso independiente, pero mantener un motor de Logic Apps toohello conexión activa. De este modo, aplicación de lógica de hello no tiene tiempo de espera o continúe con el paso siguiente de hello en el flujo de trabajo de hello antes de que la API finalice el trabajo.

Este es el patrón general de hello:

1. Asegúrese de que ese motor Hola sabe que su API acepta la solicitud de Hola y empezar a trabajar.
2. Cuando el motor de hello realiza las solicitudes posteriores de estado del trabajo, comunicar motor hello cuando finaliza la tarea hello de la API.
3. Devolver motor toohello de datos relevantes para que pueda continuar el flujo de trabajo de aplicación de lógica de Hola.

<a name="bakery-polling-action"></a>Ahora aplicar patrón de sondeo de pastelería analogía toohello anterior hello y imagine que se llama a una pastelería y orden un pastel personalizado para la entrega. proceso de Hola para realizar pastel de Hola lleva tiempo y, no desea toowait en teléfono Hola mientras pastelería Hola funciona en pastel de Hola. pastelería Hola confirma su pedido y tiene que llamar a cada 20 minutos para el estado del pastel Hola. Una vez que pasen de 20 minutos, se llama a la pastelería Hola, pero indican que el pastel no lleva a cabo y que debería llamar 20 minutos en otro. Este proceso atrás y adelante continúa hasta que se llama y pastelería Hola indica que el pedido está listo y entrega el pastel. 

Ahora vamos a volver a asignar este mismo patrón de sondeo. pastelería Hola representa la API personalizada, mientras usted, cliente de pastel de hello, representa motor de hello Logic Apps. Cuando el motor de hello llama a su API con una solicitud, la API confirma la solicitud de Hola y responde con el intervalo de tiempo de saludo al motor de hello puede comprobar el estado del trabajo. motor de Hola continúa con la comprobación de estado del trabajo hasta que la API responda que se hace que el trabajo de Hola y aplicación lógica de devuelve datos tooyour, que, a continuación, sigue el flujo de trabajo. 

![Patrón de acción de sondeo](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Estos son los pasos específicos de Hola para su toofollow API, que se describe desde la perspectiva de la API de Hola:

1. Cuando su API llegue a un trabajo toostart de solicitud HTTP, devolver inmediatamente un HTTP `202 ACCEPTED` respuesta con hello `location` encabezado que se describe más adelante en este paso. Esta respuesta permite Hola Logic Apps motor saber que recibimos su API Hola solicitud de carga de la solicitud de hello aceptadas (datos de entrada) y ahora se está procesando. 
   
   Hola `202 ACCEPTED` respuesta debe incluir estos encabezados:
   
   * *Requiere*: un `location` encabezado que especifica la dirección URL de tooa de ruta de acceso absoluta Hola donde motor de hello Logic Apps puede comprobar el estado del trabajo de la API

   * *Opcional*: A `retry-after` encabezado que especifica el número de Hola de segundos que Hola motor debe esperar antes de comprobar hello `location` dirección URL para el estado del trabajo. 

     De forma predeterminada, el motor de hello comprueba cada 20 segundos. toospecify un intervalo diferente, incluyen hello `retry-after` hello y encabezado de número de segundos hasta el siguiente sondeo de Hola.

2. Después de hello especificado paso del tiempo, Hola Logic Apps motor Hola sondeos `location` estado del trabajo de toocheck de dirección URL. La API debe realizar estas comprobaciones y devolver estas respuestas:
   
   * Si se realiza el trabajo de hello, devolver un elemento HTTP `200 OK` respuesta, junto con la carga de respuesta de hello (entrada para el paso siguiente de hello).

   * Si todavía está procesando el trabajo de hello, devuelven otro HTTP `202 ACCEPTED` respuesta, pero con Hola mismos encabezados como respuesta original Hola.

Cuando su API sigue este patrón, no tiene nada toodo de hello lógica aplicación flujo de trabajo definición toocontinue comprobar el estado del trabajo. Cuando el motor de hello obtiene HTTP `202 ACCEPTED` válido y respuesta `location` encabezado, Hola motor aspectos Hola asincrónica patrón y comprobaciones de Hola `location` encabezado hasta que la API devuelve una respuesta no 202.

> [!TIP]
> Para ver un ejemplo de modelo asincrónico, revise este [ejemplo de respuesta del controlador asincrónico en GitHub](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Realizar tareas de larga duración con patrón de acción de hello webhook

Como alternativa, puede usar el patrón de webhook de Hola para tareas de larga duración y el procesamiento asincrónico. Este patrón tiene la aplicación de lógica de hello pause y espere un "callback" de su toofinish de API de procesamiento antes de continuar el flujo de trabajo. Esta devolución de llamada es una solicitud HTTP POST que se envía una dirección URL tooa de mensaje cuando se produce un evento. 

<a name="bakery-webhook-action"></a>Ahora aplicar Hola anterior pastelería analogía toohello webhook patrones y imagine que se llama a una pastelería y orden un pastel personalizado para la entrega. proceso de Hola para realizar pastel de Hola lleva tiempo y, no desea toowait en teléfono Hola mientras pastelería Hola funciona en pastel de Hola. pastelería Hola confirma su pedido, pero esta vez, se les da el número de teléfono por lo que pueden llamar a cuando se lleva a cabo pastel Hola. En esta ocasión, pastelería Hola indica cuando el orden está preparada y entrega el pastel.

Cuando se asigne este patrón de webhook volver, pastelería Hola representa la API personalizada, mientras, al cliente de pastel de hello, representan Hola Logic Apps motor. motor de Hello llama a la API con una solicitud e incluye la dirección URL "callback".
Cuando se realiza el trabajo de hello, la API utiliza Hola URL toonotify Hola motor y devolver datos tooyour lógica app, que, a continuación, sigue el flujo de trabajo. 

Para este patrón, configure dos puntos de conexión en el controlador: `subscribe` y `unsubscribe`

*  `subscribe`punto de conexión: cuando la ejecución alcanza la acción de la API de flujo de trabajo de hello, Hola Logic Apps motor Hola llamadas `subscribe` punto de conexión. Este paso hace Hola lógica aplicación toocreate una dirección URL de devolución de llamada que la API almacena y, a continuación, espera para la devolución de llamada de Hola a través de la API cuando se completa el trabajo. La API, a continuación, llama de nuevo con una dirección URL toohello de HTTP POST y pasa los encabezados y el contenido devuelto como aplicación de lógica de entrada toohello.

* `unsubscribe`punto de conexión: si se cancela la aplicación de la lógica de hello ejecutar, Hola Logic Apps motor Hola llamadas `unsubscribe` punto de conexión. La API, a continuación, puede anular el registro de dirección URL de devolución de llamada de Hola y detener los procesos según sea necesario.

![Patrón de acción de webhook](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Actualmente, Hola diseñador la lógica de aplicación no es compatible con detección de webhook de extremos a través de Swagger. Por lo que este patrón tiene tooadd una [ **Webhook** acción](../connectors/connectors-native-webhook.md) y especifique la dirección URL de hello, encabezados y cuerpo de la solicitud. Consulte también [Acciones y desencadenadores de flujo de trabajo](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass en dirección URL de devolución de llamada de hello, puede usar hello `@listCallbackUrl()` función de flujo de trabajo en cualquiera de los campos anteriores de hello según sea necesario.

> [!TIP]
> Para ver un ejemplo de patrón de webhook, consulte este [ejemplo de desencadenador de webhook en GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Patrones de desencadenador

La API personalizada puede actuar como un [*desencadenador*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) que inicia una aplicación lógica cuando un evento o datos nuevos cumplen una condición especificada. Este desencadenador puede realizar comprobaciones periódicamente o esperar y escuchar nuevos datos o eventos en su punto de conexión de servicio. Si cumple con nuevos datos o un evento Hola condición especificada, desencadenador de Hola se activa e inicia la aplicación de lógica de hello, que está escuchando el desencadenador de toothat. las aplicaciones lógicas de toostart este modo, la API puede seguir hello [ *desencadenador de sondeo* ](#polling-triggers) o hello [ *webhook desencadenador* ](#webhook-triggers) patrón. Estos patrones son similares homólogos tootheir para [sondeo acciones](#async-pattern) y [acciones de webhook](#webhook-actions). Obtenga también más información sobre la [medición de uso para desencadenadores](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Comprobar si hay nuevos datos o eventos periódicamente con hello sondeo patrón de desencadenador

A *desencadenador de sondeo* actúa como la de hello [acción de sondeo](#async-pattern) descrito anteriormente en este tema. motor de Logic Apps Hola periódicamente llama y comprueba el punto de conexión de desencadenador de Hola para nuevos datos o eventos. Si el motor de hello busca nuevos datos o un evento que cumple la condición especificada, se activa el desencadenador de Hola. A continuación, el motor de hello crea una instancia de aplicación lógica que procesa los datos de hello como entrada. 

![Patrón de desencadenador de sondeo](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Cada solicitud de sondeo cuenta como una ejecución de acción, incluso cuando no se crea ninguna instancia de aplicación lógica. procesamiento tooprevent Hola los mismos datos varias veces, el desencadenador debe limpiar los datos que ya se lee y pasa la aplicación de la lógica de toohello.

Estos son los pasos específicos para un desencadenador de sondeo, que se describe desde la perspectiva de la API de Hola:

| ¿Se han encontrado nuevos datos o eventos?  | Respuesta de la API | 
| ------------------------- | ------------ |
| Encontrado | Devolver un elemento HTTP `200 OK` estado con la carga de respuesta de hello (entrada para el paso siguiente). <br/>Esta respuesta crea una instancia de aplicación lógica e inicia el flujo de trabajo de Hola. |
| No encontrado | Devuelve un estado de HTTP `202 ACCEPTED` con un encabezado `location` y un encabezado `retry-after`. <br/>Para los desencadenadores, Hola `location` encabezado también debe contener un `triggerState` parámetro de consulta, que normalmente es una "marca de tiempo". La API puede usar este Hola de identificador tootrack última vez que Hola lógica se inició la aplicación. |

Por ejemplo, tooperiodically Compruebe el servicio para los nuevos archivos, es posible que genere un desencadenador de sondeo que tiene estos comportamientos:

| ¿La solicitud incluye `triggerState`? | Respuesta de la API |
| -------------------------------- | -------------|
| No | Devolver un elemento HTTP `202 ACCEPTED` estado más una `location` encabezado con `triggerState` establecen toohello hora actual y Hola `retry-after` too15 de intervalo (segundos). |
| Sí | Compruebe el servicio para los archivos agregados después de hello `DateTime` para `triggerState`. |

| Número de archivos encontrados | Respuesta de la API |
| --------------------- | -------------|
| Un solo archivo | Devolver un elemento HTTP `200 OK` hello y estado de carga de contenido, actualice `triggerState` toohello `DateTime` para hello devuelve archivos y establezca `retry-after` too15 de intervalo (segundos). |
| Varios archivos | Devolver un archivo en un momento y HTTP `200 OK` estado, update `triggerState`, conjunto hello y `retry-after` too0 de intervalo (segundos). </br>Estos pasos permiten motor Hola sabe que hay más datos disponibles, y ese motor Hola inmediatamente debe solicitar datos Hola de dirección URL de Hola Hola `location` encabezado. |
| Ningún archivo | Devolver un elemento HTTP `202 ACCEPTED` estado, no cambie `triggerState`, conjunto hello y `retry-after` too15 de intervalo (segundos). |

> [!TIP]
> Para ver un ejemplo de patrón de desencadenador de sondeo, consulte este [ejemplo de controlador de desencadenador de sondeo en GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Espere y realizar escuchas de los nuevos datos o eventos con el patrón de desencadenador de hello webhook

Un desencadenador de webhook es un *desencadenador de push* que espera y escucha nuevos datos o eventos en su punto de conexión de servicio. Si cumple con nuevos datos o un evento Hola condición, Hola desencadenador se activa especificada y crea una instancia de aplicación lógica, que, a continuación, procesa los datos de hello como entrada.
Desencadenadores de Webhook actúan como hello [acciones de webhook](#webhook-actions) anteriormente descritas en este tema y se configuran con `subscribe` y `unsubscribe` los puntos de conexión. 

* `subscribe`punto de conexión: al agregar y guardar un desencadenador de webhook de la aplicación lógica, Hola Logic Apps motor Hola llamadas `subscribe` punto de conexión. Este paso hace Hola lógica aplicación toocreate una dirección URL de devolución de llamada que almacena su API. Cuando hay nuevos datos o un evento que cumpla Hola condición especificada, la API se llama de nuevo con una dirección URL toohello de HTTP POST. encabezados y la carga de contenido de hello pasan como aplicación de lógica de entrada toohello.

* `unsubscribe`punto de conexión: si se elimina el desencadenador de webhook de Hola o aplicación toda a lógica, Hola Logic Apps motor Hola llamadas `unsubscribe` punto de conexión. La API, a continuación, puede anular el registro de dirección URL de devolución de llamada de Hola y detener los procesos según sea necesario.

![Patrón de desencadenador de webhook](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Actualmente, Hola diseñador la lógica de aplicación no es compatible con detección de webhook de extremos a través de Swagger. Por lo que este patrón tiene tooadd una [ **Webhook** desencadenador](../connectors/connectors-native-webhook.md) y especifique la dirección URL de hello, encabezados y cuerpo de la solicitud. Consulte también el [desencadenador HTTPWebhook](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass en dirección URL de devolución de llamada de hello, puede usar hello `@listCallbackUrl()` función de flujo de trabajo en cualquiera de los campos anteriores de hello según sea necesario.
>
> procesamiento tooprevent Hola los mismos datos varias veces, el desencadenador debe limpiar los datos que ya se lee y pasa la aplicación de la lógica de toohello.

> [!TIP]
> Para ver un ejemplo de patrón de webhook, consulte este [ejemplo de controlador de desencadenador de webhook en GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Implementación, llamada y protección de las API personalizadas

Después de crear las API personalizadas, configure las API para la implementación de modo que pueda llamarlas de forma segura. Obtenga información acerca de cómo demasiado[implementar, llame a y proteger las API personalizadas para las aplicaciones lógicas](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Publicar tooAzure de API personalizada

toomake su API personalizadas disponibles para uso público en Azure, envíe su toohello nominaciones [programa Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Obtener ayuda

Para obtener ayuda específica sobre las API personalizadas, póngase en contacto con [customapishelp@microsoft.com](mailto:customapishelp@microsoft.com).

tooask preguntas y responder a preguntas, consulte ¿Qué otros usuarios de aplicaciones de la lógica de Azure están realizando, visitan hello [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp mejorar la lógica de aplicaciones y conectores, votar sobre o enviar ideas en hello [sitio de comentarios de usuario de las aplicaciones lógicas](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Pasos siguientes

* [Medición de uso para acciones y desencadenadores](logic-apps-pricing.md)
* [Control de los tipos de contenido](./logic-apps-content-type.md)
* [Control de errores y excepciones](./logic-apps-exception-handling.md)
* [Proteger el acceso a las aplicaciones lógicas tooyour](./logic-apps-securing-a-logic-app.md)
* [Llamada, desencadenamiento o anidamiento de aplicaciones lógicas con puntos de conexión HTTP](./logic-apps-http-endpoint.md)