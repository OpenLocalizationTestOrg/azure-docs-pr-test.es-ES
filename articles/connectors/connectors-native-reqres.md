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
# <a name="get-started-with-hello-request-and-response-components"></a>Empezar a trabajar con componentes de solicitud y respuesta de Hola
Con hello solicitud y respuesta componentes en una aplicación de lógica, puede responder en tiempo real tooevents.

Por ejemplo, puede:

* Responder tooan solicitud HTTP con los datos desde una base de datos local a través de una aplicación de lógica.
* Desencadenar una aplicación lógica desde un evento webhook externo.
* Llamar a una aplicación lógica con una acción de solicitud y respuesta desde otra aplicación lógica.

tooget a usar acciones de solicitud y respuesta de hello en una aplicación de lógica, consulte [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-request-trigger"></a>Usar hello desencadenador de solicitud HTTP
Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica. [Más información sobre los desencadenadores](connectors-overview.md).

Aquí es una secuencia de ejemplo de cómo solicitar tooset seguridad HTTP Hola diseñador la lógica de aplicación.

1. Agregar desencadenador de hello **solicitar - se recibe la solicitud HTTP de un cuando** en la aplicación lógica. También puede proporcionar un esquema JSON (mediante el uso de una herramienta como [JSONSchema.net](http://jsonschema.net)) para el cuerpo de la solicitud de saludo. Esto permite hello toogenerate diseñador símbolos (tokens) para las propiedades de solicitud de hello HTTP.
2. Agregar otra acción para que pueda guardar aplicación lógica de hello.
3. Después de guardar la aplicación de la lógica de hello, puede obtener la dirección URL de solicitud de hello HTTP de tarjeta de solicitud de Hola.
4. Una solicitud HTTP POST (puede utilizar una herramienta como [Postman](https://www.getpostman.com/)) desencadenadores de la dirección URL de toohello Hola aplicación lógica.

> [!NOTE]
> Si no define una acción de respuesta, un `202 ACCEPTED` respuesta se devuelve inmediatamente toohello autor de la llamada. Puede usar toocustomize de acción de respuesta de hello una respuesta.
> 
> 

![Desencadenador de respuesta](./media/connectors-native-reqres/using-trigger.png)

## <a name="use-hello-http-response-action"></a>Usar hello acción de respuesta HTTP
Hola acción de respuesta HTTP solo es válido cuando se usa en un flujo de trabajo activado por una solicitud HTTP. Si no define una acción de respuesta, un `202 ACCEPTED` respuesta se devuelve inmediatamente toohello autor de la llamada.  Puede agregar una acción de respuesta en cualquier paso en el flujo de trabajo de Hola. aplicación de la lógica de Hello solo mantiene solicitud entrante de hello abierto durante un minuto para una respuesta.  Después de un minuto, si no hay respuesta fue enviada desde el flujo de trabajo de hello (y existe una acción de respuesta en la definición de hello), un `504 GATEWAY TIMEOUT` se devuelve toohello autor de la llamada.

Le mostramos cómo tooadd una acción de respuesta HTTP:

1. Seleccione hello **nuevo paso** botón.
2. Elija **Add an action**(Agregar una acción).
3. En el cuadro de búsqueda de la acción de hello, escriba **respuesta** hello toolist acción de respuesta.
   
    ![Seleccione la acción de respuesta de Hola](./media/connectors-native-reqres/using-action-1.png)
4. Agregue todos los parámetros que son necesarios para el mensaje de respuesta HTTP de saludo.
   
    ![Acción de respuesta de hello completa](./media/connectors-native-reqres/using-action-2.png)
5. Haga clic en la esquina superior izquierda de Hola de hello toosave de barra de herramientas y la lógica aplicación guardará ambos y publicar (activar).

## <a name="request-trigger"></a>Desencadenador de solicitud
A continuación encontrará los detalles de Hola de desencadenador de hello admitido por este conector. Solo existe un único desencadenador de solicitud.

| Desencadenador | Description |
| --- | --- |
| Solicitud |Se produce cuando se recibe una solicitud HTTP. |

## <a name="response-action"></a>Acción de respuesta
A continuación encontrará los detalles de hello para la acción de hello admitido por este conector. Hay una única de acción de respuesta que solo puede usarse acompañada de un desencadenador de solicitud.

| Acción | Description |
| --- | --- |
| Response |Devuelve que una respuesta toohello correlacionado solicitud HTTP |

### <a name="trigger-and-action-details"></a>Detalles de los desencadenadores y las acciones
Hello en las tablas siguientes se describen los campos de entrada de hello para el desencadenador de Hola y acción y Hola detalles de salida correspondiente.

#### <a name="request-trigger"></a>Desencadenador de solicitud
Hola aquí te mostramos un campo de entrada de desencadenador de Hola de una solicitud HTTP entrante.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Esquema JSON |schema |esquema JSON de Hola Hola HTTP del cuerpo de solicitud |

<br>

**Detalles de salida**

siguiente Hola es detalles de salida de solicitud de saludo.

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| encabezados |objeto |Encabezados de solicitud |
| Cuerpo |objeto |Objeto de solicitud |

#### <a name="response-action"></a>Acción de respuesta
los siguientes Hola son campos de entrada para hello acción de respuesta HTTP. Un * significa que es un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Código de estado* |statusCode |Hola código de estado HTTP |
| Encabezados |encabezados |Un objeto JSON de cualquier tooinclude de encabezados de respuesta |
| Cuerpo |body |cuerpo de respuesta de Hola |

## <a name="next-steps"></a>Pasos siguientes
Ahora, pruebe plataforma hello y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md). Puede explorar Hola otros conectores disponibles en las aplicaciones lógicas examinando nuestro [lista de las API](apis-list.md).

