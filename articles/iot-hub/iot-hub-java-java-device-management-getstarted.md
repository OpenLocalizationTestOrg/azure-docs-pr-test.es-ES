---
title: "aaaGet comenzar con la administración de dispositivos del centro de IoT de Azure (Java) | Documentos de Microsoft"
description: "¿Cómo tooinitiate de administración de dispositivos de centro de IoT de Azure toouse reiniciar un dispositivo remoto. Usar dispositivos de IoT de Azure de hello SDK para Java tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para Java tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a>Introducción a la administración de dispositivos (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

En este tutorial se muestra cómo realizar las siguientes acciones:

* Usar hello toocreate portal Azure un centro de IoT y cree una identidad de dispositivo en el centro de IoT.
* Crear una aplicación de dispositivo simulado que implementa un dispositivo de hello tooreboot método directo. Se invocan métodos directos de nube de Hola.
* Crear una aplicación que invoca el método directo de reinicio de hello en la aplicación de dispositivo simulado de hello a través de su centro de IoT. Esta aplicación, a continuación, monitores Hola propiedades notificados de hello dispositivo toosee cuando se completa la operación de reinicio de Hola.

Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Java:

**simulated-device**. Esta aplicación:

* Se conecta a centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente.
* Recibe una llamada de método directo de reinicio.
* Simula un reinicio físico.
* Informa del tiempo Hola de último reinicio de Hola a través de una propiedad notificada.

**trigger-reboot**. Esta aplicación:

* Llama a un método directo en la aplicación de dispositivo simulado de hello.
* Muestra de Hola respuesta toohello directa llamada al método enviado por dispositivo simulado Hola
* Hello muestra actualizado informó de propiedades.

> [!NOTE]
> Para obtener información acerca de hello SDK que puede usar toobuild toorun de aplicaciones en dispositivos y el back-end de soluciones, consulte [SDK de Azure IoT][lnk-hub-sdks].

toocomplete este tutorial, necesita:

* Java SE 8. <br/> [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Java para este tutorial en Windows o Linux.
* Maven 3.  <br/> [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall [Maven] [ lnk-maven] para este tutorial en Windows o Linux.
* [Versión de Node.js 0.10.0 o posterior](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Desencadenar un reinicio remoto en dispositivo Hola utilizando un método directo

En esta sección, creará una aplicación de consola de Java que permite:

1. Método directo de reinicio de hello en la aplicación de dispositivo simulado de hello, se invoca.
1. Muestra la respuesta de Hola.
1. Hola sondeos notificado propiedades enviadas desde Hola dispositivo toodetermine cuando se completa el reinicio de Hola.

Esta aplicación de consola conecta tooyour centro de IoT método directo de tooinvoke Hola y Hola lectura notificada propiedades.

1. Cree una carpeta vacía llamada dm-get-started.

1. En carpeta dm get iniciada hello, cree un proyecto de Maven denominado **desencadenador reinicio** mediante el siguiente comando en el símbolo del sistema de Hola. siguiente Hello muestra un comando único, long:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplazarse por las carpetas de reinicio de desencadenador de toohello.

1. Con un editor de texto, abra el archivo de pom.xml de hello en carpeta de reinicio de desencadenador de Hola y agregue Hola después toohello de dependencia **dependencias** nodo. Esta dependencia permite toouse Hola iot-service-paquete de cliente de su toocommunicate de aplicación con el centro de IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven][lnk-maven-service-search].

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

1. Guarde y cierre el archivo de hello pom.xml.

1. Con un editor de texto, abra el archivo de código fuente de hello trigger-reboot\src\main\java\com\mycompany\app\App.java.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. tooimplement un subproceso que lee Hola notificado propiedades desde gemelas de dispositivo de hello cada 10 segundos, agregue siguientes de Hola anidados clase toohello **aplicación** clase:

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. método directo reinicio de tooinvoke hello en dispositivo simulado de hello, agregar Hola después código toohello **principal** método:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. toostart Hola subproceso toopoll Hola notificados propiedades de dispositivo simulado de hello, agregue Hola después código toohello **principal** método:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable toostop Hola aplicación, agregar Hola después código toohello **principal** método:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Guarde y cierre el archivo de hello trigger-reboot\src\main\java\com\mycompany\app\App.java.

1. Compilar hello **desencadenador reinicio** aplicaciones back-end y corrija los errores. En el símbolo del sistema, desplácese toohello desencadenador reinicio carpeta y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado

En esta sección, creará una aplicación de consola de Java que simula un dispositivo. aplicación Hello escucha Hola reinicio método directo llamada desde el centro de IoT y responde inmediatamente llamada toothat. Hola de aplicación, a continuación, espera unos instantes proceso de reinicio de hello toosimulate antes de usar un Hola de toonotify propiedad notificado **desencadenador reinicio** aplicación back-end que Hola reinicio está completa.

1. En carpeta dm get iniciada hello, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola. Hola te mostramos un comando único, long:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplazarse por las carpetas de toohello dispositivo simulado.

1. Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta del dispositivo simulado de Hola y agregue Hola después toohello de dependencia **dependencias** nodo. Esta dependencia permite toouse Hola iot-service-paquete de cliente de su toocommunicate de aplicación con el centro de IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven][lnk-maven-device-search].

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

1. Guarde y cierre el archivo de hello pom.xml.

1. Con un editor de texto, abra el archivo de código fuente de hello simulated-device\src\main\java\com\mycompany\app\App.java.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplace `{yourdeviceconnectionstring}` con cadena de conexión de dispositivo de Hola que anotó en hello *crear una identidad de dispositivo* sección:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement un controlador de devolución de llamada para los eventos de estado de método directo, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement un controlador de devolución de llamada para los eventos de estado de dispositivo gemelas, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement un controlador de devolución de llamada para los eventos de propiedad, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. tooimplement un subproceso toosimulate Hola el reinicio del dispositivo, agregue el siguiente de hello anidados clase toohello **aplicación** clase. subproceso de Hola se suspende durante cinco segundos y, a continuación, Establece hello **lastReboot** informó de propiedad:

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. método directo de tooimplement hello en dispositivo hello, agregue el siguiente de hello anidados clase toohello **aplicación** clase. Cuando la aplicación simulada de hello recibe una llamada toohello **reiniciar** método directo, devuelve un autor de llamada de confirmación toohello y, a continuación, inicia un Hola de subproceso tooprocess reiniciar:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. Modificar firma Hola de hello **principal** hello toothrow de método siguientes excepciones:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate una **DeviceClient**, agregar Hola después código toohello **principal** método:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart realizar escuchas para las llamadas a métodos directas, agregar Hola después código toohello **principal** método:

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. tooshut hacia abajo el simulador de dispositivos de hello, agregar Hola después código toohello **principal** método:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Guarde y cierre el archivo de hello simulated-device\src\main\java\com\mycompany\app\App.java.

1. Compilar hello **dispositivo simulado** aplicaciones back-end y corrija los errores. En el símbolo del sistema, desplácese carpeta del dispositivo simulado toohello y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun Hola aplicaciones.

1. En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después de realizar escuchas para las llamadas de método de reinicio desde el centro de IoT de toobegin de comando:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centro de IoT de Java simulados toolisten de aplicación de dispositivo para las llamadas de método directo de reinicio][1]

1. En un símbolo del sistema en carpeta de reinicio de desencadenador de hello, ejecute hello siguiendo el método de reinicio de comando toocall hello en el dispositivo simulado de su centro de IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hola de toocall de aplicación de servicio de centro de IoT de Java reiniciar método directo][2]

1. dispositivo simulado Hola responde toohello reinicio método directo llamada:

    ![Aplicación de dispositivo simulado de centro de IoT de Java responde la llamada a un método directo toohello][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22