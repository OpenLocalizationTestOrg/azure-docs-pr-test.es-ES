---
title: temas de Bus de servicio de aaaHow toouse (Ruby) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus temas y suscripciones de Azure. Los ejemplos de código están escritos para aplicaciones Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>¿Cómo toouse Service Bus temas y suscripciones con Ruby
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este artículo se describe cómo toouse Service Bus temas y suscripciones desde aplicaciones Ruby. Hello escenarios descritos se incluyen **crear temas y suscripciones, crear filtros de suscripción, enviar mensajes** tooa tema, **recibir mensajes de una suscripción**, y  **eliminar temas y suscripciones**. Para obtener más información sobre los temas y suscripciones, vea hello [pasos](#next-steps) sección.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>de un tema
Hola **Azure::ServiceBusService** objeto permite toowork con temas. Hello código siguiente se crea un **Azure::ServiceBusService** objeto. toocreate un tema, usar hello `create_topic()` método. Hola de ejemplo siguiente crea un tema o imprime errores Hola si hay alguno.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

También puede pasar un **Azure::ServiceBus::Topic** objeto con opciones adicionales, que permiten la configuración de tema predeterminada toooverride como el tamaño de cola toolive o máximo de tiempo de mensaje. Hello ejemplo siguiente se muestra configuración máximo de cola de hello too5 GB de tamaño y de tiempo too1 toolive minuto:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Creación de suscripciones
Suscripciones al tema también se crean con hello **Azure::ServiceBusService** objeto. Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes entregados cola virtual de la suscripción de toohello.

Las suscripciones son persistentes y continuará tooexist hasta que ambos se o hello tema están asociadas, se eliminan. Si la aplicación contiene lógica toocreate una suscripción, debe comprobar primero si Hola ya existe la suscripción mediante hello getSubscription método.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Crea una suscripción con el filtro de hello predeterminado (MatchAll)
Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción. Cuando Hola **MatchAll** se utiliza el filtro, tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción de Hola. Hello en el ejemplo siguiente se crea una suscripción denominada "todos los mensajes" y usa Hola predeterminado **MatchAll** filtro.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Creación de suscripciones con filtros
También puede definir filtros que le permiten toospecify que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción específica.

el tipo más flexible de filtro compatible con las suscripciones Hello es hello **Azure::ServiceBus::SqlFilter**, que implementa un subconjunto de SQL92. Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema. Para obtener más información acerca de las expresiones de Hola que pueden usarse con un filtro SQL, revise hello [SqlFilter](service-bus-messaging-sql-filter.md) sintaxis.

Puede agregar filtros tooa suscripción mediante hello `create_rule()` método de hello **Azure::ServiceBusService** objeto. Este método permite tooadd nueva filtros tooan existente suscripción.

Puesto que el filtro de hello predeterminado se aplica automáticamente tooall nuevas suscripciones, primero debe quitar el filtro predeterminado de Hola u Hola **MatchAll** invalidará cualquier otro filtro que se puede especificar. Puede quitar regla predeterminada de hello mediante hello `delete_rule()` método en hello **Azure::ServiceBusService** objeto.

Hello en el ejemplo siguiente se crea una suscripción denominada "mensajes de alta" con un **Azure::ServiceBus::SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `message_number` propiedad mayor que 3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `low-messages` con una **Azure::ServiceBus::SqlFilter** que selecciona sólo los mensajes que tienen un `message_number` propiedad menor o igual too3:

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

Cuando se envía un mensaje ahora demasiado`test-topic`, es siempre ser entregado tooreceivers suscrito toohello `all-messages` suscripción al tema y tooreceivers selectivamente entregado suscrito toohello `high-messages` y `low-messages` (suscripciones de tema según el contenido del mensaje de Hola).

## <a name="send-messages-tooa-topic"></a>Enviar tema tooa de mensajes
toosend un tema de Bus de servicio de tooa de mensaje, la aplicación debe utilizar hello `send_topic_message()` método en hello **Azure::ServiceBusService** objeto. Mensajes envían a temas de Bus tooService son instancias de hello **Azure::ServiceBus::BrokeredMessage** objetos. **Azure::ServiceBus::BrokeredMessage** objetos tienen un conjunto de propiedades estándar (como `label` y `time_to_live`), un diccionario de propiedades de toohold usado personalizadas específicas de la aplicación y un cuerpo de datos de cadena. Una aplicación puede establecer el cuerpo de Hola de mensaje de saludo pasando un toohello del valor de cadena `send_topic_message()` método y las necesarias propiedades estándar se rellenará con valores predeterminados.

Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes demasiado`test-topic`. Tenga en cuenta que hello `message_number` valor de propiedad personalizada de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determina qué suscripción lo recibe):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema. El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).

## <a name="receive-messages-from-a-subscription"></a>Recepción de mensajes de una suscripción
Los mensajes se reciben de una suscripción mediante hello `receive_subscription_message()` método en hello **Azure::ServiceBusService** objeto. De forma predeterminada, los mensajes son read(peak) y bloqueado sin eliminarla de la suscripción de Hola. Puede leer y eliminar mensajes de bienvenida de suscripción Hola Hola establecer `peek_lock` opción demasiado**false**.

comportamiento predeterminado de Hello hace Hola lectura y eliminación de una operación de dos fases, esto también hace que las aplicaciones de toosupport posible que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `delete_subscription_message()` método y proporcionar toobe de mensaje de Hola eliminado como un parámetro. Hola `delete_subscription_message()` método marcar Hola mensaje como consumido y quitarlo de la suscripción de Hola.

Si hello `:peek_lock` parámetro está establecido demasiado**false**, leer y eliminar mensajes de bienvenida se convierte en el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

Hello en el ejemplo siguiente se muestra cómo se pueden recibir mensajes y el uso de procesado `receive_subscription_message()`. ejemplo Hello primero recibe y elimina un mensaje de Hola `low-messages` suscripción mediante el uso de `:peek_lock` establecido demasiado**false**, a continuación, recibe otro mensaje de Hola `high-messages` y, a continuación, elimina Hola mensaje utilizando `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlock_subscription_message()` método en hello **Azure::ServiceBusService** objeto. Este causas hello toounlock de Bus de servicio de mensajes dentro de la suscripción de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado a un mensaje bloqueado dentro de suscripción de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará el mensaje de bienvenida de automáticamente y hacerla disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `delete_subscription_message()` se llama al método, a continuación, mensaje de bienvenida es la aplicación de toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. Esta lógica a menudo se logra mediante hello `message_id` propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminación de temas y suscripciones
Temas y suscripciones son persistentes y debe ser explícitamente eliminados a través de hello [portal de Azure] [ Azure portal] o mediante programación. ejemplo de Hola siguiente muestra cómo se denomina tema de hello toodelete `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Eliminar un tema, también elimina todas las suscripciones que están registradas en el tema de Hola. También se pueden eliminar las suscripciones de forma independiente. Hello código siguiente muestra cómo se denomina suscripción de hello toodelete `high-messages` de hello `test-topic` tema:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de temas de Bus de servicio, siga estos toolearn de vínculos más.

* Vea [Colas, temas y suscripciones](service-bus-queues-topics-subscriptions.md).
* Referencia de API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).
* Visite hello [Azure SDK para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositorio en GitHub.

[Azure portal]: https://portal.azure.com
