---
title: aaaProcess mensajes de dispositivo a la nube de Azure IoT Hub (Java) | Documentos de Microsoft
description: "¿Cómo tooprocess mensajes de dispositivo a la nube del centro de IoT mediante las reglas de enrutamiento y los extremos personalizados toodispatch mensajes tooother servicios de back-end."
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
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="2e1d4-103">Procesamiento de mensajes de dispositivo a nube de IoT Hub (Java)</span><span class="sxs-lookup"><span data-stu-id="2e1d4-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="2e1d4-104">Azure IoT Hub es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="2e1d4-105">Otros tutoriales ([empezar a trabajar con el centro de IoT] y [enviar mensajes en la nube al dispositivo con el centro de IoT][lnk-c2d]) mostrarle cómo toouse Hola básica dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="2e1d4-106">Este tutorial se basa en código de hello mostrado en hello [empezar a trabajar con el centro de IoT] tutorial y se muestra cómo toouse mensaje enrutar mensajes de dispositivo para la nube de tooprocess de forma escalable.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="2e1d4-107">tutorial de Hello ilustra cómo tooprocess mensajes que requieren acción inmediata de solución de hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="2e1d4-108">Por ejemplo, un dispositivo puede enviar un mensaje de alarma que desencadena la inserción de una incidencia en un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="2e1d4-109">Por el contrario, los mensajes de punto de datos simplemente se envían a un motor de análisis.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="2e1d4-110">Por ejemplo, telemetría de temperatura de un dispositivo que se almacenan para su análisis posterior de toobe es un mensaje de punto de datos.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="2e1d4-111">Al final de Hola de este tutorial, ejecutar tres aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="2e1d4-112">**dispositivo simulado**, una versión modificada de la aplicación hello creado en hello [empezar a trabajar con el centro de IoT] tutorial, envía mensajes de dispositivo a la nube de punto de datos cada segundo e interactivo dispositivo a la nube mensajes cada 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="2e1d4-113">Esta aplicación utiliza hello AMQP protocolo toocommunicate con centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="2e1d4-114">**leer mensajes de d2c** muestra telemetría Hola enviado por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="2e1d4-115">**lectura cola crítica** anular pone en cola los mensajes críticos de Hola de hello Service Bus cola adjuntada toohello centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1d4-116">El Centro de IoT ofrece compatibilidad con el SDK para muchas plataformas de dispositivos y lenguajes, entre los que se incluyen C, Java y JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="2e1d4-117">Para obtener instrucciones sobre cómo tooreplace Hola dispositivo en este tutorial con un dispositivo físico, y cómo tooconnect dispositivos tooan centro de IoT, vea hello [Centro para desarrolladores de Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="2e1d4-118">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2e1d4-119">Una versión de trabajo completa de hello [empezar a trabajar con el centro de IoT] tutorial.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="2e1d4-120">Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="2e1d4-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="2e1d4-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="2e1d4-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="2e1d4-122">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-122">An active Azure account.</span></span> <span data-ttu-id="2e1d4-123">(En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="2e1d4-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="2e1d4-124">También se dan por sentados ciertos conocimientos sobre [Azure Storage] y [Azure Service Bus].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="2e1d4-125">Envío de mensajes interactivos desde una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="2e1d4-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="2e1d4-126">En esta sección, modificar Hola del dispositivo que creó en hello [empezar a trabajar con el centro de IoT] toooccasionally tutorial enviar mensajes que requieren un procesamiento inmediato.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="2e1d4-127">Usar un archivo de texto del editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="2e1d4-128">Este archivo contiene código de hello para hello **dispositivo simulado** aplicación que creó en hello [empezar a trabajar con el centro de IoT] tutorial.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="2e1d4-129">Reemplace hello **MessageSender** clase con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-129">Replace hello **MessageSender** class with hello following code:</span></span>

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
   
    <span data-ttu-id="2e1d4-130">Este método agrega al azar propiedad hello `"level": "critical"` toomessages enviados por dispositivo de hello, que simula un mensaje que requiere una acción inmediata por hello aplicación back-end.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="2e1d4-131">aplicación Hello pasa esta información en las propiedades de mensaje de Hola, en lugar de en el cuerpo del mensaje Hola, para que ese centro de IoT pueda enrutar el destino del mensaje adecuado de toohello de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2e1d4-132">Puede utilizar mensajes de tooroute de propiedades de mensaje para varios escenarios incluidos frío-path, además de procesamiento toohello ruta de acceso activa en el ejemplo se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="2e1d4-133">Guarde y cierre el archivo de hello simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2e1d4-134">Para simplificar Hola simplicidad, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2e1d4-135">En el código de producción, debe implementar una directiva de reintentos como retroceso exponencial, tal como se sugiere en el artículo MSDN de hello [control de errores transitorios].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="2e1d4-136">Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="2e1d4-137">Agregar una cola tooyour IoT hub- and enrutar mensajes tooit</span><span class="sxs-lookup"><span data-stu-id="2e1d4-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="2e1d4-138">En esta sección, cree una cola de Bus de servicio, conéctelo tooyour centro de IoT y configurar la cola de toohello IoT hub toosend mensajes basada en presencia de Hola de una propiedad de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="2e1d4-139">Para obtener más información acerca de cómo tooprocess mensajes desde las colas de Bus de servicio, consulte [empezar a trabajar con colas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="2e1d4-140">Cree una cola de Service Bus como se describe en [Introducción a las colas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="2e1d4-141">Tome nota del nombre de espacio de nombres y la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="2e1d4-142">En Hola portal de Azure, abra el centro de IoT y haga clic en **extremos**.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Puntos de conexión en IoT Hub][30]

3. <span data-ttu-id="2e1d4-144">Hola **extremos** hoja, haga clic en **agregar** en Hola tooadd superior su centro de IoT tooyour de cola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="2e1d4-145">El punto de conexión de nombre hello **CriticalQueue** y usar Hola listas desplegables tooselect **cola de Service Bus**, Hola espacio de nombres de Bus de servicio en el que reside la cola y Hola nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="2e1d4-146">Cuando haya terminado, haga clic en **guardar** final Hola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Adición de un punto de conexión][31]

4. <span data-ttu-id="2e1d4-148">Ahora haga clic en **Routes** (Rutas) en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="2e1d4-149">Haga clic en **agregar** en parte superior de Hola de hello hoja toocreate agrega una regla de enrutamiento que enruta los mensajes de cola que toohello se acaba.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="2e1d4-150">Seleccione **DeviceTelemetry** como origen de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="2e1d4-151">Escriba `level="critical"` como condición de hello y elija la cola de Hola que acaba de agregar como un extremo personalizado como Hola extremo de la regla de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="2e1d4-152">Cuando haya terminado, haga clic en **guardar** final Hola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Adición de una ruta][32]

    <span data-ttu-id="2e1d4-154">Asegúrese de que la ruta de reserva de Hola se establece demasiado**ON**.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="2e1d4-155">Esta opción es la configuración predeterminada de Hola de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Ruta de reserva][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="2e1d4-157">(Opcional) Leer desde el punto de conexión de hello cola</span><span class="sxs-lookup"><span data-stu-id="2e1d4-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="2e1d4-158">Si lo desea puede leer mensajes de saludo de extremo de la cola de Hola siguiendo las instrucciones de hello en [empezar a trabajar con colas][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="2e1d4-159">Aplicación de hello nombre **lectura cola crítica**.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="2e1d4-160">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="2e1d4-160">Run hello applications</span></span>

<span data-ttu-id="2e1d4-161">Ahora son tres aplicaciones de listo toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="2e1d4-162">Hola toorun **leer mensajes de d2c** aplicación, en un símbolo del sistema o el shell de desplazarse por las carpetas de lectura d2c toohello y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Ejecución de read-d2c-messages][readd2c]

2. <span data-ttu-id="2e1d4-164">Hola toorun **lectura cola crítica** aplicación, en un símbolo del sistema o el shell de desplazarse por las carpetas de cola lectura crítica toohello y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Ejecución de read-critical-messages][readqueue]

3. <span data-ttu-id="2e1d4-166">Hola toorun **dispositivo simulado** aplicación, en un símbolo del sistema o el shell de desplazarse por las carpetas de dispositivo simulado toohello y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="2e1d4-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Ejecución de simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="2e1d4-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2e1d4-168">Next steps</span></span>

<span data-ttu-id="2e1d4-169">En este tutorial, ha aprendido cómo tooreliably enviar mensajes del dispositivo a la nube mediante la funcionalidad de enrutamiento de mensajes de Hola de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="2e1d4-170">Hola [cómo mensajes toosend en la nube al dispositivo con el centro de IoT] [ lnk-c2d] muestra cómo toosend mensajes tooyour dispositivos desde el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="2e1d4-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="2e1d4-171">ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="2e1d4-172">toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="2e1d4-173">toolearn más información acerca de enrutamiento de mensajes en el centro de IoT, consulte [enviar y recibir mensajes con el centro de IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="2e1d4-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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

[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/
[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/

[Guía del desarrollador de centro de IoT]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[empezar a trabajar con el centro de IoT]: iot-hub-java-java-getstarted.md
[Centro para desarrolladores de Azure IoT]: https://azure.microsoft.com/develop/iot
[control de errores transitorios]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
