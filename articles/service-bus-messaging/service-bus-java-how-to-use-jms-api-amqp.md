---
title: aaaHow toouse AMQP 1.0 con hello API del Bus de servicio de Java | Documentos de Microsoft
description: "¿Cómo toouse Hola Java Message Service (JMS) con un Bus de servicio de Azure y Advanced Message Queuing Protodol (AMQP) 1.0."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>¿Cómo toouse Hola Java Message Service (JMS) API con Bus de servicio y AMQP 1.0
Hola Advanced Message Queuing Protocol (AMQP) 1.0 es un protocolo de mensajería eficaz, confiable y el nivel de conexión que puede usar toobuild sólidas entre plataformas aplicaciones de mensajería.

Compatibilidad con AMQP 1.0 en el Bus de servicio significa que puede usar Hola puesta en cola y publicación/suscripción características de mensajería asíncrona desde una amplia variedad de plataformas mediante un eficaz protocolo binario. Además, puede desarrollar aplicaciones formadas por componentes creados con una mezcla de lenguajes, marcos y sistemas operativos.

Este artículo explica cómo toouse características de mensajería para el Bus de servicio (temas de las colas y publicación/suscripción) desde aplicaciones de Java mediante Hola populares Java Message Service (JMS) estándar de la API. Hay un [artículo complementario](service-bus-amqp-dotnet.md) que explica cómo toodo Hola mismo mediante Hola API de .NET de Bus de servicio. Puede usar estos toolearn juntos dos guías sobre la mensajería entre plataformas mediante AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Introducción al Bus de servicio
En esta guía se asume que ya dispone de un espacio de nombres de Service Bus con una cola denominada **queue1**. Si no lo hace, también puede [crear espacio de nombres de Hola y cola](service-bus-create-namespace-portal.md) con hello [portal de Azure](https://portal.azure.com). Para obtener más información sobre cómo los espacios de nombres del Bus de servicio de toocreate y las colas, vea [empezar a trabajar con colas de Service Bus](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Los temas y colas con particiones también admiten AMQP. Para más información, consulte [Temas y colas con particiones](service-bus-partitioning.md) y [Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Descargar la biblioteca de cliente de AMQP 1.0 JMS Hola
Para obtener información sobre dónde toodownload Hola versión más reciente de biblioteca de cliente de hello Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Debe agregar Hola siguientes cuatro archivos JAR de hello Apache Qpid JMS AMQP 1.0 distribución archive toohello CLASSPATH de Java al compilar y ejecutar aplicaciones JMS con Bus de servicio:

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>Codificación de las aplicaciones Java
### <a name="java-naming-and-directory-interface-jndi"></a>Interfaz de denominación y directorio Java (JNDI)
JMS utiliza Java Naming and Directory Interface (JNDI) de hello, toocreate una separación entre los nombres lógicos y físicos. Se resuelven dos tipos de objetos JMS usando JNDI: ConnectionFactory y Destination. JNDI usa un modelo de proveedor en el que puede conectar tareas de resolución de nombre de otro directorio servicios toohandle. Hello Apache Qpid JMS AMQP 1.0 biblioteca incluye una propiedad simple proveedor JNDI basados en archivos que se configura mediante un archivo de propiedades de los siguientes Hola de formato:

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>Configurar hello ConnectionFactory
Hola toodefine de entrada que se usa un **ConnectionFactory** en hello Qpid proveedor de JNDI de archivo de propiedades es de hello siguiendo el formato:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Donde **[jndi_name]** y **[ConnectionURL]** tienen Hola siguientes significados:

* **[jndi_name]** : nombre lógico de Hola de hello ConnectionFactory. Este es el nombre de Hola que se resolverá en la aplicación de Java de hello mediante el método Intialcontext.Lookup de JNDI de hello.
* **[ConnectionURL]** : Una dirección URL que proporciona la biblioteca JMS Hola con información de hello necesario toohello agente AMQP.

formato de Hola de hello **ConnectionURL** es como sigue:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Donde **[espacio de nombres]**, **[SASPolicyName]** y **[SASPolicyKey]** tienen Hola siguientes significados:

* **[namespace]** : Hola espacio de nombres de Bus de servicio.
* **[SASPolicyName]** : nombre de directiva de firma de acceso compartido de cola de Hola.
* **[SASPolicyKey]** : clave de directiva de firma de acceso compartido de cola de Hola.

> [!NOTE]
> Debe codificar como dirección URL contraseña de hello manualmente. Podrá encontrar una práctica utilidad de codificación de la URL en [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Configuración de destinos
Hola toodefine de entrada que se usa que es un destino en proveedor de JNDI de archivo de propiedades de hello Qpid de hello siguiendo el formato:

```
queue.[jndi_name] = [physical_name]
```

o

```
topic.[jndi_name] = [physical_name]
```

Donde **[jndi\_nombre]** y **[físico\_nombre]** tienen Hola siguientes significados:

* **[jndi_name]** : nombre lógico de hello del destino de Hola. Este es el nombre de Hola que se resolverá en la aplicación de Java de hello mediante el método Intialcontext.Lookup de JNDI de hello.
* **[physical_name]** : nombre de Hola de hello aplicación Hola de Bus de servicio entidad toowhich envía o recibe mensajes.

> [!NOTE]
> Cuando se reciben de una suscripción de tema de Bus de servicio, nombre físico Hola especificado en JNDI debe ser el nombre de Hola de tema de Hola. nombre de la suscripción de Hola se proporciona cuando se crea suscripción duradera Hola Hola código de la aplicación de JMS. Hola [Guía del desarrollador de Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) proporcionan más detalles sobre cómo trabajar con temas de Bus de servicio desde JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Escribir la aplicación de JMS hello
No existen API especiales ni opciones obligatorias al usar JMS con el Bus de servicio. Sin embargo, hay algunas restricciones que se tratarán más adelante. Al igual que con cualquier aplicación JMS, Hola lo primero que requiere configuración del entorno de JNDI de hello, toobe puede tooresolve un **ConnectionFactory** y destinos.

#### <a name="configure-hello-jndi-initialcontext"></a>Configurar Hola InitialContext JNDI
entorno de JNDI de Hello está configurado, pasando una tabla hash de la información de configuración al constructor de clase de hello javax.naming.InitialContext Hola. dos elementos necesarios Hello en la tabla hash de hello son hello dirección URL del proveedor y nombre de la clase hello de hello inicial generador de contextos. Hello código siguiente muestra cómo tooconfigure Hola JNDI entorno toouse hello Qpid propiedades basados en archivos proveedor JNDI con un archivo de propiedades denominado **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Aplicación JMS sencilla que usa una cola del Bus de servicio
Hola programa de ejemplo siguiente envía la cola de JMS TextMessages tooa Bus de servicio con el nombre lógico de JNDI Hola de cola y recibe mensajes de Hola de nuevo.

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>Ejecutar la aplicación hello
Ejecutar aplicación hello genera el resultado del formulario de hello:

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>Mensajería de diferentes plataformas entre JMS y .NET
Esta guía muestra cómo toosend y recibir mensajes tooand de Bus de servicio con JMS. Sin embargo, una de las principales ventajas de Hola de AMQP 1.0 es que permite toobe de las aplicaciones que se crea a partir de componentes escritos en lenguajes diferentes, con los mensajes intercambiados con total fidelidad y de manera confiable.

Mediante la aplicación de JMS de ejemplo de Hola se ha descrito anteriormente y una aplicación .NET similar procedente de un artículo complementario, [usando el Bus de servicio desde .NET con AMQP 1.0](service-bus-amqp-dotnet.md), puede intercambiar mensajes entre .NET y Java. Lea este artículo para obtener más información acerca de los detalles de Hola de usar AMQP 1.0 y del Bus de servicio de mensajería entre plataformas.

### <a name="jms-toonet"></a>Too.NET JMS
toodemonstrate JMS too.NET mensajería:

* Inicie la aplicación de ejemplo de Hola .NET sin ningún argumento de línea de comandos.
* Inicie la aplicación de ejemplo de Hola Java con el argumento de línea de comandos de "sendonly" Hola. En este modo, hello aplicación no recibirá mensajes de cola de hello, únicamente enviará.
* Presione **ENTRAR** varias veces en la consola de aplicación de Java de hello, lo que hará que toobe de mensajes enviado.
* Estos mensajes son recibidos por hello aplicación. NET.

#### <a name="output-from-jms-application"></a>Resultados de la aplicación JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Resultados de la aplicación .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>TooJMS de .NET
toodemonstrate tooJMS de .NET de mensajería:

* Inicie la aplicación de ejemplo de Hola .NET con el argumento de línea de comandos de "sendonly" Hola. En este modo, hello aplicación no recibirá mensajes de cola de hello, únicamente enviará.
* Inicie la aplicación de ejemplo de Hola Java sin ningún argumento de línea de comandos.
* Presione **ENTRAR** varias veces en la consola de la aplicación de .NET de hello, lo que hará que toobe de mensajes enviado.
* Estos mensajes son recibidos por hello aplicación Java.

#### <a name="output-from-net-application"></a>Resultados de la aplicación .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Resultados de la aplicación JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Características no admitidas y restricciones
Hola después restricciones existe al usar JMS en AMQP 1.0 con Bus de servicio, a saber:

* Solo se permite un elemento **MessageProducer** o **MessageConsumer** por cada **sesión**. Si necesita toocreate varios **MessageProducers** o **MessageConsumers** en una aplicación, cree una dedicado **sesión** para cada uno de ellos.
* Actualmente no se admiten las suscripciones a tema volátiles.
* Por el momento no se admiten **MessageSelectors**.
* Destinos temporales; Por ejemplo, **TemporaryQueue**, **TemporaryTopic** no se admiten actualmente, junto con hello **QueueRequestor** y **TopicRequestor**API que las utilizan.
* No se admiten las sesiones de transacción ni las transacciones distribuidas.

## <a name="summary"></a>Resumen
Este tooguide cómo se ha explicado cómo toouse características de mensajería para el agente de Service Bus (colas y publicación/suscripción temas) desde Java con Hola populares API de JMS y AMQP 1.0.

También puede utilizar AMQP 1.0 del bus de servicio desde otros lenguajes, como .NET, C, Python y PHP. Componentes creados mediante estos lenguajes diferentes pueden intercambiar mensajes con total fidelidad utilizando el soporte de hello AMQP 1.0 en el Bus de servicio y de manera confiable.

## <a name="next-steps"></a>Pasos siguientes
* [Compatibilidad de AMQP 1.0 en Azure Service Bus](service-bus-amqp-overview.md)
* [Cómo toouse AMQP 1.0 con Hola API de .NET de Bus de servicio](service-bus-dotnet-advanced-message-queuing.md)
* [Guía para desarrolladores sobre AMQP 1.0 de Service Bus](service-bus-amqp-dotnet.md)
* [Introducción a las colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Centro de desarrolladores de Java](https://azure.microsoft.com/develop/java/)

