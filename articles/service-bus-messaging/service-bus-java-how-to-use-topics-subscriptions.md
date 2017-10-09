---
title: temas de aaaHow toouse Service Bus de Azure con Java | Documentos de Microsoft
description: Uso de temas y suscripciones de Service Bus en Azure
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>¿Cómo toouse Service Bus temas y suscripciones con Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Esta guía se describe cómo toouse Service Bus temas y suscripciones. ejemplos de Hello están escritos en Java y usar hello [Azure SDK para Java][Azure SDK for Java]. Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar tema de mensajes tooa**, **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Qué son los temas y las suscripciones del Bus de servicio
Las suscripciones y los temas del Bus de servicio son compatibles con el modelo de comunicación de mensajería de *publicación/suscripción* . Cuando se usan temas y suscripciones, los componentes de una aplicación distribuida no se comunican directamente entre sí, sino que intercambian mensajes a través de un tema, que actúa como un intermediario.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

A diferencia de las colas del Bus de servicio, en las que un solo destinatario procesa cada mensaje, los temas y las suscripciones proporcionan una forma de comunicación de uno a varios mediante un patrón de publicación/suscripción. Es posible registrar varios temas de tooa de suscripciones. Cuando se envía un mensaje tooa tema, luego se convierte en disponible tooeach suscripción toohandle o proceso por separado.

Un tema de tooa de suscripción es similar a una cola virtual que recibe copias de mensajes de Hola que se enviaron toohello tema. Si lo desea, puede registrar las reglas de filtro para un tema en una base por suscripción, lo que le permite toofilter/restringir qué tema tooa de mensajes son recibidos por qué suscripciones al tema.

Las suscripciones y los temas de Bus de servicio le permiten tooscale tooprocess un gran número de mensajes a través de un gran número de usuarios y aplicaciones.

## <a name="create-a-service-namespace"></a>Creación de un espacio de nombres de servicio
toobegin con temas de Bus de servicio y las suscripciones de Azure, primero debe crear un espacio de nombres, que proporciona un contenedor de ámbito para tener acceso a recursos de Bus de servicio dentro de la aplicación.

toocreate un espacio de nombres:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar el Bus de servicio de aplicación toouse
Asegúrese de que ha instalado hello [Azure SDK para Java] [ Azure SDK for Java] antes de compilar este ejemplo. Si está usando Eclipse, puede instalar hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse] que incluye hello Azure SDK para Java. A continuación, puede agregar hello **bibliotecas de Microsoft Azure para Java** tooyour proyecto:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Agregue los siguiente hello `import` superior de toohello instrucciones Hola del archivo de Java:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Agregar Hola bibliotecas de Azure para Java tooyour ruta de acceso de compilación e incluirla en el ensamblado de implementación del proyecto.

## <a name="create-a-topic"></a>de un tema
Las operaciones de administración para los temas de Service Bus pueden realizarse mediante la clase **ServiceBusContract**. A **ServiceBusContract** objeto se construyó con una configuración apropiada que encapsula el token SAS con permisos toomanage y hello **ServiceBusContract** clase es punto único de Hola comunicación con Azure.

Hola **ServiceBusService** clase proporciona métodos toocreate, enumerar y eliminar los temas. Hola siguiente ejemplo se muestra cómo un **ServiceBusService** objeto puede ser usado toocreate un tema denominado `TestTopic`, con un espacio de nombres denominado `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Hay métodos en **TopicInfo** que habilitar propiedades de tema de hello establecerse (por ejemplo: tooset Hola predeterminado time-to-live (TTL) valor toobe aplica toomessages envía toohello tema). Hello en el ejemplo siguiente se muestra cómo toocreate un tema denominado `TestTopic` con un tamaño máximo de 5 GB:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Tenga en cuenta que puede usar hello **listTopics** método **ServiceBusContract** objetos toocheck si ya existe un tema con un nombre especificado dentro de un espacio de nombres de servicio.

## <a name="create-subscriptions"></a>Creación de suscripciones
También se crean suscripciones tootopics con hello **ServiceBusService** clase. Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes que se pasan cola virtual de la suscripción de toohello.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Crea una suscripción con el filtro de hello predeterminado (MatchAll)
Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción. Cuando Hola **MatchAll** filtro se usa, el tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción. Hello en el ejemplo siguiente se crea una suscripción denominada "AllMessages" y usa Hola predeterminado **MatchAll** filtro.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Creación de suscripciones con filtros
También puede crear filtros que le permiten tooscope que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción de tema específico.

Hola tipo más flexible de filtro compatible con las suscripciones es el [SqlFilter][SqlFilter], que implementa un subconjunto de SQL92. Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema. Para obtener más información acerca de las expresiones de Hola que pueden usarse con un filtro SQL, revise hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintaxis.

Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un [SqlFilter] [ SqlFilter] objeto que selecciona sólo los mensajes que tienen un personalizado **MessageNumber** propiedad es mayor que 3:

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un [SqlFilter] [ SqlFilter] objeto que selecciona sólo los mensajes que tienen un **MessageNumber** propiedad menor o igual too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Cuando se envía un mensaje ahora demasiado`TestTopic`, siempre se entregarán tooreceivers suscrito toohello `AllMessages` suscripción y tooreceivers selectivamente entregado suscrito toohello `HighMessages` y `LowMessages` (de suscripciones Dependiendo del contenido del mensaje).

## <a name="send-messages-tooa-topic"></a>Enviar tema tooa de mensajes
toosend un tema de Bus de servicio de tooa de mensaje, la aplicación obtiene un **ServiceBusContract** objeto. Hello código siguiente se muestra cómo un mensaje para hello toosend `TestTopic` tema creado previamente en hello `HowToSample` espacio de nombres:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

Instancias de los mensajes enviados tooService Bus temas son la [BrokeredMessage] [ BrokeredMessage] clase. [BrokeredMessage][BrokeredMessage]* objetos tienen un conjunto de métodos estándar (como **setLabel** y **TimeToLive**), un diccionario que es usado toohold personalizado propiedades específicas de la aplicación y un cuerpo de datos de aplicación arbitrarios. Una aplicación puede establecer el cuerpo de saludo del mensaje pasando cualquier objeto serializable en el constructor de saludo de la [BrokeredMessage][BrokeredMessage], hello adecuado y **DataContractSerializer**  , a continuación, será objeto de Hola de tooserialize usado. También se puede proporcionar un elemento **java.io.InputStream**.

Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes toothe `TestTopic` **MessageSender** se obtenido en el fragmento de código de hello anterior.
Tenga en cuenta cómo Hola **MessageNumber** valor de propiedad de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determinará qué suscripciones reciban):

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md). encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB. No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite de tamaño total de Hola de mensajes de saludo mantenidos por un tema. El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).

## <a name="how-tooreceive-messages-from-a-subscription"></a>¿Cómo tooreceive mensajes desde una suscripción
mensajes de tooreceive de una suscripción, use un **ServiceBusContract** objeto. Los mensajes recibidos pueden funcionar en dos modos distintos: **ReceiveAndDelete** y **PeekLock**.

Cuando se usa hello **ReceiveAndDelete** modo, de recepción es una operación de captura único: es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje, marca Hola mensaje como consumido y lo devuelve toothe aplicación. **ReceiveAndDelete** modo es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus habrá marca el mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

En **PeekLock** , el modo de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a **eliminar** en mensajes de bienvenida recibido. Al Bus de servicio ve hello **eliminar** llamada, se marcar Hola mensaje como consumido y lo quitará de tema de Hola.

Hello ejemplo siguiente muestra cómo se pueden recibir mensajes y el uso de procesado **PeekLock** modo (no en el modo de saludo predeterminado). Hello ejemplo siguiente realiza un bucle y procesa los mensajes de Hola "HighMessages" suscripción y, a continuación, se cierra cuando no hay más mensajes (o bien, se puede establecer toowait si hay mensajes nuevos).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
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
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
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
Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje. Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello **unlockMessage** método en mensajes de bienvenida recibido (en lugar de hello **deleteMessage** método). Esto provocará el mensaje de saludo toounlock de Bus de servicio dentro de tema de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.

También hay un tiempo de espera asociado con un mensaje bloqueado en el tema, y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes del tiempo de espera de bloqueo expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará automáticamente mensajes de bienvenida y hacerla disponible toobe recibido de nuevo.

Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello **deleteMessage** se emite la solicitud, entonces el mensaje de Hola será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar **al menos una vez procesamiento**; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje. A menudo esto se logra utilizando hello **getMessageId** método del mensaje de Hola, que permanece constante entre intentos de entrega.

## <a name="delete-topics-and-subscriptions"></a>Eliminación de temas y suscripciones
Hola temas toodelete de modo principal y las suscripciones es toouse una **ServiceBusContract** objeto. Eliminar un tema, también se eliminarán las suscripciones que están registradas en el tema de Hola. También se pueden eliminar las suscripciones de forma independiente.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas de Service Bus, temas y suscripciones] [ Service Bus queues, topics, and subscriptions] para obtener más información.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
