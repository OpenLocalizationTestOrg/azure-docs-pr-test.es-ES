---
title: mensajes de aaaCloud al dispositivo con el centro de IoT de Azure (Java) | Documentos de Microsoft
description: "¿Cómo toosend en la nube al dispositivo mensajes tooa del dispositivo de un centro de IoT de Azure con hello Azure IoT SDK para Java. Modificar una aplicación de dispositivo simulado tooreceive los mensajes de nube al dispositivo y modificar un mensajes de aplicaciones back-end toosend hello en la nube al dispositivo."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="6a743-104">Envío mensajes de nube a dispositivo con IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="6a743-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="6a743-105">IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="6a743-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="6a743-106">Hola [empezar a trabajar con el centro de IoT] tutorial muestra cómo aprovisionar una identidad de dispositivo en el toocreate un centro de IoT y codificar una aplicación de dispositivo simulado que envía mensajes de dispositivo para la nube.</span><span class="sxs-lookup"><span data-stu-id="6a743-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="6a743-107">Este tutorial se basa en la [empezar a trabajar con el centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="6a743-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="6a743-108">En él se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="6a743-108">It shows you how to:</span></span>

* <span data-ttu-id="6a743-109">Desde el back-end de soluciones, enviar mensajes en la nube al dispositivo tooa dispositivo a través del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6a743-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="6a743-110">Reciba mensajes de nube a dispositivo en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a743-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="6a743-111">En el back-end de soluciones, solicitar confirmación de entrega (*comentarios*) para mensajes envían tooa dispositivo desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6a743-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="6a743-112">Puede encontrar más información sobre los mensajes en la nube al dispositivo en hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="6a743-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="6a743-113">Al final de Hola de este tutorial, ejecute dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="6a743-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="6a743-114">**dispositivo simulado**, una versión modificada de la aplicación hello creado en [empezar a trabajar con el centro de IoT], que se conecta el centro de IoT tooyour y recibe los mensajes de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a743-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="6a743-115">**enviar mensajes de c2d**, que envía una aplicación de dispositivo simulado de toohello de mensaje en la nube al dispositivo a través del centro de IoT y, a continuación, recibe la confirmación de entrega.</span><span class="sxs-lookup"><span data-stu-id="6a743-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="6a743-116">El Centro de IoT ofrece compatibilidad con el SDK en muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante los SDK de dispositivos IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="6a743-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="6a743-117">Para obtener instrucciones paso a paso sobre cómo tooconnect del su dispositivo toothis tutorial código y generalmente tooAzure centro de IoT, vea hello [Centro para desarrolladores de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="6a743-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="6a743-118">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="6a743-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6a743-119">Una versión de trabajo completa de hello [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) o [mensajes del dispositivo a la nube de centro de IoT de proceso](iot-hub-java-java-process-d2c.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a743-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="6a743-120">Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="6a743-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="6a743-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="6a743-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="6a743-122">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="6a743-122">An active Azure account.</span></span> <span data-ttu-id="6a743-123">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="6a743-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="6a743-124">Recibir mensajes en la aplicación de dispositivo simulado de hello</span><span class="sxs-lookup"><span data-stu-id="6a743-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="6a743-125">En esta sección, modificar aplicación de dispositivo simulado de Hola que creó en [empezar a trabajar con el centro de IoT] mensajes de nube al dispositivo tooreceive Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6a743-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="6a743-126">Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="6a743-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="6a743-127">Agregue los siguiente hello **MessageCallback** clase como una clase anidada dentro de hello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="6a743-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="6a743-128">Hola **ejecutar** método se invoca cuando el dispositivo de hello recibe un mensaje desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="6a743-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="6a743-129">En este ejemplo, dispositivo Hola siempre notifica al centro de IoT de Hola que se ha completado el mensaje de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="6a743-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="6a743-130">Modificar hello **principal** método toocreate una **AppMessageCallback** Hola de instancia y llame al método **setMessageCallback** método antes de su apertura cliente hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="6a743-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="6a743-131">Si utiliza HTTP como transporte de hello en lugar de MQTT o AMQP, Hola **DeviceClient** instancia comprueba si hay mensajes de centro de IoT con poca frecuencia (menor que cada 25 minutos).</span><span class="sxs-lookup"><span data-stu-id="6a743-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="6a743-132">Para obtener más información acerca de las diferencias de hello entre soporte MQTT, AMQP y HTTP y la limitación de centro de IoT, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="6a743-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="6a743-133">Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:</span><span class="sxs-lookup"><span data-stu-id="6a743-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="6a743-134">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="6a743-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="6a743-135">En esta sección, creará una aplicación de consola de Java que envía mensajes en la nube al dispositivo toohello del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="6a743-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="6a743-136">Necesita Hola Id. de dispositivo del dispositivo de Hola que agregó en hello [empezar a trabajar con el centro de IoT] tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a743-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="6a743-137">También necesita Hola cadena de conexión de centro de IoT su base de datos central que se puede encontrar en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="6a743-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="6a743-138">Cree un proyecto de Maven denominado **c2d de envío de mensajes** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a743-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="6a743-139">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="6a743-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="6a743-140">En el símbolo del sistema, navegue toohello nueva carpeta de c2d de envío de mensajes.</span><span class="sxs-lookup"><span data-stu-id="6a743-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="6a743-141">Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta de c2d de envío de mensajes de Hola y agregue Hola después toohello de dependencia **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="6a743-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="6a743-142">Agregar dependencia Hola permite hello toouse **el centro de IOT java servicio cliente** paquete en su toocommunicate de aplicación con el servicio del centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="6a743-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="6a743-143">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="6a743-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="6a743-144">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="6a743-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="6a743-145">Con un editor de texto, abra el archivo send-c2d-messages\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="6a743-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="6a743-146">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="6a743-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="6a743-147">Agregar Hola después de las variables de nivel de clase toohello **aplicación** de la clase, reemplazando **{yourhubconnectionstring}** y **{yourdeviceid}** Hola valores de los indicados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="6a743-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="6a743-148">Reemplace hello **principal** método con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="6a743-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="6a743-149">Este código conecta el centro de IoT tooyour, envía un dispositivo de tooyour de mensaje y, a continuación, espera una confirmación ese mensaje de Hola dispositivo Hola recibidos y procesados:</span><span class="sxs-lookup"><span data-stu-id="6a743-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="6a743-150">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="6a743-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="6a743-151">En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="6a743-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="6a743-152">Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:</span><span class="sxs-lookup"><span data-stu-id="6a743-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="6a743-153">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="6a743-153">Run hello applications</span></span>

<span data-ttu-id="6a743-154">Ya estás listo toorun aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="6a743-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="6a743-155">En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después toobegin comando Enviar telemetría tooyour IoT hub- and toolisten para los mensajes en la nube al dispositivo enviados desde el concentrador:</span><span class="sxs-lookup"><span data-stu-id="6a743-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Ejecutar la aplicación de dispositivo simulado de hello][img-simulated-device]

2. <span data-ttu-id="6a743-157">En un símbolo del sistema en la carpeta de c2d de envío de mensajes de Hola, ejecute hello después comando toosend un mensaje de nube al dispositivo y espera una confirmación de comentarios:</span><span class="sxs-lookup"><span data-stu-id="6a743-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Ejecutar mensaje de saludo comando toosend hello en la nube al dispositivo][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="6a743-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6a743-159">Next steps</span></span>

<span data-ttu-id="6a743-160">En este tutorial, se habrá aprendido cómo toosend y recibir mensajes en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6a743-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="6a743-161">ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="6a743-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="6a743-162">toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="6a743-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[empezar a trabajar con el centro de IoT]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Guía del desarrollador de centro de IoT]: iot-hub-devguide.md
[Centro para desarrolladores de Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[control de errores transitorios]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portal de Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22