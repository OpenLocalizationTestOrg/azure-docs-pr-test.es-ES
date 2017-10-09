---
title: pone en cola con Ruby aaaHow toouse Service Bus de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Bus de servicio pone en cola en Azure. Ejemplos de código escritos en Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>¿Cómo toouse Bus de servicio pone en cola con Ruby

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Esta guía se describe cómo toouse colas de Service Bus. ejemplos de Hello están escritos en Ruby y usar hello Azure indicador. Hello escenarios descritos se incluyen **crear colas, enviar y recibir mensajes**, y **eliminar colas**. Para obtener más información acerca de las colas de Bus de servicio, vea hello [pasos](#next-steps) sección.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>¿Cómo toocreate una cola
Hola **Azure::ServiceBusService** objeto permite toowork con colas. toocreate una cola, usar hello `create_queue()` método. Hello en el ejemplo siguiente se crea una cola o imprime los errores.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

También puede pasar un **Azure::ServiceBus::Queue** objeto con opciones adicionales, lo que permite toooverride Hola predeterminada configuración de la cola, como el tamaño de cola toolive o máximo de tiempo de mensaje. Hola siguiente ejemplo muestra cómo tooset Hola GB de too5 de tamaño máximo de la cola y too1 toolive minuto de tiempo:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>¿Cómo toosend mensajes tooa cola
la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `send_queue_message()` método en hello **Azure::ServiceBusService** objeto. Los mensajes de las colas son demasiado (recibidos y enviados desde) Bus de servicio **Azure::ServiceBus::BrokeredMessage** objetos y tener un conjunto de propiedades estándar (como `label` y `time_to_live`), un diccionario que es usado toohold propiedades personalizadas de específicos de la aplicación y un cuerpo de datos de aplicación arbitrarios. Una aplicación puede establecer cuerpo Hola de mensaje de bienvenida, pasando el valor de cadena como mensaje de bienvenida y las propiedades estándares necesarias se rellenan con los valores predeterminados.

Hello en el ejemplo siguiente se muestra cómo toosend una cola de toohello de mensajes de prueba denominado `test-queue` con `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo. El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.

## <a name="how-tooreceive-messages-from-a-queue"></a>¿Cómo tooreceive mensajes desde una cola
Se reciben mensajes de una cola utilizando hello `receive_queue_message()` método en hello **Azure::ServiceBusService** objeto. De forma predeterminada, los mensajes se leen y bloqueados sin que se eliminen de cola de Hola. Sin embargo, puede eliminar los mensajes de cola de hello cuando se leen por establecer hello `:peek_lock` opción demasiado**false**.

comportamiento predeterminado de Hello hace Hola lectura y eliminación de una operación de dos fases, esto también hace que las aplicaciones de toosupport posible que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `delete_queue_message()` método y proporcionar toobe de mensaje de Hola eliminado como un parámetro. Hola `delete_queue_message()` método marcar Hola mensaje como consumido y quitarlo de la cola de Hola.

Si hello `:peek_lock` parámetro está establecido demasiado**false**, leer y eliminar mensajes de bienvenida se convierte en el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus se marcado como mensaje de Hola como consumido, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

Hello en el ejemplo siguiente se muestra cómo tooreceive y procesar mensajes usando `receive_queue_message()`. ejemplo de Hola primero recibe y elimina un mensaje mediante el uso de `:peek_lock` establecido demasiado**false**, a continuación, recibe otro mensaje y, a continuación, elimina Hola mensaje utilizando `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlock_queue_message()` método en hello **Azure::ServiceBusService** objeto. Este causas llamada hello toounlock de Bus de servicio de mensajes en cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de Hola expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida de automáticamente y la convierte en disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `delete_queue_message()` se llama al método, a continuación, mensaje de bienvenida es la aplicación de toohello entregados de nuevo cuando se reinicia. Este proceso se denomina a menudo *al menos una vez procesamiento*; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra utilizando hello `message_id` propiedad del mensaje de Hola, que permanece constante en los intentos de entrega.

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de colas de Service Bus, siga estas toolearn de vínculos más.

* Información general de [colas, temas y suscripciones](service-bus-queues-topics-subscriptions.md).
* Visite hello [Azure SDK para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositorio en GitHub.

Para obtener una comparación entre las colas de Service Bus de Azure de hello descritas en este artículo y las colas de Azure descrito en hello [cómo toouse Queue storage from. Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) artículo, consulte [colas de Azure y colas de Bus de servicio de Azure: comparación y diferencias](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

