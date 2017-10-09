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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="0fe0f-104">Introducción a los dispositivos gemelos (Java)</span><span class="sxs-lookup"><span data-stu-id="0fe0f-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="0fe0f-105">En este tutorial, creará dos aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="0fe0f-106">**add-tags-query**, una aplicación de back-end de Java que agrega etiquetas y consulta dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="0fe0f-107">**dispositivo simulado**, una aplicación de dispositivo de Java que conecta informes y centro de IoT tooyour su condición de conectividad con una propiedad notificada.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="0fe0f-108">artículo de Hello [SDK de Azure IoT](iot-hub-devguide-sdks.md) proporciona información acerca de hello Azure IoT SDK que se puede usar toobuild aplicaciones de dispositivo y back-end.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="0fe0f-109">toocomplete este tutorial, necesita:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="0fe0f-110">Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="0fe0f-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="0fe0f-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="0fe0f-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="0fe0f-112">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-112">An active Azure account.</span></span> <span data-ttu-id="0fe0f-113">(En caso de no tener ninguna, puede crear una [cuenta gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="0fe0f-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="0fe0f-114">Si prefiere identidad del dispositivo toocreate hello mediante programación, lea las secciones correspondientes de Hola Hola [conectar el centro de IoT de tooyour dispositivo usa Java](iot-hub-java-java-getstarted.md#create-a-device-identity) artículo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="0fe0f-115">Crear aplicación de servicio de hello</span><span class="sxs-lookup"><span data-stu-id="0fe0f-115">Create hello service app</span></span>

<span data-ttu-id="0fe0f-116">En esta sección, creará una aplicación Java que agrega los metadatos de ubicación como asociada a un doble de dispositivo de toohello de etiqueta en el centro de IoT **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="0fe0f-117">aplicación Hello consultará primero centro de IoT para dispositivos que se encuentran en hello Estados Unidos y, a continuación, en dispositivos que dependen de una conexión de red de telefonía móvil.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="0fe0f-118">En el equipo de desarrollo, cree una carpeta vacía denominada `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="0fe0f-119">Hola `iot-java-twin-getstarted` carpeta, cree un proyecto de Maven denominado **consulta agregar etiquetas** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="0fe0f-120">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="0fe0f-121">En el símbolo del sistema, desplácese toohello `add-tags-query` carpeta.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="0fe0f-122">Con un editor de texto, abra hello `pom.xml` archivo Hola `add-tags-query` carpeta y agregue Hola después dependencia toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="0fe0f-123">Esta dependencia permite hello toouse **cliente del servicio de iot** paquete en su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="0fe0f-124">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="0fe0f-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="0fe0f-125">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="0fe0f-126">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="0fe0f-127">Guarde y cierre hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="0fe0f-128">Con un editor de texto, abra hello `add-tags-query\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="0fe0f-129">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="0fe0f-130">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="0fe0f-131">Reemplace `{youriothubconnectionstring}` con la cadena de conexión de base de datos central de IoT que anotó en hello *crear un centro de IoT* sección:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="0fe0f-132">Hola de actualización **principal** siguiente de Hola de tooinclude de firma de método `throws` cláusula:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="0fe0f-133">Agregar Hola después código toohello **principal** Hola de método toocreate **DeviceTwin** y **DeviceTwinDevice** objetos.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="0fe0f-134">Hola **DeviceTwin** objeto controla la comunicación de hello con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="0fe0f-135">Hola **DeviceTwinDevice** objeto representa el doble de dispositivo de hello con sus propiedades y etiquetas:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="0fe0f-136">Agregue los siguiente hello `try/catch` bloquear toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="0fe0f-137">Hola tooupdate **región** y **planta** las etiquetas del dispositivo gemelas en el doble de dispositivo, agregar Hola después el código de hello `try` bloque:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="0fe0f-138">: los gemelos de tooquery Hola dispositivo en el centro de IoT, agregar Hola después código toohello `try` bloque después de código de hello que agregó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="0fe0f-139">código de Hello ejecuta dos consultas.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-139">hello code runs two queries.</span></span> <span data-ttu-id="0fe0f-140">Cada consulta devuelve un máximo de 100 dispositivos:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="0fe0f-141">Guarde y cierre hello `add-tags-query\src\main\java\com\mycompany\app\App.java` archivo</span><span class="sxs-lookup"><span data-stu-id="0fe0f-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="0fe0f-142">Compilar hello **consulta agregar etiquetas** aplicación y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="0fe0f-143">En el símbolo del sistema, desplácese toohello `add-tags-query` carpeta y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="0fe0f-144">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="0fe0f-144">Create a device app</span></span>

<span data-ttu-id="0fe0f-145">En esta sección, creará una aplicación de consola de Java que establece un valor de propiedad notificado que se envía tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="0fe0f-146">Hola `iot-java-twin-getstarted` carpeta, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="0fe0f-147">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="0fe0f-148">En el símbolo del sistema, desplácese toohello `simulated-device` carpeta.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="0fe0f-149">Con un editor de texto, abra hello `pom.xml` archivo Hola `simulated-device` carpeta y agregue Hola siguiendo las dependencias toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="0fe0f-150">Esta dependencia permite hello toouse **cliente de dispositivo iot** paquete en su toocommunicate de aplicación con el centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="0fe0f-151">Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="0fe0f-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="0fe0f-152">Agregue los siguiente hello **generar** nodo después de hello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="0fe0f-153">Esta configuración indica a la aplicación de Maven toouse Java toobuild 1,8 hello:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="0fe0f-154">Guarde y cierre hello `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="0fe0f-155">Con un editor de texto, abra hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="0fe0f-156">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="0fe0f-157">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="0fe0f-158">Reemplazar `{youriothubname}` por el nombre del centro de IoT, y `{yourdevicekey}` con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="0fe0f-159">Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="0fe0f-160">Actualmente, toouse gemelas características de dispositivos debe utilizar hello MQTT protocolo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="0fe0f-161">Agregar Hola después código toohello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="0fe0f-162">Crear un toocommunicate de cliente de dispositivo con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="0fe0f-163">Crear un **dispositivo** toostore Hola dispositivo gemelas propiedades del objeto.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="0fe0f-164">Agregar Hola después código toohello **principal** toocreate método un **connectivityType** notifican propiedad y enviar tooIoT concentrador:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="0fe0f-165">Agregar Hola siguiente código toohello final de hello **principal** método.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="0fe0f-166">Esperando hello **ENTRAR** clave permite tiempo para el estado de centro de IoT tooreport Hola de operaciones de hello dispositivo gemelas:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="0fe0f-167">Guarde y cierre hello `simulated-device\src\main\java\com\mycompany\app\App.java` archivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="0fe0f-168">Compilar hello **dispositivo simulado** aplicación y corrija los errores.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="0fe0f-169">En el símbolo del sistema, desplácese toohello `simulated-device` carpeta y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="0fe0f-170">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="0fe0f-170">Run hello apps</span></span>

<span data-ttu-id="0fe0f-171">Ya estás listo toorun hello las aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="0fe0f-172">En un símbolo del sistema en hello `add-tags-query` carpeta, ejecute hello después comando toorun hello **consulta agregar etiquetas** del servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicación de servicio de centro de IoT de Java etiquetar los valores y ejecutar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="0fe0f-174">Puede ver hello **planta** y **región** etiquetas agregan toohello gemelas de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="0fe0f-175">Hola primera consulta devuelve el dispositivo, pero hello en segundo lugar no lo hace.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="0fe0f-176">En un símbolo del sistema en hello `simulated-device` carpeta, ejecute hello después comando tooadd hello **connectivityType** notificado gemelas de dispositivos de propiedad toohello:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![cliente de dispositivo de Hello agrega Hola ** connectivityType ** notificado propiedad](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="0fe0f-178">En un símbolo del sistema en hello `add-tags-query` carpeta, ejecute hello después comando toorun hello **consulta agregar etiquetas** una segunda vez del servicio de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Tooupdate de aplicación de servicio de centro de IoT de Java etiquetar los valores y ejecutar consultas de dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="0fe0f-180">Ahora el dispositivo ha enviado hello **connectivityType** tooIoT propiedad concentrador, segunda consulta de hello devuelve el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fe0f-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0fe0f-181">Next steps</span></span>

<span data-ttu-id="0fe0f-182">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="0fe0f-183">Agrega los metadatos del dispositivo como etiquetas desde una aplicación de back-end y escribió una información de conectividad del dispositivo dispositivo aplicación tooreport en gemelas de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="0fe0f-184">También ha aprendido cómo tooquery Hola información gemelas del dispositivo mediante el lenguaje de consulta de hello centro de IoT similar a SQL.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="0fe0f-185">Hola de uso después cómo toolearn de recursos para:</span><span class="sxs-lookup"><span data-stu-id="0fe0f-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="0fe0f-186">Enviar telemetría desde dispositivos con hello [empezar a trabajar con el centro de IoT](iot-hub-java-java-getstarted.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="0fe0f-187">Controlar los dispositivos de forma interactiva (por ejemplo, al activar un ventilador desde una aplicación controlada por el usuario) con hello [usar métodos directos](iot-hub-java-java-direct-methods.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="0fe0f-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
