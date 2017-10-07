---
title: "Conector de aaaWebhook para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "¿Cómo toouse webhook acciones y desencadenadores tooperform acciones que la matriz de filtro de las aplicaciones lógicas"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 71775384-6c3a-482c-a484-6624cbe4fcc7
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: b2dee12750f3f20f10e7b257da05a79f28f90f43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-webhook-connector"></a>Empezar a trabajar con el conector de hello webhook

Con la acción de webhook de Hola y el desencadenador, puede iniciar, pausar y reanudar flujos tooperform estas tareas:

* Realizar una desencadenación desde un [Centro de eventos de Azure cuando se reciba un elemento](https://github.com/logicappsio/EventHubAPI)
* Esperar una aprobación antes de continuar con un flujo de trabajo

Obtenga más información sobre [cómo toocreate API personalizadas que admiten un webhook](../logic-apps/logic-apps-create-api-app.md).

## <a name="use-hello-webhook-trigger"></a>Utilice hello webhook desencadenador

Un [ *desencadenador* ](connectors-overview.md) es un evento que inicia un flujo de trabajo de aplicación lógica. Un desencadenador de webhook se basa en eventos y no depende del sondeo para los nuevos elementos. Al igual que hello [desencadenador de solicitud](connectors-native-reqres.md), aplicación de lógica de hello desencadena Hola instantánea que se produce un evento. desencadenador de webhook Hola registra un *dirección URL de devolución de llamada* tooa servicio y utiliza esa aplicación de lógica de dirección URL toofire hello como sea necesario.

Este es un ejemplo que muestra cómo desencadenar tooset seguridad HTTP Hola diseñador la lógica de aplicación. Hello da por sentado que ya ha implementado o se obtiene acceso a una API que sigue hello [webhook suscribir y cancelar la suscripción patrón en las aplicaciones lógicas](../logic-apps/logic-apps-create-api-app.md#webhook-triggers). Hola suscribirse llamada se realiza cada vez que una aplicación de la lógica se guarda con un webhook nuevo o cambiada de tooenabled deshabilitado. Hola cancelar la suscripción llamada se realiza cuando un desencadenador de webhook de aplicación lógica se quita y guardo o ha cambiado de toodisabled habilitado.

**desencadenador de tooadd hello webhook**

1. Agregar hello **HTTP Webhook** desencadenador como primer paso en una aplicación de la lógica de Hola.
2. Rellene los parámetros de Hola para hello webhook suscribir y cancelar la suscripción llamadas.

   Este paso sigue el mismo patrón como Hola de hello [acción HTTP](connectors-native-http.md) formato.

     ![Desencadenador HTTP](./media/connectors-native-webhook/using-trigger.png)

3. Agregue una acción como mínimo.
4. Haga clic en **guardar** aplicación lógica de toopublish Hola. Este Hola de llamadas de paso suscribirse a punto de conexión con tootrigger de dirección URL necesaria de devolución de llamada de hello esta aplicación lógica.
5. Cada vez que Hola servicio hace un `HTTP POST` dirección URL de devolución de llamada de toohello, Hola se activa de aplicación lógica e incluye los datos que se pasan en la solicitud de Hola.

## <a name="use-hello-webhook-action"></a>Use la acción de webhook Hola

Un [ *acción* ](connectors-overview.md) se efectúe una operación definida en una aplicación de lógica de flujo de trabajo de Hola. Registra una acción de webhook un *dirección URL de devolución de llamada* con un servicio y espera hasta que la dirección URL de Hola se llama antes de reanudar. Hola ["Enviar correo electrónico de aprobación"](connectors-create-api-office365-outlook.md) es un ejemplo de un conector que sigue este patrón. Puede ampliar este patrón en cualquier servicio mediante una acción de webhook Hola. 

Este es un ejemplo que muestra cómo tooset una acción de webhook en Hola diseñador la lógica de aplicación. Estos pasos se supone que ya ha implementado o se obtiene acceso a una API que sigue hello [webhook suscribir y cancelar la suscripción patrón que se usa en las aplicaciones lógicas](../logic-apps/logic-apps-create-api-app.md#webhook-actions). Hola suscribirse llamada se realiza cuando una aplicación de la lógica ejecuta la acción de webhook Hola. Hola cancelar la suscripción llamada se realiza cuando se cancela una ejecución mientras se espera una respuesta, o antes de la lógica de hello aplicación agota el tiempo.

**tooadd una acción de webhook**

1. Elija **Nuevo paso** > **Agregar una acción**.

2. En el cuadro de búsqueda de hello, escriba "webhook" toofind Hola **HTTP Webhook** acción.

    ![Acción de consulta de selección](./media/connectors-native-webhook/using-action-1.png)

3. Rellenar los parámetros de Hola para hello webhook suscribir y cancelar la suscripción llamadas

   Este paso sigue el mismo patrón como Hola de hello [acción HTTP](connectors-native-http.md) formato.

     ![Acción de consulta de finalización](./media/connectors-native-webhook/using-action-2.png)
   
   En tiempo de ejecución, Hola llamadas de aplicación lógica Hola suscribirse extremo después de llegar a ese paso.

4. Haga clic en **guardar** aplicación lógica de toopublish Hola.

## <a name="technical-details"></a>Detalles técnicos

A continuación encontrará más detalles acerca de las acciones y desencadenadores de hello es compatible con ese webhook.

## <a name="webhook-triggers"></a>Desencadenadores de webhook

| Acción | Descripción |
| --- | --- |
| Webhook HTTP |Suscribirse a un servicio de tooa de dirección URL de devolución de llamada que se puede llamar a la aplicación lógica de la toofire de la dirección URL Hola según sea necesario. |

### <a name="trigger-details"></a>Detalles del desencadenador

#### <a name="http-webhook"></a>Webhook HTTP

Suscribirse a un servicio de tooa de dirección URL de devolución de llamada que se puede llamar a la aplicación lógica de la toofire de la dirección URL Hola según sea necesario.
Un asterisco (*) indica un campo obligatorio.

| Display Name (Nombre para mostrar) | Nombre de propiedad | Descripción |
| --- | --- | --- |
| Método de suscripción* |estático |Método HTTP toouse para solicitud subscribe |
| URI de suscripción* |uri |Toouse de URI de HTTP para la solicitud subscribe |
| Método de cancelación de suscripción* |estático |Toouse de método HTTP para la solicitud de cancelación de suscripción |
| URI de cancelación de suscripción* |uri |Toouse de URI de HTTP para la solicitud de cancelación de suscripción |
| Cuerpo de suscripción |body |Cuerpo de la solicitud HTTP para realizar la suscripción. |
| Encabezados de suscripción |encabezados |Encabezados de la solicitud HTTP para realizar la suscripción. |
| Autenticación de suscripción |Autenticación |Toouse de autenticación de HTTP para suscribirse. Para más información consulte el [conector HTTP](connectors-native-http.md#authentication) |
| Cuerpo de cancelación de suscripción |body |Cuerpo de la solicitud HTTP para cancelar la suscripción. |
| Encabezados de cancelación de suscripción |encabezados |Encabezados de la solicitud HTTP para cancelar la suscripción. |
| Autenticación de cancelación de suscripción |Autenticación |Toouse de autenticación de HTTP para cancelar la suscripción. Para más información consulte el [conector HTTP](connectors-native-http.md#authentication) |

**Detalles de salida**

Solicitud de webhook

| Nombre de propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| encabezados |objeto |Encabezados de la solicitud de webhook |
| body |objeto |Objeto de la solicitud de webhook |
| Código de estado |int |Código de estado de la solicitud de webhook |

## <a name="webhook-actions"></a>Acciones de webhook

| Acción | Descripción |
| --- | --- |
| Webhook HTTP |Suscribirse a un servicio de tooa de dirección URL de devolución de llamada que se puede llamar a la dirección URL de hello tooresume un paso de flujo de trabajo según sea necesario. |

### <a name="action-details"></a>Detalles de la acción

#### <a name="http-webhook"></a>Webhook HTTP

Suscribirse a un servicio de tooa de dirección URL de devolución de llamada que se puede llamar a la dirección URL de hello tooresume un paso de flujo de trabajo según sea necesario.
Un asterisco (*) indica un campo obligatorio.

| Display Name (Nombre para mostrar) | Nombre de propiedad | Descripción |
| --- | --- | --- |
| Método de suscripción* |estático |Método HTTP toouse para solicitud subscribe |
| URI de suscripción* |uri |Toouse de URI de HTTP para la solicitud subscribe |
| Método de cancelación de suscripción* |estático |Toouse de método HTTP para la solicitud de cancelación de suscripción |
| URI de cancelación de suscripción* |uri |Toouse de URI de HTTP para la solicitud de cancelación de suscripción |
| Cuerpo de suscripción |body |Cuerpo de la solicitud HTTP para realizar la suscripción. |
| Encabezados de suscripción |encabezados |Encabezados de la solicitud HTTP para realizar la suscripción. |
| Autenticación de suscripción |Autenticación |Toouse de autenticación de HTTP para suscribirse. Para más información consulte el [conector HTTP](connectors-native-http.md#authentication) |
| Cuerpo de cancelación de suscripción |body |Cuerpo de la solicitud HTTP para cancelar la suscripción. |
| Encabezados de cancelación de suscripción |encabezados |Encabezados de la solicitud HTTP para cancelar la suscripción. |
| Autenticación de cancelación de suscripción |Autenticación |Toouse de autenticación de HTTP para cancelar la suscripción. Para más información consulte el [conector HTTP](connectors-native-http.md#authentication) |

**Detalles de salida**

Solicitud de webhook

| Nombre de propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| encabezados |objeto |Encabezados de la solicitud de webhook |
| body |objeto |Objeto de la solicitud de webhook |
| Código de estado |int |Código de estado de la solicitud de webhook |

## <a name="next-steps"></a>Pasos siguientes

* [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Buscar otros conectores](apis-list.md)