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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Creación de un módulo de Azure IoT Edge con Node.js

Este tutorial muestra cómo toocreate un módulo para el borde de IoT de Azure en JS.

En este tutorial, recorreremos el programa de instalación de entorno y cómo toowrite una [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de convertidor de datos con los paquetes de NPM de borde de IoT de Azure más recientes de Hola.

## <a name="prerequisites"></a>Requisitos previos

En esta sección, configura el entorno para el desarrollo del módulo IoT Edge. Se aplica tooboth *Windows de 64 bits* y *Linux de 64 bits (Ubuntu 14 +)* sistemas operativos.

Hola siguiente software es necesario:
* [Cliente Git](https://git-scm.com/downloads).
* [Node LTS](https://nodejs.org).
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Arquitectura

plataforma de Hello borde de IoT de Azure con un alto grado adopta hello [arquitectura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Lo que significa que esa arquitectura de hello toda borde de IoT de Azure es un sistema que procesa la entrada y genera salida; y que cada módulo individual también es un subsistema de entrada / salida pequeño. En este tutorial, se introduce Hola después de dos módulos:

1. Un módulo que recibe una señal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulada y la convierte en un mensaje con formato [JSON](https://en.wikipedia.org/wiki/JSON).
2. Un módulo que imprime hello recibido [JSON](https://en.wikipedia.org/wiki/JSON) mensaje.

Hello siguiente imagen muestra flujo de datos de hello final típico tooend para este proyecto:

![Flujo de datos entre tres módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Procesador: Módulo de conversión; Salida: módulo de impresión")

## <a name="set-up-hello-environment"></a>Configurar el entorno de Hola
A continuación le mostramos cómo tooquickly configurar entorno toostart toowrite el primer módulo de convertidor Bilitar con JS.

### <a name="create-module-project"></a>Creación del proyecto de módulo
1. Abra una ventana de línea de comandos y ejecute `yo az-iot-gw-module`.
2. Siga los pasos de Hola durante la inicialización de hello pantalla toofinish Hola de su proyecto de módulo.

### <a name="project-structure"></a>Estructura del proyecto
Un proyecto de módulo JS consta de Hola de los componentes siguientes:

`modules`-Hola personalizar archivos de código fuente del módulo JS. Reemplazar predeterminado hello `sensor.js` y `printer.js` con sus propios archivos de módulo.

`app.js`-instancia de entrada archivo toostart hello borde de Hola.

`gw.config.json`-Hola configuración archivo toocustomize Hola módulos toobe cargado por borde.

`package.json`-Hola información de metadatos para el proyecto de módulo.

`README.md`-Hola documentación básica para el proyecto de módulo.


### <a name="package-file"></a>Archivo de paquete

Esto `package.json` declara toda la información de metadatos Hola necesaria para un proyecto de módulo que incluye las dependencias de nombre, versión, entrada, las secuencias de comandos, en tiempo de ejecución y desarrollo de Hola.

Después de fragmento de código muestra cómo tooconfigure para convertidor Bilitar proyecto de ejemplo.
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


### <a name="entry-file"></a>Archivo de entrada
Hola `app.js` define Hola forma tooinitialize hello borde instancia. Aquí no es necesario toomake cualquier cambio.

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

### <a name="interface-of-module"></a>Interfaz de módulo
Puede considerar un módulo de Azure IoT Edge como un procesador de datos cuyo trabajo es recibir una entrada, procesarla y generar una salida.

Hola entrada podría ser datos del hardware (por ejemplo, un detector de movimiento), un mensaje desde otros módulos, o cualquier otra cosa (por ejemplo, un número aleatorio generado periódicamente por un temporizador).

salida de Hello es similar toohello de entrada, podría desencadenar el comportamiento de hardware (por ejemplo, Hola parpadear LED), los módulos de tooother de un mensaje o cualquier otra cosa (por ejemplo, impresión de toohello de consola).

Los módulos se comunican entre sí mediante el objeto `message`. Hola **contenido** de un `message` es una matriz de bytes que es capaz de representar cualquier tipo de dato que quiera. **Propiedades** también están disponibles en hello `message` y son simplemente una asignación de cadena a la cadena. Se puede considerar **propiedades** como encabezados de hello en una solicitud HTTP, o sus metadatos de Hola de un archivo.

En orden toodevelop un módulo del borde de IoT de Azure en JS, deberá toocreate un nuevo objeto de módulo que implementa los métodos de hello necesario `receive()`. En este momento, también puede elegir tooimplement Hola opcional `create()` o `start()`, o `destroy()` métodos así. Hola siguiente fragmento de código se muestra que Hello scaffolding de objeto de módulo JS.

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

### <a name="converter-module"></a>Módulo de conversión
| Entrada                    | Procesador                              | Salida                 | Archivo de origen            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Mensaje de datos de temperatura | Análisis y construcción de un nuevo mensaje JSON | Mensaje JSON de estructura | `converter.js` |

Este módulo es un módulo Azure IoT Edge típico. Acepta mensajes de temperatura desde otros módulos (un módulo de hardware, o en este caso, nuestro módulo Bilitar simulada); y, a continuación, normaliza el mensaje de temperatura de hello en tooa estructurada de mensaje JSON (incluidas anexar Id. de mensaje de Hola, configuración de propiedad de Hola de si necesitamos alerta de temperatura de hello tootrigger y así sucesivamente).

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

### <a name="printer-module"></a>Módulo de impresión
| Entrada                          | Procesador | Salida                     | Archivo de origen          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Cualquier mensaje de otros módulos | N/D       | Inicie sesión tooconsole de mensaje de Hola | `printer.js` |

Este módulo es sencillo y fácil de entender, que genera la ventana de terminal toohello Hola recibe mensajes (propiedad, contenido).

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Configuración
Hola último paso antes de ejecutar módulos de hello es tooconfigure hello borde de IoT de Azure y las conexiones de hello tooestablish entre módulos.

Primero necesitamos toodeclare nuestro `node` cargador (desde el borde de IoT de Azure es compatible con cargadores de los distintos idiomas) que puede estar referenciada por su `name` en secciones de hello posteriormente.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

Una vez se han declarado nuestro cargadores, también es necesario toodeclare nuestros módulos así. Cargadores de hello toodeclaring similar, puede también hacer referencia a sus `name` atributo. Al declarar un módulo, necesitamos que el cargador de hello toospecify se debe utilizar (que debe ser Hola uno definimos antes) y Hola punto de entrada (debe ser el nombre de la clase normalizada de Hola de nuestro módulo) para cada módulo. Hola `simulated_device` módulo es un módulo nativo que se incluye en el paquete en tiempo de ejecución de hello borde de IoT de Azure core. Incluir `args` Hola JSON archivo incluso si se `null`.

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

Al final de Hola de configuración de hello, establecemos conexiones Hola. Cada conexión se expresa mediante `source` y `sink`. Ambos elementos deben hacer referencia a un módulo predefinido. mensaje de salida de Hello de `source` módulo se reenvía la entrada de toohello de `sink` módulo.

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

## <a name="running-hello-modules"></a>Ejecución de los módulos de Hola
1. `npm install`
2. `npm start`

Si desea que la aplicación de hello tooterminate, presione `<Enter>` clave.

> [!IMPORTANT]
> No se recomienda toouse Ctrl + C tooterminate hello borde IoT aplicación. Como este modo puede provocar Hola proceso tooterminate anormalmente.
