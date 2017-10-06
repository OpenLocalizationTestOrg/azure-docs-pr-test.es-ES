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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="9cb57-103">Creación de definiciones de flujo de trabajo para aplicaciones lógicas mediante JSON</span><span class="sxs-lookup"><span data-stu-id="9cb57-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="9cb57-104">Puede crear definiciones de flujo de trabajo para [Azure Logic Apps](logic-apps-what-are-logic-apps.md) con un lenguaje JSON sencillo y declarativo.</span><span class="sxs-lookup"><span data-stu-id="9cb57-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="9cb57-105">Si no lo ha hecho ya, primero consulte [cómo toocreate su primera aplicación de lógica con el Diseñador de la aplicación lógica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9cb57-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9cb57-106">Consulte también hello [completo referencia de lenguaje de definición de flujo de trabajo de hello](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="9cb57-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="9cb57-107">Repetición de los pasos de una lista</span><span class="sxs-lookup"><span data-stu-id="9cb57-107">Repeat steps over a list</span></span>

<span data-ttu-id="9cb57-108">tooiterate a través de una matriz que no tiene too10, 000 elementos y realiza una acción para cada elemento, utilice hello [foreach tipo](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="9cb57-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="9cb57-109">Control de errores si algo va mal</span><span class="sxs-lookup"><span data-stu-id="9cb57-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="9cb57-110">Por lo general, desea tooinclude una *paso de corrección* : alguna lógica que se ejecuta *si y solo si* una o varias de las llamadas producirá un error.</span><span class="sxs-lookup"><span data-stu-id="9cb57-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="9cb57-111">Este ejemplo obtiene datos desde varios lugares, pero si se produce un error en la llamada de hello, deseamos tooPOST un mensaje en algún lugar por lo que se puede realizar un seguimiento de ese error más adelante:</span><span class="sxs-lookup"><span data-stu-id="9cb57-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="9cb57-112">toospecify que `postToErrorMessageQueue` solo se ejecuta después de `readData` tiene `Failed`, usar hello `runAfter` propiedad, por ejemplo, toospecify una lista de posibles valores, por lo que `runAfter` podría ser `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="9cb57-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="9cb57-113">Por último, puesto que este ejemplo controla ahora error hello, ya no se marca los Hola ejecutar como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="9cb57-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="9cb57-114">Porque agregamos paso Hola para controlar este error en este ejemplo, hello ejecutar tiene `Succeeded` aunque un paso `Failed`.</span><span class="sxs-lookup"><span data-stu-id="9cb57-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="9cb57-115">Ejecución de dos o más pasos en paralelo</span><span class="sxs-lookup"><span data-stu-id="9cb57-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="9cb57-116">toorun varias acciones en paralelo, Hola `runAfter` propiedad debe ser equivalente en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9cb57-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="9cb57-117">En este ejemplo, ambos `branch1` y `branch2` se establecen toorun después `readData`.</span><span class="sxs-lookup"><span data-stu-id="9cb57-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="9cb57-118">Como consecuencia, ambas acciones se ejecutan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="9cb57-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="9cb57-119">marca de tiempo de Hola para ambas bifurcaciones es idéntico.</span><span class="sxs-lookup"><span data-stu-id="9cb57-119">hello timestamp for both branches is identical.</span></span>

![Paralelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="9cb57-121">Unión de dos ramas paralelas</span><span class="sxs-lookup"><span data-stu-id="9cb57-121">Join two parallel branches</span></span>

<span data-ttu-id="9cb57-122">Puede combinar dos acciones que se establecen toorun en paralelo mediante la adición de elementos toohello `runAfter` propiedad como en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="9cb57-124">Asignar configuración diferente de tooa de elementos de lista</span><span class="sxs-lookup"><span data-stu-id="9cb57-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="9cb57-125">Después, supongamos que queremos tooget contenido diferente en función de valor de Hola de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="9cb57-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="9cb57-126">Podemos crear una asignación de valores toodestinations como parámetro:</span><span class="sxs-lookup"><span data-stu-id="9cb57-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="9cb57-127">En este caso, primero debemos obtener una lista de artículos.</span><span class="sxs-lookup"><span data-stu-id="9cb57-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="9cb57-128">En función de la categoría de Hola que se ha definido como un parámetro, segundo paso de hello usa un toolook de asignación de dirección URL de Hola para obtener contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="9cb57-129">Algunas veces toonote aquí:</span><span class="sxs-lookup"><span data-stu-id="9cb57-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="9cb57-130">Hola [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) función comprueba si categoría Hola coincide con uno de hello conocida categorías definidas.</span><span class="sxs-lookup"><span data-stu-id="9cb57-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="9cb57-131">Una vez tenemos categoría hello, podemos extraemos elemento Hola de asignación de hello mediante corchetes:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="9cb57-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="9cb57-132">Cadenas de proceso</span><span class="sxs-lookup"><span data-stu-id="9cb57-132">Process strings</span></span>

<span data-ttu-id="9cb57-133">Puede usar varias funciones toomanipulate cadenas.</span><span class="sxs-lookup"><span data-stu-id="9cb57-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="9cb57-134">Por ejemplo, supongamos que tenemos una cadena que queremos toopass tooa sistema, pero no está seguros acerca del control adecuado para la codificación de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9cb57-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="9cb57-135">Una opción es toobase64 codifique esta cadena.</span><span class="sxs-lookup"><span data-stu-id="9cb57-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="9cb57-136">Sin embargo, tooavoid secuencias de escape en una dirección URL, vamos tooreplace unos cuantos caracteres.</span><span class="sxs-lookup"><span data-stu-id="9cb57-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="9cb57-137">También queremos una subcadena del nombre del pedido de hello porque no se utilizan los cinco primeros caracteres de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="9cb57-138">Trabajar desde dentro de toooutside:</span><span class="sxs-lookup"><span data-stu-id="9cb57-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="9cb57-139">Obtener hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) como nombre del orderer hello, por lo que obtenemos número total de Hola de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9cb57-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="9cb57-140">Reste 5 porque deseamos una cadena más corta.</span><span class="sxs-lookup"><span data-stu-id="9cb57-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="9cb57-141">En realidad, tomar hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="9cb57-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="9cb57-142">Comenzamos en índice `5` y vaya Hola el resto de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="9cb57-143">Convertir este tooa subcadena [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) cadena.</span><span class="sxs-lookup"><span data-stu-id="9cb57-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="9cb57-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Hola todos los `+` caracteres con `-` caracteres.</span><span class="sxs-lookup"><span data-stu-id="9cb57-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="9cb57-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)Hola todos los `/` caracteres con `_` caracteres.</span><span class="sxs-lookup"><span data-stu-id="9cb57-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="9cb57-146">Trabajo con fechas</span><span class="sxs-lookup"><span data-stu-id="9cb57-146">Work with Date Times</span></span>

<span data-ttu-id="9cb57-147">Fecha hora puede ser útil, especialmente cuando se intenta toopull datos desde un origen de datos que no es compatible con naturalmente *desencadenadores*.</span><span class="sxs-lookup"><span data-stu-id="9cb57-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="9cb57-148">También puede utilizar las fechas para averiguar cuánto duran los distintos pasos.</span><span class="sxs-lookup"><span data-stu-id="9cb57-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="9cb57-149">En este ejemplo, se extrae hello `startTime` del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="9cb57-150">A continuación se obtener la hora actual de Hola y resta un segundo:</span><span class="sxs-lookup"><span data-stu-id="9cb57-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="9cb57-151">Puede usar otras unidades de tiempo, como `minutes` o `hours`.</span><span class="sxs-lookup"><span data-stu-id="9cb57-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="9cb57-152">Por último, podemos comparar estos dos valores.</span><span class="sxs-lookup"><span data-stu-id="9cb57-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="9cb57-153">Si Hola primer valor es menor que el segundo valor de hello, a continuación, en más de un segundo han transcurrido desde que primero se realizó el pedido de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="9cb57-154">fechas de tooformat, podemos utilizar formateadores de cadena.</span><span class="sxs-lookup"><span data-stu-id="9cb57-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="9cb57-155">Por ejemplo, tooget Hola RFC1123, usamos [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="9cb57-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="9cb57-156">toolearn acerca del formato de fecha, vea [lenguaje de definición de flujo de trabajo](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="9cb57-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="9cb57-157">Parámetros de implementación para entornos diferentes</span><span class="sxs-lookup"><span data-stu-id="9cb57-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="9cb57-158">Por lo general, un ciclo de vida de implementación tiene un entorno de desarrollo, un entorno de ensayo y un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="9cb57-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="9cb57-159">Por ejemplo, podría utilizar Hola misma definición en todos estos entornos, pero usar bases de datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="9cb57-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="9cb57-160">Del mismo modo, puede querer toouse Hola misma definición en diferentes regiones para lograr alta disponibilidad pero desea base de datos lógica aplicación instancia tootalk toothat de cada región.</span><span class="sxs-lookup"><span data-stu-id="9cb57-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="9cb57-161">Este escenario difiere del que toman parámetros en *en tiempo de ejecución* que en su lugar, debe usar hello `trigger()` funcionando como en el ejemplo anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9cb57-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="9cb57-162">Puede empezar con una definición muy básica, como la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9cb57-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="9cb57-163">Hola real `PUT` solicitar para hello logic apps, puede proporcionar el parámetro hello `uri`.</span><span class="sxs-lookup"><span data-stu-id="9cb57-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="9cb57-164">Dado que ya no existe un valor predeterminado, carga de aplicación lógica de hello requiere este parámetro:</span><span class="sxs-lookup"><span data-stu-id="9cb57-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

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

<span data-ttu-id="9cb57-165">En cada entorno, puede proporcionar un valor diferente para hello `connection` parámetro.</span><span class="sxs-lookup"><span data-stu-id="9cb57-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="9cb57-166">Para todos los hello opciones de que dispone para crear y administrar las aplicaciones lógicas, consulte hello [documentación de la API de REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cb57-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
