---
title: "Centro de IoT de Azure aaaUse dirigir métodos (Java) | Documentos de Microsoft"
description: "¿Cómo toouse centro de IoT de Azure dirigir métodos. Usar dispositivos de IoT de Azure de hello SDK para Java tooimplement una aplicación de dispositivo simulado que incluye un método directo y el servicio IoT de Azure SDK para Java tooimplement una aplicación de servicio que invoca el método directo Hola Hola."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a>Uso de métodos directos (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

En este tutorial, creará dos aplicaciones de consola de Java:

* **método Invoke direct**, una aplicación de back-end de Java que llama a un método de aplicación de dispositivo simulado de hello y muestra la respuesta de Hola.
* **dispositivo simulado**, una aplicación Java que simula un dispositivo que se conecta centro de IoT tooyour con la identidad de dispositivo de Hola que cree. Esta aplicación responde toohello invocado directa de back-end de Hola.

> [!NOTE]
> Para obtener información acerca de hello SDK que puede usar toobuild toorun de aplicaciones en dispositivos y el back-end de soluciones, consulte [SDK de Azure IoT][lnk-hub-sdks].

toocomplete este tutorial, necesita:

* Java SE 8. <br/> [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Java para este tutorial en Windows o Linux.
* Maven 3.  <br/> [Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall [Maven] [ lnk-maven] para este tutorial en Windows o Linux.
* [Versión de Node.js 0.10.0 o posterior](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creación de una aplicación de dispositivo simulado

En esta sección, creará una aplicación de consola de Java que responde el método tooa llamado a soluciones de hello volver final.

1. Cree una carpeta vacía llamada iot-java-direct-method.

1. En carpeta de iot java direct método hello, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola. Hola siguiente comando es un comando único, long:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplazarse por las carpetas de toohello dispositivo simulado.

1. Con un editor de texto, abra archivo pom.xml de hello en la carpeta del dispositivo simulado de Hola y agregue Hola siguiendo las dependencias toohello **dependencias** nodo. Esta dependencia permite toouse Hola iot de cliente de dispositivo empaquete en su toocommunicate de aplicación con el centro de IoT:

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

1. Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java de hello.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto. Actualmente, toouse dirigir métodos que se debe usar protocolo MQTT Hola.

1. tooreturn un centro de IoT tooyour del código de estado, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. invocaciones de método directo toohandle Hola de hello solución back-end, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. toocreate una **DeviceClient** y escuchar las invocaciones de método directo, agregue un **principal** método toohello **aplicación** clase:

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Guarde y cierre el archivo de hello simulated-device\src\main\java\com\mycompany\app\App.java

1. Compilar hello **dispositivo simulado** aplicación y corrija los errores. En el símbolo del sistema, desplácese carpeta del dispositivo simulado toohello y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Llamada a un método directo en un dispositivo

En esta sección, creará una aplicación de consola de Java que invoca un método directo y, a continuación, muestra la respuesta de Hola. Esta aplicación de consola conecta tooyour método directo de centro de IoT tooinvoke Hola.

1. En carpeta de iot java direct método hello, cree un proyecto de Maven denominado **método invoke direct** mediante el siguiente comando en el símbolo del sistema de Hola. Hola siguiente comando es un comando único, long:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplazarse por las carpetas de toohello método invoke direct.

1. Con un editor de texto, abra el archivo de pom.xml de hello en carpeta de método de invocación directa de Hola y agregue Hola después toohello de dependencia **dependencias** nodo. Esta dependencia permite toouse Hola iot-service-paquete de cliente de su toocommunicate de aplicación con el centro de IoT:

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

1. Con un editor de texto, abra el archivo invoke-direct-method\src\main\java\com\mycompany\app\App.java de hello.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. método de tooinvoke hello en dispositivo simulado de hello, agregar Hola después código toohello **principal** método:

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. Guarde y cierre el archivo de hello invoke-direct-method\src\main\java\com\mycompany\app\App.java

1. Compilar hello **método invoke direct** aplicación y corrija los errores. En el símbolo del sistema, desplácese toohello carpeta de método de invocación directa y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun hello las aplicaciones de consola.

1. En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después de realizar escuchas para las llamadas de método desde el centro de IoT de toobegin de comando:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centro de IoT de Java simulados toolisten de aplicación de dispositivo para las llamadas a métodos directas][8]

1. En un símbolo del sistema en carpeta de método de invocación directa de hello, ejecute hello después comando toocall un método en el dispositivo simulado desde el centro de IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall de aplicación de servicio de centro de IoT de Java un método directo][7]

1. dispositivo simulado de Hola responde la llamada a un método directo toohello:

    ![Aplicación de dispositivo simulado de centro de IoT de Java responde la llamada a un método directo toohello][9]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola. También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola.

tooexplore otros escenarios de IoT, consulte [programar trabajos en varios dispositivos][lnk-devguide-jobs].

toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
