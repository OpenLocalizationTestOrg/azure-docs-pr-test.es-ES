---
title: "aaaError & control de excepciones: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: Patrones para el control de errores y excepciones en Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Control de errores y excepciones en Azure Logic Apps

Aplicaciones lógicas de Azure proporciona completas herramientas y toohelp de patrones Asegúrese de que sus integraciones son sólido y flexible frente a errores. Cualquier arquitectura de integración supone Hola desafío de hacer que el tiempo de inactividad del identificador de tooappropriately seguro o problemas de sistemas dependientes. Control de errores de lógica aplicaciones facilita una experiencia de primera clase, lo que le otorga Hola herramientas necesita tooact en excepciones y errores en los flujos de trabajo.

## <a name="retry-policies"></a>Directivas de reintentos

Una directiva de reintentos es tipo más básico de Hola de excepciones y control de errores. Si una solicitud inicial agotó el tiempo o no se pudo (cualquier solicitud que da como resultado un 429 o una respuesta 5xx), esta directiva define si debería volver a intentar la acción de Hola. De forma predeterminada, todas las acciones se reintentan 4 veces adicionales durante intervalos de 20 segundos. Por tanto, si recibe la primera solicitud de hello un `500 Internal Server Error` respuesta, el motor de flujo de trabajo de Hola se detiene durante 20 segundos y los intentos de Hola solicitud de nuevo. Si después de todos los reintentos, respuesta de hello sigue siendo una excepción o error, continúa de flujo de trabajo de Hola y Hola de marcas de estado de la acción como `Failed`.

Puede configurar directivas de reintento de hello **entradas** para una acción concreta. Por ejemplo, puede configurar una tootry de directiva de reintento hasta 4 veces en intervalos de 1 hora. Para ver detalles completos sobre las propiedades de entrada, consulte [Workflow Actions and Triggers][retryPolicyMSDN] (Acciones y desencadenadores de flujo de trabajo).

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Si deseara su tooretry de acción HTTP 4 veces y espere 10 minutos entre cada intento, usaría Hola siguiente definición:

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

Para obtener más información sobre la sintaxis admitida, vea hello [sección Directiva de reintentos en desencadenadores y acciones de flujo de trabajo][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Detectar errores con hello RunAfter propiedad

Cada acción de aplicación lógica declara qué acciones deben finalizar antes de que empiece de acción de hello, como clasificación pasos hello en el flujo de trabajo. En la definición de la acción de hello, esta clasificación se denomina hello `runAfter` propiedad. Esta propiedad es un objeto que describe qué acciones y Estados de acción ejecutan la acción de Hola. De forma predeterminada, todas las acciones agregadas a través de hello diseñador la lógica de aplicación se establecen demasiado`runAfter` paso anterior de hello si hello paso anterior `Succeeded`. Sin embargo, puede personalizar esta acciones de toofire valor cuando las acciones anteriores tienen `Failed`, `Skipped`, o un conjunto posibles de estos valores. Si deseara tooadd un tooa elemento designado tema de Bus de servicio después de una acción específica `Insert_Row` se produce un error, podría utilizar Hola después `runAfter` configuración:

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

Hola aviso `runAfter` propiedad se establece toofire si hello `Insert_Row` acción es `Failed`. acción de hello toorun si es el estado de la acción de hello `Succeeded`, `Failed`, o `Skipped`, use esta sintaxis:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Las acciones que se ejecutan y completan correctamente después de que una acción anterior haya producido error se marcan como `Succeeded`. Este comportamiento significa que si se correctamente catch todos los errores en un flujo de trabajo, Hola ejecutarse está marcada como `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Acciones de tooevaluate ámbitos y resultados

Toohow similar puede ejecutar después de acciones individuales, también puede agrupar acciones entre sí dentro de un [ámbito](../logic-apps/logic-apps-loops-and-scopes.md), que actúan como una agrupación lógica de acciones. Los ámbitos son útiles para organizar las acciones de aplicación lógica y para realizar evaluaciones agregadas en estado de Hola de un ámbito. ámbito de Hello propia recibe un estado una vez han terminado todas las acciones en un ámbito. el estado del ámbito de Hola se determina con hello mismos criterios como una ejecución. Si Hola acción final en una bifurcación de la ejecución es `Failed` o `Aborted`, estado de hello es `Failed`.

toofire acciones específicas para los errores que se produjeron en el ámbito de hello, puede usar `runAfter` con un ámbito que está marcado como `Failed`. Si *cualquier* producirá un error en las acciones en el ámbito de hello, ejecutándose después de que se produce un error en un ámbito permite crear una sola acción toocatch errores.

### <a name="getting-hello-context-of-failures-with-results"></a>Introducción al contexto de Hola de errores con resultados

Aunque es útil detectar errores de un ámbito, puede que le interese toohelp contexto que entender exactamente qué acciones de error, y los errores o los códigos de estado que se devolvieron. Hola `@result()` función de flujo de trabajo proporciona contexto sobre el resultado de hello de todas las acciones en un ámbito.

`@result()`toma un único parámetro, el nombre de ámbito y devuelve una matriz de todos los resultados de acción de Hola desde dentro de ese ámbito. Estos objetos de acción incluyen hello mismo atributos como hello `@actions()` genera el objeto, incluidos la hora de inicio de la acción, hora de finalización de la acción, estado de la acción, entradas de la acción, identificador de correlación de acción y acción. contexto de toosend de todas las acciones que no se pudo dentro de un ámbito, puede emparejar fácilmente un `@result()` funcionando con un `runAfter`.

tooexecute una acción *para cada* acción en un ámbito que `Failed`, matriz de Hola de filtro de resultados tooactions que han resultado erróneas, puede emparejar `@result()` con un  **[filtro matriz](../connectors/connectors-native-query.md)**  acción y un  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  bucle. Puede tomar la matriz de resultados filtrado hello y realizar una acción para cada error mediante hello **ForEach** bucle. Este es un ejemplo, seguido por una explicación detallada, que envía una solicitud HTTP POST con el cuerpo de respuesta de Hola de todas las acciones que no se pudo ámbito hello `My_Scope`.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

Este es un toodescribe un tutorial detallado, lo que sucede:

1. resultado de hello tooget de todas las acciones de `My_Scope`, hello **filtro matriz** filtros de acción `@result('My_Scope')`.

2. Hola condición para **filtro matriz** es cualquier `@result()` elemento que tiene el estado igual demasiado`Failed`. Esta condición filtra la matriz de Hola a todos los resultados de acción de `My_Scope` tooan matriz solamente con resultados de la acción de error.

3. Realizar una **For Each** acción en hello **filtra matriz** genera. En este paso se realiza una acción *para cada* acción resultante en error que se filtrara antes.

    Si se produce un error en una sola acción en el ámbito de hello, Hola acciones en hello `foreach` ejecutar solo una vez. 
    Muchas acciones con error causan una acción por cada error.

4. Enviar una solicitud HTTP POST en hello `foreach` elemento cuerpo de respuesta, o `@item()['outputs']['body']`. Hola `@result()` forma Elem Hola igual como hello `@actions()` forma y se puede analizar Hola igual manera.

5. Incluye dos encabezados personalizados con nombre de la acción error de hello `@item()['name']` y ejecución cliente Id. de seguimiento de error de hello `@item()['clientTrackingId']`.

Como referencia, este es un ejemplo de una sola `@result()` elemento, que muestra hello `name`, `body`, y `clientTrackingId` propiedades que se analizan en el ejemplo anterior de Hola. Fuera de un elemento `foreach`, `@result()` devuelve una matriz de estos objetos.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

patrones de control de excepciones diferentes tooperform, puede usar expresiones de Hola que se ha mostrado anteriormente. Puede elegir una única acción fuera de ámbito de Hola que acepta Hola toda filtrados matriz de errores de control de excepciones de tooexecute y quitar hello `foreach`. También puede incluir otras propiedades útiles de hello `@result()` respuesta se ha mostrado anteriormente.

## <a name="azure-diagnostics-and-telemetry"></a>Diagnósticos de Azure y datos de telemetría

Hello modelos anteriores son errores de manera estupenda toohandle y excepciones dentro de una ejecución, pero también puede identificar y responder tooerrors independiente del programa Hola a ejecutarse. 
[Diagnósticos de Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) proporciona una manera sencilla de toosend todas las cuenta de almacenamiento de Azure de tooan de eventos (incluidos todos los Estados de ejecución y acción) de flujo de trabajo o un concentrador de eventos de Azure. tooevaluate ejecutar Estados, puede supervisar los registros de Hola y métricas o publicarlos en cualquier herramienta de supervisión que prefiera. Una opción posible es toostream todos los eventos de Hola a través del concentrador de eventos de Azure en [análisis de transmisiones](https://azure.microsoft.com/services/stream-analytics/). En el análisis de transmisiones, puede escribir las consultas actuales de las anomalías, medias o errores de hello registros de diagnóstico. Análisis de transmisiones puede generar fácilmente orígenes de datos de tooother como colas, temas, SQL, base de datos de Azure Cosmos y Power BI.

## <a name="next-steps"></a>Pasos siguientes

* [Vea cómo un cliente crea el control de errores con Azure Logic Apps](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Encuentre más escenarios y ejemplos de Logic Apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Obtenga información acerca de cómo toocreate automatizar las implementaciones para las aplicaciones lógicas](../logic-apps/logic-apps-create-deploy-template.md)
* [Creación e implementación de aplicaciones lógicas con Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
