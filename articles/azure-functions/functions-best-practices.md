---
title: Procedimientos recomendados de Azure Functions | Microsoft Docs
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
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="c58ca-104">Optimización del rendimiento y confiabilidad de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c58ca-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="c58ca-105">En este artículo se proporcionan instrucciones para mejorar el rendimiento y la confiabilidad de sus aplicaciones de función.</span><span class="sxs-lookup"><span data-stu-id="c58ca-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="c58ca-106">Evitar funciones de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="c58ca-106">Avoid long running functions</span></span>

<span data-ttu-id="c58ca-107">Las funciones grandes de ejecución prolongada pueden causar problemas de tiempo de espera inesperados.</span><span class="sxs-lookup"><span data-stu-id="c58ca-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="c58ca-108">Una función puede ser grande debido a numerosas dependencias de Node.js.</span><span class="sxs-lookup"><span data-stu-id="c58ca-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="c58ca-109">La importación de las dependencias también puede provocar mayores tiempos de carga que dan lugar a tiempos de expiración inesperados.</span><span class="sxs-lookup"><span data-stu-id="c58ca-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="c58ca-110">Las dependencias se cargan explícita e implícitamente.</span><span class="sxs-lookup"><span data-stu-id="c58ca-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="c58ca-111">Un módulo único cargado por el código puede cargar sus propios módulos adicionales.</span><span class="sxs-lookup"><span data-stu-id="c58ca-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="c58ca-112">Siempre que sea posible, refactorice funciones grandes en conjuntos más pequeños de funciones que trabajen juntos y devuelvan respuestas rápidas.</span><span class="sxs-lookup"><span data-stu-id="c58ca-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="c58ca-113">Por ejemplo, un webhook o una función de desencadenador HTTP podría requerir una respuesta de confirmación en un determinado período de tiempo. Es habitual que los webhooks requieran una respuesta inmediata.</span><span class="sxs-lookup"><span data-stu-id="c58ca-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="c58ca-114">Puede pasar la carga útil de desencadenador HTTP a una cola para ser procesada por una función de desencadenador de cola.</span><span class="sxs-lookup"><span data-stu-id="c58ca-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="c58ca-115">Este enfoque permite aplazar el trabajo real y devolver una respuesta inmediata.</span><span class="sxs-lookup"><span data-stu-id="c58ca-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="c58ca-116">Comunicación entre funciones</span><span class="sxs-lookup"><span data-stu-id="c58ca-116">Cross function communication</span></span>

<span data-ttu-id="c58ca-117">Cuando se integra varias funciones, normalmente es un procedimiento recomendado usar colas de almacenamiento para comunicación entre funciones.</span><span class="sxs-lookup"><span data-stu-id="c58ca-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="c58ca-118">La razón principal es que las colas de almacenamiento son más baratas y mucho más fáciles de aprovisionar.</span><span class="sxs-lookup"><span data-stu-id="c58ca-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="c58ca-119">Los mensajes individuales de una cola de almacenamiento tienen un límite de tamaño de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="c58ca-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="c58ca-120">Si tiene que pasar mensajes más grandes entre funciones, se podría usar una cola de Azure Service Bus para admitir tamaños de mensaje de hasta 256 KB.</span><span class="sxs-lookup"><span data-stu-id="c58ca-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="c58ca-121">Temas de Service Bus son útiles si necesita filtrado de mensajes antes del procesamiento.</span><span class="sxs-lookup"><span data-stu-id="c58ca-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="c58ca-122">Los concentradores de eventos son útiles para admitir comunicaciones de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="c58ca-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="c58ca-123">Escritura de funciones para que no tengan estado</span><span class="sxs-lookup"><span data-stu-id="c58ca-123">Write functions to be stateless</span></span> 

<span data-ttu-id="c58ca-124">Si es posible, las funciones no deben tener estado y ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="c58ca-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="c58ca-125">Asociar cualquier información de estado necesaria con los datos.</span><span class="sxs-lookup"><span data-stu-id="c58ca-125">Associate any required state information with your data.</span></span> <span data-ttu-id="c58ca-126">Por ejemplo, un pedido para procesar probablemente tendría un miembro `state` asociado.</span><span class="sxs-lookup"><span data-stu-id="c58ca-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="c58ca-127">Una función podría procesar un pedido en función de ese estado mientras que la propia función permanece sin estado.</span><span class="sxs-lookup"><span data-stu-id="c58ca-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="c58ca-128">Las funciones idempotentes se recomiendan especialmente con desencadenadores de temporizador.</span><span class="sxs-lookup"><span data-stu-id="c58ca-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="c58ca-129">Por ejemplo, si tiene algo que debe ejecutarse una vez al día obligatoriamente, escríbalo para poder ejecutarse en cualquier momento durante el día con los mismos resultados.</span><span class="sxs-lookup"><span data-stu-id="c58ca-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="c58ca-130">La función puede salir cuando no haya ningún trabajo para un día determinado.</span><span class="sxs-lookup"><span data-stu-id="c58ca-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="c58ca-131">Asimismo, si una ejecución anterior no se pudo completar, la siguiente ejecución debe continuar donde se quedó.</span><span class="sxs-lookup"><span data-stu-id="c58ca-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="c58ca-132">Escritura de funciones defensivas</span><span class="sxs-lookup"><span data-stu-id="c58ca-132">Write defensive functions</span></span>

<span data-ttu-id="c58ca-133">Suponga que la función podría encontrarse con una excepción en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="c58ca-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="c58ca-134">Diseñe las funciones con la capacidad de continuar a partir de un punto de error anterior durante la siguiente ejecución.</span><span class="sxs-lookup"><span data-stu-id="c58ca-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="c58ca-135">Considere un escenario que requiere las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="c58ca-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="c58ca-136">Consulta de 10 000 filas en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="c58ca-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="c58ca-137">Cree un mensaje de cola para cada una de esas filas para procesar más abajo la línea.</span><span class="sxs-lookup"><span data-stu-id="c58ca-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="c58ca-138">Dependiendo de lo complejo que sea el sistema, es posible que haya servicios de bajada implicados con un comportamiento incorrecto, interrupciones de red, límites de cuota alcanzados, etc. Todo esto puede afectar a su función en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="c58ca-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="c58ca-139">Debe diseñar las funciones para que estén preparadas para ello.</span><span class="sxs-lookup"><span data-stu-id="c58ca-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="c58ca-140">¿Cómo reacciona el código si se produce un error después de insertar 5000 de esos elementos en una cola para su procesamiento?</span><span class="sxs-lookup"><span data-stu-id="c58ca-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="c58ca-141">Realice un seguimiento de elementos de un conjunto que ha completado.</span><span class="sxs-lookup"><span data-stu-id="c58ca-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="c58ca-142">En caso contrario, podría insertarlos la próxima vez.</span><span class="sxs-lookup"><span data-stu-id="c58ca-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="c58ca-143">Esto puede tener un impacto grave en el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c58ca-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="c58ca-144">Si ya se ha procesado un elemento de la cola, permita que la función sea no operativa.</span><span class="sxs-lookup"><span data-stu-id="c58ca-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="c58ca-145">Aproveche las medidas defensivas ya proporcionadas para los componentes que se usa en la plataforma de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c58ca-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="c58ca-146">Por ejemplo, vea la información sobre el **tratamiento de mensajes dudosos en la cola** en la documentación del [desencadenador de cola de Azure Storage](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="c58ca-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="c58ca-147">No mezclar código de prueba y producción en la misma aplicación de función</span><span class="sxs-lookup"><span data-stu-id="c58ca-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="c58ca-148">Las funciones dentro de una aplicación de función compartan recursos.</span><span class="sxs-lookup"><span data-stu-id="c58ca-148">Functions within a function app share resources.</span></span> <span data-ttu-id="c58ca-149">Por ejemplo, la memoria se comparte.</span><span class="sxs-lookup"><span data-stu-id="c58ca-149">For example, memory is shared.</span></span> <span data-ttu-id="c58ca-150">Si usa una aplicación de función en producción, no agregue recursos y funciones relacionados con pruebas a ella.</span><span class="sxs-lookup"><span data-stu-id="c58ca-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="c58ca-151">Se podría producir una sobrecarga inesperada durante la ejecución de código de producción.</span><span class="sxs-lookup"><span data-stu-id="c58ca-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="c58ca-152">Asegúrese de cargar en las aplicaciones de función de producción.</span><span class="sxs-lookup"><span data-stu-id="c58ca-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="c58ca-153">La memoria se promedia entre cada función de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c58ca-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="c58ca-154">Si tiene un ensamblado compartido que se hace referencia en varias funciones. NET, colóquelo en una carpeta compartida común.</span><span class="sxs-lookup"><span data-stu-id="c58ca-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="c58ca-155">Haga referencia al ensamblado con una instrucción similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c58ca-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="c58ca-156">En caso contrario, es fácil implementar accidentalmente varias versiones de prueba del mismo binario que se comporten de manera diferente entre funciones.</span><span class="sxs-lookup"><span data-stu-id="c58ca-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="c58ca-157">No utilice el registro detallado en el código de producción.</span><span class="sxs-lookup"><span data-stu-id="c58ca-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="c58ca-158">Tiene un impacto negativo en el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="c58ca-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="c58ca-159">Uso del código asincrónico pero evitar las llamadas de bloqueo</span><span class="sxs-lookup"><span data-stu-id="c58ca-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="c58ca-160">La programación asincrónica es una práctica recomendada.</span><span class="sxs-lookup"><span data-stu-id="c58ca-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="c58ca-161">Sin embargo, evite siempre las referencias a la propiedad `Result` o las llamadas al método `Wait` en una instancia `Task`.</span><span class="sxs-lookup"><span data-stu-id="c58ca-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="c58ca-162">Este enfoque puede provocar el agotamiento de subprocesos.</span><span class="sxs-lookup"><span data-stu-id="c58ca-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="c58ca-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c58ca-163">Next steps</span></span>
<span data-ttu-id="c58ca-164">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="c58ca-164">For more information, see the following resources:</span></span>

<span data-ttu-id="c58ca-165">Como Azure Functions usa Azure App Service, también debe conocer las guías de App Service.</span><span class="sxs-lookup"><span data-stu-id="c58ca-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* <span data-ttu-id="c58ca-166">[Patterns and Practices HTTP Performance Optimizations](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/) (Patrones y procedimientos de optimización del rendimiento de HTTP)</span><span class="sxs-lookup"><span data-stu-id="c58ca-166">[Patterns and Practices HTTP Performance Optimizations](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)</span></span>

