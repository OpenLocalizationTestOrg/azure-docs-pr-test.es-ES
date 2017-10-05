---
title: Uso de AMQP 1.0 con la API de Service Bus de Java | Microsoft Docs
description: "Cómo usar Java Message Service (JMS) con el Bus de servicio de Azure y Advanced Message Queuing Protodol (AMQP) 1.0."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="a5570-103">Uso de la API de Java Message Service (JMS) con el Bus de servicio y AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="a5570-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="a5570-104">Advanced Message Queuing Protocol (AMQP) 1.0 es un protocolo de mensajes a nivel de red, confiable y eficaz que se puede utilizar para crear aplicaciones de mensajería robustas y compatibles con varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="a5570-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="a5570-105">La compatibilidad con AMQP 1.0 del Bus de servicio implica que puede utilizar las funciones de colas y publicación/suscripción de mensajería asíncrona desde una amplia variedad de plataformas mediante un eficaz protocolo binario.</span><span class="sxs-lookup"><span data-stu-id="a5570-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="a5570-106">Además, puede desarrollar aplicaciones formadas por componentes creados con una mezcla de lenguajes, marcos y sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="a5570-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="a5570-107">En este artículo se explica cómo utilizar las características de mensajería de Service Bus (colas y temas de publicación o suscripción) desde aplicaciones de Java mediante el popular estándar de API de Java Message Service (JMS).</span><span class="sxs-lookup"><span data-stu-id="a5570-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="a5570-108">Existe otro [artículo complementario](service-bus-amqp-dotnet.md) en el que se explica cómo hacer lo mismo utilizando la API de .NET de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a5570-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="a5570-109">Puede utilizar estas dos guías conjuntamente para obtener información acerca de la mensajería entre diferentes plataformas mediante AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="a5570-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="a5570-110">Introducción al Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="a5570-110">Get started with Service Bus</span></span>
<span data-ttu-id="a5570-111">En esta guía se asume que ya dispone de un espacio de nombres de Service Bus con una cola denominada **queue1**.</span><span class="sxs-lookup"><span data-stu-id="a5570-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="a5570-112">Si no es así, puede [crear el espacio de nombres y la cola](service-bus-create-namespace-portal.md) con ayuda de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5570-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a5570-113">Para obtener más información sobre cómo crear espacios de nombres y colas de Service Bus, vea [Introducción a las colas de Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="a5570-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a5570-114">Los temas y colas con particiones también admiten AMQP.</span><span class="sxs-lookup"><span data-stu-id="a5570-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="a5570-115">Para más información, consulte [Temas y colas con particiones](service-bus-partitioning.md) y [Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5570-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="a5570-116">Descarga de la biblioteca de cliente AMQP 1.0 JMS</span><span class="sxs-lookup"><span data-stu-id="a5570-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="a5570-117">Para obtener más información sobre dónde descargar la versión más reciente de la biblioteca de cliente Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="a5570-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="a5570-118">Debe agregar los cuatro archivos JAR siguientes del archivo de distribución de Apache Qpid JMS AMQP 1.0 al CLASSPATH de Java cuando vaya a crear y ejecutar aplicaciones JMS con el Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="a5570-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="a5570-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="a5570-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="a5570-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="a5570-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="a5570-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="a5570-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="a5570-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="a5570-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="a5570-123">Codificación de las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="a5570-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="a5570-124">Interfaz de denominación y directorio Java (JNDI)</span><span class="sxs-lookup"><span data-stu-id="a5570-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="a5570-125">JMS usa la interfaz de denominación y directorio Java (JNDI) para crear una separación entre los nombres lógicos y los físicos.</span><span class="sxs-lookup"><span data-stu-id="a5570-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="a5570-126">Se resuelven dos tipos de objetos JMS usando JNDI: ConnectionFactory y Destination.</span><span class="sxs-lookup"><span data-stu-id="a5570-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="a5570-127">JNDI usa un modelo de proveedor al que se pueden acoplar diferentes servicios de directorio para controlar labores de resolución de nombres.</span><span class="sxs-lookup"><span data-stu-id="a5570-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="a5570-128">La biblioteca Apache Qpid JMS AMQP 1.0 se presenta con un proveedor JNDI basado en archivo de propiedades sencillas que se configura usando un archivo de propiedades cuyo formato es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5570-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="a5570-129">Configuración de ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="a5570-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="a5570-130">La entrada usada para definir **ConnectionFactory** en el proveedor JNDI de archivo de propiedades Qpid tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5570-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="a5570-131">Donde **[jndi_name]** y **[ConnectionURL]** tienen los significados siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5570-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="a5570-132">**[jndi_name]**: el nombre lógico de ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="a5570-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="a5570-133">Este es el nombre que se resolverá en la aplicación Java usando el método JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="a5570-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="a5570-134">**[ConnectionURL]**: dirección URL que proporciona a la biblioteca JMS la información necesaria para el agente AMQP.</span><span class="sxs-lookup"><span data-stu-id="a5570-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="a5570-135">El formato de **ConnectionURL** es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5570-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="a5570-136">Donde **[namespace]**, **[SASPolicyName]** y **[SASPolicyKey]** tienen los significados siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5570-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="a5570-137">**[namespace]**: espacio de nombres de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a5570-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="a5570-138">**[SASPolicyName]**: nombre de la directiva de firma de acceso compartido de la cola.</span><span class="sxs-lookup"><span data-stu-id="a5570-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="a5570-139">**[SASPolicyKey]**: clave de la directiva de firma de acceso compartido de la cola.</span><span class="sxs-lookup"><span data-stu-id="a5570-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="a5570-140">debe codificar la contraseña manualmente como dirección URL.</span><span class="sxs-lookup"><span data-stu-id="a5570-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="a5570-141">Podrá encontrar una práctica utilidad de codificación de la URL en [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="a5570-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="a5570-142">Configuración de destinos</span><span class="sxs-lookup"><span data-stu-id="a5570-142">Configure destinations</span></span>
<span data-ttu-id="a5570-143">La entrada usada para definir un destino en el proveedor JNDI de archivo de propiedades Qpid tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="a5570-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="a5570-144">o</span><span class="sxs-lookup"><span data-stu-id="a5570-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="a5570-145">Donde **[jndi\_name]** and **[physical\_name]** tienen los significados siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5570-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="a5570-146">**[jndi_name]**: el nombre lógico del destino.</span><span class="sxs-lookup"><span data-stu-id="a5570-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="a5570-147">Este es el nombre que se resolverá en la aplicación Java usando el método JNDI IntialContext.lookup().</span><span class="sxs-lookup"><span data-stu-id="a5570-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="a5570-148">**[physical_name]**: nombre de la entidad de Service Bus a la que la aplicación envía mensajes o de la que los recibe.</span><span class="sxs-lookup"><span data-stu-id="a5570-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="a5570-149">al recibir de una suscripción al tema del Bus de servicio, el nombre físico especificado en JNDI debe ser el nombre del tema.</span><span class="sxs-lookup"><span data-stu-id="a5570-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="a5570-150">El nombre de la suscripción se proporciona cuando la suscripción duradera se crea en el código de aplicación JMS.</span><span class="sxs-lookup"><span data-stu-id="a5570-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="a5570-151">La [Guía para desarrolladores sobre AMQP 1.0 de Service Bus](service-bus-amqp-dotnet.md) proporciona más información sobre cómo trabajar con temas de Service Bus desde JMS.</span><span class="sxs-lookup"><span data-stu-id="a5570-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="a5570-152">Escritura de la aplicación JMS</span><span class="sxs-lookup"><span data-stu-id="a5570-152">Write the JMS application</span></span>
<span data-ttu-id="a5570-153">No existen API especiales ni opciones obligatorias al usar JMS con el Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a5570-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="a5570-154">Sin embargo, hay algunas restricciones que se tratarán más adelante.</span><span class="sxs-lookup"><span data-stu-id="a5570-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="a5570-155">Como con cualquier otra aplicación JMS, el primer requisito necesario es configurar el entorno JNDI para poder resolver **ConnectionFactory** y los destinos.</span><span class="sxs-lookup"><span data-stu-id="a5570-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="a5570-156">Configuración de JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="a5570-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="a5570-157">El entorno JNDI se configura pasando una tabla hash con información de configuración al constructor de la clase javax.naming.InitialContext.</span><span class="sxs-lookup"><span data-stu-id="a5570-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="a5570-158">Los dos elementos necesarios de la tabla hash son el nombre de la clase de Initial Context Factory y la URL del proveedor.</span><span class="sxs-lookup"><span data-stu-id="a5570-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="a5570-159">El código siguiente indica cómo configurar el entorno JNDI para usar el proveedor JNDI basado en archivo de propiedades Qpid con un archivo de propiedades llamado **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="a5570-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="a5570-160">Aplicación JMS sencilla que usa una cola del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="a5570-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="a5570-161">El programa de ejemplo siguiente envía JMS TextMessages a una cola de bus de servicio con el nombre lógico JNDI de QUEUE y recibe los mensajes de vuelta.</span><span class="sxs-lookup"><span data-stu-id="a5570-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="a5570-162">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a5570-162">Run the application</span></span>
<span data-ttu-id="a5570-163">Al ejecutar la aplicación se obtienen resultados del tipo:</span><span class="sxs-lookup"><span data-stu-id="a5570-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="a5570-164">Mensajería de diferentes plataformas entre JMS y .NET</span><span class="sxs-lookup"><span data-stu-id="a5570-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="a5570-165">Esta guía le ha mostrado cómo enviar y recibir mensajes con el Bus de servicio como origen y destino usando JMS.</span><span class="sxs-lookup"><span data-stu-id="a5570-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="a5570-166">Sin embargo, una de las ventajas principales de AMQP 1.0 es que permite que las aplicaciones estén formadas por componentes escritos en diferentes lenguajes, a la vez que garantiza que los mensajes se intercambien con total seguridad y fidelidad.</span><span class="sxs-lookup"><span data-stu-id="a5570-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="a5570-167">Utilizando la aplicación JMS de ejemplo descrita anteriormente y una aplicación .NET similar tomada de un artículo complementario, [Uso de Service Bus desde .NET con AMQP 1.0](service-bus-amqp-dotnet.md), es posible intercambiar mensajes entre .NET y Java.</span><span class="sxs-lookup"><span data-stu-id="a5570-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="a5570-168">Lea este artículo para obtener más información sobre la mensajería multiplataforma mediante Service Bus y AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="a5570-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="a5570-169">De JMS a .NET</span><span class="sxs-lookup"><span data-stu-id="a5570-169">JMS to .NET</span></span>
<span data-ttu-id="a5570-170">Para comprobar cómo funciona la mensajería de JMS a .NET:</span><span class="sxs-lookup"><span data-stu-id="a5570-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="a5570-171">Inicie la aplicación de ejemplo .NET sin ningún argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a5570-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="a5570-172">Inicie la aplicación de ejemplo Java con el argumento de línea de comandos “sendonly”.</span><span class="sxs-lookup"><span data-stu-id="a5570-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="a5570-173">De esta manera, la aplicación no recibirá mensajes de la cola, sino que solo los enviará.</span><span class="sxs-lookup"><span data-stu-id="a5570-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="a5570-174">Presione **Entrar** unas cuantas veces en la consola de la aplicación Java para enviar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="a5570-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="a5570-175">Estos mensajes los recibe la aplicación .NET.</span><span class="sxs-lookup"><span data-stu-id="a5570-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="a5570-176">Resultados de la aplicación JMS</span><span class="sxs-lookup"><span data-stu-id="a5570-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="a5570-177">Resultados de la aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="a5570-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="a5570-178">De .NET a JMS</span><span class="sxs-lookup"><span data-stu-id="a5570-178">.NET to JMS</span></span>
<span data-ttu-id="a5570-179">Para comprobar cómo funciona la mensajería de .NET a JMS:</span><span class="sxs-lookup"><span data-stu-id="a5570-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="a5570-180">Inicie la aplicación de ejemplo .NET con el argumento de línea de comandos "sendonly".</span><span class="sxs-lookup"><span data-stu-id="a5570-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="a5570-181">De esta manera, la aplicación no recibirá mensajes de la cola, sino que solo los enviará.</span><span class="sxs-lookup"><span data-stu-id="a5570-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="a5570-182">Inicie la aplicación de ejemplo Java sin argumentos de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="a5570-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="a5570-183">Presione **Entrar** unas cuantas veces en la consola de la aplicación .NET para enviar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="a5570-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="a5570-184">Estos mensajes los recibe la aplicación Java.</span><span class="sxs-lookup"><span data-stu-id="a5570-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="a5570-185">Resultados de la aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="a5570-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="a5570-186">Resultados de la aplicación JMS</span><span class="sxs-lookup"><span data-stu-id="a5570-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="a5570-187">Características no admitidas y restricciones</span><span class="sxs-lookup"><span data-stu-id="a5570-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="a5570-188">Existen las restricciones siguientes al usar JMS sobre AMQP 1.0 con el Bus de servicio, a saber:</span><span class="sxs-lookup"><span data-stu-id="a5570-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="a5570-189">Solo se permite un elemento **MessageProducer** o **MessageConsumer** por cada **sesión**.</span><span class="sxs-lookup"><span data-stu-id="a5570-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="a5570-190">Si tiene que crear varios elementos **MessageProducers** o **MessageConsumers** en una aplicación, cree una **sesión** dedicada para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="a5570-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="a5570-191">Actualmente no se admiten las suscripciones a tema volátiles.</span><span class="sxs-lookup"><span data-stu-id="a5570-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="a5570-192">Por el momento no se admiten **MessageSelectors**.</span><span class="sxs-lookup"><span data-stu-id="a5570-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="a5570-193">Actualmente no se admiten destinos temporales, como **TemporaryQueue** y **TemporaryTopic**, junto con las API **QueueRequestor** y **TopicRequestor** que los usan.</span><span class="sxs-lookup"><span data-stu-id="a5570-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="a5570-194">No se admiten las sesiones de transacción ni las transacciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="a5570-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="a5570-195">Resumen</span><span class="sxs-lookup"><span data-stu-id="a5570-195">Summary</span></span>
<span data-ttu-id="a5570-196">En esta guía de instrucciones se indica cómo usar las características de mensajería asíncrona del Bus de servicio (colas y publicación/suscripción a temas) desde Java utilizando las populares JMS API y AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="a5570-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="a5570-197">También puede utilizar AMQP 1.0 del bus de servicio desde otros lenguajes, como .NET, C, Python y PHP.</span><span class="sxs-lookup"><span data-stu-id="a5570-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="a5570-198">Los componentes creados utilizando estos lenguajes pueden intercambiar mensajes con seguridad y fidelidad gracias a la compatibilidad de AMQP 1.0 en el bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="a5570-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5570-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a5570-199">Next steps</span></span>
* [<span data-ttu-id="a5570-200">Compatibilidad de AMQP 1.0 en Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="a5570-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="a5570-201">Uso de AMQP 1.0 con la API .NET de Service Bus</span><span class="sxs-lookup"><span data-stu-id="a5570-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="a5570-202">Guía para desarrolladores sobre AMQP 1.0 de Service Bus</span><span class="sxs-lookup"><span data-stu-id="a5570-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="a5570-203">Introducción a las colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="a5570-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="a5570-204">Centro de desarrolladores de Java</span><span class="sxs-lookup"><span data-stu-id="a5570-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

