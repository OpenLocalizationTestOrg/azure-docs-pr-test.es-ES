---
title: "un módulo de borde de IoT de Azure con Node.js aaaCreate | Documentos de Microsoft"
description: "Este tutorial muestra cómo toowrite una Bilitar datos convertidor módulo mediante Hola paquetes NPM de borde de IoT de Azure más recientes y Yeoman generador."
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
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="a5c48-103">Creación de un módulo de Azure IoT Edge con Node.js</span><span class="sxs-lookup"><span data-stu-id="a5c48-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="a5c48-104">Este tutorial muestra cómo toocreate un módulo para el borde de IoT de Azure en JS.</span><span class="sxs-lookup"><span data-stu-id="a5c48-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="a5c48-105">En este tutorial, recorreremos el programa de instalación de entorno y cómo toowrite una [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de convertidor de datos con los paquetes de NPM de borde de IoT de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5c48-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5c48-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a5c48-106">Prerequisites</span></span>

<span data-ttu-id="a5c48-107">En esta sección, configura el entorno para el desarrollo del módulo IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a5c48-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="a5c48-108">Se aplica tooboth *Windows de 64 bits* y *Linux de 64 bits (Ubuntu 14 +)* sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="a5c48-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="a5c48-109">Hola siguiente software es necesario:</span><span class="sxs-lookup"><span data-stu-id="a5c48-109">hello following software is required:</span></span>
* <span data-ttu-id="a5c48-110">[Cliente Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="a5c48-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="a5c48-111">[Node LTS](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a5c48-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="a5c48-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="a5c48-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="a5c48-113">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="a5c48-113">Architecture</span></span>

<span data-ttu-id="a5c48-114">plataforma de Hello borde de IoT de Azure con un alto grado adopta hello [arquitectura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="a5c48-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="a5c48-115">Lo que significa que esa arquitectura de hello toda borde de IoT de Azure es un sistema que procesa la entrada y genera salida; y que cada módulo individual también es un subsistema de entrada / salida pequeño.</span><span class="sxs-lookup"><span data-stu-id="a5c48-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="a5c48-116">En este tutorial, se introduce Hola después de dos módulos:</span><span class="sxs-lookup"><span data-stu-id="a5c48-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="a5c48-117">Un módulo que recibe una señal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulada y la convierte en un mensaje con formato [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="a5c48-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="a5c48-118">Un módulo que imprime hello recibido [JSON](https://en.wikipedia.org/wiki/JSON) mensaje.</span><span class="sxs-lookup"><span data-stu-id="a5c48-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="a5c48-119">Hello siguiente imagen muestra flujo de datos de hello final típico tooend para este proyecto:</span><span class="sxs-lookup"><span data-stu-id="a5c48-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="a5c48-120">![Flujo de datos entre tres módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Procesador: Módulo de conversión; Salida: módulo de impresión")</span><span class="sxs-lookup"><span data-stu-id="a5c48-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="a5c48-121">Configurar el entorno de Hola</span><span class="sxs-lookup"><span data-stu-id="a5c48-121">Set up hello environment</span></span>
<span data-ttu-id="a5c48-122">A continuación le mostramos cómo tooquickly configurar entorno toostart toowrite el primer módulo de convertidor Bilitar con JS.</span><span class="sxs-lookup"><span data-stu-id="a5c48-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="a5c48-123">Creación del proyecto de módulo</span><span class="sxs-lookup"><span data-stu-id="a5c48-123">Create module project</span></span>
1. <span data-ttu-id="a5c48-124">Abra una ventana de línea de comandos y ejecute `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="a5c48-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="a5c48-125">Siga los pasos de Hola durante la inicialización de hello pantalla toofinish Hola de su proyecto de módulo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="a5c48-126">Estructura del proyecto</span><span class="sxs-lookup"><span data-stu-id="a5c48-126">Project structure</span></span>
<span data-ttu-id="a5c48-127">Un proyecto de módulo JS consta de Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="a5c48-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="a5c48-128">`modules`-Hola personalizar archivos de código fuente del módulo JS.</span><span class="sxs-lookup"><span data-stu-id="a5c48-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="a5c48-129">Reemplazar predeterminado hello `sensor.js` y `printer.js` con sus propios archivos de módulo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="a5c48-130">`app.js`-instancia de entrada archivo toostart hello borde de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5c48-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="a5c48-131">`gw.config.json`-Hola configuración archivo toocustomize Hola módulos toobe cargado por borde.</span><span class="sxs-lookup"><span data-stu-id="a5c48-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="a5c48-132">`package.json`-Hola información de metadatos para el proyecto de módulo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="a5c48-133">`README.md`-Hola documentación básica para el proyecto de módulo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="a5c48-134">Archivo de paquete</span><span class="sxs-lookup"><span data-stu-id="a5c48-134">Package file</span></span>

<span data-ttu-id="a5c48-135">Esto `package.json` declara toda la información de metadatos Hola necesaria para un proyecto de módulo que incluye las dependencias de nombre, versión, entrada, las secuencias de comandos, en tiempo de ejecución y desarrollo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a5c48-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="a5c48-136">Después de fragmento de código muestra cómo tooconfigure para convertidor Bilitar proyecto de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="a5c48-137">Archivo de entrada</span><span class="sxs-lookup"><span data-stu-id="a5c48-137">Entry file</span></span>
<span data-ttu-id="a5c48-138">Hola `app.js` define Hola forma tooinitialize hello borde instancia.</span><span class="sxs-lookup"><span data-stu-id="a5c48-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="a5c48-139">Aquí no es necesario toomake cualquier cambio.</span><span class="sxs-lookup"><span data-stu-id="a5c48-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="a5c48-140">Interfaz de módulo</span><span class="sxs-lookup"><span data-stu-id="a5c48-140">Interface of module</span></span>
<span data-ttu-id="a5c48-141">Puede considerar un módulo de Azure IoT Edge como un procesador de datos cuyo trabajo es recibir una entrada, procesarla y generar una salida.</span><span class="sxs-lookup"><span data-stu-id="a5c48-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="a5c48-142">Hola entrada podría ser datos del hardware (por ejemplo, un detector de movimiento), un mensaje desde otros módulos, o cualquier otra cosa (por ejemplo, un número aleatorio generado periódicamente por un temporizador).</span><span class="sxs-lookup"><span data-stu-id="a5c48-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="a5c48-143">salida de Hello es similar toohello de entrada, podría desencadenar el comportamiento de hardware (por ejemplo, Hola parpadear LED), los módulos de tooother de un mensaje o cualquier otra cosa (por ejemplo, impresión de toohello de consola).</span><span class="sxs-lookup"><span data-stu-id="a5c48-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="a5c48-144">Los módulos se comunican entre sí mediante el objeto `message`.</span><span class="sxs-lookup"><span data-stu-id="a5c48-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="a5c48-145">Hola **contenido** de un `message` es una matriz de bytes que es capaz de representar cualquier tipo de dato que quiera.</span><span class="sxs-lookup"><span data-stu-id="a5c48-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="a5c48-146">**Propiedades** también están disponibles en hello `message` y son simplemente una asignación de cadena a la cadena.</span><span class="sxs-lookup"><span data-stu-id="a5c48-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="a5c48-147">Se puede considerar **propiedades** como encabezados de hello en una solicitud HTTP, o sus metadatos de Hola de un archivo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="a5c48-148">En orden toodevelop un módulo del borde de IoT de Azure en JS, deberá toocreate un nuevo objeto de módulo que implementa los métodos de hello necesario `receive()`.</span><span class="sxs-lookup"><span data-stu-id="a5c48-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="a5c48-149">En este momento, también puede elegir tooimplement Hola opcional `create()` o `start()`, o `destroy()` métodos así.</span><span class="sxs-lookup"><span data-stu-id="a5c48-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="a5c48-150">Hola siguiente fragmento de código se muestra que Hello scaffolding de objeto de módulo JS.</span><span class="sxs-lookup"><span data-stu-id="a5c48-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="a5c48-151">Módulo de conversión</span><span class="sxs-lookup"><span data-stu-id="a5c48-151">Converter module</span></span>
| <span data-ttu-id="a5c48-152">Entrada</span><span class="sxs-lookup"><span data-stu-id="a5c48-152">Input</span></span>                    | <span data-ttu-id="a5c48-153">Procesador</span><span class="sxs-lookup"><span data-stu-id="a5c48-153">Processor</span></span>                              | <span data-ttu-id="a5c48-154">Salida</span><span class="sxs-lookup"><span data-stu-id="a5c48-154">Output</span></span>                 | <span data-ttu-id="a5c48-155">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="a5c48-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="a5c48-156">Mensaje de datos de temperatura</span><span class="sxs-lookup"><span data-stu-id="a5c48-156">Temperature data message</span></span> | <span data-ttu-id="a5c48-157">Análisis y construcción de un nuevo mensaje JSON</span><span class="sxs-lookup"><span data-stu-id="a5c48-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="a5c48-158">Mensaje JSON de estructura</span><span class="sxs-lookup"><span data-stu-id="a5c48-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="a5c48-159">Este módulo es un módulo Azure IoT Edge típico.</span><span class="sxs-lookup"><span data-stu-id="a5c48-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="a5c48-160">Acepta mensajes de temperatura desde otros módulos (un módulo de hardware, o en este caso, nuestro módulo Bilitar simulada); y, a continuación, normaliza el mensaje de temperatura de hello en tooa estructurada de mensaje JSON (incluidas anexar Id. de mensaje de Hola, configuración de propiedad de Hola de si necesitamos alerta de temperatura de hello tootrigger y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="a5c48-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
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

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="a5c48-161">Módulo de impresión</span><span class="sxs-lookup"><span data-stu-id="a5c48-161">Printer module</span></span>
| <span data-ttu-id="a5c48-162">Entrada</span><span class="sxs-lookup"><span data-stu-id="a5c48-162">Input</span></span>                          | <span data-ttu-id="a5c48-163">Procesador</span><span class="sxs-lookup"><span data-stu-id="a5c48-163">Processor</span></span> | <span data-ttu-id="a5c48-164">Salida</span><span class="sxs-lookup"><span data-stu-id="a5c48-164">Output</span></span>                     | <span data-ttu-id="a5c48-165">Archivo de origen</span><span class="sxs-lookup"><span data-stu-id="a5c48-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="a5c48-166">Cualquier mensaje de otros módulos</span><span class="sxs-lookup"><span data-stu-id="a5c48-166">Any message from other modules</span></span> | <span data-ttu-id="a5c48-167">N/D</span><span class="sxs-lookup"><span data-stu-id="a5c48-167">N/A</span></span>       | <span data-ttu-id="a5c48-168">Inicie sesión tooconsole de mensaje de Hola</span><span class="sxs-lookup"><span data-stu-id="a5c48-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="a5c48-169">Este módulo es sencillo y fácil de entender, que genera la ventana de terminal toohello Hola recibe mensajes (propiedad, contenido).</span><span class="sxs-lookup"><span data-stu-id="a5c48-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="a5c48-170">Configuración</span><span class="sxs-lookup"><span data-stu-id="a5c48-170">Configuration</span></span>
<span data-ttu-id="a5c48-171">Hola último paso antes de ejecutar módulos de hello es tooconfigure hello borde de IoT de Azure y las conexiones de hello tooestablish entre módulos.</span><span class="sxs-lookup"><span data-stu-id="a5c48-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="a5c48-172">Primero necesitamos toodeclare nuestro `node` cargador (desde el borde de IoT de Azure es compatible con cargadores de los distintos idiomas) que puede estar referenciada por su `name` en secciones de hello posteriormente.</span><span class="sxs-lookup"><span data-stu-id="a5c48-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="a5c48-173">Una vez se han declarado nuestro cargadores, también es necesario toodeclare nuestros módulos así.</span><span class="sxs-lookup"><span data-stu-id="a5c48-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="a5c48-174">Cargadores de hello toodeclaring similar, puede también hacer referencia a sus `name` atributo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="a5c48-175">Al declarar un módulo, necesitamos que el cargador de hello toospecify se debe utilizar (que debe ser Hola uno definimos antes) y Hola punto de entrada (debe ser el nombre de la clase normalizada de Hola de nuestro módulo) para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="a5c48-176">Hola `simulated_device` módulo es un módulo nativo que se incluye en el paquete en tiempo de ejecución de hello borde de IoT de Azure core.</span><span class="sxs-lookup"><span data-stu-id="a5c48-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="a5c48-177">Incluir `args` Hola JSON archivo incluso si se `null`.</span><span class="sxs-lookup"><span data-stu-id="a5c48-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="a5c48-178">Al final de Hola de configuración de hello, establecemos conexiones Hola.</span><span class="sxs-lookup"><span data-stu-id="a5c48-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="a5c48-179">Cada conexión se expresa mediante `source` y `sink`.</span><span class="sxs-lookup"><span data-stu-id="a5c48-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="a5c48-180">Ambos elementos deben hacer referencia a un módulo predefinido.</span><span class="sxs-lookup"><span data-stu-id="a5c48-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="a5c48-181">mensaje de salida de Hello de `source` módulo se reenvía la entrada de toohello de `sink` módulo.</span><span class="sxs-lookup"><span data-stu-id="a5c48-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="a5c48-182">Ejecución de los módulos de Hola</span><span class="sxs-lookup"><span data-stu-id="a5c48-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="a5c48-183">Si desea que la aplicación de hello tooterminate, presione `<Enter>` clave.</span><span class="sxs-lookup"><span data-stu-id="a5c48-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5c48-184">No se recomienda toouse Ctrl + C tooterminate hello borde IoT aplicación.</span><span class="sxs-lookup"><span data-stu-id="a5c48-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="a5c48-185">Como este modo puede provocar Hola proceso tooterminate anormalmente.</span><span class="sxs-lookup"><span data-stu-id="a5c48-185">As this way may cause hello process tooterminate abnormally.</span></span>
