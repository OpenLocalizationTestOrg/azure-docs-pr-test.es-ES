---
title: Procesamiento de mensajes de dispositivo a la nube de IoT Hub de Azure (Java) | Microsoft Docs
description: "Cómo procesar mensajes de dispositivo a nube de IoT Hub mediante reglas de enrutamiento y puntos de conexión personalizados para enviar mensajes a otros servicios de back-end."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: d1aca8f39e305105d4ec9f63fbe7bee95487e294
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="e9eea-103">Procesamiento de mensajes de dispositivo a nube de IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="e9eea-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="e9eea-104">Azure IoT Hub es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="e9eea-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="e9eea-105">Otros tutoriales ([Introducción a IoT Hub] y [Envío de mensajes de nube a dispositivo con IoT Hub][lnk-c2d]) muestran cómo usar la funcionalidad básica de mensajería de dispositivo a nube y de nube a dispositivo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9eea-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="e9eea-106">Este tutorial se basa en el código que se muestra en el tutorial [Introducción a IoT Hub] y le muestra cómo usar el enrutamiento de mensajes para procesar mensajes del dispositivo a la nube de manera escalable.</span><span class="sxs-lookup"><span data-stu-id="e9eea-106">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="e9eea-107">El tutorial ilustra cómo procesar mensajes que requieren acción inmediata en el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="e9eea-107">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="e9eea-108">Por ejemplo, un dispositivo puede enviar un mensaje de alarma que desencadena la inserción de una incidencia en un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="e9eea-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="e9eea-109">Por el contrario, los mensajes de punto de datos simplemente se envían a un motor de análisis.</span><span class="sxs-lookup"><span data-stu-id="e9eea-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="e9eea-110">Por ejemplo, la telemetría de temperatura de un dispositivo que se almacena para su posterior análisis es un mensaje de punto de datos.</span><span class="sxs-lookup"><span data-stu-id="e9eea-110">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="e9eea-111">Al final de este tutorial, ejecutará tres aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="e9eea-111">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="e9eea-112">**simulated-device**, una versión modificada de la aplicación creada en el tutorial [Introducción a IoT Hub] , que envía mensajes de dispositivo a nube de punto de datos cada segundo y mensajes de dispositivo a nube interactivos cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="e9eea-112">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="e9eea-113">Esta aplicación usa el protocolo AMQP para comunicarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9eea-113">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="e9eea-114">**read-d2c-messages** muestra los datos de telemetría enviados por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e9eea-114">**read-d2c-messages** displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="e9eea-115">**read-critical-queue** quita de la cola los mensajes críticos de la cola de la instancia de Service Bus adjunta a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9eea-115">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e9eea-116">El Centro de IoT ofrece compatibilidad con el SDK para muchas plataformas de dispositivos y lenguajes, entre los que se incluyen C, Java y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e9eea-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="e9eea-117">Para instrucciones sobre cómo reemplazar el dispositivo de este tutorial con un dispositivo físico y sobre cómo conectar dispositivos a IoT Hub, consulte el [Centro para desarrolladores de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="e9eea-117">For instructions on how to replace the device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="e9eea-118">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9eea-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="e9eea-119">Una versión funcional y completa del tutorial [Introducción a IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="e9eea-119">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="e9eea-120">La versión más reciente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="e9eea-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="e9eea-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="e9eea-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="e9eea-122">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e9eea-122">An active Azure account.</span></span> <span data-ttu-id="e9eea-123">(En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="e9eea-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="e9eea-124">También se dan por sentados ciertos conocimientos sobre [Azure Storage] y [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="e9eea-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="e9eea-125">Envío de mensajes interactivos desde una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e9eea-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="e9eea-126">En esta sección, se modifica la aplicación de dispositivo que creó en el tutorial [Introducción a IoT Hub] a fin de enviar ocasionalmente mensajes que requieren un procesamiento inmediato.</span><span class="sxs-lookup"><span data-stu-id="e9eea-126">In this section, you modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="e9eea-127">Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="e9eea-127">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="e9eea-128">Este archivo contiene el código para la aplicación **simulated-device** que creó en el tutorial [Introducción a IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="e9eea-128">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="e9eea-129">Reemplace la clase **MessageSender** por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9eea-129">Replace the **MessageSender** class with the following code:</span></span>

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
                    System.out.println("Sending: " + msgStr);

                    Object lockobj = new Object();
                    EventCallback callback = new EventCallback();
                    client.sendEventAsync(msg, callback, lockobj);

                    synchronized (lockobj) {
                        lockobj.wait();
                    }
                    Thread.sleep(1000);
                }
            } catch (InterruptedException e) {
                System.out.println("Finished.");
            }
        }
    }
    ```
   
    <span data-ttu-id="e9eea-130">Con este método se agrega aleatoriamente la propiedad `"level": "critical"` a los mensajes que envía el dispositivo, lo que simula un mensaje que requiere una acción inmediata del back-end de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e9eea-130">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="e9eea-131">La aplicación pasa esta información en las propiedades del mensaje, en lugar de en el cuerpo del mensaje, de manera que este IoT Hub puede enrutar el mensaje a su destino correcto.</span><span class="sxs-lookup"><span data-stu-id="e9eea-131">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e9eea-132">Puede usar propiedades de mensaje a fin de enrutar mensajes en diferentes escenarios, como el procesamiento en frío, además del ejemplo de procesamiento en caliente que se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="e9eea-132">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>

2. <span data-ttu-id="e9eea-133">Guarde y cierre el archivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="e9eea-133">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e9eea-134">Para simplificar, en este tutorial no se implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="e9eea-134">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e9eea-135">En el código de producción, debe implementar una directiva de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling](Control de errores transitorios).</span><span class="sxs-lookup"><span data-stu-id="e9eea-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="e9eea-136">Para compilar la aplicación **simulated-device** con Maven, ejecute el siguiente comando en el símbolo del sistema en la carpeta simulated-device:</span><span class="sxs-lookup"><span data-stu-id="e9eea-136">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="e9eea-137">Adición de una cola a su IoT Hub y enrutamiento de mensajes a ella</span><span class="sxs-lookup"><span data-stu-id="e9eea-137">Add a queue to your IoT hub and route messages to it</span></span>

<span data-ttu-id="e9eea-138">En esta sección, se crea una cola de Service Bus, se conecta con el IoT Hub y se configura el IoT Hub para enviar mensajes a la cola en función de la presencia de una propiedad en el mensaje.</span><span class="sxs-lookup"><span data-stu-id="e9eea-138">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="e9eea-139">Para obtener más información acerca de cómo procesar los mensajes desde las colas de Service Bus, consulte [Introducción a las colas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="e9eea-139">For more information about how to process messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="e9eea-140">Cree una cola de Service Bus como se describe en [Introducción a las colas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="e9eea-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="e9eea-141">Tome nota del espacio de nombres y del nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="e9eea-141">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="e9eea-142">En Azure Portal, abra el centro de IoT y haga clic en **Endpoints** (Puntos de conexión).</span><span class="sxs-lookup"><span data-stu-id="e9eea-142">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Puntos de conexión en IoT Hub][30]

3. <span data-ttu-id="e9eea-144">En la hoja **Endpoints** (Puntos de conexión), haga clic en **Add** (Agregar) en la parte superior para agregar la cola al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e9eea-144">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="e9eea-145">Ponga al punto de conexión el nombre **CriticalQueue** y use las listas desplegables para seleccionar **Cola de Service Bus**, el espacio de nombres de Service Bus en el que reside la cola y el nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="e9eea-145">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="e9eea-146">Cuando haya terminado, haga clic en **Guardar** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e9eea-146">When you are done, click **Save** at the bottom.</span></span>

    ![Adición de un punto de conexión][31]

4. <span data-ttu-id="e9eea-148">Ahora haga clic en **Routes** (Rutas) en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9eea-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="e9eea-149">Haga clic en **Add** (Agregar) en la parte superior de la hoja para crear una regla que enrute los mensajes a la cola que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="e9eea-149">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="e9eea-150">Seleccione **DeviceTelemetry** como origen de los datos.</span><span class="sxs-lookup"><span data-stu-id="e9eea-150">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="e9eea-151">Escriba `level="critical"` como condición y elija la cola que acaba de agregar como punto de conexión personalizado como punto de conexión de regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="e9eea-151">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="e9eea-152">Cuando haya terminado, haga clic en **Guardar** de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="e9eea-152">When you are done, click **Save** at the bottom.</span></span>

    ![Adición de una ruta][32]

    <span data-ttu-id="e9eea-154">Asegúrese de que la ruta de reserva se establece en **ON** (Activado).</span><span class="sxs-lookup"><span data-stu-id="e9eea-154">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="e9eea-155">Esta es la configuración predeterminada del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e9eea-155">This setting is the default configuration of an IoT hub.</span></span>

    ![Ruta de reserva][33]

## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="e9eea-157">(Opcional) Lectura desde el punto de conexión de la cola</span><span class="sxs-lookup"><span data-stu-id="e9eea-157">(Optional) Read from the queue endpoint</span></span>

<span data-ttu-id="e9eea-158">Opcionalmente, puede leer los mensajes desde el punto de conexión de la cola siguiendo las instrucciones de [Introducción a las colas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="e9eea-158">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="e9eea-159">Ponga a la aplicación el nombre **read-critical-queue**.</span><span class="sxs-lookup"><span data-stu-id="e9eea-159">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="e9eea-160">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="e9eea-160">Run the applications</span></span>

<span data-ttu-id="e9eea-161">Ahora está preparado para ejecutar las tres aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e9eea-161">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="e9eea-162">Para ejecutar la aplicación **process-d2c-messages**, en un símbolo del sistema o en el shell, vaya a la carpeta read-d2c y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e9eea-162">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Ejecución de read-d2c-messages][readd2c]

2. <span data-ttu-id="e9eea-164">Para ejecutar la aplicación **read-critical-queue**, en un símbolo del sistema o el shell, navegue hasta la carpeta read-critical-queue y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="e9eea-164">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Ejecución de read-critical-messages][readqueue]

3. <span data-ttu-id="e9eea-166">Para ejecutar la aplicación **simulated-device**, en un símbolo del sistema o en el shell, vaya a la carpeta simulated-device y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e9eea-166">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Ejecución de simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="e9eea-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9eea-168">Next steps</span></span>

<span data-ttu-id="e9eea-169">En este tutorial, ha aprendido a enviar de manera confiable mensajes del dispositivo a la nube mediante la funcionalidad de enrutamiento de mensajes de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9eea-169">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="e9eea-170">El tutorial sobre [cómo enviar mensajes de dispositivo a la nube con IoT Hub][lnk-c2d] muestra cómo enviar mensajes a los dispositivos desde la solución de back-end.</span><span class="sxs-lookup"><span data-stu-id="e9eea-170">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="e9eea-171">Para ver ejemplos de soluciones completas de un extremo a otro que usan IoT Hub, consulte [Conjunto de aplicaciones de IoT de Azure][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="e9eea-171">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="e9eea-172">Para obtener más información sobre cómo desarrollar soluciones con IoT Hub, consulte la [Guía del desarrollador de IoTHub de Azure].</span><span class="sxs-lookup"><span data-stu-id="e9eea-172">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="e9eea-173">Para obtener más información sobre el enrutamiento de mensajes en IoT Hub, consulte [Envío y recepción de mensajes con IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="e9eea-173">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

<span data-ttu-id="e9eea-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="e9eea-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="e9eea-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="e9eea-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>

<span data-ttu-id="e9eea-176">[Guía del desarrollador de IoTHub de Azure]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="e9eea-176">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="e9eea-177">[Introducción a IoT Hub]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="e9eea-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
<span data-ttu-id="e9eea-178">[Centro para desarrolladores de Azure IoT]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="e9eea-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="e9eea-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span><span class="sxs-lookup"><span data-stu-id="e9eea-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span></span>

<!-- Links -->
<span data-ttu-id="e9eea-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="e9eea-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
