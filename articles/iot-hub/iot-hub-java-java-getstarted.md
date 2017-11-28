---
title: aaaGet a trabajar con el centro de IoT de Azure (Java) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosend dispositivo a la nube mensajes tooAzure centro de IoT con IoT SDK para Java. Crear dispositivo simulado y tooregister de aplicaciones de servicio, el dispositivo, enviar mensajes y leer los mensajes de centro de IoT."
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
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="1a698-104">Conectar el centro de IoT de tooyour dispositivo usa Java</span><span class="sxs-lookup"><span data-stu-id="1a698-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="1a698-105">Al final de Hola de este tutorial, tendrá tres aplicaciones de consola de Java:</span><span class="sxs-lookup"><span data-stu-id="1a698-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="1a698-106">**identidad del dispositivo crear**, que crea una identidad de dispositivo y la clave de seguridad asociadas tooconnect la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a698-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="1a698-107">**leer mensajes de d2c**, que muestra la telemetría de hello enviado por la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a698-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="1a698-108">**dispositivo simulado**, que se conecta el centro de IoT tooyour con la identidad del dispositivo Hola creado anteriormente y envía un mensaje de telemetría cada segundo mediante Hola protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="1a698-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="1a698-109">artículo de Hello [SDK de Azure IoT] [ lnk-hub-sdks] proporciona información acerca de hello Azure IoT SDK que puede usar ambos toorun aplicaciones toobuild en dispositivos y el back-end de soluciones.</span><span class="sxs-lookup"><span data-stu-id="1a698-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="1a698-110">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="1a698-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1a698-111">Hola más reciente [8 del Kit de desarrollo de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="1a698-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="1a698-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="1a698-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="1a698-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="1a698-113">An active Azure account.</span></span> <span data-ttu-id="1a698-114">(En caso de no tenerla, puede crear una [cuenta gratuita][lnk-free-trial] en solo unos minutos).</span><span class="sxs-lookup"><span data-stu-id="1a698-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="1a698-115">Como paso final, tome nota de hello **clave principal** valor.</span><span class="sxs-lookup"><span data-stu-id="1a698-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="1a698-116">A continuación, haga clic en **extremos** hello y **eventos** extremo predefinido.</span><span class="sxs-lookup"><span data-stu-id="1a698-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="1a698-117">En hello **propiedades** hoja, tome nota de hello **nombre de concentrador de eventos-compatible con** hello y **punto de conexión de concentrador de eventos-compatible con** dirección.</span><span class="sxs-lookup"><span data-stu-id="1a698-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="1a698-118">Necesita estos tres valores al crear la aplicación **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="1a698-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Hoja de mensajería de IoT Hub de Azure Portal][6]

<span data-ttu-id="1a698-120">Ahora ha creado su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1a698-120">You have now created your IoT hub.</span></span> <span data-ttu-id="1a698-121">Tener Hola nombre de host del centro de IoT, cadena de conexión de centro de IoT, clave principal del centro de IoT, nombre de concentrador de eventos-compatible con y punto de conexión compatible de concentrador de eventos necesita toocomplete este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a698-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="1a698-122">Creación de una identidad de dispositivo</span><span class="sxs-lookup"><span data-stu-id="1a698-122">Create a device identity</span></span>
<span data-ttu-id="1a698-123">En esta sección, creará una aplicación de consola de Java que crea una identidad de dispositivo en el registro de la identidad de hello en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1a698-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="1a698-124">Un dispositivo no puede conectar tooIoT concentrador a menos que tenga una entrada en el registro de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a698-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="1a698-125">Para obtener más información, vea hello **del registro de identidad** sección de hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="1a698-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="1a698-126">Al ejecutar esta aplicación de consola, se generará un identificador de dispositivo único y clave que el dispositivo pueda usar tooidentify propio cuando el dispositivo a la nube sitio envía mensajes tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="1a698-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="1a698-127">Cree una carpeta vacía denominada iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="1a698-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="1a698-128">En carpeta iot java-get-iniciada hello, cree un proyecto de Maven denominado **identidad del dispositivo crear** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a698-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="1a698-129">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="1a698-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="1a698-130">En el símbolo del sistema, desplazarse por las carpetas de identidad del dispositivo crear toohello.</span><span class="sxs-lookup"><span data-stu-id="1a698-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="1a698-131">Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta de identidad del dispositivo crear Hola y agregue Hola después toohello de dependencia **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="1a698-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="1a698-132">Esta dependencia permite toouse Hola iot-servicio-paquete de cliente de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="1a698-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="1a698-133">Puede comprobar la versión más reciente de Hola de **cliente del servicio de iot** con [búsqueda Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="1a698-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="1a698-134">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="1a698-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="1a698-135">Con un editor de texto, abra el archivo create-device-identity\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="1a698-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="1a698-136">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="1a698-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="1a698-137">Agregar Hola después de las variables de nivel de clase toohello **aplicación** de la clase, reemplazando **{yourhubconnectionstring}** con hello valor su se indicó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1a698-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="1a698-138">Modificar firma Hola de hello **principal** método tooinclude Hola excepciones como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="1a698-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="1a698-139">Agregar Hola siguiente código como cuerpo del mensaje de Hola Hola **principal** método.</span><span class="sxs-lookup"><span data-stu-id="1a698-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="1a698-140">Este código crea un dispositivo denominado *javadevice* en el registro de identidades de IoT Hub, si no existe.</span><span class="sxs-lookup"><span data-stu-id="1a698-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="1a698-141">A continuación, muestra la Id. de dispositivo de Hola y la clave que necesita más adelante:</span><span class="sxs-lookup"><span data-stu-id="1a698-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
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
      // If hello device already exists.
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

10. <span data-ttu-id="1a698-142">Guarde y cierre el archivo de hello App.java.</span><span class="sxs-lookup"><span data-stu-id="1a698-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="1a698-143">Hola toobuild **identidad del dispositivo crear** aplicación con Maven, ejecutar el siguiente comando en línea de comandos de hello en la carpeta de identidad del dispositivo crear Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="1a698-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="1a698-144">Hola toorun **identidad del dispositivo crear** aplicación con Maven, ejecutar el siguiente comando en línea de comandos de hello en la carpeta de identidad del dispositivo crear Hola de hello:</span><span class="sxs-lookup"><span data-stu-id="1a698-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="1a698-145">Tome nota de hello **Id. de dispositivo** y **clave de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="1a698-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="1a698-146">Necesita estos valores más tarde cuando se crea una aplicación que se conecte tooIoT concentrador como un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1a698-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="1a698-147">Hola del registro de identidad de centro de IoT solo almacena centro de IoT toohello de dispositivo identidades tooenable un acceso seguro.</span><span class="sxs-lookup"><span data-stu-id="1a698-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="1a698-148">Toouse de identificadores y las claves de dispositivo almacena como credenciales de seguridad y una marca de habilitado/deshabilitado que puede usar acceso toodisable para un dispositivo individual.</span><span class="sxs-lookup"><span data-stu-id="1a698-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="1a698-149">Si la aplicación necesita toostore otros metadatos específicos del dispositivo, debe usar un almacén específico de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a698-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="1a698-150">Para obtener más información, vea hello [Guía del desarrollador de centro de IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="1a698-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="1a698-151">Recepción de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="1a698-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="1a698-152">En esta sección, creará una aplicación de consola de Java que lee los mensajes de dispositivo a nube desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1a698-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="1a698-153">Un centro de IoT expone un [concentrador de eventos][lnk-event-hubs-overview]-extremo compatible tooenable tooread mensajes de dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="1a698-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="1a698-154">tookeep cosas simples, en este tutorial se crea un lector básico que no es adecuado para una implementación de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1a698-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="1a698-155">Hola [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial muestra cómo los mensajes tooprocess dispositivo a la nube a escala.</span><span class="sxs-lookup"><span data-stu-id="1a698-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="1a698-156">Hola [empezar a trabajar con concentradores de eventos] [ lnk-eventhubs-tutorial] tutorial proporciona información adicional acerca de cómo tooprocess mensajes desde los centros de eventos y es aplicable toohello los puntos de conexión compatibles con eventos de centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1a698-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="1a698-157">Hola extremo compatible de concentrador de eventos para leer mensajes de dispositivo para la nube siempre utiliza Hola protocolo AMQP.</span><span class="sxs-lookup"><span data-stu-id="1a698-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="1a698-158">En la carpeta de hello iot java-get-iniciada por el que creó en hello *crear una identidad de dispositivo* sección, cree un proyecto de Maven denominado **leer mensajes de d2c** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a698-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="1a698-159">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="1a698-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="1a698-160">En el símbolo del sistema, desplazarse por las carpetas de toohello d2c de lectura de mensajes.</span><span class="sxs-lookup"><span data-stu-id="1a698-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="1a698-161">Con un editor de texto, abra el archivo de pom.xml de hello en la carpeta de d2c de lectura de mensajes de Hola y agregue Hola después toohello de dependencia **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="1a698-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="1a698-162">Esta dependencia permite toouse paquete de cliente eventhubs hello en su tooread de aplicación desde el punto de conexión de hello compatible de concentrador de eventos:</span><span class="sxs-lookup"><span data-stu-id="1a698-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="1a698-163">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="1a698-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="1a698-164">Con un editor de texto, abra el archivo read-d2c-messages\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="1a698-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="1a698-165">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="1a698-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="1a698-166">Agregar Hola después toohello variable de nivel de clase **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="1a698-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="1a698-167">Reemplace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, y **{youreventhubcompatiblename}** con valores de hello que anotó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1a698-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="1a698-168">Agregue los siguiente hello **receiveMessages** método toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="1a698-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="1a698-169">Este método crea un **EventHubClient** tooconnect toohello compatible con el concentrador de eventos extremo de la instancia y, a continuación, crea de forma asincrónica un **PartitionReceiver** tooread de instancia de un concentrador de eventos partición.</span><span class="sxs-lookup"><span data-stu-id="1a698-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="1a698-170">Se reproduce en bucle continuo y detalles del mensaje Hola se imprimen hasta que finaliza la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="1a698-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
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
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="1a698-171">Este método usa un filtro cuando se crea el receptor de Hola para que hello receptor solo lee los mensajes enviados tooIoT concentrador después de receptor de hello empieza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="1a698-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="1a698-172">Esta técnica es útil en un entorno de prueba para que pueda ver el conjunto actual de Hola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="1a698-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="1a698-173">En un entorno de producción, el código debe asegurarse de que procesa todos los mensajes de Hola - para obtener más información, vea hello [cómo tooprocess mensajes del dispositivo a la nube de centro de IoT] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a698-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="1a698-174">Modificar firma Hola de hello **principal** método tooinclude Hola excepción como sigue:</span><span class="sxs-lookup"><span data-stu-id="1a698-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="1a698-175">Agregar Hola después código toohello **principal** método Hola **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="1a698-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="1a698-176">Este código crea dos hello **EventHubClient** y **PartitionReceiver** instancias y le permite tooclose Hola aplicación cuando haya terminado de procesar los mensajes:</span><span class="sxs-lookup"><span data-stu-id="1a698-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
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
    > <span data-ttu-id="1a698-177">Este código supone que se creó el centro de IoT en nivel de hello F1 (gratis).</span><span class="sxs-lookup"><span data-stu-id="1a698-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="1a698-178">Una instancia gratuita de IoT Hub tiene dos particiones denominadas "0" y "1".</span><span class="sxs-lookup"><span data-stu-id="1a698-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="1a698-179">Guarde y cierre el archivo de hello App.java.</span><span class="sxs-lookup"><span data-stu-id="1a698-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="1a698-180">Hola toobuild **leer mensajes de d2c** aplicación con Maven, ejecutar el siguiente comando en línea de comandos de hello en carpeta de hello d2c de lectura de mensajes de Hola:</span><span class="sxs-lookup"><span data-stu-id="1a698-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="1a698-181">Creación de una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="1a698-181">Create a device app</span></span>
<span data-ttu-id="1a698-182">En esta sección, creará una aplicación de consola de Java que simula un dispositivo que envía el centro de IoT tooan de mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="1a698-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="1a698-183">En la carpeta de hello iot java-get-iniciada por el que creó en hello *crear una identidad de dispositivo* sección, cree un proyecto de Maven denominado **dispositivo simulado** mediante el siguiente comando en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="1a698-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="1a698-184">Observe que este es un comando único y largo:</span><span class="sxs-lookup"><span data-stu-id="1a698-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="1a698-185">En el símbolo del sistema, desplazarse por las carpetas de toohello dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="1a698-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="1a698-186">Con un editor de texto, abra archivo pom.xml de hello en la carpeta del dispositivo simulado de Hola y agregue Hola siguiendo las dependencias toohello **dependencias** nodo.</span><span class="sxs-lookup"><span data-stu-id="1a698-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="1a698-187">Esta dependencia permite toouse Hola el centro de IOT-java-paquete de cliente de su toocommunicate de aplicación con el centro de IoT y tooserialize tooJSON de objetos de Java:</span><span class="sxs-lookup"><span data-stu-id="1a698-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

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
    > <span data-ttu-id="1a698-188">Puede comprobar la versión más reciente de Hola de **cliente de dispositivo iot** con [búsqueda Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="1a698-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="1a698-189">Guarde y cierre el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="1a698-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="1a698-190">Con un editor de texto, abra el archivo simulated-device\src\main\java\com\mycompany\app\App.java de hello.</span><span class="sxs-lookup"><span data-stu-id="1a698-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="1a698-191">Agregue los siguiente hello **importar** archivo toohello de instrucciones:</span><span class="sxs-lookup"><span data-stu-id="1a698-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="1a698-192">Agregar Hola después de las variables de nivel de clase toohello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="1a698-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="1a698-193">Reemplazar **{youriothubname}** por el nombre del centro de IoT, y **{yourdevicekey}** con hello dispositivo clave-valor que generó en hello *crear una identidad de dispositivo* sección:</span><span class="sxs-lookup"><span data-stu-id="1a698-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="1a698-194">Esta aplicación de ejemplo usa hello **protocolo** variable cuando se crea una instancia de un **DeviceClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="1a698-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="1a698-195">Puede usar cualquier toocommunicate de protocolo hello MQTT, AMQP o HTTP con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1a698-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="1a698-196">Agregue los siguiente Hola anidados **TelemetryDataPoint** clase dentro de hello **aplicación** clase toospecify los datos de telemetría Hola el dispositivo envía tooyour centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="1a698-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

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
9. <span data-ttu-id="1a698-197">Agregue los siguiente Hola anidados **EventCallback** clase dentro de hello **aplicación** toodisplay Hola confirmación estado de la clase que Hola centro de IoT devuelve cuando procesa un mensaje de aplicación de dispositivo de hello.</span><span class="sxs-lookup"><span data-stu-id="1a698-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="1a698-198">Este método también notifica al subproceso principal de hello en aplicación hello cuando se ha procesado el mensaje de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="1a698-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="1a698-199">Agregue los siguiente Hola anidados **MessageSender** clase dentro de hello **aplicación** clase.</span><span class="sxs-lookup"><span data-stu-id="1a698-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="1a698-200">Hola **ejecutar** método en esta clase genera el centro de IoT de tooyour de toosend datos de telemetría de ejemplo y espera una confirmación antes de enviar mensajes de bienvenida del siguiente:</span><span class="sxs-lookup"><span data-stu-id="1a698-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

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

    <span data-ttu-id="1a698-201">Este método envía un nuevo mensaje de dispositivo para la nube un segundo después de centro de IoT Hola confirma los mensajes de bienvenida del anterior.</span><span class="sxs-lookup"><span data-stu-id="1a698-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="1a698-202">mensaje de bienvenida contiene un objeto JSON serializado con deviceId hello y genera de forma aleatoria los números toosimulate un sensor de temperatura y un sensor de humedad.</span><span class="sxs-lookup"><span data-stu-id="1a698-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="1a698-203">Reemplace hello **principal** método con hello después el código que crea un centro de IoT de tooyour de subproceso toosend mensajes del dispositivo a la nube:</span><span class="sxs-lookup"><span data-stu-id="1a698-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="1a698-204">Guarde y cierre el archivo de hello App.java.</span><span class="sxs-lookup"><span data-stu-id="1a698-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="1a698-205">Hola toobuild **dispositivo simulado** aplicación con Maven, ejecute hello siguiente comando en línea de comandos de hello en la carpeta del dispositivo simulado de hello:</span><span class="sxs-lookup"><span data-stu-id="1a698-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="1a698-206">tookeep cosas simples, este tutorial no implementa ninguna directiva de reintento.</span><span class="sxs-lookup"><span data-stu-id="1a698-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="1a698-207">En el código de producción, debe implementar directivas de reintento (por ejemplo, un retroceso exponencial), como se indica en el artículo de MSDN de hello [control de errores transitorios][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="1a698-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="1a698-208">Ejecutar aplicaciones de Hola</span><span class="sxs-lookup"><span data-stu-id="1a698-208">Run hello apps</span></span>

<span data-ttu-id="1a698-209">Ya estás listo toorun Hola aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1a698-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="1a698-210">En un símbolo del sistema en carpeta de lectura d2c hello, ejecute hello después toobegin comando primera partición de hello en el centro de IoT de supervisión:</span><span class="sxs-lookup"><span data-stu-id="1a698-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Mensajes de dispositivo a la nube de toomonitor de aplicación de servicio de centro de IoT de Java][7]

2. <span data-ttu-id="1a698-212">En un símbolo del sistema en la carpeta del dispositivo simulado de hello, ejecute hello después toobegin comando Enviar centro de IoT de tooyour de datos de telemetría:</span><span class="sxs-lookup"><span data-stu-id="1a698-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Mensajes de dispositivo a la nube de toosend de aplicación de dispositivo de centro de IoT de Java][8]

3. <span data-ttu-id="1a698-214">Hola **uso** el icono Servicios hello [portal de Azure] [ lnk-portal] muestra Hola número de mensajes enviados toohello centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="1a698-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portal uso icono que muestra el número de mensajes enviados tooIoT concentrador][43]

## <a name="next-steps"></a><span data-ttu-id="1a698-216">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a698-216">Next steps</span></span>
<span data-ttu-id="1a698-217">En este tutorial, configura un nuevo centro de IoT Hola portal de Azure y, a continuación, crea una identidad de dispositivo en el registro de identidad del centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="1a698-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="1a698-218">Usar este dispositivo identidad tooenable Hola dispositivo aplicación toosend mensajes del dispositivo a la nube toohello centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1a698-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="1a698-219">También crea una aplicación que muestra los mensajes de saludo recibidos por centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="1a698-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="1a698-220">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="1a698-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="1a698-221">[Conexión del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="1a698-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="1a698-222">[Introducción a la administración de dispositivos][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="1a698-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="1a698-223">[Introducción a Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="1a698-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="1a698-224">toolearn tooextend mensajes de dispositivo a la nube de su solución y proceso de IoT a escala, vea hello [procesar mensajes del dispositivo a la nube] [ lnk-process-d2c-tutorial] tutorial.</span><span class="sxs-lookup"><span data-stu-id="1a698-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
