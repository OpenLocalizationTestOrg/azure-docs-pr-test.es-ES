---
title: temas de Service Bus de Azure aaaHow toouse con Python | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus de Azure temas y suscripciones de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>¿Cómo toouse Service Bus temas y suscripciones a Python

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artículo se describe cómo toouse Service Bus temas y suscripciones. ejemplos de Hello están escritos en Python y usar hello [paquete Azure SDK para Python][Azure Python package]. Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar tema de mensajes tooa**, **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**. Para obtener más información acerca de temas y suscripciones, vea hello [pasos](#next-steps) sección.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Si necesita tooinstall Python o hello [paquete de Python de Azure][Azure Python package], vea hello [Guía de instalación de Python](../python-how-to-install.md).

## <a name="create-a-topic"></a>de un tema
Hola **ServiceBusService** objeto permite toowork con temas. Agregue los siguiente Hola cerca de parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically Bus de servicio:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Hello código siguiente se crea un **ServiceBusService** objeto. Reemplace `mynamespace`, `sharedaccesskeyname` y `sharedaccesskey` por el espacio de nombres real, el valor y el nombre de clave de la firma de acceso compartido (SAS).

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Puede obtener los valores de Hola Hola SAS como nombre de clave y valor de hello [portal de Azure][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Hola `create_topic` método es compatible también con opciones adicionales, que permiten la configuración de tema predeterminada toooverride como tamaño de tema toolive o máximo de tiempo de mensaje. Hello en el ejemplo siguiente se establece Hola tema máximo tamaño too5 GB y un valor de hora toolive (TTL) de 1 minuto:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Creación de suscripciones
También se crean suscripciones tootopics con hello **ServiceBusService** objeto. Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes entregados cola virtual de la suscripción de toohello.

> [!NOTE]
> Las suscripciones son persistentes y continuará tooexist hasta que ambos se o hello toowhich de tema está suscrito, se eliminan.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Crea una suscripción con el filtro de hello predeterminado (MatchAll)
Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción. Cuando Hola **MatchAll** se utiliza el filtro, tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción de Hola. Hello en el ejemplo siguiente se crea una suscripción denominada `AllMessages` y utiliza Hola predeterminado **MatchAll** filtro.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Creación de suscripciones con filtros
También puede definir filtros que le permiten toospecify que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción de tema específico.

Hola tipo más flexible de filtro compatible con las suscripciones es un **SqlFilter**, que implementa un subconjunto de SQL92. Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema. Para obtener más información acerca de las expresiones de Hola que puede usarse con un filtro SQL, vea hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintaxis.

Puede agregar filtros tooa suscripción mediante hello **crear\_regla** método de hello **ServiceBusService** objeto. Este método permite tooadd nueva filtros tooan existente suscripción.

> [!NOTE]
> Porque el filtro de hello predeterminado se aplica automáticamente tooall nuevas suscripciones, primero debe quitar filtro predeterminado de Hola o hello **MatchAll** invalidará cualquier otro filtro que se puede especificar. Puede quitar regla predeterminada de hello mediante hello `delete_rule` método de hello **ServiceBusService** objeto.
> 
> 

Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `messagenumber` propiedad mayor que 3:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un `messagenumber` propiedad menor o igual too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Ahora, cuando se envía un mensaje demasiado`mytopic` siempre se entrega tooreceivers suscrito toohello **AllMessages** suscripción al tema y tooreceivers selectivamente entregado suscrito toohello **HighMessages**  y **LowMessages** suscripciones al tema (según el contenido del mensaje Hola).

## <a name="send-messages-tooa-topic"></a>Enviar tema tooa de mensajes
toosend un tema de Bus de servicio de tooa de mensaje, la aplicación debe utilizar hello `send_topic_message` método de hello **ServiceBusService** objeto.

Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes demasiado`mytopic`. Tenga en cuenta que hello `messagenumber` valor de propiedad de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determina qué suscripciones reciban):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema. El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB). Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Recepción de mensajes de una suscripción
Los mensajes se reciben de una suscripción mediante hello `receive_subscription_message` método en hello **ServiceBusService** objeto:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

Se eliminan mensajes de suscripción de hello cuando se leen cuando Hola parámetro `peek_lock` se establece demasiado**False**. Puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la cola de Hola por establecer el parámetro de hello `peek_lock` demasiado**True**.

Hola comportamiento de lectura y eliminación de mensajes de bienvenida tal como parte del programa Hola a la operación de recepción es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

Si hello `peek_lock` parámetro está establecido demasiado**True**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `delete` método en hello **mensaje** objeto. Hola `delete` método marca el mensaje Hola como consumido y lo quita de la suscripción de Hola.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlock` método en hello **mensaje** objeto. Esto provocará el mensaje de saludo toounlock de Bus de servicio de suscripción de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado dentro de suscripción de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de Hola expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida de automáticamente y la convierte en disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `delete` se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra utilizando hello **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminación de temas y suscripciones
Temas y suscripciones son persistentes y debe ser explícitamente eliminados a través de hello [portal de Azure] [ Azure portal] o mediante programación. Hello en el ejemplo siguiente se muestra cómo se denomina tema de hello toodelete `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

Eliminar un tema, también elimina todas las suscripciones que están registradas en el tema de Hola. También se pueden eliminar las suscripciones de forma independiente. Hello código siguiente muestra cómo toodelete una suscripción denominada `HighMessages` de hello `mytopic` tema:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de temas de Bus de servicio, siga estos toolearn de vínculos más.

* Vea [Colas, temas y suscripciones][Queues, topics, and subscriptions].
* Referencia para [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
