---
title: "Definición de flujos de trabajo con JSON: Azure Logic Apps | Microsoft Docs"
description: "Definiciones de flujo de trabajo en JSON para aplicaciones lógicas"
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
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="3e95b-103">Creación de definiciones de flujo de trabajo para aplicaciones lógicas mediante JSON</span><span class="sxs-lookup"><span data-stu-id="3e95b-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="3e95b-104">Puede crear definiciones de flujo de trabajo para [Azure Logic Apps](logic-apps-what-are-logic-apps.md) con un lenguaje JSON sencillo y declarativo.</span><span class="sxs-lookup"><span data-stu-id="3e95b-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="3e95b-105">Si no lo ha hecho ya, primero consulte [cómo crear su primera aplicación lógica con el diseñador de aplicaciones lógicas](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3e95b-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3e95b-106">Consulte también la [referencia completa del lenguaje de definición de flujo de trabajo](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="3e95b-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="3e95b-107">Repetición de los pasos de una lista</span><span class="sxs-lookup"><span data-stu-id="3e95b-107">Repeat steps over a list</span></span>

<span data-ttu-id="3e95b-108">Para repetir los elementos de una matriz que contiene hasta 10 000 elementos y realizar una acción para cada elemento, utilice el [tipo foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="3e95b-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="3e95b-109">Control de errores si algo va mal</span><span class="sxs-lookup"><span data-stu-id="3e95b-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="3e95b-110">Normalmente desea incluir un *paso de corrección*, es decir, cierta lógica que se ejecuta *si, y solo si*, una o varias llamadas no se han podido realizar correctamente.</span><span class="sxs-lookup"><span data-stu-id="3e95b-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="3e95b-111">En este ejemplo, obtenemos datos desde diversos lugares, pero si se produce un error en la llamada, es necesario PUBLICAR un mensaje en alguna parte para poder localizar ese error más adelante:</span><span class="sxs-lookup"><span data-stu-id="3e95b-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="3e95b-112">Para especificar que `postToErrorMessageQueue` solo se ejecuta si `readData` es `Failed`, use la propiedad `runAfter`, por ejemplo, para especificar una lista de posibles valores, para que `runAfter` pueda ser `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="3e95b-113">Por último, dado que en este ejemplo ya se ha controlado el error, la ejecución ya no se marcará como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="3e95b-114">Como hemos agregado el paso para controlar este error en este ejemplo, la ejecución es `Succeeded` aunque un paso `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="3e95b-115">Ejecución de dos o más pasos en paralelo</span><span class="sxs-lookup"><span data-stu-id="3e95b-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="3e95b-116">Para ejecutar varias acciones en paralelo, la propiedad `runAfter` debe ser equivalente en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="3e95b-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="3e95b-117">En este ejemplo, se ha establecido que `branch1` y `branch2` se ejecuten después de `readData`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="3e95b-118">Como consecuencia, ambas acciones se ejecutan en paralelo.</span><span class="sxs-lookup"><span data-stu-id="3e95b-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="3e95b-119">La marca de tiempo para ambas acciones es idéntica.</span><span class="sxs-lookup"><span data-stu-id="3e95b-119">The timestamp for both branches is identical.</span></span>

![Paralelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="3e95b-121">Unión de dos ramas paralelas</span><span class="sxs-lookup"><span data-stu-id="3e95b-121">Join two parallel branches</span></span>

<span data-ttu-id="3e95b-122">Puede unir dos acciones que se han establecido para ejecutarse en paralelo al agregar elementos a la propiedad `runAfter` como en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="3e95b-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

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

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="3e95b-124">Asignación de elementos de lista a una configuración diferente</span><span class="sxs-lookup"><span data-stu-id="3e95b-124">Map list items to a different configuration</span></span>

<span data-ttu-id="3e95b-125">A continuación, supongamos que queremos obtener contenido diferente según un valor de una propiedad.</span><span class="sxs-lookup"><span data-stu-id="3e95b-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="3e95b-126">Podemos crear una asignación de valores a destinos como un parámetro:</span><span class="sxs-lookup"><span data-stu-id="3e95b-126">We can create a map of values to destinations as a parameter:</span></span>  

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

<span data-ttu-id="3e95b-127">En este caso, primero debemos obtener una lista de artículos.</span><span class="sxs-lookup"><span data-stu-id="3e95b-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="3e95b-128">Según la categoría que se haya definido como parámetro, el segundo paso será utilizar una asignación para buscar la dirección URL para obtener el contenido.</span><span class="sxs-lookup"><span data-stu-id="3e95b-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="3e95b-129">Algunas observaciones a tener en cuenta aquí:</span><span class="sxs-lookup"><span data-stu-id="3e95b-129">Some times to note here:</span></span> 

*   <span data-ttu-id="3e95b-130">La función [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) comprueba si la categoría coincide con alguna de las categorías definidas conocidas.</span><span class="sxs-lookup"><span data-stu-id="3e95b-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="3e95b-131">Una vez que se obtiene la categoría, se puede extraer el elemento de la asignación mediante corchetes: `parameters[...]`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="3e95b-132">Cadenas de proceso</span><span class="sxs-lookup"><span data-stu-id="3e95b-132">Process strings</span></span>

<span data-ttu-id="3e95b-133">Puede usar varias funciones para manipular cadenas.</span><span class="sxs-lookup"><span data-stu-id="3e95b-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="3e95b-134">Por ejemplo, supongamos que tenemos una cadena que queremos pasar a un sistema, pero no estamos seguros acerca del control adecuado para la codificación de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3e95b-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="3e95b-135">Una opción consiste en codificar esta cadena con base64.</span><span class="sxs-lookup"><span data-stu-id="3e95b-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="3e95b-136">Sin embargo, para evitar escapes en una dirección URL, vamos a reemplazar algunos caracteres.</span><span class="sxs-lookup"><span data-stu-id="3e95b-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="3e95b-137">También queremos una subcadena del nombre del pedido, porque los cinco primeros caracteres no se usan.</span><span class="sxs-lookup"><span data-stu-id="3e95b-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

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

<span data-ttu-id="3e95b-138">Si trabajamos desde dentro hacia fuera:</span><span class="sxs-lookup"><span data-stu-id="3e95b-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="3e95b-139">Obtenga el valor de [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) del nombre del solicitante, lo que devuelve el número total de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3e95b-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="3e95b-140">Reste 5 porque deseamos una cadena más corta.</span><span class="sxs-lookup"><span data-stu-id="3e95b-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="3e95b-141">Realmente, quitamos [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="3e95b-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="3e95b-142">Comenzamos con el índice `5` y pasamos al resto de la cadena.</span><span class="sxs-lookup"><span data-stu-id="3e95b-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="3e95b-143">Convierta esta subcadena en una cadena [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64).</span><span class="sxs-lookup"><span data-stu-id="3e95b-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="3e95b-144">Use [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) para reemplazar todos los caracteres `+` por `-`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="3e95b-145">Use [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) para reemplazar todos los caracteres `/` por `_`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="3e95b-146">Trabajo con fechas</span><span class="sxs-lookup"><span data-stu-id="3e95b-146">Work with Date Times</span></span>

<span data-ttu-id="3e95b-147">Las fechas pueden ser útiles, especialmente cuando intenta extraer datos de un origen de datos que no admite de forma natural *desencadenadores*.</span><span class="sxs-lookup"><span data-stu-id="3e95b-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="3e95b-148">También puede utilizar las fechas para averiguar cuánto duran los distintos pasos.</span><span class="sxs-lookup"><span data-stu-id="3e95b-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="3e95b-149">En este ejemplo, vamos a extraer el valor `startTime` del paso anterior.</span><span class="sxs-lookup"><span data-stu-id="3e95b-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="3e95b-150">A continuación, obtenemos la hora actual y restamos un segundo:</span><span class="sxs-lookup"><span data-stu-id="3e95b-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="3e95b-151">Puede usar otras unidades de tiempo, como `minutes` o `hours`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="3e95b-152">Por último, podemos comparar estos dos valores.</span><span class="sxs-lookup"><span data-stu-id="3e95b-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="3e95b-153">Si el primero es inferior al segundo, significa que ha transcurrido más de un segundo desde la primera vez que se realizó el pedido.</span><span class="sxs-lookup"><span data-stu-id="3e95b-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="3e95b-154">Para dar formato a fechas, podemos usar formateadores de cadena.</span><span class="sxs-lookup"><span data-stu-id="3e95b-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="3e95b-155">Por ejemplo, para obtener el valor de RFC1123, usamos [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="3e95b-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="3e95b-156">Para obtener información sobre los formatos de fecha, consulte [Lenguaje de definición de flujo de trabajo](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="3e95b-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="3e95b-157">Parámetros de implementación para entornos diferentes</span><span class="sxs-lookup"><span data-stu-id="3e95b-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="3e95b-158">Por lo general, un ciclo de vida de implementación tiene un entorno de desarrollo, un entorno de ensayo y un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3e95b-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="3e95b-159">Por ejemplo, puede utilizar la misma definición en todos estos entornos pero utilizar diferentes bases de datos.</span><span class="sxs-lookup"><span data-stu-id="3e95b-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="3e95b-160">Del mismo modo, es posible que desee utilizar la misma definición en muchas regiones diferentes para lograr una alta disponibilidad, pero que cada instancia de aplicación lógica se comunique con la base de datos de esa región.</span><span class="sxs-lookup"><span data-stu-id="3e95b-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="3e95b-161">Este escenario no tiene que ver nada con tomar parámetros en *tiempo de ejecución* en aquellas ocasiones en las que debe utilizar la función `trigger()` como en el ejemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="3e95b-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="3e95b-162">Puede empezar con una definición muy básica, como la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3e95b-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="3e95b-163">En la solicitud `PUT` real para las aplicaciones lógicas, puede proporcionar el parámetro `uri`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="3e95b-164">Dado que ya no existe un valor predeterminado, la carga útil de la aplicación lógica requiere este parámetro:</span><span class="sxs-lookup"><span data-stu-id="3e95b-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
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

<span data-ttu-id="3e95b-165">En cada entorno puede proporcionar un valor diferente para el parámetro `connection`.</span><span class="sxs-lookup"><span data-stu-id="3e95b-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="3e95b-166">Consulte la [documentación sobre la API de REST](https://msdn.microsoft.com/library/azure/mt643787.aspx) para conocer todas las opciones disponibles para crear y administrar aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="3e95b-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
