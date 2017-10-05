---
title: "Introducción a la administración de dispositivos de Azure IoT Hub (Java) | Microsoft Docs"
description: "Describe cómo usar la administración de dispositivos de IoT Hub de Azure para iniciar un reinicio del dispositivo remoto. Usará el SDK de dispositivo IoT de Azure para Java con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo, además del SDK de servicio IoT de Azure para Java con el objetivo de implementar una aplicación de servicio que invoque el método directo."
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
ms.openlocfilehash: c75635f366f5ced4bf91792d1a905dd6aab8ed79
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="fbad4-104">Introducción a la administración de dispositivos (Java)</span><span class="sxs-lookup"><span data-stu-id="fbad4-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="fbad4-105">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="fbad4-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="fbad4-106">Usar Azure Portal para un IoT Hub y una identidad de dispositivo en este.</span><span class="sxs-lookup"><span data-stu-id="fbad4-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="fbad4-107">Cree una aplicación de dispositivo simulado que implemente un método directo para reiniciar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fbad4-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="fbad4-108">Los métodos directos se invocan desde la nube.</span><span class="sxs-lookup"><span data-stu-id="fbad4-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="fbad4-109">Cree una aplicación que invoque al método directo de reinicio en la aplicación de dispositivo simulado mediante su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fbad4-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="fbad4-110">Luego, esta aplicación supervisa las propiedades notificadas desde el dispositivo para ver cuándo se completa la operación de reinicio.</span><span class="sxs-lookup"><span data-stu-id="fbad4-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="fbad4-111">Al final de este tutorial, tendrá dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="fbad4-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="fbad4-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-112">**simulated-device**.</span></span> <span data-ttu-id="fbad4-113">Esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="fbad4-113">This app:</span></span>

* <span data-ttu-id="fbad4-114">Se conecta con la instancia de IoT Hub con la identidad de dispositivo que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fbad4-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="fbad4-115">Recibe una llamada de método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="fbad4-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="fbad4-116">Simula un reinicio físico.</span><span class="sxs-lookup"><span data-stu-id="fbad4-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="fbad4-117">Informa la hora de último reinicio a través de una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="fbad4-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="fbad4-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-118">**trigger-reboot**.</span></span> <span data-ttu-id="fbad4-119">Esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="fbad4-119">This app:</span></span>

* <span data-ttu-id="fbad4-120">Llama a un método directo en la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="fbad4-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="fbad4-121">Muestra la respuesta a la llamada al método directo que envía el dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="fbad4-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="fbad4-122">Muestra las propiedades notificadas actualizadas.</span><span class="sxs-lookup"><span data-stu-id="fbad4-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="fbad4-123">Para más información acerca de los diversos SDK que puede usar para crear aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución, consulte [SDK de IoT de Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="fbad4-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="fbad4-124">Para completar este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="fbad4-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="fbad4-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="fbad4-125">Java SE 8.</span></span> <br/> <span data-ttu-id="fbad4-126">[Prepare your development environment][lnk-dev-setup] (Preparación del entorno de desarrollo) describe cómo instalar Java para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="fbad4-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="fbad4-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="fbad4-127">Maven 3.</span></span>  <br/> <span data-ttu-id="fbad4-128">[Prepare your development environment][lnk-dev-setup] (Preparación del entorno de desarrollo) describe cómo instalar [Maven][lnk-maven] para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="fbad4-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="fbad4-129">[Versión de Node.js 0.10.0 o posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="fbad4-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="fbad4-130">Desencadenar un reinicio remoto en el dispositivo con un método directo</span><span class="sxs-lookup"><span data-stu-id="fbad4-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="fbad4-131">En esta sección, creará una aplicación de consola de Java que permite:</span><span class="sxs-lookup"><span data-stu-id="fbad4-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="fbad4-132">Invocar un método directo de reinicio en la aplicación de dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="fbad4-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="fbad4-133">Mostrar la respuesta.</span><span class="sxs-lookup"><span data-stu-id="fbad4-133">Displays the response.</span></span>
1. <span data-ttu-id="fbad4-134">Sondear las propiedades notificadas enviadas desde el dispositivo para determinar cuándo se completa el reinicio.</span><span class="sxs-lookup"><span data-stu-id="fbad4-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="fbad4-135">Esta aplicación de consola se conecta a la instancia de IoT Hub para invocar al método directo y leer las propiedades notificadas.</span><span class="sxs-lookup"><span data-stu-id="fbad4-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="fbad4-136">Cree una carpeta vacía llamada dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="fbad4-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="fbad4-137">En la carpeta dm-get-started, cree un proyecto de Maven denominado **trigger-reboot** mediante el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fbad4-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="fbad4-138">El siguiente es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="fbad4-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="fbad4-139">En el símbolo del sistema, vaya a la carpeta trigger-reboot.</span><span class="sxs-lookup"><span data-stu-id="fbad4-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="fbad4-140">Con un editor de texto, abra el archivo pom.xml en la carpeta trigger-reboot y agregue la dependencia siguiente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="fbad4-141">Esta dependencia le permite usar el paquete iot-service-client en la aplicación para comunicarse con la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="fbad4-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="fbad4-142">Puede comprobar la versión más reciente de **iot-service-client** mediante la [funcionalidad de búsqueda de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="fbad4-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="fbad4-143">Agregue el nodo **build** después del nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="fbad4-144">Esta configuración indica a Maven que use Java 1.8 para compilar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="fbad4-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="fbad4-145">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="fbad4-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="fbad4-146">Con un editor de texto, abra el archivo de origen trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="fbad4-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="fbad4-147">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="fbad4-147">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="fbad4-148">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="fbad4-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="fbad4-149">Reemplace `{youriothubconnectionstring}` por la cadena de conexión de IoT Hub que anotó en la sección *Creación de un IoT Hub*:</span><span class="sxs-lookup"><span data-stu-id="fbad4-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="fbad4-150">Para implementar un subproceso que lee las propiedades notificadas desde el dispositivo gemelo cada 10 segundos, agregue la clase anidada siguiente a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="fbad4-151">Para invocar al método directo de reinicio en el dispositivo simulado, agregue el código siguiente al método **main**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-151">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

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

1. <span data-ttu-id="fbad4-152">Para iniciar el subproceso que sondea las propiedades notificadas desde el dispositivo simulado, agregue el código siguiente al método **main**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-152">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="fbad4-153">Para poder detener la aplicación, agregue el código siguiente al método **main**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-153">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="fbad4-154">Guarde y cierre el archivo trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="fbad4-154">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="fbad4-155">Compile la aplicación de back-end **trigger-reboot** y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="fbad4-155">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="fbad4-156">En el símbolo del sistema, vaya a la carpeta trigger-reboot y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbad4-156">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="fbad4-157">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="fbad4-157">Create a simulated device app</span></span>

<span data-ttu-id="fbad4-158">En esta sección, creará una aplicación de consola de Java que simula un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fbad4-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="fbad4-159">La aplicación escucha la llamada al método directo de reinicio desde IoT Hub y la responder inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="fbad4-159">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="fbad4-160">Luego, la aplicación se suspende unos instantes para simular el proceso de reinicio antes de usar una propiedad notificada para notificar a la aplicación back-end **trigger-reboot** que se completó el reinicio.</span><span class="sxs-lookup"><span data-stu-id="fbad4-160">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="fbad4-161">En la carpeta dm-get-started, cree un proyecto Maven denominado **simulated-device** con el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="fbad4-161">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="fbad4-162">El siguiente es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="fbad4-162">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="fbad4-163">En el símbolo del sistema, vaya a la nueva carpeta simulated-device.</span><span class="sxs-lookup"><span data-stu-id="fbad4-163">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="fbad4-164">Con un editor de texto, abra el archivo pom.xml en la carpeta simulated-device y agregue la dependencia siguiente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-164">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="fbad4-165">Esta dependencia le permite usar el paquete iot-service-client en la aplicación para comunicarse con la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="fbad4-165">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="fbad4-166">Puede comprobar la versión más reciente de **iot-device-client** mediante la [funcionalidad de búsqueda de Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="fbad4-166">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="fbad4-167">Agregue el nodo **build** después del nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-167">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="fbad4-168">Esta configuración indica a Maven que use Java 1.8 para compilar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="fbad4-168">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="fbad4-169">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="fbad4-169">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="fbad4-170">Con un editor de texto, abra el archivo de origen simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="fbad4-170">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="fbad4-171">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="fbad4-171">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="fbad4-172">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="fbad4-172">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="fbad4-173">Reemplace `{yourdeviceconnectionstring}` por la cadena de conexión de dispositivo que anotó en la sección *Creación de una identidad de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="fbad4-173">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="fbad4-174">Para implementar un controlador de devolución de llamada para los eventos de estado de método directo, agregue la clase anidada siguiente a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-174">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="fbad4-175">Para implementar un controlador de devolución de llamada para los eventos de estado de dispositivo gemelo, agregue la clase anidada siguiente a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-175">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="fbad4-176">Para implementar un controlador de devolución de llamada para los eventos de propiedad, agregue la clase anidada siguiente a la clase **App**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-176">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="fbad4-177">Para implementar un subproceso que simule el reinicio del dispositivo, agregue la clase anidada siguiente a la clase **App**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-177">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="fbad4-178">El subproceso se suspende durante cinco segundos y luego establece la propiedad notificada **lastReboot**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-178">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="fbad4-179">Para implementar el método directo en el dispositivo, agregue la clase anidada siguiente a la clase **App**.</span><span class="sxs-lookup"><span data-stu-id="fbad4-179">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="fbad4-180">Cuando la aplicación simulada recibe una llamada al método directo de **reinicio**, devuelve una confirmación al autor de la llamada y luego inicia un subproceso para procesar el reinicio:</span><span class="sxs-lookup"><span data-stu-id="fbad4-180">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

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

1. <span data-ttu-id="fbad4-181">Modifique la signatura del método **main** para generar las excepciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="fbad4-181">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="fbad4-182">Para crear instancias de **DeviceClient**, agregue el código siguiente al método **main**:</span><span class="sxs-lookup"><span data-stu-id="fbad4-182">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="fbad4-183">Agregue el código siguiente al método **main** para empezar a escuchar las llamadas al método directo:</span><span class="sxs-lookup"><span data-stu-id="fbad4-183">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="fbad4-184">Agregue el código siguiente al método **main** para apagar el simulador de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="fbad4-184">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="fbad4-185">Guarde y cierre el archivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="fbad4-185">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="fbad4-186">Compile la aplicación back-end **simulated-device** y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="fbad4-186">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="fbad4-187">En el símbolo del sistema, vaya a la carpeta simulated-device y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="fbad4-187">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="fbad4-188">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fbad4-188">Run the apps</span></span>

<span data-ttu-id="fbad4-189">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fbad4-189">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="fbad4-190">En un símbolo del sistema en la carpeta simulated-device, ejecute el comando siguiente para empezar a escuchar las llamadas al método de reinicio desde la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="fbad4-190">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aplicación de dispositivo simulado IoT Hub de Java para escuchar las llamadas al método directo de reinicio][1]

1. <span data-ttu-id="fbad4-192">En un símbolo del sistema en la carpeta trigger-reboot, ejecute el comando siguiente para llamar al método de reinicio en el dispositivo simulado desde la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="fbad4-192">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aplicación de servicio IoT Hub de Java para llamar al método directo de reinicio][2]

1. <span data-ttu-id="fbad4-194">El dispositivo simulado responde a la llamada al método directo de reinicio:</span><span class="sxs-lookup"><span data-stu-id="fbad4-194">The simulated device responds to the reboot direct method call:</span></span>

    ![La aplicación de dispositivo simulado IoT Hub de Java responde a la llamada al método directo][3]

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