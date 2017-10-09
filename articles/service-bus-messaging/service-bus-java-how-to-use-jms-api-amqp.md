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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="03a53-103">¿Cómo toouse Hola Java Message Service (JMS) API con Bus de servicio y AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="03a53-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="03a53-104">Hola Advanced Message Queuing Protocol (AMQP) 1.0 es un protocolo de mensajería eficaz, confiable y el nivel de conexión que puede usar toobuild sólidas entre plataformas aplicaciones de mensajería.</span><span class="sxs-lookup"><span data-stu-id="03a53-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="03a53-105">Compatibilidad con AMQP 1.0 en el Bus de servicio significa que puede usar Hola puesta en cola y publicación/suscripción características de mensajería asíncrona desde una amplia variedad de plataformas mediante un eficaz protocolo binario.</span><span class="sxs-lookup"><span data-stu-id="03a53-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="03a53-106">Además, puede desarrollar aplicaciones formadas por componentes creados con una mezcla de lenguajes, marcos y sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="03a53-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="03a53-107">Este artículo explica cómo toouse características de mensajería para el Bus de servicio (temas de las colas y publicación/suscripción) desde aplicaciones de Java mediante Hola populares Java Message Service (JMS) estándar de la API.</span><span class="sxs-lookup"><span data-stu-id="03a53-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="03a53-108">Hay un [artículo complementario](service-bus-amqp-dotnet.md) que explica cómo toodo Hola mismo mediante Hola API de .NET de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="03a53-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="03a53-109">Puede usar estos toolearn juntos dos guías sobre la mensajería entre plataformas mediante AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="03a53-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="03a53-110">Introducción al Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="03a53-110">Get started with Service Bus</span></span>
<span data-ttu-id="03a53-111">En esta guía se asume que ya dispone de un espacio de nombres de Service Bus con una cola denominada **queue1**.</span><span class="sxs-lookup"><span data-stu-id="03a53-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="03a53-112">Si no lo hace, también puede [crear espacio de nombres de Hola y cola](service-bus-create-namespace-portal.md) con hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03a53-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="03a53-113">Para obtener más información sobre cómo los espacios de nombres del Bus de servicio de toocreate y las colas, vea [empezar a trabajar con colas de Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="03a53-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="03a53-114">Los temas y colas con particiones también admiten AMQP.</span><span class="sxs-lookup"><span data-stu-id="03a53-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="03a53-115">Para más información, consulte [Temas y colas con particiones](service-bus-partitioning.md) y [Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03a53-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="03a53-116">Descargar la biblioteca de cliente de AMQP 1.0 JMS Hola</span><span class="sxs-lookup"><span data-stu-id="03a53-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="03a53-117">Para obtener información sobre dónde toodownload Hola versión más reciente de biblioteca de cliente de hello Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="03a53-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="03a53-118">Debe agregar Hola siguientes cuatro archivos JAR de hello Apache Qpid JMS AMQP 1.0 distribución archive toohello CLASSPATH de Java al compilar y ejecutar aplicaciones JMS con Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="03a53-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="03a53-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="03a53-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="03a53-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="03a53-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="03a53-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="03a53-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="03a53-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="03a53-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="03a53-123">Codificación de las aplicaciones Java</span><span class="sxs-lookup"><span data-stu-id="03a53-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="03a53-124">Interfaz de denominación y directorio Java (JNDI)</span><span class="sxs-lookup"><span data-stu-id="03a53-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="03a53-125">JMS utiliza Java Naming and Directory Interface (JNDI) de hello, toocreate una separación entre los nombres lógicos y físicos.</span><span class="sxs-lookup"><span data-stu-id="03a53-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="03a53-126">Se resuelven dos tipos de objetos JMS usando JNDI: ConnectionFactory y Destination.</span><span class="sxs-lookup"><span data-stu-id="03a53-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="03a53-127">JNDI usa un modelo de proveedor en el que puede conectar tareas de resolución de nombre de otro directorio servicios toohandle.</span><span class="sxs-lookup"><span data-stu-id="03a53-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="03a53-128">Hello Apache Qpid JMS AMQP 1.0 biblioteca incluye una propiedad simple proveedor JNDI basados en archivos que se configura mediante un archivo de propiedades de los siguientes Hola de formato:</span><span class="sxs-lookup"><span data-stu-id="03a53-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="03a53-129">Configurar hello ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="03a53-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="03a53-130">Hola toodefine de entrada que se usa un **ConnectionFactory** en hello Qpid proveedor de JNDI de archivo de propiedades es de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="03a53-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="03a53-131">Donde **[jndi_name]** y **[ConnectionURL]** tienen Hola siguientes significados:</span><span class="sxs-lookup"><span data-stu-id="03a53-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="03a53-132">**[jndi_name]** : nombre lógico de Hola de hello ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="03a53-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="03a53-133">Este es el nombre de Hola que se resolverá en la aplicación de Java de hello mediante el método Intialcontext.Lookup de JNDI de hello.</span><span class="sxs-lookup"><span data-stu-id="03a53-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="03a53-134">**[ConnectionURL]** : Una dirección URL que proporciona la biblioteca JMS Hola con información de hello necesario toohello agente AMQP.</span><span class="sxs-lookup"><span data-stu-id="03a53-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="03a53-135">formato de Hola de hello **ConnectionURL** es como sigue:</span><span class="sxs-lookup"><span data-stu-id="03a53-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="03a53-136">Donde **[espacio de nombres]**, **[SASPolicyName]** y **[SASPolicyKey]** tienen Hola siguientes significados:</span><span class="sxs-lookup"><span data-stu-id="03a53-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="03a53-137">**[namespace]** : Hola espacio de nombres de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="03a53-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="03a53-138">**[SASPolicyName]** : nombre de directiva de firma de acceso compartido de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="03a53-139">**[SASPolicyKey]** : clave de directiva de firma de acceso compartido de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="03a53-140">Debe codificar como dirección URL contraseña de hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="03a53-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="03a53-141">Podrá encontrar una práctica utilidad de codificación de la URL en [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="03a53-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="03a53-142">Configuración de destinos</span><span class="sxs-lookup"><span data-stu-id="03a53-142">Configure destinations</span></span>
<span data-ttu-id="03a53-143">Hola toodefine de entrada que se usa que es un destino en proveedor de JNDI de archivo de propiedades de hello Qpid de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="03a53-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="03a53-144">o</span><span class="sxs-lookup"><span data-stu-id="03a53-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="03a53-145">Donde **[jndi\_nombre]** y **[físico\_nombre]** tienen Hola siguientes significados:</span><span class="sxs-lookup"><span data-stu-id="03a53-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="03a53-146">**[jndi_name]** : nombre lógico de hello del destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="03a53-147">Este es el nombre de Hola que se resolverá en la aplicación de Java de hello mediante el método Intialcontext.Lookup de JNDI de hello.</span><span class="sxs-lookup"><span data-stu-id="03a53-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="03a53-148">**[physical_name]** : nombre de Hola de hello aplicación Hola de Bus de servicio entidad toowhich envía o recibe mensajes.</span><span class="sxs-lookup"><span data-stu-id="03a53-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="03a53-149">Cuando se reciben de una suscripción de tema de Bus de servicio, nombre físico Hola especificado en JNDI debe ser el nombre de Hola de tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="03a53-150">nombre de la suscripción de Hola se proporciona cuando se crea suscripción duradera Hola Hola código de la aplicación de JMS.</span><span class="sxs-lookup"><span data-stu-id="03a53-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="03a53-151">Hola [Guía del desarrollador de Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) proporcionan más detalles sobre cómo trabajar con temas de Bus de servicio desde JMS.</span><span class="sxs-lookup"><span data-stu-id="03a53-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="03a53-152">Escribir la aplicación de JMS hello</span><span class="sxs-lookup"><span data-stu-id="03a53-152">Write hello JMS application</span></span>
<span data-ttu-id="03a53-153">No existen API especiales ni opciones obligatorias al usar JMS con el Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="03a53-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="03a53-154">Sin embargo, hay algunas restricciones que se tratarán más adelante.</span><span class="sxs-lookup"><span data-stu-id="03a53-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="03a53-155">Al igual que con cualquier aplicación JMS, Hola lo primero que requiere configuración del entorno de JNDI de hello, toobe puede tooresolve un **ConnectionFactory** y destinos.</span><span class="sxs-lookup"><span data-stu-id="03a53-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="03a53-156">Configurar Hola InitialContext JNDI</span><span class="sxs-lookup"><span data-stu-id="03a53-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="03a53-157">entorno de JNDI de Hello está configurado, pasando una tabla hash de la información de configuración al constructor de clase de hello javax.naming.InitialContext Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="03a53-158">dos elementos necesarios Hello en la tabla hash de hello son hello dirección URL del proveedor y nombre de la clase hello de hello inicial generador de contextos.</span><span class="sxs-lookup"><span data-stu-id="03a53-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="03a53-159">Hello código siguiente muestra cómo tooconfigure Hola JNDI entorno toouse hello Qpid propiedades basados en archivos proveedor JNDI con un archivo de propiedades denominado **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="03a53-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="03a53-160">Aplicación JMS sencilla que usa una cola del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="03a53-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="03a53-161">Hola programa de ejemplo siguiente envía la cola de JMS TextMessages tooa Bus de servicio con el nombre lógico de JNDI Hola de cola y recibe mensajes de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="03a53-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="03a53-162">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="03a53-162">Run hello application</span></span>
<span data-ttu-id="03a53-163">Ejecutar aplicación hello genera el resultado del formulario de hello:</span><span class="sxs-lookup"><span data-stu-id="03a53-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="03a53-164">Mensajería de diferentes plataformas entre JMS y .NET</span><span class="sxs-lookup"><span data-stu-id="03a53-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="03a53-165">Esta guía muestra cómo toosend y recibir mensajes tooand de Bus de servicio con JMS.</span><span class="sxs-lookup"><span data-stu-id="03a53-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="03a53-166">Sin embargo, una de las principales ventajas de Hola de AMQP 1.0 es que permite toobe de las aplicaciones que se crea a partir de componentes escritos en lenguajes diferentes, con los mensajes intercambiados con total fidelidad y de manera confiable.</span><span class="sxs-lookup"><span data-stu-id="03a53-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="03a53-167">Mediante la aplicación de JMS de ejemplo de Hola se ha descrito anteriormente y una aplicación .NET similar procedente de un artículo complementario, [usando el Bus de servicio desde .NET con AMQP 1.0](service-bus-amqp-dotnet.md), puede intercambiar mensajes entre .NET y Java.</span><span class="sxs-lookup"><span data-stu-id="03a53-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="03a53-168">Lea este artículo para obtener más información acerca de los detalles de Hola de usar AMQP 1.0 y del Bus de servicio de mensajería entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="03a53-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="03a53-169">Too.NET JMS</span><span class="sxs-lookup"><span data-stu-id="03a53-169">JMS too.NET</span></span>
<span data-ttu-id="03a53-170">toodemonstrate JMS too.NET mensajería:</span><span class="sxs-lookup"><span data-stu-id="03a53-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="03a53-171">Inicie la aplicación de ejemplo de Hola .NET sin ningún argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="03a53-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="03a53-172">Inicie la aplicación de ejemplo de Hola Java con el argumento de línea de comandos de "sendonly" Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="03a53-173">En este modo, hello aplicación no recibirá mensajes de cola de hello, únicamente enviará.</span><span class="sxs-lookup"><span data-stu-id="03a53-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="03a53-174">Presione **ENTRAR** varias veces en la consola de aplicación de Java de hello, lo que hará que toobe de mensajes enviado.</span><span class="sxs-lookup"><span data-stu-id="03a53-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="03a53-175">Estos mensajes son recibidos por hello aplicación. NET.</span><span class="sxs-lookup"><span data-stu-id="03a53-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="03a53-176">Resultados de la aplicación JMS</span><span class="sxs-lookup"><span data-stu-id="03a53-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="03a53-177">Resultados de la aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="03a53-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="03a53-178">TooJMS de .NET</span><span class="sxs-lookup"><span data-stu-id="03a53-178">.NET tooJMS</span></span>
<span data-ttu-id="03a53-179">toodemonstrate tooJMS de .NET de mensajería:</span><span class="sxs-lookup"><span data-stu-id="03a53-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="03a53-180">Inicie la aplicación de ejemplo de Hola .NET con el argumento de línea de comandos de "sendonly" Hola.</span><span class="sxs-lookup"><span data-stu-id="03a53-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="03a53-181">En este modo, hello aplicación no recibirá mensajes de cola de hello, únicamente enviará.</span><span class="sxs-lookup"><span data-stu-id="03a53-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="03a53-182">Inicie la aplicación de ejemplo de Hola Java sin ningún argumento de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="03a53-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="03a53-183">Presione **ENTRAR** varias veces en la consola de la aplicación de .NET de hello, lo que hará que toobe de mensajes enviado.</span><span class="sxs-lookup"><span data-stu-id="03a53-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="03a53-184">Estos mensajes son recibidos por hello aplicación Java.</span><span class="sxs-lookup"><span data-stu-id="03a53-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="03a53-185">Resultados de la aplicación .NET</span><span class="sxs-lookup"><span data-stu-id="03a53-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="03a53-186">Resultados de la aplicación JMS</span><span class="sxs-lookup"><span data-stu-id="03a53-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="03a53-187">Características no admitidas y restricciones</span><span class="sxs-lookup"><span data-stu-id="03a53-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="03a53-188">Hola después restricciones existe al usar JMS en AMQP 1.0 con Bus de servicio, a saber:</span><span class="sxs-lookup"><span data-stu-id="03a53-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="03a53-189">Solo se permite un elemento **MessageProducer** o **MessageConsumer** por cada **sesión**.</span><span class="sxs-lookup"><span data-stu-id="03a53-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="03a53-190">Si necesita toocreate varios **MessageProducers** o **MessageConsumers** en una aplicación, cree una dedicado **sesión** para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="03a53-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="03a53-191">Actualmente no se admiten las suscripciones a tema volátiles.</span><span class="sxs-lookup"><span data-stu-id="03a53-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="03a53-192">Por el momento no se admiten **MessageSelectors**.</span><span class="sxs-lookup"><span data-stu-id="03a53-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="03a53-193">Destinos temporales; Por ejemplo, **TemporaryQueue**, **TemporaryTopic** no se admiten actualmente, junto con hello **QueueRequestor** y **TopicRequestor**API que las utilizan.</span><span class="sxs-lookup"><span data-stu-id="03a53-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="03a53-194">No se admiten las sesiones de transacción ni las transacciones distribuidas.</span><span class="sxs-lookup"><span data-stu-id="03a53-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="03a53-195">Resumen</span><span class="sxs-lookup"><span data-stu-id="03a53-195">Summary</span></span>
<span data-ttu-id="03a53-196">Este tooguide cómo se ha explicado cómo toouse características de mensajería para el agente de Service Bus (colas y publicación/suscripción temas) desde Java con Hola populares API de JMS y AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="03a53-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="03a53-197">También puede utilizar AMQP 1.0 del bus de servicio desde otros lenguajes, como .NET, C, Python y PHP.</span><span class="sxs-lookup"><span data-stu-id="03a53-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="03a53-198">Componentes creados mediante estos lenguajes diferentes pueden intercambiar mensajes con total fidelidad utilizando el soporte de hello AMQP 1.0 en el Bus de servicio y de manera confiable.</span><span class="sxs-lookup"><span data-stu-id="03a53-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03a53-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03a53-199">Next steps</span></span>
* [<span data-ttu-id="03a53-200">Compatibilidad de AMQP 1.0 en Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="03a53-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="03a53-201">Cómo toouse AMQP 1.0 con Hola API de .NET de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="03a53-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="03a53-202">Guía para desarrolladores sobre AMQP 1.0 de Service Bus</span><span class="sxs-lookup"><span data-stu-id="03a53-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="03a53-203">Introducción a las colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="03a53-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="03a53-204">Centro de desarrolladores de Java</span><span class="sxs-lookup"><span data-stu-id="03a53-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

