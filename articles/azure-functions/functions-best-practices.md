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
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Optimizar el rendimiento de Hola y confiabilidad de las funciones de Azure

Este artículo proporciona rendimiento de orientación tooimprove hello y la confiabilidad de las aplicaciones de la función. 


## <a name="avoid-long-running-functions"></a>Evitar funciones de ejecución prolongada

Las funciones grandes de ejecución prolongada pueden causar problemas de tiempo de espera inesperados. Una función puede llegar a ser grande debido a dependencias de Node.js toomany. La importación de las dependencias también puede provocar mayores tiempos de carga que dan lugar a tiempos de expiración inesperados. Las dependencias se cargan explícita e implícitamente. Un módulo único cargado por el código puede cargar sus propios módulos adicionales.  

Siempre que sea posible, refactorice funciones grandes en conjuntos más pequeños de funciones que trabajen juntos y devuelvan respuestas rápidas. Por ejemplo, un webhook o en función de activación HTTP puede requerir una respuesta de confirmación en un determinado período de tiempo; es habitual webhooks toorequire una respuesta inmediata. Carga de desencadenador de hello HTTP puede pasar a un toobe de cola procesado por una función de activación de cola. Este enfoque permite trabajo real de toodefer hello y devolver una respuesta inmediata.


## <a name="cross-function-communication"></a>Comunicación entre funciones

Cuando se integra varias funciones, suele ser una mejor práctica toouse las colas de almacenamiento para la función comunicación cruzada.  razón principal de Hello es colas de almacenamiento están más baratas y mucho más fácil tooprovision. 

Los mensajes individuales en una cola de almacenamiento están limitados en tamaño too64 KB. Si necesita toopass mensajes más grandes entre funciones, una cola de Service Bus de Azure pueden tamaños de los mensajes utilizados toosupport seguridad too256 KB.

Temas de Service Bus son útiles si necesita filtrado de mensajes antes del procesamiento.

Los concentradores de eventos son las comunicaciones de gran volumen de toosupport útil.


## <a name="write-functions-toobe-stateless"></a>Escribir funciones toobe sin estado 

Si es posible, las funciones no deben tener estado y ser idempotentes. Asociar cualquier información de estado necesaria con los datos. Por ejemplo, un pedido para procesar probablemente tendría un miembro `state` asociado. Una función ha podido procesar un orden basado en ese estado mientras Hola sí misma sigue estando sin estado. 

Las funciones idempotentes se recomiendan especialmente con desencadenadores de temporizador. Por ejemplo, si tiene algo que sin duda debe ejecutarse una vez al día, escríbalo para poder ejecutarse cualquier momento durante el día de hello con hello mismos resultados. función Hello puede salir cuando no hay ningún trabajo para un día determinado. Si una ejecución anterior no pudo toocomplete, Hola ejecutar a continuación debe elegir donde se quedó.


## <a name="write-defensive-functions"></a>Escritura de funciones defensivas

Suponga que la función podría encontrarse con una excepción en cualquier momento. Diseñar las funciones con hello capacidad toocontinue desde un punto de error anterior durante la ejecución del siguiente Hola. Considere un escenario que requiere Hola siguientes acciones:

1. Consulta de 10 000 filas en una base de datos.
2. Crear un mensaje de la cola para cada una de esas tooprocess de filas más línea hello hacia abajo.
 
Dependiendo de lo complejo que sea el sistema, es posible que haya servicios de bajada implicados con un comportamiento incorrecto, interrupciones de red, límites de cuota alcanzados, etc. Todo esto puede afectar a su función en cualquier momento. Debe toodesign su toobe funciones preparado para él.

¿Cómo reacciona el código si se produce un error después de insertar 5000 de esos elementos en una cola para su procesamiento? Realice un seguimiento de elementos de un conjunto que ha completado. En caso contrario, podría insertarlos la próxima vez. Esto puede tener un impacto grave en el flujo de trabajo. 

Si ya se ha procesado un elemento de la cola, permitir la función toobe una operación inefectiva.

Sacar partido de las medidas defensivas ya proporcionada para los componentes que se use en la plataforma de funciones de Azure de Hola. Por ejemplo, vea **control de mensajes de la cola de mensajes dudosos** en la documentación de Hola para [cola de almacenamiento de Azure desencadena](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>No combinación de prueba y producción escribir código en hello misma aplicación (función)

Las funciones dentro de una aplicación de función compartan recursos. Por ejemplo, la memoria se comparte. Si usa una aplicación de la función en producción, no agregue funciones relacionadas con la prueba y tooit de recursos. Se podría producir una sobrecarga inesperada durante la ejecución de código de producción.

Asegúrese de cargar en las aplicaciones de función de producción. Memoria se promedian a través de cada función de la aplicación hello.

Si tiene un ensamblado compartido que se hace referencia en varias funciones. NET, colóquelo en una carpeta compartida común. Ensamblado de Hola de referencia con un toohello similar de instrucción siguiente ejemplo: 

    #r "..\Shared\MyAssembly.dll". 

En caso contrario, es fácil tooaccidentally implementar varias versiones de prueba de hello mismo binario que se comporten de manera diferente entre las funciones.

No utilice el registro detallado en el código de producción. Tiene un impacto negativo en el rendimiento.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Uso del código asincrónico pero evitar las llamadas de bloqueo

La programación asincrónica es una práctica recomendada. Sin embargo, evite siempre hace referencia a hello `Result` propiedad o llamar a `Wait` método en un `Task` instancia. Este enfoque puede provocar el agotamiento de toothread.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes:

Como Azure Functions usa Azure App Service, también debe conocer las guías de App Service.
* [Patterns and Practices HTTP Performance Optimizations](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/) (Patrones y procedimientos de optimización del rendimiento de HTTP)

