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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="176ca-104">Programación y difusión de trabajos (Java)</span><span class="sxs-lookup"><span data-stu-id="176ca-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="176ca-105">Utilice los trabajos de tooschedule y realizar un seguimiento de centro de IoT de Azure que actualizan millones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="176ca-106">Use los trabajos para:</span><span class="sxs-lookup"><span data-stu-id="176ca-106">Use jobs to:</span></span>

* <span data-ttu-id="176ca-107">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="176ca-107">Update desired properties</span></span>
* <span data-ttu-id="176ca-108">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="176ca-108">Update tags</span></span>
* <span data-ttu-id="176ca-109">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="176ca-109">Invoke direct methods</span></span>

<span data-ttu-id="176ca-110">Un trabajo encapsula una de estas acciones y realiza un seguimiento Hola ejecución con un conjunto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="176ca-111">Una consulta de gemelas de dispositivo define conjunto de Hola de trabajo Hola se ejecuta en los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="176ca-112">Por ejemplo, una aplicación de back-end puede usar un tooinvoke de trabajo un método directo en 10.000 dispositivos que reinicia dispositivos Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="176ca-113">Especifique el conjunto de Hola de dispositivos con una consulta de gemelas de dispositivo y programar toorun de trabajo de hello en el futuro.</span><span class="sxs-lookup"><span data-stu-id="176ca-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="176ca-114">progreso de realiza un seguimiento del trabajo de Hello como cada uno de los dispositivos de Hola recibir y ejecutar el método directo de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="176ca-115">toolearn más información acerca de cada una de estas funciones, vea:</span><span class="sxs-lookup"><span data-stu-id="176ca-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="176ca-116">Dispositivo gemelo y propiedades: [Introducción a los dispositivos gemelos ](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="176ca-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="176ca-117">Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos](iot-hub-devguide-direct-methods.md) y [Tutorial: Uso de métodos directos](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="176ca-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="176ca-118">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="176ca-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="176ca-119">Creación de una aplicación de dispositivo que implemente un método directo denominado **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="176ca-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="176ca-120">aplicación de dispositivo de Hello también recibe cambios de la propiedad deseada desde aplicaciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="176ca-121">Crear una aplicación de back-end que crea un Hola de trabajo toocall **lockDoor** método directo en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="176ca-122">Otro trabajo envía la propiedad deseada actualiza toomultiple dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="176ca-123">Al final de Hola de este tutorial, tendrá una aplicación de dispositivo de consola de java y una aplicación de back-end de la consola de java:</span><span class="sxs-lookup"><span data-stu-id="176ca-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="176ca-124">**dispositivo simulado** que se conecta el centro de IoT tooyour, implementa hello **lockDoor** dirigir deseado de método y controla los cambios de propiedad.</span><span class="sxs-lookup"><span data-stu-id="176ca-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="176ca-125">**programar trabajos** que usan Hola de trabajos toocall **lockDoor** directo gemelas del dispositivo de hello método y actualizar las propiedades en varios dispositivos adecuadas.</span><span class="sxs-lookup"><span data-stu-id="176ca-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="176ca-126">artículo de Hello [SDK de Azure IoT](iot-hub-devguide-sdks.md) proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="176ca-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="176ca-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="176ca-127">Prerequisites</span></span>

<span data-ttu-id="176ca-128">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="176ca-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="176ca-129">Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="176ca-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="176ca-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="176ca-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="176ca-131">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="176ca-131">An active Azure account.</span></span> <span data-ttu-id="176ca-132">(En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="176ca-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="176ca-133">Si prefiere identidad del dispositivo toocreate hello mediante programación, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo usa Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artículo.</span><span class="sxs-lookup"><span data-stu-id="176ca-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="176ca-134">También puede usar hello [el centro de IOT explorador](https://github.com/Azure/iothub-explorer) herramienta tooadd un centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="176ca-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="176ca-135">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="176ca-135">Create hello service app</span></span>

<span data-ttu-id="176ca-136">En esta sección, creará una aplicación de consola de Java que usa trabajos para:</span><span class="sxs-lookup"><span data-stu-id="176ca-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="176ca-137">Llamar a hello **lockDoor** método directo en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="176ca-138">Enviar propiedades deseadas toomultiple dispositivos.</span><span class="sxs-lookup"><span data-stu-id="176ca-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="176ca-139">aplicación de hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="176ca-139">toocreate hello app:</span></span>

1. <span data-ttu-id="176ca-140">En el equipo de desarrollo, cree una carpeta vacía denominada `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="176ca-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="176ca-141">Hola `iot-java-schedule-jobs` carpeta, cree un proyecto de Maven denominado **programar trabajos** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="176ca-142">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="176ca-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="176ca-143">En el símbolo del sistema, desplácese toohello `schedule-jobs` carpeta.</span><span class="sxs-lookup"><span data-stu-id="176ca-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="176ca-144">Con un editor de texto, abra hello `pom.xml` archivo Hola `schedule-jobs` carpeta y agregue Hola después dependencia toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="176ca-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="176ca-145">Esta dependencia permite hello toouse **cliente del servicio de iot** paquete en su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="176ca-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="176ca-146">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="176ca-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="176ca-147">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="176ca-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="176ca-148">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="176ca-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="176ca-149">Guarde y cierre hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="176ca-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="176ca-150">Con un editor de texto, abra hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="176ca-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="176ca-151">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="176ca-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="176ca-152">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="176ca-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="176ca-153">Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:</span><span class="sxs-lookup"><span data-stu-id="176ca-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="176ca-154">Agregar Hola siguiendo el método toohello **aplicación** clase tooschedule un hello tooupdate de trabajo **Building** y **Floor** deseado propiedades en gemelas de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="176ca-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="176ca-155">tooschedule un Hola de toocall trabajo **lockDoor** método, agregue Hola siguiendo el método toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="176ca-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="176ca-156">toomonitor un trabajo, agregar Hola siguiendo el método toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="176ca-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="176ca-157">tooquery para obtener detalles de Hola de trabajos de hello ejecutó, agregue Hola siguiente método:</span><span class="sxs-lookup"><span data-stu-id="176ca-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="176ca-158">Hola de actualización **principal** siguiente de Hola de tooinclude de firma de método `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="176ca-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="176ca-159">toorun y monitor de dos trabajos de forma secuencial, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="176ca-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="176ca-160">Guarde y cierre hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` archivo</span><span class="sxs-lookup"><span data-stu-id="176ca-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="176ca-161">Compilar hello **programar trabajos** aplicación y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="176ca-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="176ca-162">En el símbolo del sistema, desplácese toohello `schedule-jobs` carpeta y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="176ca-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="176ca-163">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="176ca-163">Create a device app</span></span>

<span data-ttu-id="176ca-164">En esta sección, creará una aplicación de consola de Java identificadores Hola propiedades deseadas enviadas desde el centro de IoT e implementa llamada de método directo Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="176ca-165">Hola `iot-java-schedule-jobs` carpeta, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="176ca-166">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="176ca-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="176ca-167">En el símbolo del sistema, desplácese toohello `simulated-device` carpeta.</span><span class="sxs-lookup"><span data-stu-id="176ca-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="176ca-168">Con un editor de texto, abra hello `pom.xml` archivo Hola `simulated-device` carpeta y agregue Hola siguiendo las dependencias toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="176ca-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="176ca-169">Esta dependencia permite hello toouse **cliente de dispositivo iot** paquete en su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="176ca-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="176ca-170">Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="176ca-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="176ca-171">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="176ca-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="176ca-172">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="176ca-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="176ca-173">Guarde y cierre hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="176ca-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="176ca-174">Con un editor de texto, abra hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="176ca-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="176ca-175">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="176ca-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="176ca-176">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="176ca-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="176ca-177">Reemplazar `{youriothubname}` por el nombre del centro de IoT, y `{yourdevicekey}` con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="176ca-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="176ca-178">Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="176ca-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="176ca-179">Actualmente, toouse gemelas características de dispositivos debe utilizar hello MQTT protocolo.</span><span class="sxs-lookup"><span data-stu-id="176ca-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="176ca-180">tooprint dispositivo gemelas notificaciones toohello consola, agregue el siguiente Hola anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="176ca-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="176ca-181">tooprint dirigir toohello de notificaciones de método de la consola, agregue el siguiente Hola anidado toohello de clase **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="176ca-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="176ca-182">llamadas a métodos directas toohandle centro de IoT, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="176ca-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="176ca-183">Hola de actualización **principal** siguiente de Hola de tooinclude de firma de método `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="176ca-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="176ca-184">Agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="176ca-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="176ca-185">Crear un toocommunicate de cliente de dispositivo con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="176ca-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="176ca-186">Crear un **dispositivo** toostore Hola dispositivo gemelas propiedades del objeto.</span><span class="sxs-lookup"><span data-stu-id="176ca-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="176ca-187">Servicios de cliente de dispositivo de hello toostart, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="176ca-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="176ca-188">toowait para hello de hello usuario toopress **ENTRAR** clave antes de apagar, agregue Hola siguiente código toohello final del programa Hola a **principal** método:</span><span class="sxs-lookup"><span data-stu-id="176ca-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="176ca-189">Guarde y cierre hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="176ca-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="176ca-190">Compilar hello **dispositivo simulado** aplicación y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="176ca-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="176ca-191">En el símbolo del sistema, desplácese toohello `simulated-device` carpeta y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="176ca-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="176ca-192">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="176ca-192">Run hello apps</span></span>

<span data-ttu-id="176ca-193">Ya estás listo toorun hello las aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="176ca-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="176ca-194">En un símbolo del sistema en hello `simulated-device` carpeta, ejecute hello después de la aplicación de dispositivo de comando toostart hello realizando escuchas para los cambios de la propiedad deseada y llamadas a métodos directas:</span><span class="sxs-lookup"><span data-stu-id="176ca-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![inicia el cliente de dispositivo de Hola](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="176ca-196">En un símbolo del sistema en hello `schedule-jobs` carpeta, ejecute hello después comando toorun hello **programar trabajos** toorun dos trabajos de aplicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="176ca-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="176ca-197">Hola primero establece valores de propiedad de hello deseado, llamadas segundo Hola Hola método directo:</span><span class="sxs-lookup"><span data-stu-id="176ca-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![La aplicación de IoT Hub de Java crea dos trabajos](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="176ca-199">aplicación de dispositivo de Hello controla Hola deseado de cambio de propiedad y llame al método de hello método directo:</span><span class="sxs-lookup"><span data-stu-id="176ca-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![cliente de dispositivo de Hello responde toohello cambios](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="176ca-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="176ca-201">Next steps</span></span>

<span data-ttu-id="176ca-202">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="176ca-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="176ca-203">Crea una aplicación de back-end toorun dos trabajos.</span><span class="sxs-lookup"><span data-stu-id="176ca-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="176ca-204">primer trabajo de Hello establece valores de propiedad deseados y trabajo de segundo Hola llamado a un método directo.</span><span class="sxs-lookup"><span data-stu-id="176ca-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="176ca-205">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="176ca-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="176ca-206">Enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="176ca-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="176ca-207">Controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario) con hello [usar métodos directos](iot-hub-java-java-direct-methods.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="176ca-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
