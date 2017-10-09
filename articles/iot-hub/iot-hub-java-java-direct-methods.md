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
# <a name="use-direct-methods-java"></a><span data-ttu-id="e4ba8-104">Uso de métodos directos (Java)</span><span class="sxs-lookup"><span data-stu-id="e4ba8-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="e4ba8-105">En este tutorial, creará dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="e4ba8-106">**método Invoke direct**, una aplicación de back-end de Java que llama a un método de aplicación de dispositivo simulado de hello y muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="e4ba8-107">**dispositivo simulado**, una aplicación Java que simula un dispositivo que se conecta centro de IoT tooyour con la identidad de dispositivo de Hola que cree.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="e4ba8-108">Esta aplicación responde toohello invocado directa de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="e4ba8-109">Para obtener información acerca de hello SDK que puede usar toobuild toorun de aplicaciones en dispositivos y el back-end de soluciones, consulte [SDK de Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="e4ba8-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="e4ba8-110">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="e4ba8-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-111">Java SE 8.</span></span> <br/> <span data-ttu-id="e4ba8-112">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Java para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="e4ba8-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-113">Maven 3.</span></span>  <br/> <span data-ttu-id="e4ba8-114">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall [Maven] [ lnk-maven] para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="e4ba8-115">[Versión de Node.js 0.10.0 o posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e4ba8-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e4ba8-116">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="e4ba8-116">Create a simulated device app</span></span>

<span data-ttu-id="e4ba8-117">En esta sección, creará una aplicación de consola de Java que responde el método tooa llamado a soluciones de hello volver final.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="e4ba8-118">Cree una carpeta vacía llamada iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="e4ba8-119">En carpeta de iot java direct método hello, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="e4ba8-120">Hola siguiente comando es un comando único, long:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="e4ba8-121">En el símbolo del sistema, desplazarse por las carpetas de toohello dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="e4ba8-122">Con un editor de texto, abra archivo pom.xml de hello en la carpeta del dispositivo simulado de Hola y agregue Hola siguiendo las dependencias toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="e4ba8-123">Esta dependencia permite toouse Hola iot de cliente de dispositivo empaquete en su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="e4ba8-124">Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="e4ba8-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="e4ba8-125">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="e4ba8-126">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="e4ba8-127">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="e4ba8-128">Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="e4ba8-129">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="e4ba8-130">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="e4ba8-131">Reemplazar `{youriothubname}` por el nombre del centro de IoT, y `{yourdevicekey}` con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="e4ba8-132">Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="e4ba8-133">Actualmente, toouse dirigir métodos que se debe usar protocolo MQTT Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="e4ba8-134">tooreturn un centro de IoT tooyour del código de estado, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="e4ba8-135">invocaciones de método directo toohandle Hola de hello solución back-end, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="e4ba8-136">toocreate una **DeviceClient** y escuchar las invocaciones de método directo, agregue un **principal** método toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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

1. <span data-ttu-id="e4ba8-137">Guarde y cierre el archivo de hello simulated-device\src\main\java\com\mycompany\app\App.java</span><span class="sxs-lookup"><span data-stu-id="e4ba8-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="e4ba8-138">Compilar hello **dispositivo simulado** aplicación y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="e4ba8-139">En el símbolo del sistema, desplácese carpeta del dispositivo simulado toohello y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="e4ba8-140">Llamada a un método directo en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="e4ba8-140">Call a direct method on a device</span></span>

<span data-ttu-id="e4ba8-141">En esta sección, creará una aplicación de consola de Java que invoca un método directo y, a continuación, muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="e4ba8-142">Esta aplicación de consola conecta tooyour método directo de centro de IoT tooinvoke Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="e4ba8-143">En carpeta de iot java direct método hello, cree un proyecto de Maven denominado **método invoke direct** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="e4ba8-144">Hola siguiente comando es un comando único, long:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="e4ba8-145">En el símbolo del sistema, desplazarse por las carpetas de toohello método invoke direct.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="e4ba8-146">Con un editor de texto, abra el archivo de pom.xml de hello en carpeta de método de invocación directa de Hola y agregue Hola después toohello de dependencia **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="e4ba8-147">Esta dependencia permite toouse Hola iot-service-paquete de cliente de su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="e4ba8-148">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="e4ba8-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="e4ba8-149">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="e4ba8-150">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="e4ba8-151">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="e4ba8-152">Con un editor de texto, abra el archivo invoke-direct-method\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="e4ba8-153">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="e4ba8-154">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="e4ba8-155">Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="e4ba8-156">método de tooinvoke hello en dispositivo simulado de hello, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="e4ba8-157">Guarde y cierre el archivo de hello invoke-direct-method\src\main\java\com\mycompany\app\App.java</span><span class="sxs-lookup"><span data-stu-id="e4ba8-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="e4ba8-158">Compilar hello **método invoke direct** aplicación y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="e4ba8-159">En el símbolo del sistema, desplácese toohello carpeta de método de invocación directa y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="e4ba8-160">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="e4ba8-160">Run hello apps</span></span>

<span data-ttu-id="e4ba8-161">Ya estás listo toorun hello las aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="e4ba8-162">En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después de realizar escuchas para las llamadas de método desde el centro de IoT de toobegin de comando:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centro de IoT de Java simulados toolisten de aplicación de dispositivo para las llamadas a métodos directas][8]

1. <span data-ttu-id="e4ba8-164">En un símbolo del sistema en carpeta de método de invocación directa de hello, ejecute hello después comando toocall un método en el dispositivo simulado desde el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Toocall de aplicación de servicio de centro de IoT de Java un método directo][7]

1. <span data-ttu-id="e4ba8-166">dispositivo simulado de Hola responde la llamada a un método directo toohello:</span><span class="sxs-lookup"><span data-stu-id="e4ba8-166">hello simulated device responds toohello direct method call:</span></span>

    ![Aplicación de dispositivo simulado de centro de IoT de Java responde la llamada a un método directo toohello][9]

## <a name="next-steps"></a><span data-ttu-id="e4ba8-168">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4ba8-168">Next steps</span></span>

<span data-ttu-id="e4ba8-169">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e4ba8-170">Utiliza este toomethods dispositivo identidad tooenable Hola simulada dispositivos aplicación tooreact invocado por la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="e4ba8-171">También crea una aplicación que invoca los métodos en el dispositivo de Hola y muestra la respuesta de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="e4ba8-172">tooexplore otros escenarios de IoT, consulte [programar trabajos en varios dispositivos][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="e4ba8-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="e4ba8-173">toolearn cómo tooextend llama a su método de programación y de solución de IoT en varios dispositivos, vea hello [programación y los trabajos de difusión] [ lnk-tutorial-jobs] tutorial.</span><span class="sxs-lookup"><span data-stu-id="e4ba8-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
