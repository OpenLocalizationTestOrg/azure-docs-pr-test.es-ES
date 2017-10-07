---
title: "prácticas recomendadas de aaaBest para las funciones de Azure | Documentos de Microsoft"
description: "Información acerca de los procedimientos recomendados y los patrones de Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, patrones, procedimientos recomendados, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="b90d7-104">Optimizar el rendimiento de Hola y confiabilidad de las funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="b90d7-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="b90d7-105">Este artículo proporciona rendimiento de orientación tooimprove hello y la confiabilidad de las aplicaciones de la función.</span><span class="sxs-lookup"><span data-stu-id="b90d7-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="b90d7-106">Evitar funciones de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="b90d7-106">Avoid long running functions</span></span>

<span data-ttu-id="b90d7-107">Las funciones grandes de ejecución prolongada pueden causar problemas de tiempo de espera inesperados.</span><span class="sxs-lookup"><span data-stu-id="b90d7-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="b90d7-108">Una función puede llegar a ser grande debido a dependencias de Node.js toomany.</span><span class="sxs-lookup"><span data-stu-id="b90d7-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="b90d7-109">La importación de las dependencias también puede provocar mayores tiempos de carga que dan lugar a tiempos de expiración inesperados.</span><span class="sxs-lookup"><span data-stu-id="b90d7-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="b90d7-110">Las dependencias se cargan explícita e implícitamente.</span><span class="sxs-lookup"><span data-stu-id="b90d7-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="b90d7-111">Un módulo único cargado por el código puede cargar sus propios módulos adicionales.</span><span class="sxs-lookup"><span data-stu-id="b90d7-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="b90d7-112">Siempre que sea posible, refactorice funciones grandes en conjuntos más pequeños de funciones que trabajen juntos y devuelvan respuestas rápidas.</span><span class="sxs-lookup"><span data-stu-id="b90d7-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="b90d7-113">Por ejemplo, un webhook o en función de activación HTTP puede requerir una respuesta de confirmación en un determinado período de tiempo; es habitual webhooks toorequire una respuesta inmediata.</span><span class="sxs-lookup"><span data-stu-id="b90d7-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="b90d7-114">Carga de desencadenador de hello HTTP puede pasar a un toobe de cola procesado por una función de activación de cola.</span><span class="sxs-lookup"><span data-stu-id="b90d7-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="b90d7-115">Este enfoque permite trabajo real de toodefer hello y devolver una respuesta inmediata.</span><span class="sxs-lookup"><span data-stu-id="b90d7-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="b90d7-116">Comunicación entre funciones</span><span class="sxs-lookup"><span data-stu-id="b90d7-116">Cross function communication</span></span>

<span data-ttu-id="b90d7-117">Cuando se integra varias funciones, suele ser una mejor práctica toouse las colas de almacenamiento para la función comunicación cruzada.</span><span class="sxs-lookup"><span data-stu-id="b90d7-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="b90d7-118">razón principal de Hello es colas de almacenamiento están más baratas y mucho más fácil tooprovision.</span><span class="sxs-lookup"><span data-stu-id="b90d7-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="b90d7-119">Los mensajes individuales en una cola de almacenamiento están limitados en tamaño too64 KB.</span><span class="sxs-lookup"><span data-stu-id="b90d7-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="b90d7-120">Si necesita toopass mensajes más grandes entre funciones, una cola de Service Bus de Azure pueden tamaños de los mensajes utilizados toosupport seguridad too256 KB.</span><span class="sxs-lookup"><span data-stu-id="b90d7-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="b90d7-121">Temas de Service Bus son útiles si necesita filtrado de mensajes antes del procesamiento.</span><span class="sxs-lookup"><span data-stu-id="b90d7-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="b90d7-122">Los concentradores de eventos son las comunicaciones de gran volumen de toosupport útil.</span><span class="sxs-lookup"><span data-stu-id="b90d7-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="b90d7-123">Escribir funciones toobe sin estado</span><span class="sxs-lookup"><span data-stu-id="b90d7-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="b90d7-124">Si es posible, las funciones no deben tener estado y ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="b90d7-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="b90d7-125">Asociar cualquier información de estado necesaria con los datos.</span><span class="sxs-lookup"><span data-stu-id="b90d7-125">Associate any required state information with your data.</span></span> <span data-ttu-id="b90d7-126">Por ejemplo, un pedido para procesar probablemente tendría un miembro `state` asociado.</span><span class="sxs-lookup"><span data-stu-id="b90d7-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="b90d7-127">Una función ha podido procesar un orden basado en ese estado mientras Hola sí misma sigue estando sin estado.</span><span class="sxs-lookup"><span data-stu-id="b90d7-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="b90d7-128">Las funciones idempotentes se recomiendan especialmente con desencadenadores de temporizador.</span><span class="sxs-lookup"><span data-stu-id="b90d7-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="b90d7-129">Por ejemplo, si tiene algo que sin duda debe ejecutarse una vez al día, escríbalo para poder ejecutarse cualquier momento durante el día de hello con hello mismos resultados.</span><span class="sxs-lookup"><span data-stu-id="b90d7-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="b90d7-130">función Hello puede salir cuando no hay ningún trabajo para un día determinado.</span><span class="sxs-lookup"><span data-stu-id="b90d7-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="b90d7-131">Si una ejecución anterior no pudo toocomplete, Hola ejecutar a continuación debe elegir donde se quedó.</span><span class="sxs-lookup"><span data-stu-id="b90d7-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="b90d7-132">Escritura de funciones defensivas</span><span class="sxs-lookup"><span data-stu-id="b90d7-132">Write defensive functions</span></span>

<span data-ttu-id="b90d7-133">Suponga que la función podría encontrarse con una excepción en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="b90d7-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="b90d7-134">Diseñar las funciones con hello capacidad toocontinue desde un punto de error anterior durante la ejecución del siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="b90d7-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="b90d7-135">Considere un escenario que requiere Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="b90d7-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="b90d7-136">Consulta de 10 000 filas en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="b90d7-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="b90d7-137">Crear un mensaje de la cola para cada una de esas tooprocess de filas más línea hello hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="b90d7-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="b90d7-138">Dependiendo de lo complejo que sea el sistema, es posible que haya servicios de bajada implicados con un comportamiento incorrecto, interrupciones de red, límites de cuota alcanzados, etc. Todo esto puede afectar a su función en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="b90d7-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="b90d7-139">Debe toodesign su toobe funciones preparado para él.</span><span class="sxs-lookup"><span data-stu-id="b90d7-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="b90d7-140">¿Cómo reacciona el código si se produce un error después de insertar 5000 de esos elementos en una cola para su procesamiento?</span><span class="sxs-lookup"><span data-stu-id="b90d7-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="b90d7-141">Realice un seguimiento de elementos de un conjunto que ha completado.</span><span class="sxs-lookup"><span data-stu-id="b90d7-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="b90d7-142">En caso contrario, podría insertarlos la próxima vez.</span><span class="sxs-lookup"><span data-stu-id="b90d7-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="b90d7-143">Esto puede tener un impacto grave en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b90d7-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="b90d7-144">Si ya se ha procesado un elemento de la cola, permitir la función toobe una operación inefectiva.</span><span class="sxs-lookup"><span data-stu-id="b90d7-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="b90d7-145">Sacar partido de las medidas defensivas ya proporcionada para los componentes que se use en la plataforma de funciones de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="b90d7-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="b90d7-146">Por ejemplo, vea **control de mensajes de la cola de mensajes dudosos** en la documentación de Hola para [cola de almacenamiento de Azure desencadena](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="b90d7-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="b90d7-147">No combinación de prueba y producción escribir código en hello misma aplicación (función)</span><span class="sxs-lookup"><span data-stu-id="b90d7-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="b90d7-148">Las funciones dentro de una aplicación de función compartan recursos.</span><span class="sxs-lookup"><span data-stu-id="b90d7-148">Functions within a function app share resources.</span></span> <span data-ttu-id="b90d7-149">Por ejemplo, la memoria se comparte.</span><span class="sxs-lookup"><span data-stu-id="b90d7-149">For example, memory is shared.</span></span> <span data-ttu-id="b90d7-150">Si usa una aplicación de la función en producción, no agregue funciones relacionadas con la prueba y tooit de recursos.</span><span class="sxs-lookup"><span data-stu-id="b90d7-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="b90d7-151">Se podría producir una sobrecarga inesperada durante la ejecución de código de producción.</span><span class="sxs-lookup"><span data-stu-id="b90d7-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="b90d7-152">Asegúrese de cargar en las aplicaciones de función de producción.</span><span class="sxs-lookup"><span data-stu-id="b90d7-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="b90d7-153">Memoria se promedian a través de cada función de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b90d7-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="b90d7-154">Si tiene un ensamblado compartido que se hace referencia en varias funciones. NET, colóquelo en una carpeta compartida común.</span><span class="sxs-lookup"><span data-stu-id="b90d7-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="b90d7-155">Ensamblado de Hola de referencia con un toohello similar de instrucción siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b90d7-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="b90d7-156">En caso contrario, es fácil tooaccidentally implementar varias versiones de prueba de hello mismo binario que se comporten de manera diferente entre las funciones.</span><span class="sxs-lookup"><span data-stu-id="b90d7-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="b90d7-157">No utilice el registro detallado en el código de producción.</span><span class="sxs-lookup"><span data-stu-id="b90d7-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="b90d7-158">Tiene un impacto negativo en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b90d7-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="b90d7-159">Uso del código asincrónico pero evitar las llamadas de bloqueo</span><span class="sxs-lookup"><span data-stu-id="b90d7-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="b90d7-160">La programación asincrónica es una práctica recomendada.</span><span class="sxs-lookup"><span data-stu-id="b90d7-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="b90d7-161">Sin embargo, evite siempre hace referencia a hello `Result` propiedad o llamar a `Wait` método en un `Task` instancia.</span><span class="sxs-lookup"><span data-stu-id="b90d7-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="b90d7-162">Este enfoque puede provocar el agotamiento de toothread.</span><span class="sxs-lookup"><span data-stu-id="b90d7-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="b90d7-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b90d7-163">Next steps</span></span>
<span data-ttu-id="b90d7-164">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b90d7-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="b90d7-165">Como Azure Functions usa Azure App Service, también debe conocer las guías de App Service.</span><span class="sxs-lookup"><span data-stu-id="b90d7-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* <span data-ttu-id="b90d7-166">[Patterns and Practices HTTP Performance Optimizations](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/) (Patrones y procedimientos de optimización del rendimiento de HTTP)</span><span class="sxs-lookup"><span data-stu-id="b90d7-166">[Patterns and Practices HTTP Performance Optimizations](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)</span></span>

