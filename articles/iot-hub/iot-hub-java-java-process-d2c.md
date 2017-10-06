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
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Procesamiento de mensajes de dispositivo a nube de IoT Hub (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

Azure IoT Hub es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de la solución. Otros tutoriales ([empezar a trabajar con el centro de IoT] y [enviar mensajes en la nube al dispositivo con el centro de IoT][lnk-c2d]) mostrarle cómo toouse Hola básica dispositivo a la nube y en la nube al dispositivo funcionalidad de mensajería del centro de IoT.

Este tutorial se basa en código de hello mostrado en hello [empezar a trabajar con el centro de IoT] tutorial y se muestra cómo toouse mensaje enrutar mensajes de dispositivo para la nube de tooprocess de forma escalable. tutorial de Hello ilustra cómo tooprocess mensajes que requieren acción inmediata de solución de hello back-end. Por ejemplo, un dispositivo puede enviar un mensaje de alarma que desencadena la inserción de una incidencia en un sistema CRM. Por el contrario, los mensajes de punto de datos simplemente se envían a un motor de análisis. Por ejemplo, telemetría de temperatura de un dispositivo que se almacenan para su análisis posterior de toobe es un mensaje de punto de datos.

Al final de Hola de este tutorial, ejecutar tres aplicaciones de consola de Java:

* **dispositivo simulado**, una versión modificada de la aplicación hello creado en hello [empezar a trabajar con el centro de IoT] tutorial, envía mensajes de dispositivo a la nube de punto de datos cada segundo e interactivo dispositivo a la nube mensajes cada 10 segundos. Esta aplicación utiliza hello AMQP protocolo toocommunicate con centro de IoT.
* **leer mensajes de d2c** muestra telemetría Hola enviado por la aplicación de dispositivo.
* **lectura cola crítica** anular pone en cola los mensajes críticos de Hola de hello Service Bus cola adjuntada toohello centro de IoT.

> [!NOTE]
> El Centro de IoT ofrece compatibilidad con el SDK para muchas plataformas de dispositivos y lenguajes, entre los que se incluyen C, Java y JavaScript. Para obtener instrucciones sobre cómo tooreplace Hola dispositivo en este tutorial con un dispositivo físico, y cómo tooconnect dispositivos tooan centro de IoT, vea hello [Centro para desarrolladores de Azure IoT].

toocomplete este tutorial, necesita Hola siguientes:

* Una versión de trabajo completa de hello [empezar a trabajar con el centro de IoT] tutorial.
* Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Una cuenta de Azure activa. (En caso de no tener ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos).

También se dan por sentados ciertos conocimientos sobre [Azure Storage] y [Azure Service Bus].

## <a name="send-interactive-messages-from-a-device-app"></a>Envío de mensajes interactivos desde una aplicación de dispositivo
En esta sección, modificar Hola del dispositivo que creó en hello [empezar a trabajar con el centro de IoT] toooccasionally tutorial enviar mensajes que requieren un procesamiento inmediato.

1. Usar un archivo de texto del editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java. Este archivo contiene código de hello para hello **dispositivo simulado** aplicación que creó en hello [empezar a trabajar con el centro de IoT] tutorial.

2. Reemplace hello **MessageSender** clase con el siguiente código de hello:

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
   
    Este método agrega al azar propiedad hello `"level": "critical"` toomessages enviados por dispositivo de hello, que simula un mensaje que requiere una acción inmediata por hello aplicación back-end. aplicación Hello pasa esta información en las propiedades de mensaje de Hola, en lugar de en el cuerpo del mensaje Hola, para que ese centro de IoT pueda enrutar el destino del mensaje adecuado de toohello de mensaje de Hola.
   
   > [!NOTE]
   > Puede utilizar mensajes de tooroute de propiedades de mensaje para varios escenarios incluidos frío-path, además de procesamiento toohello ruta de acceso activa en el ejemplo se muestra aquí.

2. Guarde y cierre el archivo de hello simulated-device\src\main\java\com\mycompany\app\App.java.

    > [!NOTE]
    > Para simplificar Hola simplicidad, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar una directiva de reintentos como retroceso exponencial, tal como se sugiere en el artículo MSDN de hello [control de errores transitorios].

3. Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Agregar una cola tooyour IoT hub- and enrutar mensajes tooit

En esta sección, cree una cola de Bus de servicio, conéctelo tooyour centro de IoT y configurar la cola de toohello IoT hub toosend mensajes basada en presencia de Hola de una propiedad de mensaje de Hola. Para obtener más información acerca de cómo tooprocess mensajes desde las colas de Bus de servicio, consulte [empezar a trabajar con colas][lnk-sb-queues-java].

1. Cree una cola de Service Bus como se describe en [Introducción a las colas][lnk-sb-queues-java]. Tome nota del nombre de espacio de nombres y la cola de Hola.

2. En Hola portal de Azure, abra el centro de IoT y haga clic en **extremos**.

    ![Puntos de conexión en IoT Hub][30]

3. Hola **extremos** hoja, haga clic en **agregar** en Hola tooadd superior su centro de IoT tooyour de cola. El punto de conexión de nombre hello **CriticalQueue** y usar Hola listas desplegables tooselect **cola de Service Bus**, Hola espacio de nombres de Bus de servicio en el que reside la cola y Hola nombre de la cola. Cuando haya terminado, haga clic en **guardar** final Hola.

    ![Adición de un punto de conexión][31]

4. Ahora haga clic en **Routes** (Rutas) en IoT Hub. Haga clic en **agregar** en parte superior de Hola de hello hoja toocreate agrega una regla de enrutamiento que enruta los mensajes de cola que toohello se acaba. Seleccione **DeviceTelemetry** como origen de Hola de datos. Escriba `level="critical"` como condición de hello y elija la cola de Hola que acaba de agregar como un extremo personalizado como Hola extremo de la regla de enrutamiento. Cuando haya terminado, haga clic en **guardar** final Hola.

    ![Adición de una ruta][32]

    Asegúrese de que la ruta de reserva de Hola se establece demasiado**ON**. Esta opción es la configuración predeterminada de Hola de un centro de IoT.

    ![Ruta de reserva][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Opcional) Leer desde el punto de conexión de hello cola

Si lo desea puede leer mensajes de saludo de extremo de la cola de Hola siguiendo las instrucciones de hello en [empezar a trabajar con colas][lnk-sb-queues-java]. Aplicación de hello nombre **lectura cola crítica**.

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola

Ahora son tres aplicaciones de listo toorun Hola.

1. Hola toorun **leer mensajes de d2c** aplicación, en un símbolo del sistema o el shell de desplazarse por las carpetas de lectura d2c toohello y ejecute el siguiente comando de hello:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Ejecución de read-d2c-messages][readd2c]

2. Hola toorun **lectura cola crítica** aplicación, en un símbolo del sistema o el shell de desplazarse por las carpetas de cola lectura crítica toohello y ejecute el siguiente comando de hello:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Ejecución de read-critical-messages][readqueue]

3. Hola toorun **dispositivo simulado** aplicación, en un símbolo del sistema o el shell de desplazarse por las carpetas de dispositivo simulado toohello y ejecute el siguiente comando de hello:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Ejecución de simulated-device][simulateddevice]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo tooreliably enviar mensajes del dispositivo a la nube mediante la funcionalidad de enrutamiento de mensajes de Hola de centro de IoT.

Hola [cómo mensajes toosend en la nube al dispositivo con el centro de IoT] [ lnk-c2d] muestra cómo toosend mensajes tooyour dispositivos desde el back-end de soluciones.

ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite][lnk-suite].

toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].

toolearn más información acerca de enrutamiento de mensajes en el centro de IoT, consulte [enviar y recibir mensajes con el centro de IoT][lnk-devguide-messaging].

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
