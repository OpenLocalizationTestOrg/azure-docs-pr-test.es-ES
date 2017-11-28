---
title: "Creación de un módulo de Azure IoT Edge con Java | Microsoft Docs"
description: "En este tutorial se muestra cómo escribir un módulo de conversión de datos BLE con los paquetes Maven de Azure IoT Edge más recientes."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: 0c430272225d79737baec2be15ed7c93991cdeac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="8545c-103">Creación de un módulo de Azure IoT Edge con Java</span><span class="sxs-lookup"><span data-stu-id="8545c-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="8545c-104">En este tutorial se muestra cómo compilar un módulo para Azure IoT Edge en Java.</span><span class="sxs-lookup"><span data-stu-id="8545c-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="8545c-105">En este tutorial se abordará la configuración de entorno y cómo escribir un módulo de conversión de datos [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) con los paquetes Maven de Azure IoT Edge más recientes.</span><span class="sxs-lookup"><span data-stu-id="8545c-105">In this tutorial, we will walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8545c-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8545c-106">Prerequisites</span></span>

<span data-ttu-id="8545c-107">En esta sección, configurará el entorno para el desarrollo del módulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8545c-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="8545c-108">Se aplica a sistemas operativos *Windows de 64 bits* y *Linux de 64 bits (Ubuntu/Debian 8)*.</span><span class="sxs-lookup"><span data-stu-id="8545c-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="8545c-109">Se requiere el software siguiente:</span><span class="sxs-lookup"><span data-stu-id="8545c-109">The following software is required:</span></span>

* <span data-ttu-id="8545c-110">[Cliente Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="8545c-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="8545c-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="8545c-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="8545c-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="8545c-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="8545c-113">Abra una ventana de terminal de línea de comandos y clone el repositorio siguiente:</span><span class="sxs-lookup"><span data-stu-id="8545c-113">Open a command-line terminal window and clone the following repository:</span></span>

1. <span data-ttu-id="8545c-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="8545c-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="8545c-115">Arquitectura global</span><span class="sxs-lookup"><span data-stu-id="8545c-115">Overall architecture</span></span>

<span data-ttu-id="8545c-116">La plataforma Azure IoT Edge adopta en gran medida la [arquitectura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="8545c-116">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="8545c-117">Esto significa que toda la arquitectura de Azure IoT Edge es un sistema que procesa entradas y genera salidas, y que cada módulo individual también es un pequeño subsistema de entrada-salida.</span><span class="sxs-lookup"><span data-stu-id="8545c-117">Which means that the entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="8545c-118">En este tutorial, se presentarán los dos módulos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8545c-118">In this tutorial, we will introduce the following two modules:</span></span>

1. <span data-ttu-id="8545c-119">Un módulo que recibe una señal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulada y la convierte en un mensaje con formato [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="8545c-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="8545c-120">Un módulo que imprime el mensaje [JSON](https://en.wikipedia.org/wiki/JSON) recibido.</span><span class="sxs-lookup"><span data-stu-id="8545c-120">A module which prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="8545c-121">La imagen siguiente muestra el flujo de datos de un extremo a otro típico para este proyecto:</span><span class="sxs-lookup"><span data-stu-id="8545c-121">The following image displays the typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="8545c-122">![Flujo de datos entre tres módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Procesador: Módulo de conversión; Salida: módulo de impresión")</span><span class="sxs-lookup"><span data-stu-id="8545c-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="8545c-123">Descripción del código</span><span class="sxs-lookup"><span data-stu-id="8545c-123">Understanding the code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="8545c-124">Estructura del proyecto Maven</span><span class="sxs-lookup"><span data-stu-id="8545c-124">Maven project structure</span></span>

<span data-ttu-id="8545c-125">Como los paquetes de Azure IoT Edge se basan en Maven, es necesario crear una estructura de proyecto Maven típica, que contiene un archivo `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="8545c-125">Since Azure IoT Edge packages are based on Maven, we need to create a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="8545c-126">El archivo POM se hereda del paquete `com.microsoft.azure.gateway.gateway-module-base`, que declara todas las dependencias que un proyecto de módulo necesita, que incluye los archivos binarios en tiempo de ejecución, la ruta de acceso al archivo de configuración de puerta de enlace y el comportamiento de ejecución.</span><span class="sxs-lookup"><span data-stu-id="8545c-126">The POM inherits from the `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of the dependencies needed by a module project which includes the runtime binaries, the gateway configuration file path, and the execution behavior.</span></span> <span data-ttu-id="8545c-127">Esto permite ahorrar mucho tiempo y elimina la necesidad de escribir y reescribir cientos de líneas de código una y otra vez.</span><span class="sxs-lookup"><span data-stu-id="8545c-127">This saves us lots of time and eliminate the need to write and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="8545c-128">Es necesario actualizar el archivo pom.xml mediante la declaración de las dependencias/complementos requeridos y el nombre del archivo de configuración que el módulo usará, como se muestra en el siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="8545c-128">We need to update the pom.xml file by declaring the required dependencies/plugins and the name of the configuration file to be used by our module as shown in the following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set the filename of the Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="8545c-129">Descripción básica de un módulo de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="8545c-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="8545c-130">Puede considerar un módulo de Azure IoT Edge como un procesador de datos cuyo trabajo es recibir una entrada, procesarla y generar una salida.</span><span class="sxs-lookup"><span data-stu-id="8545c-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="8545c-131">La entrada pueden ser datos del hardware (como un detector de movimiento), un mensaje de otros módulos o cualquier otro elemento (como un número aleatorio que un temporizador genera periódicamente).</span><span class="sxs-lookup"><span data-stu-id="8545c-131">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="8545c-132">La salida es similar a la entrada, podría desencadenar un comportamiento de hardware (como un LED parpadeante), un mensaje a otros módulos o cualquier otro elemento (como imprimir en la consola).</span><span class="sxs-lookup"><span data-stu-id="8545c-132">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="8545c-133">Los módulos se comunican entre sí mediante la clase `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="8545c-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="8545c-134">El **contenido** de un objeto `Message` es una matriz de bytes capaz de representar cualquier tipo de datos que desee.</span><span class="sxs-lookup"><span data-stu-id="8545c-134">The **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="8545c-135">Las **propiedades** también están disponibles en el objeto `Message` y son simplemente una asignación de cadena a cadena.</span><span class="sxs-lookup"><span data-stu-id="8545c-135">**Properties** are also available in the `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="8545c-136">Puede considerar las **propiedades** como los encabezados de una solicitud HTTP o los metadatos de un archivo.</span><span class="sxs-lookup"><span data-stu-id="8545c-136">You may think of **Properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="8545c-137">Para desarrollar un módulo de Azure IoT Edge en Java, debe crear una nueva clase de módulo que se hereda de `com.microsoft.azure.gateway.core.GatewayModule` e implementar los métodos abstractos `receive()` y `destroy()` requeridos.</span><span class="sxs-lookup"><span data-stu-id="8545c-137">In order to develop an Azure IoT Edge module in Java, you need to create a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement the required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="8545c-138">En este momento, también puede elegir implementar los métodos `start()` o `create()` opcionales.</span><span class="sxs-lookup"><span data-stu-id="8545c-138">At this point, you may also choose to implement the optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="8545c-139">El fragmento de código siguiente muestra cómo comenzar a crear un módulo de Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8545c-139">The following code snippet shows you how to get started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let the GatewayModule do the dirty work of initialization. It's also
       a good time to parse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire the resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time to release all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic to process the input message. This method is required. */
    // ...
    /* Use publish() method to do the output. You are
       allowed to publish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="8545c-140">Módulo de conversión</span><span class="sxs-lookup"><span data-stu-id="8545c-140">Converter module</span></span>

| <span data-ttu-id="8545c-141">Entrada</span><span class="sxs-lookup"><span data-stu-id="8545c-141">Input</span></span>                    | <span data-ttu-id="8545c-142">Procesador</span><span class="sxs-lookup"><span data-stu-id="8545c-142">Processor</span></span>                              | <span data-ttu-id="8545c-143">Salida</span><span class="sxs-lookup"><span data-stu-id="8545c-143">Output</span></span>                 | <span data-ttu-id="8545c-144">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="8545c-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="8545c-145">Mensaje de datos de temperatura</span><span class="sxs-lookup"><span data-stu-id="8545c-145">Temperature data message</span></span> | <span data-ttu-id="8545c-146">Análisis y construcción de un nuevo mensaje JSON</span><span class="sxs-lookup"><span data-stu-id="8545c-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="8545c-147">Mensaje JSON de estructura</span><span class="sxs-lookup"><span data-stu-id="8545c-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="8545c-148">Este módulo es un módulo Azure IoT Edge típico.</span><span class="sxs-lookup"><span data-stu-id="8545c-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="8545c-149">Acepta mensajes de temperatura de otros módulos (un módulo de hardware o, en este caso, nuestro módulo BLE simulado) y, luego, normaliza el mensaje de temperatura en un mensaje JSON estructurado (incluido adjuntar el identificador de mensaje, establecer la propiedad que indica si es necesario desencadenar la alerta de temperatura, etc.).</span><span class="sxs-lookup"><span data-stu-id="8545c-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="8545c-150">Módulo de impresión</span><span class="sxs-lookup"><span data-stu-id="8545c-150">Printer module</span></span>

| <span data-ttu-id="8545c-151">Entrada</span><span class="sxs-lookup"><span data-stu-id="8545c-151">Input</span></span>                          | <span data-ttu-id="8545c-152">Procesador</span><span class="sxs-lookup"><span data-stu-id="8545c-152">Processor</span></span> | <span data-ttu-id="8545c-153">Salida</span><span class="sxs-lookup"><span data-stu-id="8545c-153">Output</span></span>                     | <span data-ttu-id="8545c-154">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="8545c-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="8545c-155">Cualquier mensaje de otros módulos</span><span class="sxs-lookup"><span data-stu-id="8545c-155">Any message from other modules</span></span> | <span data-ttu-id="8545c-156">N/D</span><span class="sxs-lookup"><span data-stu-id="8545c-156">N/A</span></span>       | <span data-ttu-id="8545c-157">Registro del mensaje en la consola</span><span class="sxs-lookup"><span data-stu-id="8545c-157">Log the message to console</span></span> | `PrinterModule.java` |

<span data-ttu-id="8545c-158">Este módulo es simple y fácil de entender, y genera una salida de los mensajes recibidos en la ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="8545c-158">This is a simple, self-explanatory, module which outputs the received messages to the terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="8545c-159">Configuración de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="8545c-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="8545c-160">El paso final antes de ejecutar los módulos es configurar Azure IoT Edge y establecer las conexiones entre los módulos.</span><span class="sxs-lookup"><span data-stu-id="8545c-160">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="8545c-161">Primero es necesario declarar el cargador de Java (debido a que Azure IoT Edge admite cargadores de distintos lenguajes) al que se podría hacer referencia mediante su `name` en las secciones más adelante.</span><span class="sxs-lookup"><span data-stu-id="8545c-161">First we need to declare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="8545c-162">Una vez que declaremos los cargadores, también será necesario declarar los módulos.</span><span class="sxs-lookup"><span data-stu-id="8545c-162">Once we have declared our loaders, we will also need to declare our modules as well.</span></span> <span data-ttu-id="8545c-163">De manera similar a declarar los cargadores, también su atributo `name` podría hacer referencia a ellos.</span><span class="sxs-lookup"><span data-stu-id="8545c-163">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="8545c-164">Cuando se declara un módulo, es necesario especificar el cargador que debe usar (que debe ser el que se definió anteriormente) y el punto de entrada (que debe ser el nombre de clase normalizado de nuestro módulo) de cada módulo.</span><span class="sxs-lookup"><span data-stu-id="8545c-164">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="8545c-165">El módulo `simulated_device` es un módulo nativo que se incluye en el paquete en tiempo de ejecución principal de Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8545c-165">The `simulated_device` module is a native module which is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="8545c-166">Siempre debe incluir `args` en el archivo JSON incluso si es `null`.</span><span class="sxs-lookup"><span data-stu-id="8545c-166">You should always include `args` in the JSON file even if it is `null`.</span></span>

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="8545c-167">Establecemos las conexiones al final de la configuración.</span><span class="sxs-lookup"><span data-stu-id="8545c-167">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="8545c-168">Cada conexión se expresa mediante `source` y `sink`.</span><span class="sxs-lookup"><span data-stu-id="8545c-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="8545c-169">Ambos elementos deben hacer referencia a un módulo predefinido.</span><span class="sxs-lookup"><span data-stu-id="8545c-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="8545c-170">El mensaje de salida del módulo `source` se desviará a la entrada del módulo `sink`.</span><span class="sxs-lookup"><span data-stu-id="8545c-170">The output message of `source` module will be forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="8545c-171">Ejecución de los módulos</span><span class="sxs-lookup"><span data-stu-id="8545c-171">Running the modules</span></span>

<span data-ttu-id="8545c-172">Use `mvn package` para compilar todo en la carpeta `target/`.</span><span class="sxs-lookup"><span data-stu-id="8545c-172">Use `mvn package` to build everything into the `target/` folder.</span></span> <span data-ttu-id="8545c-173">También se recomienda `mvn clean package` para realizar una compilación limpia.</span><span class="sxs-lookup"><span data-stu-id="8545c-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="8545c-174">Use `mvn exec:exec` para ejecutar Azure IoT Edge y debería ver que los datos de temperatura y todas las propiedades se imprimen en la consola a una tarifa fija.</span><span class="sxs-lookup"><span data-stu-id="8545c-174">Use `mvn exec:exec` to run the Azure IoT Edge and you should observe that the temperature data and all the properties are printed to the console at a fixed rate.</span></span>

<span data-ttu-id="8545c-175">Si desea finalizar la aplicación, presione la tecla `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="8545c-175">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8545c-176">No se recomienda usar Ctrl + C para finalizar la aplicación de puerta de enlace de IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8545c-176">It is not recommended to use Ctrl + C to terminate the IoT Edge gateway application.</span></span> <span data-ttu-id="8545c-177">Esto podría provocar que el proceso se finalice de forma anómala.</span><span class="sxs-lookup"><span data-stu-id="8545c-177">As this may cause the process to terminate abnormally.</span></span>

