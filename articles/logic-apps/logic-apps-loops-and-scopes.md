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
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="65b6f-103">Desagrupación, ámbitos y bucles de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="65b6f-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="65b6f-104">Lógica de aplicaciones proporciona una serie de formas toowork con matrices, colecciones, lotes y bucles dentro de un flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="65b6f-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="65b6f-105">Matrices y bucle ForEach</span><span class="sxs-lookup"><span data-stu-id="65b6f-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="65b6f-106">Lógica de aplicaciones permite tooloop sobre un conjunto de datos y realizar una acción para cada elemento.</span><span class="sxs-lookup"><span data-stu-id="65b6f-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="65b6f-107">Esto es posible a través de hello `foreach` acción.</span><span class="sxs-lookup"><span data-stu-id="65b6f-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="65b6f-108">En el Diseñador de hello, puede especificar tooadd un bucle for each.</span><span class="sxs-lookup"><span data-stu-id="65b6f-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="65b6f-109">Después de seleccionar la matriz de hello sobre que desea tooiterate, puede comenzar a agregar acciones.</span><span class="sxs-lookup"><span data-stu-id="65b6f-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="65b6f-110">Actualmente están limitados tooonly una acción por bucle foreach, pero esta restricción se eliminará en hello próximas semanas.</span><span class="sxs-lookup"><span data-stu-id="65b6f-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="65b6f-111">Una vez en el bucle de hello puede empezar toospecify lo que debe ocurrir en todos los valores de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="65b6f-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="65b6f-112">Si utiliza la vista de código, puede especificar un bucle ForEach como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="65b6f-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="65b6f-113">Se trata de un ejemplo de un bucle ForEach que envía un correo electrónico a cada dirección de correo electrónico que contenga "microsoft.com":</span><span class="sxs-lookup"><span data-stu-id="65b6f-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="65b6f-114">Un `foreach` acción puede iterar por matrices de too5, 000 filas.</span><span class="sxs-lookup"><span data-stu-id="65b6f-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="65b6f-115">De forma predeterminada, cada iteración se ejecutará en paralelo.</span><span class="sxs-lookup"><span data-stu-id="65b6f-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="65b6f-116">Bucles ForEach secuenciales</span><span class="sxs-lookup"><span data-stu-id="65b6f-116">Sequential ForEach loops</span></span>

<span data-ttu-id="65b6f-117">tooenable un tooexecute de bucle foreach secuencialmente, Hola `Sequential` se debe agregar la opción de operación.</span><span class="sxs-lookup"><span data-stu-id="65b6f-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="65b6f-118">Bucle Until</span><span class="sxs-lookup"><span data-stu-id="65b6f-118">Until loop</span></span>
  
  <span data-ttu-id="65b6f-119">Puede realizar una acción o una serie de acciones hasta que se cumpla una condición.</span><span class="sxs-lookup"><span data-stu-id="65b6f-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="65b6f-120">Hello escenario más común para esto está llamando a un punto de conexión hasta que llegue la respuesta de Hola que está buscando.</span><span class="sxs-lookup"><span data-stu-id="65b6f-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="65b6f-121">En el Diseñador de hello, puede especificar tooadd un hasta que el bucle.</span><span class="sxs-lookup"><span data-stu-id="65b6f-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="65b6f-122">Después de agregar acciones dentro del bucle de hello, se puede establecer la condición de salida de hello, así como Hola límites de bucle.</span><span class="sxs-lookup"><span data-stu-id="65b6f-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="65b6f-123">Hay un retraso de 1 minuto entre los ciclos de bucle.</span><span class="sxs-lookup"><span data-stu-id="65b6f-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="65b6f-124">Si utiliza la vista de código, puede especificar un bucle Until como el siguiente.</span><span class="sxs-lookup"><span data-stu-id="65b6f-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="65b6f-125">Este es un ejemplo de una llamada a un extremo HTTP hasta que el cuerpo de la respuesta de hello tiene el valor de hello 'Completed'.</span><span class="sxs-lookup"><span data-stu-id="65b6f-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="65b6f-126">Se completará cuando:</span><span class="sxs-lookup"><span data-stu-id="65b6f-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="65b6f-127">La respuesta HTTP tenga el estado "Completado".</span><span class="sxs-lookup"><span data-stu-id="65b6f-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="65b6f-128">Haya realizado intentos durante 1 hora.</span><span class="sxs-lookup"><span data-stu-id="65b6f-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="65b6f-129">Haya entrado en bucle 100 veces.</span><span class="sxs-lookup"><span data-stu-id="65b6f-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="65b6f-130">SplitOn y desagrupación</span><span class="sxs-lookup"><span data-stu-id="65b6f-130">SplitOn and debatching</span></span>

<span data-ttu-id="65b6f-131">En ocasiones, un desencadenador puede recibir una matriz de elementos que desee toodebatch e iniciar un flujo de trabajo por cada elemento.</span><span class="sxs-lookup"><span data-stu-id="65b6f-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="65b6f-132">Esto puede realizarse a través de hello `spliton` comando.</span><span class="sxs-lookup"><span data-stu-id="65b6f-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="65b6f-133">De forma predeterminada, si el archivo swagger desencadenador especifica una carga que es una matriz, se agregará `spliton` e iniciará una ejecución por cada elemento.</span><span class="sxs-lookup"><span data-stu-id="65b6f-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="65b6f-134">Solo pueden agregarse SplitOn tooa desencadenador.</span><span class="sxs-lookup"><span data-stu-id="65b6f-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="65b6f-135">Puede invalidarse o configurarse manualmente en la definición de vista de código.</span><span class="sxs-lookup"><span data-stu-id="65b6f-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="65b6f-136">Actualmente SplitOn puede debatch matrices de too5, 000 elementos.</span><span class="sxs-lookup"><span data-stu-id="65b6f-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="65b6f-137">No puede tener un `spliton` y también implementar Hola respuesta sincrónica patrón.</span><span class="sxs-lookup"><span data-stu-id="65b6f-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="65b6f-138">Cualquier flujo de trabajo llama a que tiene un `response` acción además demasiado`spliton` se ejecutan de forma asincrónica y enviar inmediato `202 Accepted` respuesta.</span><span class="sxs-lookup"><span data-stu-id="65b6f-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="65b6f-139">SplitOn puede especificarse en la vista de código como el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="65b6f-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="65b6f-140">De este modo, se recibe una matriz de elementos y realiza desagrupaciones en cada fila.</span><span class="sxs-lookup"><span data-stu-id="65b6f-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="65b6f-141">Ámbitos</span><span class="sxs-lookup"><span data-stu-id="65b6f-141">Scopes</span></span>

<span data-ttu-id="65b6f-142">Es posible toogroup una serie de acciones conjuntamente con un ámbito.</span><span class="sxs-lookup"><span data-stu-id="65b6f-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="65b6f-143">Esto es especialmente útil para implementar el control de excepciones.</span><span class="sxs-lookup"><span data-stu-id="65b6f-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="65b6f-144">En el Diseñador de hello puede agregar un nuevo ámbito y empezar a agregar cualquier acción en su interior.</span><span class="sxs-lookup"><span data-stu-id="65b6f-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="65b6f-145">Puede definir ámbitos en la vista de código como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="65b6f-145">You can define scopes in code-view like hello following:</span></span>


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