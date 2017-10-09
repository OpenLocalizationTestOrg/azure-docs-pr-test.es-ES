---
title: pone en cola aaaHow toouse Service Bus de Azure con Java | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Bus de servicio pone en cola en Azure. Ejemplos de código escritos en Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a>¿Cómo toouse Bus de servicio pone en cola con Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artículo se describe cómo toouse colas de Service Bus. ejemplos de Hello están escritos en Java y usar hello [Azure SDK para Java][Azure SDK for Java]. Hello escenarios descritos se incluyen **crear colas**, **enviar y recibir mensajes**, y **eliminar colas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación toouse
Asegúrese de que ha instalado hello [Azure SDK para Java] [ Azure SDK for Java] antes de compilar este ejemplo. Si está usando Eclipse, puede instalar hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse] que incluye hello Azure SDK para Java. A continuación, puede agregar hello **bibliotecas de Microsoft Azure para Java** tooyour proyecto:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Agregue los siguiente hello `import` superior de toohello instrucciones Hola del archivo de Java:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Creación de una cola
Las operaciones de administración para las colas de Service Bus se pueden realizar por medio de la clase **ServiceBusContract**. A **ServiceBusContract** objeto se construyó con una configuración apropiada que encapsula el token SAS con permisos toomanage y hello **ServiceBusContract** clase es punto único de Hola comunicación con Azure.

Hola **ServiceBusService** clase proporciona métodos toocreate, enumerar y eliminar las colas. Hola de ejemplo siguiente se muestra cómo un **ServiceBusService** objeto puede ser usado toocreate una cola con el nombre `TestQueue`, con un espacio de nombres denominado `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Hay métodos en `QueueInfo` que permiten propiedades de hello cola toobe optimizado (por ejemplo: tooset Hola predeterminado time-to-live (TTL) valor toobe aplica toomessages envía toohello cola). Hello en el ejemplo siguiente se muestra cómo toocreate una cola denominada `TestQueue` con un tamaño máximo de 5 GB:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Tenga en cuenta que puede usar hello `listQueues` método **ServiceBusContract** objetos toocheck si ya existe una cola con un nombre especificado dentro de un espacio de nombres de servicio.

## <a name="send-messages-tooa-queue"></a>Cola de mensajes tooa de envío
una cola de Service Bus de mensajes tooa toosend, la aplicación obtiene un **ServiceBusContract** objeto. Hola el siguiente código se muestra cómo un mensaje para hello toosend `TestQueue` cola creada previamente en hello `HowToSample` espacio de nombres:

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Mensajes envían a y recibidos de Bus de servicio colas son instancias de hello [BrokeredMessage] [ BrokeredMessage] clase. [BrokeredMessage] [ BrokeredMessage] objetos tienen un conjunto de propiedades estándar (como [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) y [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un diccionario que es usado toohold personalizado propiedades específicas de la aplicación y un cuerpo de datos de aplicación arbitrarios. Una aplicación puede establecer cuerpo Hola de mensaje de saludo pasando cualquier objeto serializable en el constructor de Hola de hello [BrokeredMessage][BrokeredMessage], y, a continuación, se utilizará el serializador adecuado Hola objeto de hello tooserialize. También puede especificar un objeto **java.IO.InputStream**.

Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes toothe `TestQueue` **MessageSender** se obtenido en el fragmento de código de hello anterior:

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo. El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.

## <a name="receive-messages-from-a-queue"></a>mensajes de una cola
mensajes de tooreceive de modo principal de saludo de una cola es toouse una **ServiceBusContract** objeto. Los mensajes recibidos pueden funcionar en dos modos distintos: **ReceiveAndDelete** y **PeekLock**.

Cuando se usa hello **ReceiveAndDelete** modo, de recepción es una operación de captura único: es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje en una cola, marca Hola mensaje como consumido y lo devuelve toohello aplicación. **ReceiveAndDelete** modo (que es el modo predeterminado de hello) es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.
Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

En **PeekLock** , el modo de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a **eliminar** en mensajes de bienvenida recibido. Al Bus de servicio ve hello **eliminar** llamada, se marca el mensaje Hola como consumido y quitarlo de la cola de Hola.

Hello en el ejemplo siguiente se muestra cómo se pueden recibir mensajes y el uso de procesado **PeekLock** modo (no en el modo de saludo predeterminado). hace un bucle infinito Hello ejemplo siguiente y procesa los mensajes que llegan en nuestro `TestQueue`:

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>No se puede leer mensajes y cómo se bloquea la aplicación de toohandle
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello **unlockMessage** método en mensajes de bienvenida recibido (en lugar de hello **deleteMessage** método). Este causas hello toounlock de Bus de servicio de mensajes en cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado con un mensaje bloqueado de la cola, y si la aplicación hello falla tooprocess Hola mensaje antes de que el tiempo de espera de bloqueo expire (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida automáticamente y hace disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello **deleteMessage** se emite la solicitud, a continuación, mensaje de bienvenida es la aplicación de toohello entregados de nuevo cuando se reinicia. Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra utilizando hello **getMessageId** método del mensaje de Hola, que permanece constante en los intentos de entrega.

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas, temas y suscripciones] [ Queues, topics, and subscriptions] para obtener más información.

Para obtener más información, vea hello [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
