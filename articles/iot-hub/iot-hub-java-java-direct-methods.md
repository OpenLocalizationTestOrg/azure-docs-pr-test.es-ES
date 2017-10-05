---
title: "Uso de métodos directos de Azure IoT Hub (Java) | Microsoft Docs"
description: "Describe cómo usar los métodos directos de IoT Hub de Azure. Usará el SDK de dispositivo IoT de Azure para Java con el fin de implementar una aplicación de dispositivo simulado que incluye un método directo, además del SDK de servicio IoT de Azure para Java con el objetivo de implementar una aplicación de servicio que invoque el método directo."
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
ms.openlocfilehash: 6243a1a8cc971c53c797182b2beb6f594d2ac5f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="53766-104">Uso de métodos directos (Java)</span><span class="sxs-lookup"><span data-stu-id="53766-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="53766-105">En este tutorial, creará dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="53766-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="53766-106">**invoke-direct-method**, una aplicación de back-end de Java que llama a un método de la aplicación de dispositivo simulado y muestra la respuesta.</span><span class="sxs-lookup"><span data-stu-id="53766-106">**invoke-direct-method**, a Java back-end app that calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="53766-107">**simulated-device**, una aplicación de Java que simula un dispositivo que se conecta a la instancia de IoT Hub con la identidad de dispositivo que crea.</span><span class="sxs-lookup"><span data-stu-id="53766-107">**simulated-device**, a Java app that simulates a device connecting to your IoT hub with the device identity you create.</span></span> <span data-ttu-id="53766-108">Esta aplicación responde a la invocación directa desde el back-end.</span><span class="sxs-lookup"><span data-stu-id="53766-108">This app responds to the direct invoked from the back end.</span></span>

> [!NOTE]
> <span data-ttu-id="53766-109">Para más información acerca de los diversos SDK que puede usar para crear aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución, consulte [SDK de IoT de Azure][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="53766-109">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="53766-110">Para completar este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="53766-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="53766-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="53766-111">Java SE 8.</span></span> <br/> <span data-ttu-id="53766-112">[Prepare your development environment][lnk-dev-setup] (Preparación del entorno de desarrollo) describe cómo instalar Java para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="53766-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="53766-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="53766-113">Maven 3.</span></span>  <br/> <span data-ttu-id="53766-114">[Prepare your development environment][lnk-dev-setup] (Preparación del entorno de desarrollo) describe cómo instalar [Maven][lnk-maven] para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="53766-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="53766-115">[Versión de Node.js 0.10.0 o posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="53766-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="53766-116">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="53766-116">Create a simulated device app</span></span>

<span data-ttu-id="53766-117">En esta sección, creará una aplicación de consola de Java que responda a un método llamado por el back-end de solución.</span><span class="sxs-lookup"><span data-stu-id="53766-117">In this section, you create a Java console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="53766-118">Cree una carpeta vacía llamada iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="53766-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="53766-119">En la carpeta iot-java-direct-method, cree un proyecto de Maven denominado **simulated-device** mediante el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="53766-119">In the iot-java-direct-method folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="53766-120">El siguiente es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="53766-120">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="53766-121">En el símbolo del sistema, vaya a la nueva carpeta simulated-device.</span><span class="sxs-lookup"><span data-stu-id="53766-121">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="53766-122">Con un editor de texto, abra el archivo pom.xml de la carpeta simulated-device y agregue las siguientes dependencias al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="53766-122">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="53766-123">Esta dependencia le permite usar el paquete iot-device-client en la aplicación para comunicarse con la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="53766-123">This dependency enables you to use the iot-device-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="53766-124">Puede comprobar la versión más reciente de **iot-device-client** mediante la [funcionalidad de búsqueda de Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="53766-124">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="53766-125">Agregue el nodo **build** después del nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="53766-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="53766-126">Esta configuración indica a Maven que use Java 1.8 para compilar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="53766-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="53766-127">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="53766-127">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="53766-128">Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="53766-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="53766-129">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="53766-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="53766-130">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="53766-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="53766-131">Reemplace `{youriothubname}` por el nombre de la instancia de IoT Hub y `{yourdevicekey}` por el valor de la clave de dispositivo que generó en la sección *Creación de una identidad de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="53766-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="53766-132">Esta aplicación de ejemplo usa la variable **protocol** al crear una instancia de un objeto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="53766-132">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="53766-133">Actualmente, si desea usar métodos directos, debe usar el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="53766-133">Currently, to use direct methods you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="53766-134">Agregue la clase anidada siguiente a la clase **App** para devolver un código de estado a la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="53766-134">To return a status code to your IoT hub, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="53766-135">Agregue la clase anidada siguiente a la clase **App** para controlar las invocaciones de método directo desde el back-end de la solución:</span><span class="sxs-lookup"><span data-stu-id="53766-135">To handle the direct method invocations from the solution back end, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="53766-136">Agregue un método **main** a la clase **App** para crear un **DeviceClient** y escuchar las invocaciones de método directo:</span><span class="sxs-lookup"><span data-stu-id="53766-136">To create a **DeviceClient** and listen for direct method invocations, add a **main** method to the **App** class:</span></span>

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
        System.out.println("Subscribed to direct methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key to exit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="53766-137">Guarde y cierre el archivo simulated-device\src\main\java\com\mycompany\app\App.java</span><span class="sxs-lookup"><span data-stu-id="53766-137">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="53766-138">Compile la aplicación **simulated-device** y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="53766-138">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="53766-139">En el símbolo del sistema, vaya a la carpeta simulated-device y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="53766-139">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="53766-140">Llamada a un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="53766-140">Call a direct method on a device</span></span>

<span data-ttu-id="53766-141">En esta sección, creará una aplicación de consola de Java que invoca a un método directo y luego muestra la respuesta.</span><span class="sxs-lookup"><span data-stu-id="53766-141">In this section, you create a Java console app that invokes a direct method and then displays the response.</span></span> <span data-ttu-id="53766-142">Esta aplicación de consola se conecta a la instancia de IoT Hub para invocar al método directo.</span><span class="sxs-lookup"><span data-stu-id="53766-142">This console app connects to your IoT Hub to invoke the direct method.</span></span>

1. <span data-ttu-id="53766-143">En la carpeta iot-java-direct-method, cree un proyecto de Maven denominado **invoke-direct-method** mediante el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="53766-143">In the iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using the following command at your command prompt.</span></span> <span data-ttu-id="53766-144">El siguiente es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="53766-144">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="53766-145">En el símbolo del sistema, vaya a la carpeta invoke-direct-method.</span><span class="sxs-lookup"><span data-stu-id="53766-145">At your command prompt, navigate to the invoke-direct-method folder.</span></span>

1. <span data-ttu-id="53766-146">Con un editor de texto, abra el archivo pom.xml en la carpeta invoke-direct-method y agregue la dependencia siguiente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="53766-146">Using a text editor, open the pom.xml file in the invoke-direct-method folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="53766-147">Esta dependencia le permite usar el paquete iot-service-client en la aplicación para comunicarse con la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="53766-147">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="53766-148">Puede comprobar la versión más reciente de **iot-service-client** mediante la [funcionalidad de búsqueda de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="53766-148">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="53766-149">Agregue el nodo **build** después del nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="53766-149">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="53766-150">Esta configuración indica a Maven que use Java 1.8 para compilar la aplicación:</span><span class="sxs-lookup"><span data-stu-id="53766-150">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="53766-151">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="53766-151">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="53766-152">Con un editor de texto, abra el archivo invoke-direct-method\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="53766-152">Using a text editor, open the invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="53766-153">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="53766-153">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="53766-154">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="53766-154">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="53766-155">Reemplace `{youriothubconnectionstring}` por la cadena de conexión de IoT Hub que anotó en la sección *Creación de un IoT Hub*:</span><span class="sxs-lookup"><span data-stu-id="53766-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line to be written";
    ```

1. <span data-ttu-id="53766-156">Agregue el código siguiente al método **main** para invocar el método en el dispositivo simulado:</span><span class="sxs-lookup"><span data-stu-id="53766-156">To invoke the method on the simulated device, add the following code to the **main** method:</span></span>

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

1. <span data-ttu-id="53766-157">Guarde y cierre el archivo invoke-direct-method\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="53766-157">Save and close the invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="53766-158">Compile la aplicación **invoke-direct-method** y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="53766-158">Build the **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="53766-159">En el símbolo del sistema, vaya a la carpeta invoke-direct-method y ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="53766-159">At your command prompt, navigate to the invoke-direct-method folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="53766-160">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="53766-160">Run the apps</span></span>

<span data-ttu-id="53766-161">Ya está preparado para ejecutar las aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="53766-161">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="53766-162">En un símbolo del sistema, en la carpeta simulated-device, ejecute el comando siguiente para empezar a escuchar las llamadas de método desde la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="53766-162">At a command prompt in the simulated-device folder, run the following command to begin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aplicación de dispositivo simulado IoT Hub de Java para escuchar las llamadas al método directo][8]

1. <span data-ttu-id="53766-164">En un símbolo del sistema en la carpeta invoke-direct-method, ejecute el comando siguiente para llamar a un método en el dispositivo simulado desde la instancia de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="53766-164">At a command prompt in the invoke-direct-method folder, run the following command to call a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Aplicación de servicio IoT Hub de Java para llamar a un método directo][7]

1. <span data-ttu-id="53766-166">El dispositivo simulado responde a la llamada al método directo:</span><span class="sxs-lookup"><span data-stu-id="53766-166">The simulated device responds to the direct method call:</span></span>

    ![La aplicación de dispositivo simulado IoT Hub de Java responde a la llamada al método directo][9]

## <a name="next-steps"></a><span data-ttu-id="53766-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="53766-168">Next steps</span></span>

<span data-ttu-id="53766-169">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="53766-169">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="53766-170">Usó esta identidad de dispositivo para que la aplicación del dispositivo simulado reaccionara a los métodos que se invoquen desde la nube.</span><span class="sxs-lookup"><span data-stu-id="53766-170">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="53766-171">También creó una aplicación que invoca métodos en el dispositivo y muestra la respuesta del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53766-171">You also created an app that invokes methods on the device and displays the response from the device.</span></span>

<span data-ttu-id="53766-172">Para explorar otros escenarios de IoT, consulte [Programación de trabajos en varios dispositivos][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="53766-172">To explore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="53766-173">Para información sobre cómo ampliar la solución de IoT y programar llamadas de método en varios dispositivos, consulte el tutorial [Programación de trabajos en varios dispositivos][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="53766-173">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
