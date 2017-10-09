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
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Envío mensajes de nube a dispositivo con IoT Hub (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

IoT Hub de Azure es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y una solución de back-end. Hola [empezar a trabajar con el centro de IoT] tutorial muestra cómo aprovisionar una identidad de dispositivo en el toocreate un centro de IoT y codificar una aplicación de dispositivo simulado que envía mensajes de dispositivo para la nube.

Este tutorial se basa en la [empezar a trabajar con el centro de IoT]. En él se muestra cómo realizar las siguientes acciones:

* Desde el back-end de soluciones, enviar mensajes en la nube al dispositivo tooa dispositivo a través del centro de IoT.
* Reciba mensajes de nube a dispositivo en un dispositivo.
* En el back-end de soluciones, solicitar confirmación de entrega (*comentarios*) para mensajes envían tooa dispositivo desde el centro de IoT.

Puede encontrar más información sobre los mensajes en la nube al dispositivo en hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].

Al final de Hola de este tutorial, ejecute dos aplicaciones de consola de Java:

* **dispositivo simulado**, una versión modificada de la aplicación hello creado en [empezar a trabajar con el centro de IoT], que se conecta el centro de IoT tooyour y recibe los mensajes de la nube al dispositivo.
* **enviar mensajes de c2d**, que envía una aplicación de dispositivo simulado de toohello de mensaje en la nube al dispositivo a través del centro de IoT y, a continuación, recibe la confirmación de entrega.

> [!NOTE]
> El Centro de IoT ofrece compatibilidad con el SDK en muchas plataformas de dispositivos y lenguajes (incluido C, Java y Javascript), mediante los SDK de dispositivos IoT de Azure. Para obtener instrucciones paso a paso sobre cómo tooconnect del su dispositivo toothis tutorial código y generalmente tooAzure centro de IoT, vea hello [Centro para desarrolladores de Azure IoT].

toocomplete este tutorial, necesita Hola siguientes:

* Una versión de trabajo completa de hello [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) o [mensajes del dispositivo a la nube de centro de IoT de proceso](iot-hub-java-java-process-d2c.md) tutorial.
* Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

## <a name="receive-messages-in-hello-simulated-device-app"></a>Recibir mensajes en la aplicación de dispositivo simulado de hello

En esta sección, modificar aplicación de dispositivo simulado de Hola que creó en [empezar a trabajar con el centro de IoT] mensajes de nube al dispositivo tooreceive Hola centro de IoT.

1. Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java de hello.

2. Agregue los siguiente hello **MessageCallback** clase como una clase anidada dentro de hello **aplicación** clase. Hola **ejecutar** método se invoca cuando el dispositivo de hello recibe un mensaje desde el centro de IoT. En este ejemplo, dispositivo Hola siempre notifica al centro de IoT de Hola que se ha completado el mensaje de bienvenida:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Modificar hello **principal** método toocreate una **AppMessageCallback** Hola de instancia y llame al método **setMessageCallback** método antes de su apertura cliente hello como sigue:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > Si utiliza HTTP como transporte de hello en lugar de MQTT o AMQP, Hola **DeviceClient** instancia comprueba si hay mensajes de centro de IoT con poca frecuencia (menor que cada 25 minutos). Para obtener más información acerca de las diferencias de hello entre soporte MQTT, AMQP y HTTP y la limitación de centro de IoT, vea hello [Guía del desarrollador de centro de IoT][IoT Hub developer guide - C2D].

4. Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Envío de mensajes de nube a dispositivo

En esta sección, creará una aplicación de consola de Java que envía mensajes en la nube al dispositivo toohello del dispositivo simulado. Necesita Hola Id. de dispositivo del dispositivo de Hola que agregó en hello [empezar a trabajar con el centro de IoT] tutorial. También necesita Hola cadena de conexión de centro de IoT su base de datos central que se puede encontrar en hello [portal de Azure].

1. Cree un proyecto de Maven denominado **c2d de envío de mensajes** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. En el símbolo del sistema, navegue toohello nueva carpeta de c2d de envío de mensajes.

3. Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta de c2d de envío de mensajes de Hola y agregue Hola después toohello de dependencia **dependencias** nodo. Agregar dependencia Hola permite hello toouse **el centro de IOT java servicio cliente** paquete en su toocommunicate de aplicación con el servicio del centro de IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven][lnk-maven-service-search].

4. Guarde y cierre el archivo de hello pom.xml.

5. Con un editor de texto, abra el archivo send-c2d-messages\src\main\java\com\mycompany\app\App.java de hello.

6. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Agregar Hola después de las variables de nivel de clase toohello **aplicación** de la clase, reemplazando **{yourhubconnectionstring}** y **{yourdeviceid}** Hola valores de los indicados anteriormente:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Reemplace hello **principal** método con el siguiente código de hello. Este código conecta el centro de IoT tooyour, envía un dispositivo de tooyour de mensaje y, a continuación, espera una confirmación ese mensaje de Hola dispositivo Hola recibidos y procesados:
   
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
    > Por simplificar, este tutorial no implementa ninguna directiva de reintentos. En el código de producción, debe implementar directivas de reintento (por ejemplo, retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios].


9. Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun aplicaciones de Hola.

1. En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después toobegin comando Enviar telemetría tooyour IoT hub- and toolisten para los mensajes en la nube al dispositivo enviados desde el concentrador:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Ejecutar la aplicación de dispositivo simulado de hello][img-simulated-device]

2. En un símbolo del sistema en la carpeta de c2d de envío de mensajes de Hola, ejecute hello después comando toosend un mensaje de nube al dispositivo y espera una confirmación de comentarios:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Ejecutar mensaje de saludo comando toosend hello en la nube al dispositivo][img-send-command]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se habrá aprendido cómo toosend y recibir mensajes en la nube al dispositivo. 

ver ejemplos de toosee de soluciones completas de-to-end que usar el centro de IoT, consulte [Azure IoT Suite].

toolearn más sobre el desarrollo de soluciones con el centro de IoT, vea hello [Guía del desarrollador de centro de IoT].

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