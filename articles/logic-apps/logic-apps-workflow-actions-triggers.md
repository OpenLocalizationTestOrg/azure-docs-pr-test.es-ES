---
title: "aaaWorkflow acciones y desencadenadores: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Acciones y desencadenadores de flujo de trabajo para Azure Logic Apps

Las aplicaciones lógicas constan de desencadenadores y acciones. Existen seis tipos de desencadenadores. Cada tipo tiene una interfaz y un comportamiento diferentes. También puede aprender sobre otros detalles examinando detalles Hola de hello [lenguaje de definición de flujo de trabajo](logic-apps-workflow-definition-language.md).  
  
Siga leyendo toolearn más información acerca de los desencadenadores, acciones y cómo puede usarlos toobuild lógica aplicaciones tooimprove los procesos empresariales y flujos de trabajo.  
  
### <a name="triggers"></a>Desencadenadores  

Un desencadenador especifica llamadas de Hola que pueden iniciar una ejecución de su flujo de trabajo de aplicación lógica. Estas son dos maneras diferentes de hello tooinitiate una ejecución del flujo de trabajo:  
  
-   Un desencadenador de sondeo  

-   Un desencadenador de inserción: por llamada hello [API de REST de servicios de flujo de trabajo](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Todos los desencadenadores contienen estos elementos de nivel superior:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Tipos de desencadenadores y sus entradas  

Puede usar estos tipos de desencadenadores:
  
-   **Solicitar** \- hace un extremo para toocall de aplicación lógica de hello  
  
-   **Periodicidad**: se desencadena en función de una programación definida.  
  
-   **HTTP**: sondea un punto de conexión web HTTP. punto de conexión de Hello HTTP debe ajustarse contrato de activación específico tooa \- mediante un 202\-patrón asincrónico, o devolviendo una matriz  
  
-   **ApiConnection** \- desencadenan sondeos como Hola HTTP, sin embargo, aprovecha las ventajas de hello [API administrada por Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- abre un extremo, similar toohello Manual desencadenador, sin embargo, llama también a tooa especifica la dirección URL tooregister y anular el registro  
  
-   **ApiConnectionWebhook** \- funciona como Hola HTTPWebhook desencadenador aprovechando las ventajas de hello API administrada por Microsoft       
    Cada tipo de desencadenador tiene un conjunto de **entradas** diferente que define su comportamiento.  
  
## <a name="request-trigger"></a>Desencadenador de solicitud  

Este desencadenador actúa como un punto de conexión que se llama a través de una solicitud HTTP tooinvoke la aplicación lógica. Un desencadenador de solicitud es similar a este ejemplo:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

También hay una propiedad opcional denominada **schema**:  
  
|Nombre del elemento|Obligatorio|Descripción|  
|----------------|------------|---------------|  
|schema|No|Un esquema JSON que valida la solicitud entrante de Hola. Resulta útil para ayudar a los pasos de flujo de trabajo posterior a saber qué tooreference de propiedades.|

tooinvoke este extremo, necesita hello toocall *listCallbackUrl* API. Consulte [API de REST de servicio de flujo de trabajo](https://docs.microsoft.com/rest/api/logic/workflows).  
  
## <a name="recurrence-trigger"></a>Desencadenador de periodicidad  

Un desencadenador de periodicidad es aquel que se ejecuta según una programación definida. Ese tipo de desencadenador podría parecerse a este ejemplo:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Como puede ver, es un toorun de manera sencilla un flujo de trabajo.  
  
|Nombre del elemento|Obligatorio|Descripción|  
|----------------|------------|---------------|  
|frequency|Sí|¿Con qué frecuencia hello desencadenador se ejecuta. Use solo uno de estos valores posibles: segundo, minuto, hora, día, semana, mes o año.|  
|interval|Sí|Intervalo de hello dada la frecuencia de repetición de Hola|  
|startTime|No|Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria.|  
|timeZone|no|Si se especifica una hora de inicio sin una diferencia horaria con UTC, se usará esta zona horaria.|  
  
También puede programar un desencadenador que se toostart ejecute en algún momento futuro Hola. Por ejemplo, si desea que toostart semanales notificar todos los lunes puede programar toostart de aplicación lógica de hello todos los lunes mediante la creación de hello después desencadenador:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>Desencadenador HTTP  

Desencadenadores HTTP sondean un extremo especificado y comprobación Hola respuesta toodetermine si se debe ejecutar el flujo de trabajo de Hola. objeto de entradas de Hello toma conjunto Hola de parámetros necesarios tooconstruct una llamada HTTP:  
  
|Nombre del elemento|Obligatorio|Descripción|Tipo|  
|----------------|------------|---------------|--------|  
|estático|yes|Puede ser uno de hello siguiendo métodos HTTP: GET, POST, PUT, HEAD, PATCH o DELETE|String|  
|uri|yes|Hola extremo http o https que se llama. 2 kilobytes como máximo.|String|  
|Consultas|No|Objeto que representa la dirección de URL de hello consulta parámetros tooadd toohello. Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.|Objeto|  
|encabezados|No|Objeto que representa cada uno de los encabezados de Hola que se envía la solicitud de toohello. Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Objeto|  
|body|No|Objeto que representa la carga de Hola que se envía el punto de conexión toohello.|Objeto|  
|retryPolicy|No|Un objeto que le permite personalizar el comportamiento de reintento de hello errores de 4xx o 5xx.|Objeto|  
|authentication|No|Método de hello representa que Hola solicitud se debe autenticar. Para más información sobre este objeto, consulte [Autenticación saliente de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Aparte del programador, hay una propiedad más admitida: `authority`. De forma predeterminada, este valor es `https://login.windows.net` cuando no se especifica, pero puede usar una audiencia diferente como `https://login.windows\-ppe.net`.|Objeto|  
  
desencadenador de Hello HTTP requiere Hola API HTTP tooconform con un toowork de modelo específico bien con la aplicación lógica. Requiere Hola siguientes campos:  
  
|Response|Descripción|  
|------------|---------------|  
|Código de estado|Código de estado 200 \(Aceptar\) toocause una ejecución. Cualquier otro código de estado no provoca una ejecución.|  
|Encabezado Retry\-after|Número de segundos hasta que la aplicación de la lógica de hello sondea extremo Hola de nuevo.|  
|Encabezado Location|Hola toocall de dirección URL en el siguiente intervalo de sondeo de Hola. Si no se especifica, se utiliza la dirección URL original de Hola.|  
  
Estos son algunos ejemplos de diferentes comportamientos para diferentes tipos de solicitudes:  
  
|Response code|Retry\-After|Comportamiento|  
|-----------------|----------------|------------|  
|200|\(Ninguna\)|No es un desencadenador válido, reintento\-After es motor Hola necesario; de lo contrario nunca sondea la siguiente solicitud de Hola.|  
|202|60|No se desencadenará el flujo de trabajo de Hola. próximo intento de Hola se realiza en un minuto.|  
|200|10|Ejecutar el flujo de trabajo de Hola y comprobar de nuevo para el contenido de más de 10 segundos.|  
|400|\(Ninguna\)|No se ejecutan el flujo de trabajo de hello, si la solicitud es incorrecta. Si no hay ningún **directiva de reintentos** definido, a continuación, se utiliza la directiva predeterminada de Hola. Una vez alcanzado el número de Hola de reintentos, el desencadenador de hello ya no es válido.|  
|500|\(Ninguna\)|Error del servidor, no se ejecutan el flujo de trabajo de Hola.  Si no hay ningún **directiva de reintentos** definido, a continuación, se utiliza la directiva predeterminada de Hola. Una vez alcanzado el número de Hola de reintentos, el desencadenador de hello ya no es válido.|  
  
salidas de Hola de un desencadenador HTTP ser similar a este ejemplo:  
  
|Nombre del elemento|Descripción|Tipo|  
|----------------|---------------|--------|  
|encabezados|encabezados de Hola de respuesta de http de Hola.|Objeto|  
|body|cuerpo de Hola de respuesta de http de Hola.|Objeto|  
  
## <a name="api-connection-trigger"></a>Desencadenador de conexión de API  

Hola API conexión desencadenador es similar toohello HTTP en su funcionalidad básica. Sin embargo, los parámetros de Hola para identificar la acción de hello son diferentes. Aquí tiene un ejemplo:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Nombre del elemento|Obligatorio|Tipo|Descripción|  
|----------------|------------|--------|---------------|  
|host|Sí||Hola ApiApp había hospedado puerta de enlace y el identificador.|  
|estático|Sí|String|Puede ser uno de hello siguiendo métodos HTTP: **obtener**, **POST**, **colocar**, **eliminar**, **PATCH**, o  **HEAD**|  
|Consultas|No|Objeto|Toobe de parámetros de consulta de hello representa agrega dirección URL de toohello. Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.|  
|encabezados|No|Objeto|Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello. Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Objeto|Representa la carga de Hola que se envía el punto de conexión toohello.|  
|retryPolicy|No|Objeto|Permite el comportamiento para reintentar hello toocustomize errores de 4xx o 5xx.|  
|Autenticación|No|Objeto|Método de hello representa que Hola solicitud se debe autenticar. Para más información sobre este objeto, consulte [Autenticación saliente de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).|  
  
propiedades de Hola para host son:  
  
|Nombre del elemento|Obligatorio|Descripción|  
|----------------|------------|---------------|  
|api runtimeUrl|Sí|punto de conexión de Hola de hello API administrada.|  
|connection name||Debe ser un parámetro de referencia tooa llamado `$connection` y es el nombre de Hola de conexión de API de hello administrado que Hola usos de flujo de trabajo.|
  
salidas de Hola de un desencadenador de conexión de API son:
  
|Nombre del elemento|Tipo|Descripción|  
|----------------|--------|---------------|  
|encabezados|Objeto|encabezados de Hola de respuesta de http de Hola.|  
|body|Objeto|cuerpo de Hola de respuesta de http de Hola.|  
  
## <a name="httpwebhook-trigger"></a>Desencadenador HTTPWebhook  

Aperturas de desencadenador de Hello HTTPWebhook un punto de conexión, desencadenador manual de toohello similares, pero hello HTTPWebhook desencadenador también llama a tooa especifica la dirección URL tooregister y anular el registro. Este es un ejemplo del aspecto que podría tener un desencadenador HTTPWebhook:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Muchas de estas secciones son opcionales y comportamiento de Hola de hello Webhook depende de qué secciones se proporciona o se omite.  
propiedades de Hola de un Webhook son los siguientes:  
  
|Nombre del elemento|Obligatorio|Descripción|  
|----------------|------------|---------------|  
|subscribe|No|Hola solicitud que se llama al desencadenador de Hola se crea y realiza el registro inicial del Hola de salida.|  
|unsubscribe|No|Hola solicitud de salida cuando se elimina el desencadenador de Hola.|  
  
-   **Suscribirse** Hola salida llamada que ha realizado toostart escucha tooevents. Esta llamada se inicia con hello es el mismo conjunto de parámetros que Hola acciones HTTP normales. Esta llamada saliente se realiza cualquier Hola tiempo cambios de flujo de trabajo de cualquier manera, por ejemplo, siempre que las credenciales de Hola se revierten y el cambio de parámetros de entrada del desencadenador de Hola.
  
    toosupport esta llamada, hay una nueva función: `@listCallbackUrl()`. Esta función devuelve una dirección URL única para este desencadenador específico en este flujo de trabajo. Que representa el identificador único de Hola para los extremos de Hola que utilizan Hola REST de servicio.  
  
-   **Unsubscribe** se llama cuando una operación representa este desencadenador como no válido, lo que incluye:  
  
    -   Eliminar o deshabilitar el desencadenador de Hola  
  
    -   Eliminación o deshabilitación de flujo de trabajo de Hola  
  
    -   Eliminar o deshabilitar la suscripción de Hola  
  
    aplicación de la lógica de Hello llama automáticamente a Hola acción Cancelar la suscripción. Hola parámetros de función toothis Hola igual como desencadenador de hello HTTP.  
  
    Hello salidas de desencadenador de hello HTTPWebhook son contenido de saludo de solicitud entrante de hello:  
  
|Nombre del elemento|Tipo|Descripción|  
|-----------------|--------|---------------|  
|encabezados|Objeto|encabezados de saludo de solicitud de http de Hola.|  
|body|Objeto|cuerpo de saludo de solicitud de http de Hola.|  

Se pueden especificar límites en una acción de webhook en hello misma manera que [HTTP asincrónica límites](#asynchronous-limits).
  

## <a name="conditions"></a>Condiciones  

Para cualquier desencadenador, puede usar uno o más toodetermine condiciones si debe ejecutar el flujo de trabajo de Hola o no. Por ejemplo:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

En este caso, Hola desencadenadores solo de informe del flujo de trabajo de hello `sendReports` parámetro se establece tootrue. Por último, las condiciones pueden hacer referencia a código de estado de Hola de desencadenador de Hola. Por ejemplo, podría iniciar un flujo de trabajo solo cuando su sitio web devuelva un código de estado 500, como se indica a continuación:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Cuando hace referencia a cualquier expresión de código de estado de Hola de desencadenador de hello \(de ninguna manera\), Hola comportamiento predeterminado \(desencadenador solo en 200 \(Aceptar\) \) se reemplaza. Por ejemplo, si desea tootrigger de código de estado 200 y el código de estado 201, tendrá que tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` como la condición.  
  
## <a name="start-multiple-runs-for-a-request"></a>Inicio de varias ejecuciones para una solicitud

tookick desactivar varias ejecuciones para una única solicitud `splitOn` es útil, por ejemplo, cuando se desea toopoll un punto de conexión que puede tener varios elementos nuevos entre los intervalos de sondeo.
  
Con `splitOn`, especificar propiedad Hola dentro de la carga de respuesta de Hola que contiene la matriz de Hola de elementos, cada uno de los cuales desea toouse toostart una ejecución del desencadenador de Hola. Por ejemplo, imagine que tiene una API que devuelve Hola después de respuesta:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
La lógica de aplicación solo necesita contenido de filas de hello, por lo que puede crear el desencadenador como en este ejemplo:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
A continuación, en la definición de flujo de trabajo de hello `@triggerBody().name` devuelve `mycoolrow` para hello ejecuta por primera vez, y `another row` para la segunda ejecución de Hola. Hola desencadenador salidas aspecto mostrado en este ejemplo:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Por tanto, si usas `SplitOn`, no se puede obtener propiedades de Hola que están fuera de la matriz de hello, en este caso, hello `Status` campo.  
  
> [!NOTE]  
> En este ejemplo, utilizamos hello `?` tooavoid capaz de operador toobe un error si hello `Rows` propiedad no está presente. 
  
## <a name="single-run-instance"></a>Instancia de ejecución única

Puede configurar desencadenadores que tengan un incendio de periodicidad propiedad tooonly si han completado todas las ejecuciones activas. Si se produce una periodicidad programada mientras hay una ejecución en curso, el desencadenador de hello omite y espera hasta Hola siguiente repetición programada intervalo toocheck nuevo.

Puede configurar a través de opciones de la operación de hello:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Tipos y entradas  

Hay muchos tipos de acciones, cada una con un comportamiento único. Las acciones de colección pueden contener muchas otras acciones dentro de sí mismas.

### <a name="standard-actions"></a>Acciones estándar  

-   **HTTP**: esta acción llama a un punto de conexión web HTTP.  
  
-   **ApiConnection** \- esta acción se comporta como Hola acción HTTP, pero usa Hola API administrada por Microsoft.  
  
-   **ApiConnectionWebhook** \- como HTTPWebhook, pero utiliza Hola API administrada por Microsoft.  
  
-   **Response**: esta acción define una respuesta para una llamada entrante.  
  
-   **Wait**: esta acción simple espera una cantidad fija de tiempo o hasta una hora específica.  
  
-   **Workflow**: esta acción representa un flujo de trabajo anidado.  

-   **Función**: esta acción representa una función de Azure.

### <a name="collection-actions"></a>Acciones de colección

-   **Scope**: esta acción es una agrupación lógica de otras acciones.

-   **Condición** \- esta acción evalúa una expresión y ejecuta la bifurcación de resultado de hello correspondiente.

-   **ForEach**\-: esta acción de bucle recorre en iteración una matriz y realiza acciones internas para cada elemento.

-   **Hasta que** \- esta acción bucle ejecuta acciones internas hasta que una condición da como resultado tootrue.
  
Cada tipo de acción tiene un conjunto diferente de **entradas** que definen el comportamiento de la acción.  
  
## <a name="http-action"></a>Acción HTTP  

Acciones HTTP llamar a un punto de conexión especificada y comprobación Hola respuesta toodetermine si se debe ejecutar el flujo de trabajo de Hola. Hola **entradas** objeto toma conjunto Hola de parámetros necesarios tooconstruct Hola HTTP llamada:  
  
|Nombre del elemento|Obligatorio|Tipo|Descripción|  
|----------------|------------|--------|---------------|  
|estático|Sí|String|Puede ser uno de hello siguiendo métodos HTTP: **obtener**, **POST**, **colocar**, **eliminar**, **PATCH**, o  **HEAD**|  
|uri|Sí|String|Hola extremo http o https que se llama. La longitud máxima es de 2 kilobytes.|  
|Consultas|No|Objeto|Representa la URL de hello consulta parámetros tooadd toohello. Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.|  
|encabezados|No|Objeto|Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello. Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Objeto|Representa la carga de Hola que se envía el punto de conexión toohello.|  
|retryPolicy|No|Objeto|Le permite personalizar el comportamiento de reintento de hello errores de 4xx o 5xx.|  
|operationsOptions|No|String|Define el conjunto de Hola de toooverride comportamientos especiales.|  
|Autenticación|No|Objeto|Método de hello representa que Hola solicitud se debe autenticar. Para más información sobre este objeto, consulte [Autenticación saliente de Scheduler](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Aparte de scheduler, hay una propiedad más que se admite: `authority`. De forma predeterminada, es `https://login.windows.net` cuando no se especifica, pero se puede usar una audiencia diferente como `https://login.windows\-ppe.net`.|  
  
Las acciones HTTP \(y las acciones de conexión de API\) admiten directivas de reintentos. Una directiva de reintentos aplica a los errores toointermittent, caracterizados como código de estado HTTP 408 y 429, 5xx, excepciones de conectividad de tooany de suma de los códigos. Esta directiva se describe mediante hello *retryPolicy* objeto definido como se muestra aquí:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
intervalo de reintento de saludo se especifica en formato ISO 8601 Hola. Este intervalo tiene un valor predeterminado y el valor mínimo de 20 segundos, mientras el valor máximo de hello es una hora. Hola predeterminado y máximo de reintentos son cuatro horas. Si no se especificó la definición de directiva de reintento de hello, un `fixed` estrategia se usa con valores de recuento y el intervalo de reintento predeterminados. Directiva de reintentos de hello toodisable, establezca su tipo demasiado`None`.  
  
Por ejemplo, hello acción siguiente vuelve obteniendo noticias más recientes de hello dos veces, si hay errores intermitentes, para un total de tres ejecuciones, con un retraso de 30 segundos entre cada intento de:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Patrones asincrónicos

De forma predeterminada, todas las acciones basadas en HTTP admiten el patrón estándar de operación asincrónica de Hola. Por lo que si el servidor remoto de Hola indica que la solicitud hello es aceptado para su procesamiento con un 202 \(aceptado\) respuesta, motor de Logic Apps Hola mantiene sondeo URL Hola especificada en el encabezado de ubicación de la respuesta de hello hasta alcanzar un terminal estado \(un no\-respuesta 202\).  
  
comportamiento asincrónico de hello toodisable previamente descrito, establezca un `DisableAsyncPattern` opción en entradas de la acción de Hola. En este caso, la salida de hello de acción de Hola se basa en hello inicial 202 respuesta Hola servidor.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Límites asincrónicos

Un patrón asincrónico puede estar limitado en su intervalo de tiempo específico de tooa de duración.  Si el intervalo de tiempo de hello transcurre sin que se alcance un estado terminal, se marcarán estado Hola de acción de hello `Cancelled` con el código `ActionTimedOut`.  tiempo de espera de Hello límite se especifica en formato ISO 8601.  Límites se pueden especificar con la sintaxis de hello:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>API Connection  

API Connection es una acción que hace referencia a un conector administrado por Microsoft.
Esta acción requiere una conexión válida de tooa de referencia y obtener información sobre la API de Hola y los parámetros requeridos.

|Nombre del elemento|Obligatorio|Tipo|Descripción|  
|----------------|------------|--------|---------------|  
|host|Sí|Objeto|Representa la información de conector de hello como objeto de conexión de toohello de referencia y runtimeUrl Hola|
|estático|Sí|String|Puede ser uno de hello siguiendo métodos HTTP: **obtener**, **POST**, **colocar**, **eliminar**, **PATCH**, o  **HEAD**|  
|path|Sí|String|ruta de acceso de Hola de operación de hello API.|  
|Consultas|No|Objeto|Representa la URL de hello consulta parámetros tooadd toohello. Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.|  
|encabezados|No|Objeto|Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello. Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Objeto|Representa la carga de Hola que se envía el punto de conexión toohello.|  
|retryPolicy|No|Objeto|Le permite personalizar el comportamiento de reintento de hello errores de 4xx o 5xx.|  
|operationsOptions|No|String|Define el conjunto de Hola de toooverride comportamientos especiales.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>Acción Webhook de API Connection

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

Se pueden especificar límites en una acción de webhook en hello misma manera que [HTTP asincrónica límites](#asynchronous-limits).
  
## <a name="response-action"></a>Acción de respuesta  

Este tipo de acción contiene la carga de respuesta completo Hola de una solicitud HTTP e incluye un statusCode, cuerpo y encabezados:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
acción de respuesta de Hello tiene restricciones especiales que no son aplicables a las acciones de tooother. Concretamente:  
  
-   Las acciones de respuesta no pueden ser paralelas en una definición de porque es necesaria una solicitud entrante de toohello de respuesta determinista.  
  
-   Si se alcanza una acción de respuesta después de solicitud entrante de hello ha recibido una respuesta, la acción de Hola se considera no se pudo \(conflicto\), y como resultado, es Hola ejecutar `Failed`.  
  
-   Un flujo de trabajo con acciones de respuesta no puede tener `splitOn` en su desencadenador porque una llamada provoca muchas ejecuciones. Como resultado, esto se debe validar al flujo de hello es PUT y causa una solicitud incorrecta.  
  
## <a name="wait-action"></a>Acción Wait  

Hola `wait` acción suspende la ejecución de flujo de trabajo para el intervalo especificado de saludo. Por ejemplo, toowait 15 minutos, puede usar este fragmento de código:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
O bien, toowait hasta un momento específico en el tiempo, puede utilizar este ejemplo:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> duración de la espera de Hello puede especificarse ya sea mediante hello **intervalo** objeto o hello **hasta** objeto, pero no ambos.  
  
|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|interval|No|Objeto|duración en función de la cantidad de tiempo de espera de Hola.|  
|interval unit|Sí|string|Uno de estos intervalos: segundo, minuto, hora, día, semana, mes o año.|  
|interval count|Sí|String|Duración en función de hello unidad interna proporcionada.|  
|until|No|Objeto|duración en función de un punto en el tiempo de espera de Hola.|  
|until timestamp|Sí|String|Cadena &#124; Hola punto en el tiempo en UTC cuando Hola espera expira.|  

## <a name="query-action"></a>Acción de consulta

Hola `query` acción le permite filtrar una matriz basada en una condición. Por ejemplo, tooselect un número superior a 2, puede usar:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

Hola salida de hello `query` acción es una matriz que tiene elementos de matriz de entrada de Hola que satisfacen la condición de Hola.

> [!NOTE]
> Si no hay valores satisfacen hello `where` condición, hello resultado es una matriz vacía.

|Nombre|Obligatorio|Tipo|Descripción|
|--------|------------|--------|---------------|
|De|Sí|Matriz|matriz de origen Hola.|
|donde|Sí|String|Hola condition tooapply tooeach, elemento de matriz de origen Hola.|

## <a name="select-action"></a>Acción Select

Hola `select` acción permite proyectar cada elemento de una matriz con un nuevo valor.
Por ejemplo, tooconvert una matriz de números en una matriz de objetos, puede usar:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

Hola salida de hello `select` acción es una matriz cuya Hola misma cardinalidad Hola matriz de entrada, con cada elemento transformada según lo definido por hello `select` propiedad. Si la entrada de hello es una matriz vacía, salida de hello también es una matriz vacía.

|Nombre|Obligatorio|Tipo|Descripción|
|--------|------------|--------|---------------|
|De|Sí|Matriz|matriz de origen Hola.|
|select|Sí|Cualquiera|elemento de Hello proyección tooapply tooeach de matriz de origen Hola.|

## <a name="terminate-action"></a>Acción Terminate

Hola acción terminar detiene la ejecución de Hola y flujo de trabajo ejecutar, anular cualquier acción en curso, omitiendo las acciones restantes. Por ejemplo, tooterminate una ejecución con el estado **error**, puede usar Hola siguiente fragmento de código:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Hola no afecta a las acciones que ya ha completado terminar la acción.

|Nombre|Obligatorio|Tipo|Descripción|
|--------|------------|--------|---------------|
|runStatus|Sí|String|destino de Hello estado de ejecución. **Failed** o **Cancelled**.|
|runError|No|Objeto|Detalles del error Hola. Solo es compatible cuando **runStatus** se establece demasiado**error**.|
|runError code|No|String|Hola ejecutar código de error.|
|runError message|No|String|Hola ejecutar el mensaje de error.|

## <a name="compose-action"></a>Acción Compose

Hola redactar acción le permite construir un objeto arbitrario. salida de Hello de hello redactar acción es resultado de hello de evaluar sus entradas. Por ejemplo, puede usar hello crear salidas de toomerge de acción de varias acciones:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Hola **redactar** acción puede ser usado tooconstruct ningún resultado, incluidos objetos, matrices y cualquier otro tipo de lógica de aplicaciones como XML y binario lo admitidos de forma nativa.

## <a name="table-action"></a>Acción Table

Hola `table` permite tooconvert una matriz de elementos en una **CSV** o **HTML** tabla.

Si @triggerBody() es

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

Y deje que la acción de Hola se define como

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

Hola anterior generaría

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>apples</td></tr><tr><td>1</td><td>oranges</td></tr></tbody></table>"

En la tabla de orden toocustomize hello, puede especificar las columnas de hello explícitamente. Por ejemplo:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

Hola anterior generaría

<table><thead><tr><th>produce id</th><th>Description</th></tr></thead><tbody><tr><td>0</td><td>fresh apples</td></tr><tr><td>1</td><td>fresh oranges</td></tr></tbody></table>"

Si hello `from` valor de la propiedad es una matriz vacía, la salida de hello es una tabla vacía.

|Nombre|Obligatorio|Tipo|Descripción|
|--------|------------|--------|---------------|
|De|Sí|Matriz|matriz de origen Hola.|
|formato|Sí|String|Hola formato, ya sea **CSV** o **HTML**.|
|columnas|No|Matriz|columnas de Hola. Permite la forma de toooverride Hola predeterminada de la tabla de Hola.|
|column header|No|String|encabezado de Hola de columna de Hola.|
|column value|Sí|String|valor de Hola de columna de Hola.|

## <a name="workflow-action"></a>Acción Workflow   

|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|host id|Sí|String|Identificador de recurso de Hola de flujo de trabajo de Hola que quieres toocall.|  
|host triggerName|Sí|String|nombre de Hola de desencadenador de Hola que desea tooinvoke.|  
|Consultas|No|Objeto|Representa la URL de hello consulta parámetros tooadd toohello. Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.|  
|encabezados|No|Objeto|Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello. Por ejemplo, idioma de hello tooset y el tipo en una solicitud:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Objeto|Representa la carga de hello enviado toohello extremo.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Se realiza una comprobación de acceso en el flujo de trabajo de hello \(más específicamente, desencadenador de hello\), lo que significa que necesita tener acceso a toohello flujo de trabajo.  
  
Hola salidas de hello `workflow` acción se basan en la que define en hello `response` acción en el flujo de trabajo de hello secundario. Si no ha definido alguno `response` acción y, a continuación, salidas de hello están vacíos.  

## <a name="function-action"></a>Acción de la función   

|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|function id|Sí|String|Hola Id. de recurso de función hello que desea tooinvoke.|  
|estático|No|String|Hola método HTTP utiliza la función de hello tooinvoke. De forma predeterminada, es `POST` cuando no se especifica.|  
|Consultas|No|Objeto|Representa la URL de hello consulta parámetros tooadd toohello. Por ejemplo, `"queries" : { "api-version": "2015-02-01" }` agrega `?api-version=2015-02-01` toohello URL.|  
|encabezados|No|Objeto|Representa cada uno de los encabezados de Hola que se envía la solicitud de toohello. Por ejemplo, el idioma de hello tooset y el tipo en una solicitud: `"headers" : { "Accept-Language": "en-us" }`.|  
|body|No|Objeto|Representa la carga de hello enviado toohello extremo.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Cuando se guarda la aplicación de la lógica de hello, realizamos algunas comprobaciones de la función hello al que hace referencia:
-   Se necesita la función de toohello de acceso de toohave.
-   Solo se permite el desencadenador HTTP estándar o webhook JSON genérico.
-   No debe tener ninguna ruta definida.
-   Solo se permite el nivel de autorización "function" y "anonymous".

dirección URL de desencadenador de Hello recuperan, almacenado en memoria caché y utiliza en tiempo de ejecución. Por lo que si cualquier operación invalida la dirección URL de hello en caché, se produce un error en la acción de hello en tiempo de ejecución. toowork evitar este problema, guarde Hola aplicación lógica de nuevo, lo que provocará tooretrieve de aplicación lógica y almacenar en caché URL de desencadenador de hello nuevo.

## <a name="collection-actions-scopes-and-loops"></a>Acciones de colección (ámbitos y bucles)

Algunos tipos de acciones pueden contener acciones dentro de sí mismas. Pueden hacer referencia a acciones de referencia dentro de una colección directamente fuera de la colección de Hola. Si ha definido `http` en un ámbito, `@body('http')` sigue siendo válido en cualquier parte de un flujo de trabajo. Las acciones dentro de una colección pueden `runAfter` solo otras acciones en Hola misma colección.

## <a name="scope-action"></a>Acción Scope

Hola `scope` acción permite lógicamente agrupar acciones en un flujo de trabajo.

|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|actions|Sí|Objeto|Acciones interna tooexecute ámbito Hola|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>Acción ForEach

Esta acción de bucle recorre en iteración una matriz y realiza acciones internas para cada elemento. De forma predeterminada, bucle foreach de Hola se ejecuta en paralelo (20 ejecuciones en paralelo a la vez). Puede establecer reglas de ejecución con hello `operationOptions` parámetro.

|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|actions|Sí|Objeto|Tooexecute acciones interna en el bucle de Hola|
|foreach|Sí|cadena|Hola matriz tooiterate sobre|
|operationOptions|no|string|Las opciones de comportamiento de la operación. Actualmente sólo admite `sequential` tooexecute iteraciones secuencialmente (comportamiento predeterminado es paralelo)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Acción Until

Esta acción bucle ejecuta acciones internas hasta que una condición da como resultado tootrue.

|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|actions|Sí|Objeto|Tooexecute acciones interna en el bucle de Hola|
|expresión|Sí|cadena|Hola tooevaluate expresión después de cada iteración|
|limit|yes|Objeto|se deben definir límites de Hola de bucle de hello - al menos un límite|
|count|no|int|Hola limitar toohello el número de iteraciones que se pueden realizar|
|timeout|no|cadena|tiempo de espera de Hola de cuánto tiempo debe entrar en bucle.  Formato ISO 8601|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Condiciones: acción If

Hola `If` acción le permite evaluar una condición y ejecutar una rama en función de si la expresión de Hola se evalúa como demasiado`true`.

|Nombre|Obligatorio|Tipo|Descripción|  
|--------|------------|--------|---------------|  
|actions|Sí|Objeto|Acciones interna tooexecute cuando la expresión se evalúa como demasiado`true`|
|expresión|Sí|cadena|Hola expresión tooevaluate|
|else|no|Objeto|Acciones interna tooexecute cuando la expresión se evalúa como demasiado`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Hello tabla siguiente muestra ejemplos de cómo condiciones pueden utilizarse expresiones en una acción:  
  
|Valor JSON|Resultado|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Cualquier valor que se evaluaría tootrue hace que esta condición toopass. Solo se admiten expresiones de tipo Boolean. tooconvert otro tipos tooBoolean, utilizar funciones `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Se admiten funciones de comparación. Para este ejemplo de Hola, acción de hello solo se ejecuta cuando la salida de hello de act1 es mayor que el umbral de Hola.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Las funciones de lógica son también compatible toocreate anidar expresiones booleanas. En este caso, acción de Hola se ejecuta cuando la salida de hello de act1 esté por encima del umbral de Hola o por debajo de 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Puede usar toocheck de funciones de matriz si una matriz tiene todos los elementos. En este caso, la acción de hello ejecuta cuando Hola errores matriz está vacía.| 
|`"expression": "parameters('hasSpecialAction')"`|Error: no es una condición válida porque se requiere @ para las condiciones.|  
  
Si una condición se evalúa correctamente, la condición de hello está marcada como `Succeeded`. Las acciones dentro de cualquier hello `actions` o `else` objetos evaluación demasiado`Succeeded` cuando se ejecuta y se realizó correctamente, `Failed` cuando se ejecuta y no se pudo, o `Skipped` cuando no se ejecuta esa rama.

## <a name="next-steps"></a>Pasos siguientes

[API de REST de Servicio de flujo de trabajo](https://docs.microsoft.com/rest/api/logic/workflows)
