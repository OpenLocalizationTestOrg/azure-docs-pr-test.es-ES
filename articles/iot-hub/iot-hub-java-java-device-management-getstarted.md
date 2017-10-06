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
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="c2ff8-104">Introducción a la administración de dispositivos (Java)</span><span class="sxs-lookup"><span data-stu-id="c2ff8-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="c2ff8-105">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="c2ff8-106">Usar hello toocreate portal Azure un centro de IoT y cree una identidad de dispositivo en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="c2ff8-107">Crear una aplicación de dispositivo simulado que implementa un dispositivo de hello tooreboot método directo.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="c2ff8-108">Se invocan métodos directos de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="c2ff8-109">Crear una aplicación que invoca el método directo de reinicio de hello en la aplicación de dispositivo simulado de hello a través de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="c2ff8-110">Esta aplicación, a continuación, monitores Hola propiedades notificados de hello dispositivo toosee cuando se completa la operación de reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="c2ff8-111">Al final de Hola de este tutorial, tiene dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="c2ff8-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-112">**simulated-device**.</span></span> <span data-ttu-id="c2ff8-113">Esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-113">This app:</span></span>

* <span data-ttu-id="c2ff8-114">Se conecta a centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="c2ff8-115">Recibe una llamada de método directo de reinicio.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="c2ff8-116">Simula un reinicio físico.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="c2ff8-117">Informa del tiempo Hola de último reinicio de Hola a través de una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="c2ff8-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-118">**trigger-reboot**.</span></span> <span data-ttu-id="c2ff8-119">Esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-119">This app:</span></span>

* <span data-ttu-id="c2ff8-120">Llama a un método directo en la aplicación de dispositivo simulado de hello.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="c2ff8-121">Muestra de Hola respuesta toohello directa llamada al método enviado por dispositivo simulado Hola</span><span class="sxs-lookup"><span data-stu-id="c2ff8-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="c2ff8-122">Hello muestra actualizado informó de propiedades.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ff8-123">Para obtener información acerca de hello SDK que puede usar toobuild toorun de aplicaciones en dispositivos y el back-end de soluciones, consulte [SDK de Azure IoT][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="c2ff8-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="c2ff8-124">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="c2ff8-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-125">Java SE 8.</span></span> <br/> <span data-ttu-id="c2ff8-126">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall Java para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c2ff8-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-127">Maven 3.</span></span>  <br/> <span data-ttu-id="c2ff8-128">[Preparar el entorno de desarrollo] [ lnk-dev-setup] describe cómo tooinstall [Maven] [ lnk-maven] para este tutorial en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="c2ff8-129">[Versión de Node.js 0.10.0 o posterior](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="c2ff8-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="c2ff8-130">Desencadenar un reinicio remoto en dispositivo Hola utilizando un método directo</span><span class="sxs-lookup"><span data-stu-id="c2ff8-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="c2ff8-131">En esta sección, creará una aplicación de consola de Java que permite:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="c2ff8-132">Método directo de reinicio de hello en la aplicación de dispositivo simulado de hello, se invoca.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="c2ff8-133">Muestra la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-133">Displays hello response.</span></span>
1. <span data-ttu-id="c2ff8-134">Hola sondeos notificado propiedades enviadas desde Hola dispositivo toodetermine cuando se completa el reinicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="c2ff8-135">Esta aplicación de consola conecta tooyour centro de IoT método directo de tooinvoke Hola y Hola lectura notificada propiedades.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="c2ff8-136">Cree una carpeta vacía llamada dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="c2ff8-137">En carpeta dm get iniciada hello, cree un proyecto de Maven denominado **desencadenador reinicio** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="c2ff8-138">siguiente Hello muestra un comando único, long:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c2ff8-139">En el símbolo del sistema, desplazarse por las carpetas de reinicio de desencadenador de toohello.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="c2ff8-140">Con un editor de texto, abra el archivo de pom.xml de hello en carpeta de reinicio de desencadenador de Hola y agregue Hola después toohello de dependencia **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c2ff8-141">Esta dependencia permite toouse Hola iot-service-paquete de cliente de su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c2ff8-142">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="c2ff8-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="c2ff8-143">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c2ff8-144">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c2ff8-145">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="c2ff8-146">Con un editor de texto, abra el archivo de código fuente de hello trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="c2ff8-147">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-147">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="c2ff8-148">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c2ff8-149">Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="c2ff8-150">tooimplement un subproceso que lee Hola notificado propiedades desde gemelas de dispositivo de hello cada 10 segundos, agregue siguientes de Hola anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="c2ff8-151">método directo reinicio de tooinvoke hello en dispositivo simulado de hello, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="c2ff8-152">toostart Hola subproceso toopoll Hola notificados propiedades de dispositivo simulado de hello, agregue Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="c2ff8-153">tooenable toostop Hola aplicación, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="c2ff8-154">Guarde y cierre el archivo de hello trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c2ff8-155">Compilar hello **desencadenador reinicio** aplicaciones back-end y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="c2ff8-156">En el símbolo del sistema, desplácese toohello desencadenador reinicio carpeta y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="c2ff8-157">Creación de una aplicación de dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="c2ff8-157">Create a simulated device app</span></span>

<span data-ttu-id="c2ff8-158">En esta sección, creará una aplicación de consola de Java que simula un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="c2ff8-159">aplicación Hello escucha Hola reinicio método directo llamada desde el centro de IoT y responde inmediatamente llamada toothat.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="c2ff8-160">Hola de aplicación, a continuación, espera unos instantes proceso de reinicio de hello toosimulate antes de usar un Hola de toonotify propiedad notificado **desencadenador reinicio** aplicación back-end que Hola reinicio está completa.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="c2ff8-161">En carpeta dm get iniciada hello, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="c2ff8-162">Hola te mostramos un comando único, long:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="c2ff8-163">En el símbolo del sistema, desplazarse por las carpetas de toohello dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="c2ff8-164">Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta del dispositivo simulado de Hola y agregue Hola después toohello de dependencia **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="c2ff8-165">Esta dependencia permite toouse Hola iot-service-paquete de cliente de su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="c2ff8-166">Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="c2ff8-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="c2ff8-167">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="c2ff8-168">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="c2ff8-169">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="c2ff8-170">Con un editor de texto, abra el archivo de código fuente de hello simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="c2ff8-171">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-171">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="c2ff8-172">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="c2ff8-173">Reemplace `{yourdeviceconnectionstring}` con cadena de conexión de dispositivo de Hola que anotó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="c2ff8-174">tooimplement un controlador de devolución de llamada para los eventos de estado de método directo, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="c2ff8-175">tooimplement un controlador de devolución de llamada para los eventos de estado de dispositivo gemelas, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="c2ff8-176">tooimplement un controlador de devolución de llamada para los eventos de propiedad, agregue el siguiente de hello anidados clase toohello **aplicación** clase:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="c2ff8-177">tooimplement un subproceso toosimulate Hola el reinicio del dispositivo, agregue el siguiente de hello anidados clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="c2ff8-178">subproceso de Hola se suspende durante cinco segundos y, a continuación, Establece hello **lastReboot** informó de propiedad:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="c2ff8-179">método directo de tooimplement hello en dispositivo hello, agregue el siguiente de hello anidados clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="c2ff8-180">Cuando la aplicación simulada de hello recibe una llamada toohello **reiniciar** método directo, devuelve un autor de llamada de confirmación toohello y, a continuación, inicia un Hola de subproceso tooprocess reiniciar:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

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

1. <span data-ttu-id="c2ff8-181">Modificar firma Hola de hello **principal** hello toothrow de método siguientes excepciones:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="c2ff8-182">tooinstantiate una **DeviceClient**, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="c2ff8-183">toostart realizar escuchas para las llamadas a métodos directas, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="c2ff8-184">tooshut hacia abajo el simulador de dispositivos de hello, agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="c2ff8-185">Guarde y cierre el archivo de hello simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="c2ff8-186">Compilar hello **dispositivo simulado** aplicaciones back-end y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="c2ff8-187">En el símbolo del sistema, desplácese carpeta del dispositivo simulado toohello y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="c2ff8-188">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="c2ff8-188">Run hello apps</span></span>

<span data-ttu-id="c2ff8-189">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c2ff8-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="c2ff8-190">En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después de realizar escuchas para las llamadas de método de reinicio desde el centro de IoT de toobegin de comando:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Centro de IoT de Java simulados toolisten de aplicación de dispositivo para las llamadas de método directo de reinicio][1]

1. <span data-ttu-id="c2ff8-192">En un símbolo del sistema en carpeta de reinicio de desencadenador de hello, ejecute hello siguiendo el método de reinicio de comando toocall hello en el dispositivo simulado de su centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hola de toocall de aplicación de servicio de centro de IoT de Java reiniciar método directo][2]

1. <span data-ttu-id="c2ff8-194">dispositivo simulado Hola responde toohello reinicio método directo llamada:</span><span class="sxs-lookup"><span data-stu-id="c2ff8-194">hello simulated device responds toohello reboot direct method call:</span></span>

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