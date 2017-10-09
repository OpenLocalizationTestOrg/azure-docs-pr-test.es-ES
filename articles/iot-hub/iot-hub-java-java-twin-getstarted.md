---
title: "aaaGet partió gemelos de dispositivo del centro de IoT de Azure (Java) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dispositivo: los gemelos tooadd etiquetas y, a continuación, utilice una consulta de centro de IoT. Usar dispositivos de IoT de Azure de hello SDK para hello servicio IoT de Azure SDK para Java tooimplement una aplicación de servicio que agrega etiquetas de Hola y ejecuta consultas del centro de IoT hello y aplicación de dispositivo de Java tooimplement hello."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Introducción a los dispositivos gemelos (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

En este tutorial, creará dos aplicaciones de consola de Java:

* **add-tags-query**, una aplicación de back-end de Java que agrega etiquetas y consulta dispositivos gemelos.
* **dispositivo simulado**, una aplicación de dispositivo de Java que conecta informes y centro de IoT tooyour su condición de conectividad con una propiedad notificada.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT](iot-hub-devguide-sdks.md) proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.

toocomplete este tutorial, necesita:

* Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Una cuenta de Azure activa. (En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si prefiere identidad del dispositivo toocreate hello mediante programación, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo usa Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artículo.

## <a name="create-hello-service-app"></a>Crear aplicación de servicio de hello

En esta sección, creará una aplicación Java que agrega los metadatos de ubicación como asociada a un doble de dispositivo de toohello de etiqueta en el centro de IoT **myDeviceId**. aplicación Hello consultará primero centro de IoT para dispositivos que se encuentran en hello Estados Unidos y, a continuación, en dispositivos que dependen de una conexión de red de telefonía móvil.

1. En el equipo de desarrollo, cree una carpeta vacía denominada `iot-java-twin-getstarted`.

1. Hola `iot-java-twin-getstarted` carpeta, cree un proyecto de Maven denominado **consulta agregar etiquetas** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplácese toohello `add-tags-query` carpeta.

1. Con un editor de texto, abra hello `pom.xml` archivo Hola `add-tags-query` carpeta y agregue Hola después dependencia toohello **dependencias** nodo. Esta dependencia permite hello toouse **cliente del servicio de iot** paquete en su toocommunicate de aplicación con el centro de IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo. Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Guarde y cierre hello `pom.xml` archivo.

1. Con un editor de texto, abra hello `add-tags-query\src\main\java\com\mycompany\app\App.java` archivo.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Hola de actualización **principal** siguiente de Hola de tooinclude de firma de método `throws` cláusula:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Agregar Hola después código toohello **principal** Hola de método toocreate **DeviceTwin** y **DeviceTwinDevice** objetos. Hola **DeviceTwin** objeto controla la comunicación de hello con el centro de IoT. Hola **DeviceTwinDevice** objeto representa el doble de dispositivo de hello con sus propiedades y etiquetas:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Agregue los siguiente hello `try/catch` bloquear toohello **principal** método:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. Hola tooupdate **región** y **planta** las etiquetas del dispositivo gemelas en el doble de dispositivo, agregar Hola después el código de hello `try` bloque:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. : los gemelos de tooquery Hola dispositivo en el centro de IoT, agregar Hola después código toohello `try` bloque después de código de hello que agregó en el paso anterior de Hola. código de Hello ejecuta dos consultas. Cada consulta devuelve un máximo de 100 dispositivos:

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Guarde y cierre hello `add-tags-query\src\main\java\com\mycompany\app\App.java` archivo

1. Compilar hello **consulta agregar etiquetas** aplicación y corrija los errores. En el símbolo del sistema, desplácese toohello `add-tags-query` carpeta y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Creación de una aplicación de dispositivo

En esta sección, creará una aplicación de consola de Java que establece un valor de propiedad notificado que se envía tooIoT concentrador.

1. Hola `iot-java-twin-getstarted` carpeta, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplácese toohello `simulated-device` carpeta.

1. Con un editor de texto, abra hello `pom.xml` archivo Hola `simulated-device` carpeta y agregue Hola siguiendo las dependencias toohello **dependencias** nodo. Esta dependencia permite hello toouse **cliente de dispositivo iot** paquete en su toocommunicate de aplicación con el centro de IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo. Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. Guarde y cierre hello `pom.xml` archivo.

1. Con un editor de texto, abra hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplazar `{youriothubname}` por el nombre del centro de IoT, y `{yourdevicekey}` con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto. Actualmente, toouse gemelas características de dispositivos debe utilizar hello MQTT protocolo.

1. Agregar Hola después código toohello **principal** método:
    * Crear un toocommunicate de cliente de dispositivo con el centro de IoT.
    * Crear un **dispositivo** toostore Hola dispositivo gemelas propiedades del objeto.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Agregar Hola después código toohello **principal** toocreate método un **connectivityType** notifican propiedad y enviar tooIoT concentrador:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Agregar Hola siguiente código toohello final de hello **principal** método. Esperando hello **ENTRAR** clave permite tiempo para el estado de centro de IoT tooreport Hola de operaciones de hello dispositivo gemelas:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Guarde y cierre hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.

1. Compilar hello **dispositivo simulado** aplicación y corrija los errores. En el símbolo del sistema, desplácese toohello `simulated-device` carpeta y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun hello las aplicaciones de consola.

1. En un símbolo del sistema en hello `add-tags-query` carpeta, ejecute hello después comando toorun hello **consulta agregar etiquetas** del servicio de aplicaciones:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicación de servicio de centro de IoT de Java etiquetar los valores y ejecutar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    Puede ver hello **planta** y **región** etiquetas agregan toohello gemelas de dispositivo. Hola primera consulta devuelve el dispositivo, pero hello en segundo lugar no lo hace.

1. En un símbolo del sistema en hello `simulated-device` carpeta, ejecute hello después comando tooadd hello **connectivityType** notificado gemelas de dispositivos de propiedad toohello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![cliente de dispositivo de Hello agrega Hola ** connectivityType ** notificado propiedad](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. En un símbolo del sistema en hello `add-tags-query` carpeta, ejecute hello después comando toorun hello **consulta agregar etiquetas** una segunda vez del servicio de aplicaciones:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicación de servicio de centro de IoT de Java etiquetar los valores y ejecutar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Ahora el dispositivo ha enviado hello **connectivityType** tooIoT propiedad concentrador, segunda consulta de hello devuelve el dispositivo.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Agrega los metadatos del dispositivo como etiquetas desde una aplicación de back-end y escribió una información de conectividad del dispositivo dispositivo aplicación tooreport en gemelas de dispositivo de Hola. También ha aprendido cómo tooquery Hola información gemelas del dispositivo mediante el lenguaje de consulta de hello centro de IoT similar a SQL.

Hola de uso después cómo toolearn de recursos para:

* Enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) tutorial.
* Controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario) con hello [usar métodos directos](iot-hub-java-java-direct-methods.md) tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
