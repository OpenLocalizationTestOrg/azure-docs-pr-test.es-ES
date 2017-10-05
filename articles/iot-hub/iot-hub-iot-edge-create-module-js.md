---
title: "Creación de un módulo de Azure IoT Edge con Node.js | Microsoft Docs"
description: "En este tutorial se muestra cómo escribir un módulo de conversión de datos BLE con el generador Yeoman y los paquetes NPM de Azure IoT Edge más recientes."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="63b67-103">Creación de un módulo de Azure IoT Edge con Node.js</span><span class="sxs-lookup"><span data-stu-id="63b67-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="63b67-104">En este tutorial se muestra cómo crear un módulo para Azure IoT Edge en JS.</span><span class="sxs-lookup"><span data-stu-id="63b67-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="63b67-105">En este tutorial se aborda la configuración de entorno y cómo escribir un módulo de conversión de datos [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) con los paquetes NPM de Azure IoT Edge más recientes.</span><span class="sxs-lookup"><span data-stu-id="63b67-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63b67-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="63b67-106">Prerequisites</span></span>

<span data-ttu-id="63b67-107">En esta sección, configura el entorno para el desarrollo del módulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="63b67-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="63b67-108">Se aplica a sistemas operativos *Windows de 64 bits* y *Linux de 64 bits (Ubuntu 14+)*.</span><span class="sxs-lookup"><span data-stu-id="63b67-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="63b67-109">Se requiere el software siguiente:</span><span class="sxs-lookup"><span data-stu-id="63b67-109">The following software is required:</span></span>
* <span data-ttu-id="63b67-110">[Cliente Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="63b67-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="63b67-111">[Node LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="63b67-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="63b67-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="63b67-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="63b67-113">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="63b67-113">Architecture</span></span>

<span data-ttu-id="63b67-114">La plataforma Azure IoT Edge adopta en gran medida la [arquitectura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="63b67-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="63b67-115">Esto significa que toda la arquitectura de Azure IoT Edge es un sistema que procesa entradas y genera salidas, y que cada módulo individual también es un pequeño subsistema de entrada-salida.</span><span class="sxs-lookup"><span data-stu-id="63b67-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="63b67-116">En este tutorial, se presentan los dos módulos siguientes:</span><span class="sxs-lookup"><span data-stu-id="63b67-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="63b67-117">Un módulo que recibe una señal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulada y la convierte en un mensaje con formato [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="63b67-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="63b67-118">Un módulo que imprime el mensaje [JSON](https://en.wikipedia.org/wiki/JSON) recibido.</span><span class="sxs-lookup"><span data-stu-id="63b67-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="63b67-119">La imagen siguiente muestra el flujo de datos de extremo a extremo típico para este proyecto:</span><span class="sxs-lookup"><span data-stu-id="63b67-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="63b67-120">![Flujo de datos entre tres módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Procesador: Módulo de conversión; Salida: módulo de impresión")</span><span class="sxs-lookup"><span data-stu-id="63b67-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="63b67-121">Configuración del entorno</span><span class="sxs-lookup"><span data-stu-id="63b67-121">Set up the environment</span></span>
<span data-ttu-id="63b67-122">A continuación se muestra cómo configura rápidamente el entorno para comenzar a escribir el primer módulo de conversión BLE con JS.</span><span class="sxs-lookup"><span data-stu-id="63b67-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="63b67-123">Creación del proyecto de módulo</span><span class="sxs-lookup"><span data-stu-id="63b67-123">Create module project</span></span>
1. <span data-ttu-id="63b67-124">Abra una ventana de línea de comandos y ejecute `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="63b67-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="63b67-125">Siga los pasos que aparecen en la pantalla para finalizar la inicialización del proyecto de módulo.</span><span class="sxs-lookup"><span data-stu-id="63b67-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="63b67-126">Estructura del proyecto</span><span class="sxs-lookup"><span data-stu-id="63b67-126">Project structure</span></span>
<span data-ttu-id="63b67-127">Un proyecto de módulo JS consta de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="63b67-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="63b67-128">`modules`: los archivos de origen del módulo JS personalizados.</span><span class="sxs-lookup"><span data-stu-id="63b67-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="63b67-129">Reemplace los archivos `sensor.js` y `printer.js` predeterminados por sus propios archivos de módulo.</span><span class="sxs-lookup"><span data-stu-id="63b67-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="63b67-130">`app.js`: el archivo de entrada para iniciar la instancia de Edge.</span><span class="sxs-lookup"><span data-stu-id="63b67-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="63b67-131">`gw.config.json`: el archivo de configuración para personalizar los módulos para que los cargue Edge.</span><span class="sxs-lookup"><span data-stu-id="63b67-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="63b67-132">`package.json`: la información de metadatos para el proyecto de módulo.</span><span class="sxs-lookup"><span data-stu-id="63b67-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="63b67-133">`README.md`: la documentación básica para el proyecto de módulo.</span><span class="sxs-lookup"><span data-stu-id="63b67-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="63b67-134">Archivo de paquete</span><span class="sxs-lookup"><span data-stu-id="63b67-134">Package file</span></span>

<span data-ttu-id="63b67-135">Este archivo `package.json` declara toda la información de metadatos necesaria para un proyecto de módulo que incluye el nombre, la versión, la entrada, los scripts, el entorno en tiempo de ejecución y las dependencias de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="63b67-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="63b67-136">El fragmento de código siguiente muestra cómo configurar para el proyecto de ejemplo de conversión BLE.</span><span class="sxs-lookup"><span data-stu-id="63b67-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a><span data-ttu-id="63b67-137">Archivo de entrada</span><span class="sxs-lookup"><span data-stu-id="63b67-137">Entry file</span></span>
<span data-ttu-id="63b67-138">El archivo `app.js` define la forma de inicializar la instancia de Edge.</span><span class="sxs-lookup"><span data-stu-id="63b67-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="63b67-139">Aquí no es necesario hacer ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="63b67-139">Here we don't need to make any change.</span></span>

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a><span data-ttu-id="63b67-140">Interfaz de módulo</span><span class="sxs-lookup"><span data-stu-id="63b67-140">Interface of module</span></span>
<span data-ttu-id="63b67-141">Puede considerar un módulo de Azure IoT Edge como un procesador de datos cuyo trabajo es recibir una entrada, procesarla y generar una salida.</span><span class="sxs-lookup"><span data-stu-id="63b67-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="63b67-142">La entrada pueden ser datos del hardware (como un detector de movimiento), un mensaje de otros módulos o cualquier otro elemento (como un número aleatorio que un temporizador genera periódicamente).</span><span class="sxs-lookup"><span data-stu-id="63b67-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="63b67-143">La salida es similar a la entrada, podría desencadenar un comportamiento de hardware (como un LED parpadeante), un mensaje a otros módulos o cualquier otro elemento (como imprimir en la consola).</span><span class="sxs-lookup"><span data-stu-id="63b67-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="63b67-144">Los módulos se comunican entre sí mediante el objeto `message`.</span><span class="sxs-lookup"><span data-stu-id="63b67-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="63b67-145">El **contenido** de un objeto `message` es una matriz de bytes capaz de representar cualquier tipo de datos que desee.</span><span class="sxs-lookup"><span data-stu-id="63b67-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="63b67-146">Las **propiedades** también están disponibles en el objeto `message` y son simplemente una asignación de cadena a cadena.</span><span class="sxs-lookup"><span data-stu-id="63b67-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="63b67-147">Puede considerar las **propiedades** como los encabezados de una solicitud HTTP o los metadatos de un archivo.</span><span class="sxs-lookup"><span data-stu-id="63b67-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="63b67-148">Para desarrollar un módulo de Azure IoT Edge en JS, debe crear un objeto de módulo nuevo que implemente los métodos requeridos `receive()`.</span><span class="sxs-lookup"><span data-stu-id="63b67-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="63b67-149">En este momento, también puede elegir implementar los métodos `create()`, `start()` o `destroy()` opcionales.</span><span class="sxs-lookup"><span data-stu-id="63b67-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="63b67-150">El fragmento de código siguiente muestra el scaffolding del objeto del módulo JS.</span><span class="sxs-lookup"><span data-stu-id="63b67-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a><span data-ttu-id="63b67-151">Módulo de conversión</span><span class="sxs-lookup"><span data-stu-id="63b67-151">Converter module</span></span>
| <span data-ttu-id="63b67-152">Entrada</span><span class="sxs-lookup"><span data-stu-id="63b67-152">Input</span></span>                    | <span data-ttu-id="63b67-153">Procesador</span><span class="sxs-lookup"><span data-stu-id="63b67-153">Processor</span></span>                              | <span data-ttu-id="63b67-154">Salida</span><span class="sxs-lookup"><span data-stu-id="63b67-154">Output</span></span>                 | <span data-ttu-id="63b67-155">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="63b67-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="63b67-156">Mensaje de datos de temperatura</span><span class="sxs-lookup"><span data-stu-id="63b67-156">Temperature data message</span></span> | <span data-ttu-id="63b67-157">Análisis y construcción de un nuevo mensaje JSON</span><span class="sxs-lookup"><span data-stu-id="63b67-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="63b67-158">Mensaje JSON de estructura</span><span class="sxs-lookup"><span data-stu-id="63b67-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="63b67-159">Este módulo es un módulo Azure IoT Edge típico.</span><span class="sxs-lookup"><span data-stu-id="63b67-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="63b67-160">Acepta mensajes de temperatura de otros módulos (un módulo de hardware o, en este caso, nuestro módulo BLE simulado) y, luego, normaliza el mensaje de temperatura en un mensaje JSON estructurado (incluido adjuntar el identificador de mensaje, establecer la propiedad que indica si es necesario desencadenar la alerta de temperatura, etc.).</span><span class="sxs-lookup"><span data-stu-id="63b67-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="63b67-161">Módulo de impresión</span><span class="sxs-lookup"><span data-stu-id="63b67-161">Printer module</span></span>
| <span data-ttu-id="63b67-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="63b67-162">Input</span></span>                          | <span data-ttu-id="63b67-163">Procesador</span><span class="sxs-lookup"><span data-stu-id="63b67-163">Processor</span></span> | <span data-ttu-id="63b67-164">Salida</span><span class="sxs-lookup"><span data-stu-id="63b67-164">Output</span></span>                     | <span data-ttu-id="63b67-165">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="63b67-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="63b67-166">Cualquier mensaje de otros módulos</span><span class="sxs-lookup"><span data-stu-id="63b67-166">Any message from other modules</span></span> | <span data-ttu-id="63b67-167">N/D</span><span class="sxs-lookup"><span data-stu-id="63b67-167">N/A</span></span>       | <span data-ttu-id="63b67-168">Registro del mensaje en la consola</span><span class="sxs-lookup"><span data-stu-id="63b67-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="63b67-169">Este módulo es simple y fácil de entender, y genera una salida de los mensajes recibidos (propiedad, contenido) en la ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="63b67-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="63b67-170">Configuración</span><span class="sxs-lookup"><span data-stu-id="63b67-170">Configuration</span></span>
<span data-ttu-id="63b67-171">El paso final antes de ejecutar los módulos es configurar Azure IoT Edge y establecer las conexiones entre los módulos.</span><span class="sxs-lookup"><span data-stu-id="63b67-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="63b67-172">Primero es necesario declarar el cargador `node` (debido a que Azure IoT Edge admite cargadores de distintos lenguajes) al que se podría hacer referencia mediante su `name` en las secciones más adelante.</span><span class="sxs-lookup"><span data-stu-id="63b67-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="63b67-173">Una vez que declaremos los cargadores, también es necesario declarar los módulos.</span><span class="sxs-lookup"><span data-stu-id="63b67-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="63b67-174">De manera similar a declarar los cargadores, también su atributo `name` podría hacer referencia a ellos.</span><span class="sxs-lookup"><span data-stu-id="63b67-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="63b67-175">Cuando se declara un módulo, es necesario especificar el cargador que debe usar (que debe ser el que se definió anteriormente) y el punto de entrada (que debe ser el nombre de clase normalizado de nuestro módulo) de cada módulo.</span><span class="sxs-lookup"><span data-stu-id="63b67-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="63b67-176">El módulo `simulated_device` es un módulo nativo que se incluye en el paquete en tiempo de ejecución principal de Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="63b67-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="63b67-177">Incluya `args` en el archivo JSON incluso si es `null`.</span><span class="sxs-lookup"><span data-stu-id="63b67-177">Include `args` in the JSON file even if it is `null`.</span></span>

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
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="63b67-178">Establecemos las conexiones al final de la configuración.</span><span class="sxs-lookup"><span data-stu-id="63b67-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="63b67-179">Cada conexión se expresa mediante `source` y `sink`.</span><span class="sxs-lookup"><span data-stu-id="63b67-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="63b67-180">Ambos elementos deben hacer referencia a un módulo predefinido.</span><span class="sxs-lookup"><span data-stu-id="63b67-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="63b67-181">El mensaje de salida del módulo `source` se desvía a la entrada del módulo `sink`.</span><span class="sxs-lookup"><span data-stu-id="63b67-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-the-modules"></a><span data-ttu-id="63b67-182">Ejecución de los módulos</span><span class="sxs-lookup"><span data-stu-id="63b67-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="63b67-183">Si desea finalizar la aplicación, presione la tecla `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="63b67-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63b67-184">No se recomienda usar Ctrl + C para finalizar la aplicación IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="63b67-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="63b67-185">Hacerlo podría provocar que el proceso se finaliza de forma anómala.</span><span class="sxs-lookup"><span data-stu-id="63b67-185">As this way may cause the process to terminate abnormally.</span></span>
