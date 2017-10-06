---
title: los flujos de trabajo aaaDefine con JSON - Azure Logic Apps | Documentos de Microsoft
description: "¿Cómo toowrite definiciones de flujo de trabajo en JSON para logic apps"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Creación de definiciones de flujo de trabajo para aplicaciones lógicas mediante JSON

Puede crear definiciones de flujo de trabajo para [Azure Logic Apps](logic-apps-what-are-logic-apps.md) con un lenguaje JSON sencillo y declarativo. Si no lo ha hecho ya, primero consulte [cómo toocreate su primera aplicación de lógica con el Diseñador de la aplicación lógica](logic-apps-create-a-logic-app.md). Consulte también hello [completo referencia de lenguaje de definición de flujo de trabajo de hello](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Repetición de los pasos de una lista

tooiterate a través de una matriz que no tiene too10, 000 elementos y realiza una acción para cada elemento, utilice hello [foreach tipo](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Control de errores si algo va mal

Por lo general, desea tooinclude una *paso de corrección* : alguna lógica que se ejecuta *si y solo si* una o varias de las llamadas producirá un error. Este ejemplo obtiene datos desde varios lugares, pero si se produce un error en la llamada de hello, deseamos tooPOST un mensaje en algún lugar por lo que se puede realizar un seguimiento de ese error más adelante:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify que `postToErrorMessageQueue` solo se ejecuta después de `readData` tiene `Failed`, usar hello `runAfter` propiedad, por ejemplo, toospecify una lista de posibles valores, por lo que `runAfter` podría ser `["Succeeded", "Failed"]`.

Por último, puesto que este ejemplo controla ahora error hello, ya no se marca los Hola ejecutar como `Failed`. Porque agregamos paso Hola para controlar este error en este ejemplo, hello ejecutar tiene `Succeeded` aunque un paso `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Ejecución de dos o más pasos en paralelo

toorun varias acciones en paralelo, Hola `runAfter` propiedad debe ser equivalente en tiempo de ejecución. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

En este ejemplo, ambos `branch1` y `branch2` se establecen toorun después `readData`. Como consecuencia, ambas acciones se ejecutan en paralelo. marca de tiempo de Hola para ambas bifurcaciones es idéntico.

![Paralelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Unión de dos ramas paralelas

Puede combinar dos acciones que se establecen toorun en paralelo mediante la adición de elementos toohello `runAfter` propiedad como en el ejemplo anterior de Hola.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Paralelo](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>Asignar configuración diferente de tooa de elementos de lista

Después, supongamos que queremos tooget contenido diferente en función de valor de Hola de una propiedad. Podemos crear una asignación de valores toodestinations como parámetro:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

En este caso, primero debemos obtener una lista de artículos. En función de la categoría de Hola que se ha definido como un parámetro, segundo paso de hello usa un toolook de asignación de dirección URL de Hola para obtener contenido de Hola.

Algunas veces toonote aquí: 

*   Hola [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) función comprueba si categoría Hola coincide con uno de hello conocida categorías definidas.

*   Una vez tenemos categoría hello, podemos extraemos elemento Hola de asignación de hello mediante corchetes:`parameters[...]`

## <a name="process-strings"></a>Cadenas de proceso

Puede usar varias funciones toomanipulate cadenas. Por ejemplo, supongamos que tenemos una cadena que queremos toopass tooa sistema, pero no está seguros acerca del control adecuado para la codificación de caracteres. Una opción es toobase64 codifique esta cadena. Sin embargo, tooavoid secuencias de escape en una dirección URL, vamos tooreplace unos cuantos caracteres. 

También queremos una subcadena del nombre del pedido de hello porque no se utilizan los cinco primeros caracteres de Hola.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Trabajar desde dentro de toooutside:

1. Obtener hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) como nombre del orderer hello, por lo que obtenemos número total de Hola de caracteres.

2. Reste 5 porque deseamos una cadena más corta.

3. En realidad, tomar hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Comenzamos en índice `5` y vaya Hola el resto de la cadena de Hola.

4. Convertir este tooa subcadena [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) cadena.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Hola todos los `+` caracteres con `-` caracteres.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Hola todos los `/` caracteres con `_` caracteres.

## <a name="work-with-date-times"></a>Trabajo con fechas

Fecha hora puede ser útil, especialmente cuando se intenta toopull datos desde un origen de datos que no es compatible con naturalmente *desencadenadores*. También puede utilizar las fechas para averiguar cuánto duran los distintos pasos.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

En este ejemplo, se extrae hello `startTime` del paso anterior Hola. A continuación se obtener la hora actual de Hola y resta un segundo:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

Puede usar otras unidades de tiempo, como `minutes` o `hours`. Por último, podemos comparar estos dos valores. Si Hola primer valor es menor que el segundo valor de hello, a continuación, en más de un segundo han transcurrido desde que primero se realizó el pedido de Hola.

fechas de tooformat, podemos utilizar formateadores de cadena. Por ejemplo, tooget Hola RFC1123, usamos [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). toolearn acerca del formato de fecha, vea [lenguaje de definición de flujo de trabajo](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Parámetros de implementación para entornos diferentes

Por lo general, un ciclo de vida de implementación tiene un entorno de desarrollo, un entorno de ensayo y un entorno de producción. Por ejemplo, podría utilizar Hola misma definición en todos estos entornos, pero usar bases de datos diferentes. Del mismo modo, puede querer toouse Hola misma definición en diferentes regiones para lograr alta disponibilidad pero desea base de datos lógica aplicación instancia tootalk toothat de cada región.
Este escenario difiere del que toman parámetros en *en tiempo de ejecución* que en su lugar, debe usar hello `trigger()` funcionando como en el ejemplo anterior de Hola.

Puede empezar con una definición muy básica, como la de este ejemplo:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

Hola real `PUT` solicitar para hello logic apps, puede proporcionar el parámetro hello `uri`. Dado que ya no existe un valor predeterminado, carga de aplicación lógica de hello requiere este parámetro:

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

En cada entorno, puede proporcionar un valor diferente para hello `connection` parámetro. 

Para todos los hello opciones de que dispone para crear y administrar las aplicaciones lógicas, consulte hello [documentación de la API de REST](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
