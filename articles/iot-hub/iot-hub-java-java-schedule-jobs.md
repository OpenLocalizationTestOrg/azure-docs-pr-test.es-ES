---
title: "Programación de trabajos con Azure IoT Hub (Java) | Microsoft Docs"
description: "Cómo programar un trabajo de Azure IoT Hub para invocar un método directo y definir una propiedad deseada en varios dispositivos. Usará el SDK de dispositivo IoT de Azure para Java con el fin de implementar las aplicaciones de dispositivo simulado, además del SDK de servicio IoT de Azure para Java con el objetivo de implementar una aplicación de servicio para ejecutar el trabajo."
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
ms.openlocfilehash: 003a548ef2da2921a699df1aa9f7aee366d341ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="b26d0-104">Programación y difusión de trabajos (Java)</span><span class="sxs-lookup"><span data-stu-id="b26d0-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="b26d0-105">Use Azure IoT Hub para programar y realizar el seguimiento de los trabajos que actualizan millones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="b26d0-106">Use los trabajos para:</span><span class="sxs-lookup"><span data-stu-id="b26d0-106">Use jobs to:</span></span>

* <span data-ttu-id="b26d0-107">Actualizar las propiedades deseadas</span><span class="sxs-lookup"><span data-stu-id="b26d0-107">Update desired properties</span></span>
* <span data-ttu-id="b26d0-108">Actualizar etiquetas</span><span class="sxs-lookup"><span data-stu-id="b26d0-108">Update tags</span></span>
* <span data-ttu-id="b26d0-109">Invocar métodos directos</span><span class="sxs-lookup"><span data-stu-id="b26d0-109">Invoke direct methods</span></span>

<span data-ttu-id="b26d0-110">Un trabajo encapsula una de estas acciones y realiza el seguimiento de la ejecución en un conjunto de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="b26d0-111">Una consulta de dispositivo gemelo define el conjunto de dispositivos en que se ejecuta el trabajo.</span><span class="sxs-lookup"><span data-stu-id="b26d0-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="b26d0-112">Por ejemplo, una aplicación de back-end puede utilizar un trabajo para invocar un método directo en 10 000 dispositivos que reinicie los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="b26d0-113">Especifique el conjunto de dispositivos con una consulta de dispositivo gemelo y programe el trabajo para que se ejecute en otro momento.</span><span class="sxs-lookup"><span data-stu-id="b26d0-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="b26d0-114">Este trabajo realiza el seguimiento del progreso mientras los dispositivos reciben y ejecutan el método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="b26d0-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="b26d0-115">Para más información sobre estas funcionalidades, vea:</span><span class="sxs-lookup"><span data-stu-id="b26d0-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="b26d0-116">Dispositivo gemelo y propiedades: [Introducción a los dispositivos gemelos ](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="b26d0-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="b26d0-117">Métodos directos: [Guía del desarrollador de IoT Hub: métodos directos](iot-hub-devguide-direct-methods.md) y [Tutorial: Uso de métodos directos](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="b26d0-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="b26d0-118">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="b26d0-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="b26d0-119">Creación de una aplicación de dispositivo que implemente un método directo denominado **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="b26d0-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="b26d0-120">La aplicación de dispositivo también recibe cambios en la propiedad deseada de la aplicación de back-end.</span><span class="sxs-lookup"><span data-stu-id="b26d0-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="b26d0-121">Creación de una aplicación de back-end que cree un trabajo para llamar al método directo **lockDoor** en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="b26d0-122">Otro trabajo envía las actualizaciones en la propiedad deseada a varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="b26d0-123">Al final de este tutorial, tendrá una aplicación de dispositivo de consola de Java y una aplicación de back-end de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="b26d0-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="b26d0-124">**simulated-device**, que se conecta a la instancia de IoT Hub, implementa el método directo **lockDoor** y controla los cambios en la propiedad deseada.</span><span class="sxs-lookup"><span data-stu-id="b26d0-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="b26d0-125">**schedule-jobs**, que usa trabajos para llamar al método directo **lockDoor** y actualizar las propiedades del dispositivo gemelo deseadas en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="b26d0-126">En el artículo [SDK de IoT de Azure](iot-hub-devguide-sdks.md) se proporciona información sobre los SDK de IoT de Azure que se pueden usar para crear aplicaciones de dispositivo y de back-end.</span><span class="sxs-lookup"><span data-stu-id="b26d0-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b26d0-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b26d0-127">Prerequisites</span></span>

<span data-ttu-id="b26d0-128">Para completar este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="b26d0-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="b26d0-129">La versión más reciente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="b26d0-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="b26d0-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="b26d0-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="b26d0-131">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b26d0-131">An active Azure account.</span></span> <span data-ttu-id="b26d0-132">(En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="b26d0-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="b26d0-133">Si prefiere crear la identidad del dispositivo mediante programación, lea la sección correspondiente en el artículo [Conexión del dispositivo en IoT Hub con Java](iot-hub-java-java-getstarted.md#create-a-device-identity).</span><span class="sxs-lookup"><span data-stu-id="b26d0-133">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="b26d0-134">También puede usar la herramienta [iothub-explorer](https://github.com/Azure/iothub-explorer) para agregar un dispositivo a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b26d0-134">You can also use the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="b26d0-135">Creación de la aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="b26d0-135">Create the service app</span></span>

<span data-ttu-id="b26d0-136">En esta sección, creará una aplicación de consola de Java que usa trabajos para:</span><span class="sxs-lookup"><span data-stu-id="b26d0-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="b26d0-137">Llamar al método directo **lockDoor** en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-137">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="b26d0-138">Usar las propiedades deseadas en varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-138">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="b26d0-139">Para crear la aplicación:</span><span class="sxs-lookup"><span data-stu-id="b26d0-139">To create the app:</span></span>

1. <span data-ttu-id="b26d0-140">En el equipo de desarrollo, cree una carpeta vacía denominada `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="b26d0-141">En la carpeta `iot-java-schedule-jobs`, cree un proyecto de Maven denominado **schedule-jobs** mediante el siguiente comando en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b26d0-141">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="b26d0-142">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="b26d0-143">En el símbolo del sistema, vaya a la carpeta `schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-143">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="b26d0-144">Con un editor de texto, abra el archivo `pom.xml` en la carpeta `schedule-jobs` y agregue la dependencia siguiente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="b26d0-144">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="b26d0-145">Esta dependencia permite usar el paquete **iot-service-client** en la aplicación para comunicarse con la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="b26d0-145">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b26d0-146">Puede comprobar la versión más reciente de **iot-service-client** mediante la [búsqueda de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="b26d0-146">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="b26d0-147">Agregue el nodo **build** después del nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="b26d0-147">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="b26d0-148">Esta configuración indica a Maven que use Java 1.8 para compilar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="b26d0-148">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="b26d0-149">Guarde y cierre el archivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="b26d0-150">Con un editor de texto, abra el archivo `schedule-jobs\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-150">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="b26d0-151">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-151">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="b26d0-152">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="b26d0-152">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="b26d0-153">Reemplace `{youriothubconnectionstring}` por la cadena de conexión de IoT Hub que anotó en la sección *Creación de una instancia de IoT Hub*:</span><span class="sxs-lookup"><span data-stu-id="b26d0-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="b26d0-154">Agregue el método siguiente a la clase **App** para programar un trabajo de actualización de las propiedades **Building** y **Floor** deseadas en el dispositivo gemelo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-154">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
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

1. <span data-ttu-id="b26d0-155">Para programar un trabajo de llamada al método **lockDoor**, agregue el método siguiente a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-155">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
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

1. <span data-ttu-id="b26d0-156">Para supervisar un trabajo, agregue el siguiente método a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-156">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
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

1. <span data-ttu-id="b26d0-157">Para consultar los detalles de los trabajos ejecutados, agregue el método siguiente:</span><span class="sxs-lookup"><span data-stu-id="b26d0-157">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="b26d0-158">Actualice la firma del método **main** para incluir la cláusula `throws` siguiente:</span><span class="sxs-lookup"><span data-stu-id="b26d0-158">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="b26d0-159">Para ejecutar y supervisar dos trabajos de forma secuencial, agregue el código siguiente al método **main**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-159">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
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

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="b26d0-160">Guarde y cierre el archivo `schedule-jobs\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-160">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="b26d0-161">Compile la aplicación **schedule-jobs** y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="b26d0-161">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="b26d0-162">En el símbolo del sistema, vaya a la carpeta `schedule-jobs` y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b26d0-162">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="b26d0-163">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="b26d0-163">Create a device app</span></span>

<span data-ttu-id="b26d0-164">En esta sección, creará una aplicación de consola de Java que controla las propiedades deseadas enviadas desde IoT Hub e implementa la llamada al método directo.</span><span class="sxs-lookup"><span data-stu-id="b26d0-164">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="b26d0-165">En la carpeta `iot-java-schedule-jobs`, cree un proyecto de Maven denominado **simulated-device** con el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b26d0-165">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="b26d0-166">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="b26d0-167">En el símbolo del sistema, vaya a la carpeta `simulated-device`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-167">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="b26d0-168">Con un editor de texto, abra el archivo `pom.xml` en la carpeta `simulated-device` y agregue las dependencias siguientes al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="b26d0-168">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="b26d0-169">Esta dependencia permite usar el paquete **iot-device-client** en la aplicación para comunicarse con la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="b26d0-169">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b26d0-170">Puede comprobar la versión más reciente de **iot-device-client** mediante la [búsqueda de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="b26d0-170">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="b26d0-171">Agregue el nodo **build** después del nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="b26d0-171">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="b26d0-172">Esta configuración indica a Maven que use Java 1.8 para compilar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="b26d0-172">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="b26d0-173">Guarde y cierre el archivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-173">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="b26d0-174">Con un editor de texto, abra el archivo `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-174">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="b26d0-175">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-175">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="b26d0-176">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="b26d0-176">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="b26d0-177">Reemplace `{youriothubname}` por el nombre de la instancia de IoT Hub y `{yourdevicekey}` por el valor de la clave de dispositivo que generó en la sección *Creación de una identidad de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="b26d0-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="b26d0-178">Esta aplicación de ejemplo usa la variable **protocol** al crear una instancia de un objeto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="b26d0-178">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="b26d0-179">Actualmente, para usar características de dispositivos gemelos, debe usar el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="b26d0-179">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="b26d0-180">Para imprimir las notificaciones de dispositivos gemelos en la consola, agregue la siguiente clase anidada a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-180">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="b26d0-181">Para imprimir las notificaciones de métodos directos en la consola, agregue la siguiente clase anidada a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-181">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="b26d0-182">Para controlar las llamadas a métodos directos desde IoT Hub, agregue la siguiente clase anidada a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-182">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="b26d0-183">Actualice la firma del método **main** para incluir la cláusula `throws` siguiente:</span><span class="sxs-lookup"><span data-stu-id="b26d0-183">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="b26d0-184">Agregue el siguiente código al final del método **main**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-184">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="b26d0-185">Cree un cliente de dispositivo para comunicarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b26d0-185">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="b26d0-186">Cree un objeto **Device** para almacenar las propiedades del dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="b26d0-186">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="b26d0-187">Para iniciar los servicios de cliente de dispositivo, agregue el código siguiente al método **main**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-187">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
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

1. <span data-ttu-id="b26d0-188">Para esperar a que el usuario presione la tecla **ENTRAR** antes de apagarlo, agregue el código siguiente al final del método **main**:</span><span class="sxs-lookup"><span data-stu-id="b26d0-188">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="b26d0-189">Guarde y cierre el archivo `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="b26d0-189">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="b26d0-190">Compile la aplicación **simulated-device** y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="b26d0-190">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="b26d0-191">En el símbolo del sistema, vaya a la carpeta `simulated-device` y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="b26d0-191">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="b26d0-192">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b26d0-192">Run the apps</span></span>

<span data-ttu-id="b26d0-193">Ya está preparado para ejecutar las aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="b26d0-193">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="b26d0-194">En un símbolo del sistema en la carpeta `simulated-device`, ejecute el siguiente comando para iniciar la escucha de cambios en las propiedades deseadas y de llamadas a métodos directos de la aplicación de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-194">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![El cliente de dispositivo se inicia](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="b26d0-196">En un símbolo del sistema en la carpeta `schedule-jobs`, ejecute el siguiente comando para ejecutar la aplicación de servicio **schedule-jobs** a fin de ejecutar dos trabajos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-196">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="b26d0-197">El primero establece los valores de la propiedad deseada, mientras que el segundo llama al método directo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-197">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![La aplicación de IoT Hub de Java crea dos trabajos](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="b26d0-199">La aplicación de dispositivo controla el cambio de la propiedad deseada y la llamada al método directo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-199">The device app handles the desired property change and the direct method call:</span></span>

    ![El cliente de dispositivo responde a los cambios](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="b26d0-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b26d0-201">Next steps</span></span>

<span data-ttu-id="b26d0-202">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b26d0-202">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="b26d0-203">Crea una aplicación de back-end para ejecutar dos trabajos.</span><span class="sxs-lookup"><span data-stu-id="b26d0-203">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="b26d0-204">El primer trabajo establece los valores de la propiedad deseada, y el segundo llama a un método directo.</span><span class="sxs-lookup"><span data-stu-id="b26d0-204">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="b26d0-205">Use los siguientes recursos para obtener información sobre cómo:</span><span class="sxs-lookup"><span data-stu-id="b26d0-205">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="b26d0-206">Enviar telemetría desde dispositivos con el tutorial [Introducción a IoT Hub](iot-hub-java-java-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="b26d0-206">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="b26d0-207">Controlar los dispositivos de forma interactiva (por ejemplo, encender un ventilador desde una aplicación controlada por el usuario), con el tutorial [Uso de métodos directos](iot-hub-java-java-direct-methods.md).</span><span class="sxs-lookup"><span data-stu-id="b26d0-207">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
