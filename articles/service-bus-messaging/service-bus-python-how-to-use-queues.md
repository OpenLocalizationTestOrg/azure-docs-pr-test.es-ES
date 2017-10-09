---
title: pone en cola con Python aaaHow toouse Service Bus de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus de Azure pone en cola de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>¿Cómo toouse Bus de servicio pone en cola con Python

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artículo se describe cómo toouse colas de Service Bus. ejemplos de Hello están escritos en Python y usar hello [paquete de Python Azure Service Bus][Python Azure Service Bus package]. Hello escenarios descritos se incluyen **crear colas, enviar y recibir mensajes**, y **eliminar colas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> tooinstall Python o hello [paquete de Python Azure Service Bus][Python Azure Service Bus package], vea hello [Guía de instalación de Python](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Creación de una cola
Hola **ServiceBusService** objeto permite toowork con colas. Agregue Hola después código cerca de la parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically Bus de servicio:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Hello código siguiente se crea un **ServiceBusService** objeto. Reemplace `mynamespace`, `sharedaccesskeyname` y `sharedaccesskey` por el espacio de nombres, el valor y el nombre de clave de la firma de acceso compartido (SAS).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello valores de nombre de clave de SAS de Hola y el valor pueden encontrarse en hello [portal de Azure] [ Azure portal] información de conexión, o en Visual Studio hello **propiedades** panel al seleccionar Hola nombres de Bus de servicio en el Explorador de servidores (como se muestra en la sección anterior de hello).

```python
bus_service.create_queue('taskqueue')
```

Hola `create_queue` método es compatible también con opciones adicionales, que permiten la configuración de la cola de toooverride de forma predeterminada como la hora del mensaje toolive (TTL) o tamaño máximo de cola. Hello en el ejemplo siguiente se establece Hola cola máximo tamaño too5 GB y minuto de hello TTL valor too1:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>Cola de mensajes tooa de envío
la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `send_queue_message` método en hello **ServiceBusService** objeto.

Hello en el ejemplo siguiente se muestra cómo toosend una cola de toohello de mensajes de prueba denominado `taskqueue` con `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo. El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB. Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>mensajes de una cola
Se reciben mensajes de una cola utilizando hello `receive_queue_message` método en hello **ServiceBusService** objeto:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

Se eliminan mensajes de cola de hello cuando se leen cuando Hola parámetro `peek_lock` se establece demasiado**False**. Puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la cola de Hola por establecer el parámetro de hello `peek_lock` demasiado**True**.

Hola comportamiento de lectura y eliminación de mensajes de bienvenida tal como parte del programa Hola a la operación de recepción es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

Si hello `peek_lock` parámetro está establecido demasiado**True**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola recibir proceso que realiza la llamada hello **eliminar** método en hello **mensaje** objeto. Hola **eliminar** método marcar Hola mensaje como consumido y quitarlo de la cola de Hola.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello **desbloquear** método en hello **mensaje** objeto. Esto provocará el mensaje de saludo toounlock de Bus de servicio de cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si se produce un error de aplicación de hello tooprocess Hola mensaje antes de Hola tiempo de espera de bloqueo expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará automáticamente mensajes de bienvenida y hacerla disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello **eliminar** se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar **al menos una vez procesamiento**; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra utilizando hello **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido los conceptos básicos de Hola de colas de Service Bus, vea estos toolearn artículos más.

* [Colas, temas y suscripciones][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

