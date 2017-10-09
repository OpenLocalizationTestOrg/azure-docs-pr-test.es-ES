---
title: trabajos de aaaSchedule con el centro de IoT de Azure (Java) | Documentos de Microsoft
description: "¿Cómo tooschedule un centro de IoT de Azure tooinvoke un método directo del trabajo y establecer una propiedad deseada en varios dispositivos. Usar dispositivos de IoT de Azure de hello SDK para hello servicio IoT de Azure SDK para Java tooimplement un trabajo de servicio aplicación toorun hello y aplicaciones de Java tooimplement Hola simulada dispositivos."
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
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Programación y difusión de trabajos (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Utilice los trabajos de tooschedule y realizar un seguimiento de centro de IoT de Azure que actualizan millones de dispositivos. Use los trabajos para:

* Actualizar las propiedades deseadas
* Actualizar etiquetas
* Invocar métodos directos

Un trabajo encapsula una de estas acciones y realiza un seguimiento Hola ejecución con un conjunto de dispositivos. Una consulta de gemelas de dispositivo define conjunto de Hola de trabajo Hola se ejecuta en los dispositivos. Por ejemplo, una aplicación de back-end puede usar un tooinvoke de trabajo un método directo en 10.000 dispositivos que reinicia dispositivos Hola. Especifique el conjunto de Hola de dispositivos con una consulta de gemelas de dispositivo y programar toorun de trabajo de hello en el futuro. progreso de realiza un seguimiento del trabajo de Hello como cada uno de los dispositivos de Hola recibir y ejecutar el método directo de reinicio de Hola.

toolearn más información acerca de cada una de estas funciones, vea:

* Dispositivo gemelo y propiedades: [Introducción a los dispositivos gemelos ](iot-hub-java-java-twin-getstarted.md)
* Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos](iot-hub-devguide-direct-methods.md) y [Tutorial: Uso de métodos directos](iot-hub-java-java-direct-methods.md)

En este tutorial se muestra cómo realizar las siguientes acciones:

* Creación de una aplicación de dispositivo que implemente un método directo denominado **lockDoor**. aplicación de dispositivo de Hello también recibe cambios de la propiedad deseada desde aplicaciones de back-end de Hola.
* Crear una aplicación de back-end que crea un Hola de trabajo toocall **lockDoor** método directo en varios dispositivos. Otro trabajo envía la propiedad deseada actualiza toomultiple dispositivos.

Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de java y una aplicación de back-end de la consola de java:

**dispositivo simulado** que se conecta el centro de IoT tooyour, implementa hello **lockDoor** dirigir deseado de método y controla los cambios de propiedad.

**programar trabajos** que usan Hola de trabajos toocall **lockDoor** directo gemelas del dispositivo de hello método y actualizar las propiedades en varios dispositivos adecuadas.

> [!NOTE]
> artículo de Hello [SDK de Azure IoT](iot-hub-devguide-sdks.md) proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesita:

* Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Una cuenta de Azure activa. (En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Si prefiere identidad del dispositivo toocreate hello mediante programación, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo usa Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artículo. También puede usar hello [el centro de IOT explorador](https://github.com/Azure/iothub-explorer) herramienta tooadd un centro de IoT tooyour de dispositivo.

## <a name="create-hello-service-app"></a>Crear aplicación de servicio de hello

En esta sección, creará una aplicación de consola de Java que usa trabajos para:

* Llamar a hello **lockDoor** método directo en varios dispositivos.
* Enviar propiedades deseadas toomultiple dispositivos.

aplicación de hello toocreate:

1. En el equipo de desarrollo, cree una carpeta vacía denominada `iot-java-schedule-jobs`.

1. Hola `iot-java-schedule-jobs` carpeta, cree un proyecto de Maven denominado **programar trabajos** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. En el símbolo del sistema, desplácese toohello `schedule-jobs` carpeta.

1. Con un editor de texto, abra hello `pom.xml` archivo Hola `schedule-jobs` carpeta y agregue Hola después dependencia toohello **dependencias** nodo. Esta dependencia permite hello toouse **cliente del servicio de iot** paquete en su toocommunicate de aplicación con el centro de IoT:

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

1. Con un editor de texto, abra hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` archivo.

1. Agregue los siguiente hello **importar** archivo toohello de instrucciones:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase. Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Agregar Hola siguiendo el método toohello **aplicación** clase tooschedule un hello tooupdate de trabajo **Building** y **Floor** deseado propiedades en gemelas de dispositivo de hello:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule un Hola de toocall trabajo **lockDoor** método, agregue Hola siguiendo el método toohello **aplicación** clase:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor un trabajo, agregar Hola siguiendo el método toohello **aplicación** clase:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery para obtener detalles de Hola de trabajos de hello ejecutó, agregue Hola siguiente método:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Hola de actualización **principal** siguiente de Hola de tooinclude de firma de método `throws` cláusula:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun y monitor de dos trabajos de forma secuencial, agregar Hola después código toohello **principal** método:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Guarde y cierre hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` archivo

1. Compilar hello **programar trabajos** aplicación y corrija los errores. En el símbolo del sistema, desplácese toohello `schedule-jobs` carpeta y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Creación de una aplicación de dispositivo

En esta sección, creará una aplicación de consola de Java identificadores Hola propiedades deseadas enviadas desde el centro de IoT e implementa llamada de método directo Hola.

1. Hola `iot-java-schedule-jobs` carpeta, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola. Observe que este es un comando único y largo:

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto. Actualmente, toouse gemelas características de dispositivos debe utilizar hello MQTT protocolo.

1. tooprint dispositivo gemelas notificaciones toohello consola, agregue el siguiente Hola anidados clase toohello **aplicación** clase:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint dirigir toohello de notificaciones de método de la consola, agregue el siguiente Hola anidado toohello de clase **aplicación** clase:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. llamadas a métodos directas toohandle centro de IoT, agregue el siguiente de hello anidados clase toohello **aplicación** clase:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Hola de actualización **principal** siguiente de Hola de tooinclude de firma de método `throws` cláusula:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Agregar Hola después código toohello **principal** método:
    * Crear un toocommunicate de cliente de dispositivo con el centro de IoT.
    * Crear un **dispositivo** toostore Hola dispositivo gemelas propiedades del objeto.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. Servicios de cliente de dispositivo de hello toostart, agregar Hola después código toohello **principal** método:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait para hello de hello usuario toopress **ENTRAR** clave antes de apagar, agregue Hola siguiente código toohello final del programa Hola a **principal** método:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Guarde y cierre hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.

1. Compilar hello **dispositivo simulado** aplicación y corrija los errores. En el símbolo del sistema, desplácese toohello `simulated-device` carpeta y ejecución Hola siguiente comando:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Ejecutar aplicaciones de Hola

Ya estás listo toorun hello las aplicaciones de consola.

1. En un símbolo del sistema en hello `simulated-device` carpeta, ejecute hello después de la aplicación de dispositivo de comando toostart hello realizando escuchas para los cambios de la propiedad deseada y llamadas a métodos directas:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![inicia el cliente de dispositivo de Hola](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. En un símbolo del sistema en hello `schedule-jobs` carpeta, ejecute hello después comando toorun hello **programar trabajos** toorun dos trabajos de aplicación de servicio. Hola primero establece valores de propiedad de hello deseado, llamadas segundo Hola Hola método directo:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![La aplicación de IoT Hub de Java crea dos trabajos](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. aplicación de dispositivo de Hello controla Hola deseado de cambio de propiedad y llame al método de hello método directo:

    ![cliente de dispositivo de Hello responde toohello cambios](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola. Crea una aplicación de back-end toorun dos trabajos. primer trabajo de Hello establece valores de propiedad deseados y trabajo de segundo Hola llamado a un método directo.

Hola de uso después cómo toolearn de recursos para:

* Enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) tutorial.
* Controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario) con hello [usar métodos directos](iot-hub-java-java-direct-methods.md) tutorial.
