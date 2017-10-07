---
title: "aaaCreate bucles y ámbitos o debatch datos en flujos de trabajo: las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Crear bucles tooiterate a través de los datos, agrupar acciones en los ámbitos, o debatch datos toostart varios flujos de trabajo en las aplicaciones lógicas de Azure."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>Desagrupación, ámbitos y bucles de aplicaciones lógicas
  
Lógica de aplicaciones proporciona una serie de formas toowork con matrices, colecciones, lotes y bucles dentro de un flujo de trabajo.
  
## <a name="foreach-loop-and-arrays"></a>Matrices y bucle ForEach
  
Lógica de aplicaciones permite tooloop sobre un conjunto de datos y realizar una acción para cada elemento.  Esto es posible a través de hello `foreach` acción.  En el Diseñador de hello, puede especificar tooadd un bucle for each.  Después de seleccionar la matriz de hello sobre que desea tooiterate, puede comenzar a agregar acciones.  Actualmente están limitados tooonly una acción por bucle foreach, pero esta restricción se eliminará en hello próximas semanas.  Una vez en el bucle de hello puede empezar toospecify lo que debe ocurrir en todos los valores de matriz de Hola.

Si utiliza la vista de código, puede especificar un bucle ForEach como el siguiente.  Se trata de un ejemplo de un bucle ForEach que envía un correo electrónico a cada dirección de correo electrónico que contenga "microsoft.com":

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
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
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  Un `foreach` acción puede iterar por matrices de too5, 000 filas.  De forma predeterminada, cada iteración se ejecutará en paralelo.  

### <a name="sequential-foreach-loops"></a>Bucles ForEach secuenciales

tooenable un tooexecute de bucle foreach secuencialmente, Hola `Sequential` se debe agregar la opción de operación.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Bucle Until
  
  Puede realizar una acción o una serie de acciones hasta que se cumpla una condición.  Hello escenario más común para esto está llamando a un punto de conexión hasta que llegue la respuesta de Hola que está buscando.  En el Diseñador de hello, puede especificar tooadd un hasta que el bucle.  Después de agregar acciones dentro del bucle de hello, se puede establecer la condición de salida de hello, así como Hola límites de bucle.  Hay un retraso de 1 minuto entre los ciclos de bucle.
  
  Si utiliza la vista de código, puede especificar un bucle Until como el siguiente.  Este es un ejemplo de una llamada a un extremo HTTP hasta que el cuerpo de la respuesta de hello tiene el valor de hello 'Completed'.  Se completará cuando: 
  
  * La respuesta HTTP tenga el estado "Completado".
  * Haya realizado intentos durante 1 hora.
  * Haya entrado en bucle 100 veces.
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn y desagrupación

En ocasiones, un desencadenador puede recibir una matriz de elementos que desee toodebatch e iniciar un flujo de trabajo por cada elemento.  Esto puede realizarse a través de hello `spliton` comando.  De forma predeterminada, si el archivo swagger desencadenador especifica una carga que es una matriz, se agregará `spliton` e iniciará una ejecución por cada elemento.  Solo pueden agregarse SplitOn tooa desencadenador.  Puede invalidarse o configurarse manualmente en la definición de vista de código.  Actualmente SplitOn puede debatch matrices de too5, 000 elementos.  No puede tener un `spliton` y también implementar Hola respuesta sincrónica patrón.  Cualquier flujo de trabajo llama a que tiene un `response` acción además demasiado`spliton` se ejecutan de forma asincrónica y enviar inmediato `202 Accepted` respuesta.  

SplitOn puede especificarse en la vista de código como el siguiente ejemplo de Hola.  De este modo, se recibe una matriz de elementos y realiza desagrupaciones en cada fila.

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>Ámbitos

Es posible toogroup una serie de acciones conjuntamente con un ámbito.  Esto es especialmente útil para implementar el control de excepciones.  En el Diseñador de hello puede agregar un nuevo ámbito y empezar a agregar cualquier acción en su interior.  Puede definir ámbitos en la vista de código como Hola siguiente:


```
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