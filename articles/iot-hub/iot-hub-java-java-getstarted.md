---
title: "Introducción a Azure IoT Hub (Java) | Microsoft Docs"
description: "Obtenga información sobre cómo enviar mensajes del dispositivo a la nube a una instancia de Azure IoT Hub mediante los SDK de IoT para Java. Cree aplicaciones de servicio y de dispositivo simuladas para registrar el dispositivo, enviar mensajes y leerlos en IoT Hub."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 707356a49970bcd76a55ee1b8a6fbddf6a6ba390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a><span data-ttu-id="12289-104">Conexión del dispositivo en IoT Hub con Java</span><span class="sxs-lookup"><span data-stu-id="12289-104">Connect your device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="12289-105">Al final de este tutorial tendrá tres aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="12289-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="12289-106">**create-device-identity**, que crea una identidad de dispositivo y una clave de seguridad asociada para conectar la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12289-106">**create-device-identity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="12289-107">**read-d2c-messages**, que muestra los datos de telemetría enviados por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12289-107">**read-d2c-messages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="12289-108">**simulated-device**, que se conecta con su instancia de IoT Hub con la identidad del dispositivo creada anteriormente y envía un mensaje de telemetría cada segundo mediante el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="12289-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="12289-109">En el artículo [Azure Iot SDKs][lnk-hub-sdks] (SDK de IoT de Azure) se proporciona información acerca de los diversos SDK que puede usar para crear ambas aplicaciones para que se ejecuten en dispositivos y en el back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="12289-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>

<span data-ttu-id="12289-110">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12289-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="12289-111">La versión más reciente de [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="12289-111">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="12289-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="12289-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="12289-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="12289-113">An active Azure account.</span></span> <span data-ttu-id="12289-114">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="12289-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="12289-115">El último paso es tomar nota del valor de **Primary key** (Clave principal).</span><span class="sxs-lookup"><span data-stu-id="12289-115">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="12289-116">A continuación, haga clic en **Endpoints** (Puntos de conexión) y en el punto de conexión integrado en **Events** (Eventos).</span><span class="sxs-lookup"><span data-stu-id="12289-116">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="12289-117">En la hoja **Properties** (Propiedades), anote los valores del **nombre compatible con el centro de eventos** y con la dirección del **punto de conexión compatible con centro de eventos**.</span><span class="sxs-lookup"><span data-stu-id="12289-117">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="12289-118">Necesita estos tres valores al crear la aplicación **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="12289-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Hoja de mensajería de IoT Hub de Azure Portal][6]

<span data-ttu-id="12289-120">Ahora ha creado su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-120">You have now created your IoT hub.</span></span> <span data-ttu-id="12289-121">Ahora tiene el nombre de host de IoT Hub, la cadena de conexión de IoT Hub, la clave principal de IoT Hub, el nombre compatible con Event Hubs y el punto de conexión compatible con Event Hubs que necesita para completar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="12289-121">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="12289-122">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="12289-122">Create a device identity</span></span>
<span data-ttu-id="12289-123">En esta sección, creará una aplicación de consola Java que crea una identidad de dispositivo en el registro de identidades de su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-123">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="12289-124">No se puede conectar un dispositivo a IoT Hub a menos que tenga una entrada en el registro de identidades.</span><span class="sxs-lookup"><span data-stu-id="12289-124">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="12289-125">Para más información, consulte la sección sobre el **registro de la identidad** de la [guía para desarrolladores de IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="12289-125">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="12289-126">Cuando ejecuta esta aplicación de consola, se genera una clave y un identificador de dispositivo únicos con el que el dispositivo puede identificarse cuando envía mensajes de dispositivo a la nube a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-126">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="12289-127">Cree una carpeta vacía denominada iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="12289-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="12289-128">En la carpeta iot-java-get-started, cree un proyecto de Maven denominado **create-device-identity** mediante el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="12289-128">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="12289-129">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="12289-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="12289-130">En el símbolo del sistema, vaya a la nueva carpeta create-device-identity.</span><span class="sxs-lookup"><span data-stu-id="12289-130">At your command prompt, navigate to the create-device-identity folder.</span></span>

3. <span data-ttu-id="12289-131">Con un editor de texto, abra el archivo pom.xml en la carpeta create-device-identity y agregue la siguiente dependencia al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="12289-131">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="12289-132">Esta dependencia le permite usar el paquete iot-service-client en su aplicación:</span><span class="sxs-lookup"><span data-stu-id="12289-132">This dependency enables you to use the iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="12289-133">Puede comprobar la versión más reciente de **iot-service-client** mediante la [funcionalidad de búsqueda de Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="12289-133">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="12289-134">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="12289-134">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="12289-135">Mediante un editor de texto, abra el archivo create-device-identity\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="12289-135">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="12289-136">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="12289-136">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="12289-137">Agregue las siguientes variables de nivel de clase a la clase **App** y sustituya **{yourhubconnectionstring}** por el valor anotado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="12289-137">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="12289-138">Modifique la firma del método **main** para incluir las excepciones de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="12289-138">Modify the signature of the **main** method to include the exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="12289-139">Agregue el siguiente código como cuerpo del método **main** .</span><span class="sxs-lookup"><span data-stu-id="12289-139">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="12289-140">Este código crea un dispositivo denominado *javadevice* en el registro de identidades de IoT Hub, si no existe.</span><span class="sxs-lookup"><span data-stu-id="12289-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="12289-141">Después muestra el identificador de dispositivo y la clave que necesitará más adelante:</span><span class="sxs-lookup"><span data-stu-id="12289-141">It then displays the device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="12289-142">Guarde y cierre el archivo App.java.</span><span class="sxs-lookup"><span data-stu-id="12289-142">Save and close the App.java file.</span></span>

11. <span data-ttu-id="12289-143">Para compilar la aplicación **create-device-identity** con Maven, ejecute el siguiente comando en el símbolo del sistema en la carpeta create-device-identity:</span><span class="sxs-lookup"><span data-stu-id="12289-143">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="12289-144">Para ejecutar la aplicación **create-device-identity** con Maven, ejecute el siguiente comando en el símbolo del sistema en la carpeta create-device-identity:</span><span class="sxs-lookup"><span data-stu-id="12289-144">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="12289-145">Anote el **identificador del dispositivo** y la **clave del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="12289-145">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="12289-146">Los necesitará más adelante cuando cree una aplicación que se conecta a IoT Hub como dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12289-146">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="12289-147">El registro de identidades de IoT Hub solo almacena identidades de dispositivos para permitir el acceso seguro a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-147">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="12289-148">Almacena las claves y los identificadores de dispositivo para usarlos como credenciales de seguridad, y un indicador de habilitado o deshabilitado que permite deshabilitar el acceso a un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="12289-148">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="12289-149">Si la aplicación necesita almacenar otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12289-149">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="12289-150">Consulte la [guía para desarrolladores de IoT Hub][lnk-devguide-identity] para más información.</span><span class="sxs-lookup"><span data-stu-id="12289-150">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="12289-151">Recepción de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="12289-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="12289-152">En esta sección, creará una aplicación de consola de Java que lee los mensajes de dispositivo a nube desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="12289-153">IoT Hub expone un punto de conexión compatible con [Event Hubs][lnk-event-hubs-overview] para poder leer los mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="12289-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="12289-154">Para simplificar las cosas, este tutorial crea un lector básico que no es apto para una implementación de alta capacidad de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="12289-154">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="12289-155">El [tutorial: procesamiento de mensajes de dispositivo a la nube][lnk-process-d2c-tutorial] muestra cómo procesar mensajes de dispositivo a la nube a escala.</span><span class="sxs-lookup"><span data-stu-id="12289-155">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="12289-156">En el tutorial [Introducción a Event Hubs][lnk-eventhubs-tutorial] se proporciona información adicional acerca de cómo procesar los mensajes desde Event Hubs. Dicha información se puede aplicar a los puntos de conexión de IoT Hub compatibles con Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="12289-156">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="12289-157">El punto de conexión compatible con Event Hubs para leer mensajes de dispositivo a la nube siempre usa el protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="12289-157">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="12289-158">En la carpeta iot-java-get-started creada en la sección *Creación de una identidad de dispositivo*, cree un proyecto de Maven denominado **read-d2c-messages** mediante el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="12289-158">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="12289-159">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="12289-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="12289-160">En el símbolo del sistema, vaya a la nueva carpeta read-d2c-messages.</span><span class="sxs-lookup"><span data-stu-id="12289-160">At your command prompt, navigate to the read-d2c-messages folder.</span></span>

3. <span data-ttu-id="12289-161">Con un editor de texto, abra el archivo pom.xml en la carpeta read-d2c-messages y agregue la siguiente dependencia al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="12289-161">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="12289-162">Esta dependencia permite usar el paquete eventhubs-client en la aplicación para leer desde el punto de conexión compatible con Event Hubs:</span><span class="sxs-lookup"><span data-stu-id="12289-162">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="12289-163">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="12289-163">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="12289-164">Con un editor de texto, abra el archivo read-d2c-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="12289-164">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="12289-165">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="12289-165">Add the following **import** statements to the file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="12289-166">Agregue la siguiente variable de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="12289-166">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="12289-167">Reemplace **{youriothubkey}**, **{youreventhubcompatiblenamespace}** y **{youreventhubcompatiblename}** por los valores anotados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="12289-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="12289-168">Agregue el siguiente método **receiveMessages** a la clase **App**.</span><span class="sxs-lookup"><span data-stu-id="12289-168">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="12289-169">Dicho método crea una instancia de **EventHubClient** para conectarse al punto de conexión compatible con Event Hubs y, luego, crea una instancia de **PartitionReceiver** de forma asincrónica para leer desde una partición de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="12289-169">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="12289-170">Se repite continuamente e imprime los detalles de los mensajes hasta que finaliza la aplicación.</span><span class="sxs-lookup"><span data-stu-id="12289-170">It loops continuously and prints the message details until the app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="12289-171">Este método utiliza un filtro cuando crea el receptor para que este solo lea los mensajes enviados a IoT Hub después de que el receptor comience a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="12289-171">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="12289-172">Esta técnica es útil en un entorno de prueba, porque puede ver el conjunto actual de mensajes.</span><span class="sxs-lookup"><span data-stu-id="12289-172">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="12289-173">En un entorno de producción, el código debe garantizar que se procesan todos los mensajes. Consulte el tutorial[procesamiento de mensajes de dispositivo a la nube de IoT Hub][lnk-process-d2c-tutorial] para más información.</span><span class="sxs-lookup"><span data-stu-id="12289-173">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="12289-174">Modifique la firma del método **main** para incluir la excepción de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="12289-174">Modify the signature of the **main** method to include the exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="12289-175">Agregue el siguiente código al método **main** de la clase **App**.</span><span class="sxs-lookup"><span data-stu-id="12289-175">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="12289-176">Este código crea las dos instancias de **EventHubClient** y **PartitionReceiver**, lo que le permite cerrar la aplicación cuando haya terminado de procesar los mensajes:</span><span class="sxs-lookup"><span data-stu-id="12289-176">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="12289-177">Este código supone que usted creó la instancia de IoT Hub en el nivel F1 (gratis).</span><span class="sxs-lookup"><span data-stu-id="12289-177">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="12289-178">Una instancia gratuita de IoT Hub tiene dos particiones denominadas "0" y "1".</span><span class="sxs-lookup"><span data-stu-id="12289-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="12289-179">Guarde y cierre el archivo App.java.</span><span class="sxs-lookup"><span data-stu-id="12289-179">Save and close the App.java file.</span></span>

12. <span data-ttu-id="12289-180">Para compilar la aplicación **read-d2c-messages** con Maven, ejecute el siguiente comando en el símbolo del sistema en la carpeta read-d2c-messages:</span><span class="sxs-lookup"><span data-stu-id="12289-180">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="12289-181">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="12289-181">Create a device app</span></span>
<span data-ttu-id="12289-182">En esta sección, creará una aplicación de consola de Java que simula un dispositivo que envía mensajes de dispositivo a nube a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="12289-183">En la carpeta iot-java-get-started que ha creado en la sección *Creación de una identidad de dispositivo*, cree un proyecto de Maven denominado **simulated-device** mediante el comando siguiente en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="12289-183">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="12289-184">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="12289-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="12289-185">En el símbolo del sistema, vaya a la nueva carpeta simulated-device.</span><span class="sxs-lookup"><span data-stu-id="12289-185">At your command prompt, navigate to the simulated-device folder.</span></span>

3. <span data-ttu-id="12289-186">Con un editor de texto, abra el archivo pom.xml de la carpeta simulated-device y agregue las siguientes dependencias al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="12289-186">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="12289-187">Esta dependencia le permite usar el paquete iothub-java-client en la aplicación para comunicarse con la instancia de IoT Hub y serializar los objetos de Java a JSON:</span><span class="sxs-lookup"><span data-stu-id="12289-187">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="12289-188">Puede comprobar la versión más reciente de **iot-device-client** mediante la [funcionalidad de búsqueda de Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="12289-188">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="12289-189">Guarde y cierre el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="12289-189">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="12289-190">Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="12289-190">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="12289-191">Agregue las siguientes instrucciones **import** al archivo:</span><span class="sxs-lookup"><span data-stu-id="12289-191">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="12289-192">Agregue las siguientes variables de nivel de clase a la clase **App** .</span><span class="sxs-lookup"><span data-stu-id="12289-192">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="12289-193">Reemplace **{youriothubname}** por el nombre de la instancia de IoT Hub y **{yourdevicekey}** por el valor de la clave de dispositivo que ha generado en la sección *Creación de una identidad de dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="12289-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="12289-194">Esta aplicación de ejemplo usa la variable **protocol** al crear una instancia de un objeto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="12289-194">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="12289-195">Puede usar el protocolo MQTT, AMQP o HTTP para comunicarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12289-195">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>

8. <span data-ttu-id="12289-196">Agregue la siguiente clase **TelemetryDataPoint** anidada dentro de la clase **App** para especificar los datos de telemetría que el dispositivo envía a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="12289-196">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="12289-197">Agregue la siguiente clase **EventCallback** anidada dentro de la clase **App** para mostrar el estado de confirmación que devuelve IoT Hub cuando procesa un mensaje de la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="12289-197">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the device app.</span></span> <span data-ttu-id="12289-198">Este método también notifica el subproceso principal de la aplicación cuando se ha procesado el mensaje:</span><span class="sxs-lookup"><span data-stu-id="12289-198">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="12289-199">Agregue la siguiente clase **MessageSender** anidada dentro de la clase **App**.</span><span class="sxs-lookup"><span data-stu-id="12289-199">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="12289-200">El método **run** de esta clase genera datos de telemetría de ejemplo que se envían a IoT Hub y espera confirmación antes de enviar el siguiente mensaje:</span><span class="sxs-lookup"><span data-stu-id="12289-200">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    <span data-ttu-id="12289-201">Este método envía un nuevo mensaje de dispositivo a nube un segundo después de que IoT Hub reconozca el mensaje anterior.</span><span class="sxs-lookup"><span data-stu-id="12289-201">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="12289-202">El mensaje contiene un objeto JSON serializado con el valor de deviceId y un número generado aleatoriamente para simular un sensor de temperatura y otro de humedad.</span><span class="sxs-lookup"><span data-stu-id="12289-202">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="12289-203">Reemplace el método **main** por el siguiente código, que crea un subproceso para enviar mensajes del dispositivo a la nube a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="12289-203">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="12289-204">Guarde y cierre el archivo App.java.</span><span class="sxs-lookup"><span data-stu-id="12289-204">Save and close the App.java file.</span></span>

13. <span data-ttu-id="12289-205">Para compilar la aplicación **simulated-device** con Maven, ejecute el siguiente comando en el símbolo del sistema en la carpeta simulated-device:</span><span class="sxs-lookup"><span data-stu-id="12289-205">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="12289-206">Por simplificar, este tutorial no implementa ninguna directiva de reintentos.</span><span class="sxs-lookup"><span data-stu-id="12289-206">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="12289-207">En el código de producción, deberá implementar directivas de reintentos (por ejemplo, retroceso exponencial), tal y como se sugiere en el artículo de MSDN [Transient Fault Handling][lnk-transient-faults] (Tratamiento de errores temporales).</span><span class="sxs-lookup"><span data-stu-id="12289-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="12289-208">Ejecución de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="12289-208">Run the apps</span></span>

<span data-ttu-id="12289-209">Ya está preparado para ejecutar las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="12289-209">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="12289-210">En un símbolo del sistema, en la carpeta read-d2c, ejecute el siguiente comando para empezar la supervisión de la primera partición de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="12289-210">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Aplicación cliente de servicio de IoT Hub de Java para supervisar mensajes del dispositivo a la nube][7]

2. <span data-ttu-id="12289-212">En un símbolo del sistema, en la carpeta simulated-device, ejecute el siguiente comando para empezar el envío de datos de telemetría a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="12289-212">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Aplicación de dispositivo de IoT Hub de Java para enviar mensajes del dispositivo a la nube][8]

3. <span data-ttu-id="12289-214">El icono **Uso** de [Azure Portal][lnk-portal] muestra el número de mensajes enviados a IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="12289-214">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Icono Uso de Azure Portal que muestra el número de mensajes enviados a IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="12289-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12289-216">Next steps</span></span>
<span data-ttu-id="12289-217">En este tutorial, configuró un centro de IoT nuevo en Azure Portal y, después, creó una identidad de dispositivo en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="12289-217">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="12289-218">Usó esta identidad de dispositivo para habilitar la aplicación del dispositivo para enviar a IoT Hub los mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="12289-218">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="12289-219">También creó otra aplicación que muestra los mensajes recibidos por el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="12289-219">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="12289-220">Para continuar la introducción a IoT Hub y explorar otros escenarios de IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="12289-220">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="12289-221">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="12289-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="12289-222">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="12289-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="12289-223">[Introducción a Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="12289-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="12289-224">Para aprender a ampliar su solución IoT y cómo procesar mensajes de dispositivo a la nube a escala, consulte [Tutorial: procesamiento de mensajes de dispositivo a la nube][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="12289-224">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
