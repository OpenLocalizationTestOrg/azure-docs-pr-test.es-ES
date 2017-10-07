---
title: aaaGet a trabajar con el centro de IoT de Azure (Java) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosend dispositivo a la nube mensajes tooAzure centro de IoT con IoT SDK para Java. Crear dispositivo simulado y tooregister de aplicaciones de servicio, el dispositivo, enviar mensajes y leer los mensajes de centro de IoT."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Conectar el centro de IoT de tooyour dispositivo usa Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Al final de Hola de este tutorial, tendrá tres aplicaciones de consola de Java:

* **identidad del dispositivo crear**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo.
* **leer mensajes de d2c**, que muestra la telemetría de hello enviado por la aplicación de dispositivo.
* **dispositivo simulado**, que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y envía un mensaje de telemetría cada segundo mediante Hola protocolo MQTT.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.

toocomplete este tutorial, necesita Hola siguientes:

* Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Una cuenta de Azure activa. (En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Como paso final, tome nota de hello **clave principal** valor. A continuación, haga clic en **extremos** hello y **eventos** extremo predefinido. En hello **propiedades** hoja, tome nota de hello **nombre de concentrador de eventos-compatible con** hello y **punto de conexión de concentrador de eventos-compatible con** dirección. Necesita estos tres valores al crear la aplicación **read-d2c-messages**.

![Hoja de mensajería de IoT Hub de Azure Portal][6]

Ahora ha creado su instancia de IoT Hub. Tener Hola nombre de host del centro de IoT, cadena de conexión de centro de IoT, clave principal del centro de IoT, nombre de concentrador de eventos-compatible con y punto de conexión compatible de concentrador de eventos necesita toocomplete este tutorial.

## <a name="create-a-device-identity"></a>Creación de una identidad de dispositivo
En esta sección, creará una aplicación de consola de Java que crea una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT. Un dispositivo no puede conectar tooIoT concentrador a menos que tenga una entrada en el registro de la identidad de Hola. Para obtener más información, vea hello **del registro de identidad** sección de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity]. Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.

1. Cree una carpeta vacía denominada iot-java-get-started. En carpeta iot java-get-iniciada hello, cree un proyecto de Maven denominado **identidad del dispositivo crear** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. En el símbolo del sistema, desplazarse por las carpetas de identidad del dispositivo crear toohello.

3. Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta de identidad del dispositivo crear Hola y agregue Hola después toohello de dependencia **dependencias** nodo. Esta dependencia permite toouse Hola iot-servicio-paquete de cliente de la aplicación:

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

5. Con un editor de texto, abra el archivo create-device-identity\src\main\java\com\mycompany\app\App.java de hello.

6. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Agregar Hola después de las variables de nivel de clase toohello **aplicación** de la clase, reemplazando **{yourhubconnectionstring}** con hello valor su se indicó anteriormente:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Modificar firma Hola de hello **principal** método tooinclude Hola excepciones como se indica a continuación:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Agregar Hola siguiente código como cuerpo del mensaje de Hola Hola **principal** método. Este código crea un dispositivo denominado *javadevice* en el registro de identidades de IoT Hub, si no existe. A continuación, muestra la Id. de dispositivo de Hola y la clave que necesita más adelante:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Guarde y cierre el archivo de hello App.java.

11. Hola toobuild **identidad del dispositivo crear** aplicación con Maven, ejecutar el siguiente comando en línea de comandos de hello en la carpeta de identidad del dispositivo crear Hola de hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. Hola toorun **identidad del dispositivo crear** aplicación con Maven, ejecutar el siguiente comando en línea de comandos de hello en la carpeta de identidad del dispositivo crear Hola de hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Tome nota de hello **Id. de dispositivo** y **clave de dispositivo**. Necesita estos valores más tarde cuando se crea una aplicación que se conecte tooIoT concentrador como un dispositivo.

> [!NOTE]
> Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro. Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual. Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación. Para obtener más información, vea hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Recepción de mensajes de dispositivo a nube

En esta sección, creará una aplicación de consola de Java que lee los mensajes de dispositivo a nube desde IoT Hub. Un centro de IoT expone un [concentrador de eventos][lnk-event-hubs-overview]-extremo compatible tooenable tooread mensajes de dispositivo a la nube. tookeep cosas simples, en este tutorial se crea un lector básico que no es adecuado para una implementación de alto rendimiento. Hola [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial muestra cómo los mensajes tooprocess dispositivo a la nube a escala. Hola [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial proporciona información adicional acerca de cómo tooprocess mensajes desde los centros de eventos y es aplicable toohello los puntos de conexión compatibles con eventos de centro de IoT Hub.

> [!NOTE]
> Hola extremo compatible de concentrador de eventos para leer mensajes de dispositivo para la nube siempre utiliza Hola protocolo AMQP.

1. En la carpeta de hello iot java-get-iniciada por el que creó en hello *crear una identidad de dispositivo* sección, cree un proyecto de Maven denominado **leer mensajes de d2c** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. En el símbolo del sistema, desplazarse por las carpetas de toohello d2c de lectura de mensajes.

3. Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta de d2c de lectura de mensajes de Hola y agregue Hola después toohello de dependencia **dependencias** nodo. Esta dependencia permite toouse paquete de cliente eventhubs hello en su tooread de aplicación desde el punto de conexión de hello compatible de concentrador de eventos:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Guarde y cierre el archivo de hello pom.xml.

5. Con un editor de texto, abra el archivo read-d2c-messages\src\main\java\com\mycompany\app\App.java de hello.

6. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Agregar Hola después toohello variable de nivel de clase **aplicación** clase. Reemplace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, y **{youreventhubcompatiblename}** con valores de hello que anotó anteriormente:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Agregue los siguiente hello **receiveMessages** método toohello **aplicación** clase. Este método crea un **EventHubClient** tooconnect toohello compatible con el concentrador de eventos extremo de la instancia y, a continuación, crea de forma asincrónica un **PartitionReceiver** tooread de instancia de un concentrador de eventos partición. Se reproduce en bucle continuo y detalles del mensaje Hola se imprimen hasta que finaliza la aplicación hello.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Este método usa un filtro cuando se crea el receptor de Hola para que hello receptor solo lee los mensajes enviados tooIoT concentrador después de receptor de hello empieza a ejecutarse. Esta técnica es útil en un entorno de prueba para que pueda ver el conjunto actual de Hola de mensajes. En un entorno de producción, el código debe asegurarse de que procesa todos los mensajes de Hola - para obtener más información, vea hello [cómo tooprocess mensajes del dispositivo a la nube de centro de IoT] [ lnk-process-d2c-tutorial] tutorial.

9. Modificar firma Hola de hello **principal** método tooinclude Hola excepción como sigue:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Agregar Hola después código toohello **principal** método Hola **aplicación** clase. Este código crea dos hello **EventHubClient** y **PartitionReceiver** instancias y le permite tooclose Hola aplicación cuando haya terminado de procesar los mensajes:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Este código supone que se creó el centro de IoT en nivel de hello F1 (gratis). Una instancia gratuita de IoT Hub tiene dos particiones denominadas "0" y "1".

11. Guarde y cierre el archivo de hello App.java.

12. Hola toobuild **leer mensajes de d2c** aplicación con Maven, ejecutar el siguiente comando en línea de comandos de hello en carpeta de hello d2c de lectura de mensajes de Hola:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Creación de una aplicación de dispositivo
En esta sección, creará una aplicación de consola de Java que simula un dispositivo que envía el centro de IoT tooan de mensajes del dispositivo a la nube.

1. En la carpeta de hello iot java-get-iniciada por el que creó en hello *crear una identidad de dispositivo* sección, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. En el símbolo del sistema, desplazarse por las carpetas de toohello dispositivo simulado.

3. Con un editor de texto, abra archivo pom.xml de hello en la carpeta del dispositivo simulado de Hola y agregue Hola siguiendo las dependencias toohello **dependencias** nodo. Esta dependencia permite toouse Hola el centro de IOT-java-paquete de cliente de su toocommunicate de aplicación con el centro de IoT y tooserialize tooJSON de objetos de Java:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven][lnk-maven-device-search].

4. Guarde y cierre el archivo de hello pom.xml.

5. Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java de hello.

6. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplazar **{youriothubname}** por el nombre del centro de IoT, y **{yourdevicekey}** con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto. Puede usar cualquier toocommunicate de protocolo hello MQTT, AMQP o HTTP con el centro de IoT.

8. Agregue los siguiente Hola anidados **TelemetryDataPoint** clase dentro de hello **aplicación** clase toospecify los datos de telemetría Hola el dispositivo envía tooyour centro de IoT:

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Agregue los siguiente Hola anidados **EventCallback** clase dentro de hello **aplicación** toodisplay Hola confirmación estado de la clase que Hola centro de IoT devuelve cuando procesa un mensaje de aplicación de dispositivo de hello. Este método también notifica al subproceso principal de hello en aplicación hello cuando se ha procesado el mensaje de bienvenida:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Agregue los siguiente Hola anidados **MessageSender** clase dentro de hello **aplicación** clase. Hola **ejecutar** método en esta clase genera el centro de IoT de tooyour de toosend datos de telemetría de ejemplo y espera una confirmación antes de enviar mensajes de bienvenida del siguiente:

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
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

    Este método envía un nuevo mensaje de dispositivo para la nube un segundo después de centro de IoT Hola confirma los mensajes de bienvenida del anterior. mensaje de bienvenida contiene un objeto JSON serializado con deviceId hello y genera de forma aleatoria los números toosimulate un sensor de temperatura y un sensor de humedad.

11. Reemplace hello **principal** método con hello después el código que crea un centro de IoT de tooyour de subproceso toosend mensajes del dispositivo a la nube:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Guarde y cierre el archivo de hello App.java.

13. Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento. En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun Hola aplicaciones.

1. En un símbolo del sistema en carpeta de lectura d2c hello, ejecute hello después toobegin comando primera partición de hello en el centro de IoT de supervisión:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Mensajes de dispositivo a la nube de toomonitor de aplicación de servicio de centro de IoT de Java][7]

2. En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después toobegin comando Enviar centro de IoT de tooyour de datos de telemetría:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Mensajes de dispositivo a la nube de toosend de aplicación de dispositivo de centro de IoT de Java][8]

3. Hola **uso** el icono Servicios hello [portal de Azure] [ lnk-portal] muestra Hola número de mensajes enviados toohello centro de IoT:

    ![Azure portal uso icono que muestra el número de mensajes enviados tooIoT concentrador][43]

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Usar este dispositivo identidad tooenable Hola dispositivo aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT. También crea una aplicación que muestra los mensajes de saludo recibidos por centro de IoT Hola.

toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:

* [Conexión del dispositivo][lnk-connect-device]
* [Introducción a la administración de dispositivos][lnk-device-management]
* [Introducción a Azure IoT Edge][lnk-iot-edge]

toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
