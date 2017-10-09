---
title: "un módulo de borde de IoT de Azure con Java aaaCreate | Documentos de Microsoft"
description: "Este tutorial muestra cómo toowrite una Bilitar datos convertidor módulo mediante Hola paquetes de Azure IoT borde Maven más recientes."
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
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="831c3-103">Creación de un módulo de Azure IoT Edge con Java</span><span class="sxs-lookup"><span data-stu-id="831c3-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="831c3-104">En este tutorial se muestra cómo compilar un módulo para Azure IoT Edge en Java.</span><span class="sxs-lookup"><span data-stu-id="831c3-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="831c3-105">En este tutorial, se le guiará a través de la configuración del entorno y cómo toowrite una [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de convertidor de datos con los paquetes de Azure IoT borde Maven más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="831c3-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="831c3-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="831c3-106">Prerequisites</span></span>

<span data-ttu-id="831c3-107">En esta sección, configurará el entorno para el desarrollo del módulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="831c3-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="831c3-108">Se aplica tooboth *Windows de 64 bits* y *Linux de 64 bits (8 Debian y Ubuntu)* sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="831c3-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="831c3-109">Hola siguiente software es necesario:</span><span class="sxs-lookup"><span data-stu-id="831c3-109">hello following software is required:</span></span>

* <span data-ttu-id="831c3-110">[Cliente Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="831c3-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="831c3-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="831c3-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="831c3-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="831c3-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="831c3-113">Abra una línea de comandos Hola terminal de ventana y clone después de repositorio:</span><span class="sxs-lookup"><span data-stu-id="831c3-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="831c3-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="831c3-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="831c3-115">Arquitectura global</span><span class="sxs-lookup"><span data-stu-id="831c3-115">Overall architecture</span></span>

<span data-ttu-id="831c3-116">plataforma de Hello borde de IoT de Azure con un alto grado adopta hello [arquitectura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="831c3-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="831c3-117">Lo que significa que esa arquitectura de hello toda borde de IoT de Azure es un sistema que procesa la entrada y genera salida; y que cada módulo individual también es un subsistema de entrada / salida pequeño.</span><span class="sxs-lookup"><span data-stu-id="831c3-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="831c3-118">En este tutorial, se explicará Hola después de dos módulos:</span><span class="sxs-lookup"><span data-stu-id="831c3-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="831c3-119">Un módulo que recibe una señal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulada y la convierte en un mensaje con formato [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="831c3-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="831c3-120">Un módulo que imprime hello recibido [JSON](https://en.wikipedia.org/wiki/JSON) mensaje.</span><span class="sxs-lookup"><span data-stu-id="831c3-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="831c3-121">Hello siguiente imagen muestra hello típica-to-end de flujo de datos para este proyecto:</span><span class="sxs-lookup"><span data-stu-id="831c3-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="831c3-122">![Flujo de datos entre tres módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Procesador: Módulo de conversión; Salida: módulo de impresión")</span><span class="sxs-lookup"><span data-stu-id="831c3-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="831c3-123">Comprensión del código de hello</span><span class="sxs-lookup"><span data-stu-id="831c3-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="831c3-124">Estructura del proyecto Maven</span><span class="sxs-lookup"><span data-stu-id="831c3-124">Maven project structure</span></span>

<span data-ttu-id="831c3-125">Puesto que los paquetes de borde de IoT de Azure se basan en Maven, es necesario toocreate una estructura de proyectos de Maven típica, que contiene un `pom.xml` archivo.</span><span class="sxs-lookup"><span data-stu-id="831c3-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="831c3-126">Hello POM hereda de hello `com.microsoft.azure.gateway.gateway-module-base` paquete, que declara todas las dependencias de hello necesarias para un proyecto de módulo que incluye los archivos binarios de hello en tiempo de ejecución, ruta de acceso de archivo de configuración de puerta de enlace de Hola y comportamiento de ejecución de Hola de.</span><span class="sxs-lookup"><span data-stu-id="831c3-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="831c3-127">Esto nos ahorra una gran cantidad de tiempo y eliminar Hola necesidad toowrite y vuelva a escribir una y otra vez cientos de líneas de código.</span><span class="sxs-lookup"><span data-stu-id="831c3-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="831c3-128">Necesitamos tooupdate el archivo pom.xml declarando Hola requiere dependencias/plugins y el nombre de Hola de toobe de archivo de configuración de hello utilizado por el módulo como se muestra en el siguiente fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="831c3-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

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

  <!-- Set hello filename of hello Azure IoT Edge configuration located
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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="831c3-129">Descripción básica de un módulo de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="831c3-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="831c3-130">Puede considerar un módulo de Azure IoT Edge como un procesador de datos cuyo trabajo es recibir una entrada, procesarla y generar una salida.</span><span class="sxs-lookup"><span data-stu-id="831c3-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="831c3-131">Hola entrada podría ser datos del hardware (por ejemplo, un detector de movimiento), un mensaje desde otros módulos, o cualquier otra cosa (por ejemplo, un número aleatorio generado periódicamente por un temporizador).</span><span class="sxs-lookup"><span data-stu-id="831c3-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="831c3-132">salida de Hello es similar toohello de entrada, podría desencadenar el comportamiento de hardware (por ejemplo, Hola parpadear LED), los módulos de tooother de un mensaje o cualquier otra cosa (por ejemplo, impresión de toohello de consola).</span><span class="sxs-lookup"><span data-stu-id="831c3-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="831c3-133">Los módulos se comunican entre sí mediante la clase `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="831c3-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="831c3-134">Hola **contenido** de un `Message` es una matriz de bytes que se puede representar cualquier tipo de datos que desee.</span><span class="sxs-lookup"><span data-stu-id="831c3-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="831c3-135">**Propiedades** también están disponibles en hello `Message` y son simplemente una asignación de cadena a la cadena.</span><span class="sxs-lookup"><span data-stu-id="831c3-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="831c3-136">Se puede considerar **propiedades** como encabezados de hello en una solicitud HTTP, o sus metadatos de Hola de un archivo.</span><span class="sxs-lookup"><span data-stu-id="831c3-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="831c3-137">En orden toodevelop un módulo de borde de IoT de Azure en Java, deberá toocreate una nueva clase de módulo que se hereda de `com.microsoft.azure.gateway.core.GatewayModule` e implementar los métodos abstractos de hello necesario `receive()` y `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="831c3-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="831c3-138">En este momento, también puede elegir tooimplement Hola opcional `start()` o `create()` también métodos.</span><span class="sxs-lookup"><span data-stu-id="831c3-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="831c3-139">Hola siguiente fragmento de código muestra cómo tooget inicia la creación de un módulo de borde de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="831c3-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="831c3-140">Módulo de conversión</span><span class="sxs-lookup"><span data-stu-id="831c3-140">Converter module</span></span>

| <span data-ttu-id="831c3-141">Entrada</span><span class="sxs-lookup"><span data-stu-id="831c3-141">Input</span></span>                    | <span data-ttu-id="831c3-142">Procesador</span><span class="sxs-lookup"><span data-stu-id="831c3-142">Processor</span></span>                              | <span data-ttu-id="831c3-143">Salida</span><span class="sxs-lookup"><span data-stu-id="831c3-143">Output</span></span>                 | <span data-ttu-id="831c3-144">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="831c3-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="831c3-145">Mensaje de datos de temperatura</span><span class="sxs-lookup"><span data-stu-id="831c3-145">Temperature data message</span></span> | <span data-ttu-id="831c3-146">Análisis y construcción de un nuevo mensaje JSON</span><span class="sxs-lookup"><span data-stu-id="831c3-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="831c3-147">Mensaje JSON de estructura</span><span class="sxs-lookup"><span data-stu-id="831c3-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="831c3-148">Este módulo es un módulo Azure IoT Edge típico.</span><span class="sxs-lookup"><span data-stu-id="831c3-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="831c3-149">Acepta mensajes de temperatura desde otros módulos (un módulo de hardware, o en este caso, nuestro módulo Bilitar simulada); y, a continuación, normaliza el mensaje de temperatura de hello en tooa estructurada de mensaje JSON (incluidas anexar Id. de mensaje de Hola, configuración de propiedad de Hola de si necesitamos alerta de temperatura de hello tootrigger y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="831c3-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="831c3-150">Módulo de impresión</span><span class="sxs-lookup"><span data-stu-id="831c3-150">Printer module</span></span>

| <span data-ttu-id="831c3-151">Entrada</span><span class="sxs-lookup"><span data-stu-id="831c3-151">Input</span></span>                          | <span data-ttu-id="831c3-152">Procesador</span><span class="sxs-lookup"><span data-stu-id="831c3-152">Processor</span></span> | <span data-ttu-id="831c3-153">Salida</span><span class="sxs-lookup"><span data-stu-id="831c3-153">Output</span></span>                     | <span data-ttu-id="831c3-154">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="831c3-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="831c3-155">Cualquier mensaje de otros módulos</span><span class="sxs-lookup"><span data-stu-id="831c3-155">Any message from other modules</span></span> | <span data-ttu-id="831c3-156">N/D</span><span class="sxs-lookup"><span data-stu-id="831c3-156">N/A</span></span>       | <span data-ttu-id="831c3-157">Inicie sesión tooconsole de mensaje de Hola</span><span class="sxs-lookup"><span data-stu-id="831c3-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="831c3-158">Se trata de un módulo sencillo y fácil de entender, que genera la ventana de terminal toohello Hola recibe mensajes.</span><span class="sxs-lookup"><span data-stu-id="831c3-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="831c3-159">Configuración de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="831c3-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="831c3-160">Hola último paso antes de ejecutar módulos de hello es tooconfigure hello borde de IoT de Azure y las conexiones de hello tooestablish entre módulos.</span><span class="sxs-lookup"><span data-stu-id="831c3-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="831c3-161">Primero necesitamos toodeclare nuestro cargador de Java (desde el borde de IoT de Azure es compatible con cargadores de los distintos idiomas) que puede estar referenciada por su `name` en secciones de hello posteriormente.</span><span class="sxs-lookup"><span data-stu-id="831c3-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

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

<span data-ttu-id="831c3-162">Una vez se han declarado nuestro cargadores, también tendrá toodeclare nuestros módulos así.</span><span class="sxs-lookup"><span data-stu-id="831c3-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="831c3-163">Cargadores de hello toodeclaring similar, puede también hacer referencia a sus `name` atributo.</span><span class="sxs-lookup"><span data-stu-id="831c3-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="831c3-164">Al declarar un módulo, necesitamos que el cargador de hello toospecify se debe utilizar (que debe ser Hola uno definimos antes) y Hola punto de entrada (debe ser el nombre de la clase normalizada de Hola de nuestro módulo) para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="831c3-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="831c3-165">Hola `simulated_device` módulo es un módulo nativo que se incluye en el paquete en tiempo de ejecución de hello borde de IoT de Azure core.</span><span class="sxs-lookup"><span data-stu-id="831c3-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="831c3-166">Siempre debe incluir `args` Hola JSON archivo incluso si se `null`.</span><span class="sxs-lookup"><span data-stu-id="831c3-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="831c3-167">Al final de Hola de configuración de hello, establecemos conexiones Hola.</span><span class="sxs-lookup"><span data-stu-id="831c3-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="831c3-168">Cada conexión se expresa mediante `source` y `sink`.</span><span class="sxs-lookup"><span data-stu-id="831c3-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="831c3-169">Ambos elementos deben hacer referencia a un módulo predefinido.</span><span class="sxs-lookup"><span data-stu-id="831c3-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="831c3-170">mensaje de salida de Hello de `source` módulo se reenviarán entrada toohello de `sink` módulo.</span><span class="sxs-lookup"><span data-stu-id="831c3-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="831c3-171">Ejecución de los módulos de Hola</span><span class="sxs-lookup"><span data-stu-id="831c3-171">Running hello modules</span></span>

<span data-ttu-id="831c3-172">Use `mvn package` toobuild todo en hello `target/` carpeta.</span><span class="sxs-lookup"><span data-stu-id="831c3-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="831c3-173">También se recomienda `mvn clean package` para realizar una compilación limpia.</span><span class="sxs-lookup"><span data-stu-id="831c3-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="831c3-174">Use `mvn exec:exec` toorun hello borde de IoT de Azure y se debe tener en cuenta que los datos de temperatura de Hola y todas las propiedades de hello son consola toohello impreso con una tarifa fija.</span><span class="sxs-lookup"><span data-stu-id="831c3-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="831c3-175">Si desea que la aplicación de hello tooterminate, presione `<Enter>` clave.</span><span class="sxs-lookup"><span data-stu-id="831c3-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="831c3-176">No se recomienda toouse Ctrl + C tooterminate hello borde IoT aplicación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="831c3-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="831c3-177">Como esto puede provocar Hola proceso tooterminate anormalmente.</span><span class="sxs-lookup"><span data-stu-id="831c3-177">As this may cause hello process tooterminate abnormally.</span></span>

