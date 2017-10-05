---
title: "Creación de bucles y ámbitos, o división de datos en flujos de trabajo - Azure Logic Apps | Microsoft Docs"
description: "Cree bucles para recorrer los datos, agrupar acciones en ámbitos, o dividir datos para iniciar más flujos de trabajo en Azure Logic Apps."
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
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="1c678-103">Desagrupación, ámbitos y bucles de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="1c678-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="1c678-104">Logic Apps proporciona una serie de métodos para trabajar con matrices, colecciones, lotes y bucles en un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="1c678-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="1c678-105">Matrices y bucle ForEach</span><span class="sxs-lookup"><span data-stu-id="1c678-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="1c678-106">Las aplicaciones lógicas permiten crear bucles en un conjunto de datos y realizar una acción en cada elemento.</span><span class="sxs-lookup"><span data-stu-id="1c678-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="1c678-107">Esto es posible gracias a la acción `foreach` .</span><span class="sxs-lookup"><span data-stu-id="1c678-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="1c678-108">En el diseñador, puede especificar que se agregue un bucle ForEach.</span><span class="sxs-lookup"><span data-stu-id="1c678-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="1c678-109">Después de seleccionar la matriz en la que desea realizar la iteración, puede empezar a agregar acciones.</span><span class="sxs-lookup"><span data-stu-id="1c678-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="1c678-110">En estos momentos, solo puede agregar una acción por cada bucle ForEach, pero esta restricción se eliminará en las próximas semanas.</span><span class="sxs-lookup"><span data-stu-id="1c678-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="1c678-111">En el bucle se puede empezar a especificar qué debe ocurrir en cada valor de la matriz.</span><span class="sxs-lookup"><span data-stu-id="1c678-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="1c678-112">Si utiliza la vista de código, puede especificar un bucle ForEach como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="1c678-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="1c678-113">Se trata de un ejemplo de un bucle ForEach que envía un correo electrónico a cada dirección de correo electrónico que contenga "microsoft.com":</span><span class="sxs-lookup"><span data-stu-id="1c678-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="1c678-114">Una acción `foreach` puede iterar hasta 5000 filas en las matrices.</span><span class="sxs-lookup"><span data-stu-id="1c678-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="1c678-115">De forma predeterminada, cada iteración se ejecutará en paralelo.</span><span class="sxs-lookup"><span data-stu-id="1c678-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="1c678-116">Bucles ForEach secuenciales</span><span class="sxs-lookup"><span data-stu-id="1c678-116">Sequential ForEach loops</span></span>

<span data-ttu-id="1c678-117">Para habilitar un bucle foreach para ejecutarse de manera secuencial, la operación `Sequential` se debe agregar la opción.</span><span class="sxs-lookup"><span data-stu-id="1c678-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="1c678-118">Bucle Until</span><span class="sxs-lookup"><span data-stu-id="1c678-118">Until loop</span></span>
  
  <span data-ttu-id="1c678-119">Puede realizar una acción o una serie de acciones hasta que se cumpla una condición.</span><span class="sxs-lookup"><span data-stu-id="1c678-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="1c678-120">El escenario más común para este fin es llamar a un punto de conexión hasta que obtenga la respuesta que busca.</span><span class="sxs-lookup"><span data-stu-id="1c678-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="1c678-121">En el diseñador, puede especificar que se agregue un bucle Until.</span><span class="sxs-lookup"><span data-stu-id="1c678-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="1c678-122">Después de agregar las acciones dentro del bucle, puede establecer la condición de salida, así como los límites de bucle.</span><span class="sxs-lookup"><span data-stu-id="1c678-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="1c678-123">Hay un retraso de 1 minuto entre los ciclos de bucle.</span><span class="sxs-lookup"><span data-stu-id="1c678-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="1c678-124">Si utiliza la vista de código, puede especificar un bucle Until como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="1c678-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="1c678-125">Se trata de un ejemplo de una llamada a un punto de conexión HTTP hasta que el cuerpo de respuesta tenga el valor "Completado".</span><span class="sxs-lookup"><span data-stu-id="1c678-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="1c678-126">Se completará cuando:</span><span class="sxs-lookup"><span data-stu-id="1c678-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="1c678-127">La respuesta HTTP tenga el estado "Completado".</span><span class="sxs-lookup"><span data-stu-id="1c678-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="1c678-128">Haya realizado intentos durante 1 hora.</span><span class="sxs-lookup"><span data-stu-id="1c678-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="1c678-129">Haya entrado en bucle 100 veces.</span><span class="sxs-lookup"><span data-stu-id="1c678-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="1c678-130">SplitOn y desagrupación</span><span class="sxs-lookup"><span data-stu-id="1c678-130">SplitOn and debatching</span></span>

<span data-ttu-id="1c678-131">A veces, un desencadenador puede recibir una matriz de elementos que desea desagrupar e iniciar un flujo de trabajo por elemento.</span><span class="sxs-lookup"><span data-stu-id="1c678-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="1c678-132">Esto puede realizarse a través del comando `spliton` .</span><span class="sxs-lookup"><span data-stu-id="1c678-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="1c678-133">De forma predeterminada, si el archivo swagger desencadenador especifica una carga que es una matriz, se agregará `spliton` e iniciará una ejecución por cada elemento.</span><span class="sxs-lookup"><span data-stu-id="1c678-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="1c678-134">SplitOn solo puede agregarse a un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="1c678-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="1c678-135">Puede invalidarse o configurarse manualmente en la definición de vista de código.</span><span class="sxs-lookup"><span data-stu-id="1c678-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="1c678-136">En estos momentos, SplitOn puede desagrupar hasta 5000 elementos en matrices.</span><span class="sxs-lookup"><span data-stu-id="1c678-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="1c678-137">No puede tener `spliton` ni tampoco implementar el patrón de respuesta sincrónica.</span><span class="sxs-lookup"><span data-stu-id="1c678-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="1c678-138">Cualquier flujo de trabajo que tiene una acción `response`, además de `spliton`, se ejecutará de forma asincrónica y enviará una respuesta `202 Accepted` inmediata.</span><span class="sxs-lookup"><span data-stu-id="1c678-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="1c678-139">SplitOn se puede especificar en la vista código como en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1c678-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="1c678-140">De este modo, se recibe una matriz de elementos y realiza desagrupaciones en cada fila.</span><span class="sxs-lookup"><span data-stu-id="1c678-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="1c678-141">Ámbitos</span><span class="sxs-lookup"><span data-stu-id="1c678-141">Scopes</span></span>

<span data-ttu-id="1c678-142">Se pueden agrupar una serie de acciones con un ámbito.</span><span class="sxs-lookup"><span data-stu-id="1c678-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="1c678-143">Esto es especialmente útil para implementar el control de excepciones.</span><span class="sxs-lookup"><span data-stu-id="1c678-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="1c678-144">En el diseñador puede agregar un nuevo ámbito y empezar a agregar las acciones dentro de él.</span><span class="sxs-lookup"><span data-stu-id="1c678-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="1c678-145">Puede definir ámbitos en la vista código de forma similar a esta:</span><span class="sxs-lookup"><span data-stu-id="1c678-145">You can define scopes in code-view like the following:</span></span>


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