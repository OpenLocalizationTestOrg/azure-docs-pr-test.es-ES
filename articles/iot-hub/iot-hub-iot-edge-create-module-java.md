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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Creación de un módulo de Azure IoT Edge con Java

En este tutorial se muestra cómo compilar un módulo para Azure IoT Edge en Java.

En este tutorial, se le guiará a través de la configuración del entorno y cómo toowrite una [Bilitar](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) módulo de convertidor de datos con los paquetes de Azure IoT borde Maven más recientes de Hola.

## <a name="prerequisites"></a>Requisitos previos

En esta sección, configurará el entorno para el desarrollo del módulo IoT Edge. Se aplica tooboth *Windows de 64 bits* y *Linux de 64 bits (8 Debian y Ubuntu)* sistemas operativos.

Hola siguiente software es necesario:

* [Cliente Git](https://git-scm.com/downloads).
* [**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* [Maven](https://maven.apache.org/install.html).

Abra una línea de comandos Hola terminal de ventana y clone después de repositorio:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Arquitectura global

plataforma de Hello borde de IoT de Azure con un alto grado adopta hello [arquitectura Von Neumann](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Lo que significa que esa arquitectura de hello toda borde de IoT de Azure es un sistema que procesa la entrada y genera salida; y que cada módulo individual también es un subsistema de entrada / salida pequeño. En este tutorial, se explicará Hola después de dos módulos:

1. Un módulo que recibe una señal [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) simulada y la convierte en un mensaje con formato [JSON](https://en.wikipedia.org/wiki/JSON).
2. Un módulo que imprime hello recibido [JSON](https://en.wikipedia.org/wiki/JSON) mensaje.

Hello siguiente imagen muestra hello típica-to-end de flujo de datos para este proyecto:

![Flujo de datos entre tres módulos](media/iot-hub-iot-edge-create-module/dataflow.png "Entrada: módulo BLE simulado; Procesador: Módulo de conversión; Salida: módulo de impresión")

## <a name="understanding-hello-code"></a>Comprensión del código de hello

### <a name="maven-project-structure"></a>Estructura del proyecto Maven

Puesto que los paquetes de borde de IoT de Azure se basan en Maven, es necesario toocreate una estructura de proyectos de Maven típica, que contiene un `pom.xml` archivo.

Hello POM hereda de hello `com.microsoft.azure.gateway.gateway-module-base` paquete, que declara todas las dependencias de hello necesarias para un proyecto de módulo que incluye los archivos binarios de hello en tiempo de ejecución, ruta de acceso de archivo de configuración de puerta de enlace de Hola y comportamiento de ejecución de Hola de. Esto nos ahorra una gran cantidad de tiempo y eliminar Hola necesidad toowrite y vuelva a escribir una y otra vez cientos de líneas de código.

Necesitamos tooupdate el archivo pom.xml declarando Hola requiere dependencias/plugins y el nombre de Hola de toobe de archivo de configuración de hello utilizado por el módulo como se muestra en el siguiente fragmento de código de hello.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Descripción básica de un módulo de Azure IoT Edge

Puede considerar un módulo de Azure IoT Edge como un procesador de datos cuyo trabajo es recibir una entrada, procesarla y generar una salida.

Hola entrada podría ser datos del hardware (por ejemplo, un detector de movimiento), un mensaje desde otros módulos, o cualquier otra cosa (por ejemplo, un número aleatorio generado periódicamente por un temporizador).

salida de Hello es similar toohello de entrada, podría desencadenar el comportamiento de hardware (por ejemplo, Hola parpadear LED), los módulos de tooother de un mensaje o cualquier otra cosa (por ejemplo, impresión de toohello de consola).

Los módulos se comunican entre sí mediante la clase `com.microsoft.azure.gateway.messaging.Message`. Hola **contenido** de un `Message` es una matriz de bytes que se puede representar cualquier tipo de datos que desee. **Propiedades** también están disponibles en hello `Message` y son simplemente una asignación de cadena a la cadena. Se puede considerar **propiedades** como encabezados de hello en una solicitud HTTP, o sus metadatos de Hola de un archivo.

En orden toodevelop un módulo de borde de IoT de Azure en Java, deberá toocreate una nueva clase de módulo que se hereda de `com.microsoft.azure.gateway.core.GatewayModule` e implementar los métodos abstractos de hello necesario `receive()` y `destroy()`. En este momento, también puede elegir tooimplement Hola opcional `start()` o `create()` también métodos. Hola siguiente fragmento de código muestra cómo tooget inicia la creación de un módulo de borde de IoT de Azure.

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

### <a name="converter-module"></a>Módulo de conversión

| Entrada                    | Procesador                              | Salida                 | Archivo de origen            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Mensaje de datos de temperatura | Análisis y construcción de un nuevo mensaje JSON | Mensaje JSON de estructura | `ConverterModule.java` |

Este módulo es un módulo Azure IoT Edge típico. Acepta mensajes de temperatura desde otros módulos (un módulo de hardware, o en este caso, nuestro módulo Bilitar simulada); y, a continuación, normaliza el mensaje de temperatura de hello en tooa estructurada de mensaje JSON (incluidas anexar Id. de mensaje de Hola, configuración de propiedad de Hola de si necesitamos alerta de temperatura de hello tootrigger y así sucesivamente).

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

### <a name="printer-module"></a>Módulo de impresión

| Entrada                          | Procesador | Salida                     | Archivo de origen          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Cualquier mensaje de otros módulos | N/D       | Inicie sesión tooconsole de mensaje de Hola | `PrinterModule.java` |

Se trata de un módulo sencillo y fácil de entender, que genera la ventana de terminal toohello Hola recibe mensajes.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Configuración de Azure IoT Edge

Hola último paso antes de ejecutar módulos de hello es tooconfigure hello borde de IoT de Azure y las conexiones de hello tooestablish entre módulos.

Primero necesitamos toodeclare nuestro cargador de Java (desde el borde de IoT de Azure es compatible con cargadores de los distintos idiomas) que puede estar referenciada por su `name` en secciones de hello posteriormente.

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

Una vez se han declarado nuestro cargadores, también tendrá toodeclare nuestros módulos así. Cargadores de hello toodeclaring similar, puede también hacer referencia a sus `name` atributo. Al declarar un módulo, necesitamos que el cargador de hello toospecify se debe utilizar (que debe ser Hola uno definimos antes) y Hola punto de entrada (debe ser el nombre de la clase normalizada de Hola de nuestro módulo) para cada módulo. Hola `simulated_device` módulo es un módulo nativo que se incluye en el paquete en tiempo de ejecución de hello borde de IoT de Azure core. Siempre debe incluir `args` Hola JSON archivo incluso si se `null`.

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

Al final de Hola de configuración de hello, establecemos conexiones Hola. Cada conexión se expresa mediante `source` y `sink`. Ambos elementos deben hacer referencia a un módulo predefinido. mensaje de salida de Hello de `source` módulo se reenviarán entrada toohello de `sink` módulo.

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

## <a name="running-hello-modules"></a>Ejecución de los módulos de Hola

Use `mvn package` toobuild todo en hello `target/` carpeta. También se recomienda `mvn clean package` para realizar una compilación limpia.

Use `mvn exec:exec` toorun hello borde de IoT de Azure y se debe tener en cuenta que los datos de temperatura de Hola y todas las propiedades de hello son consola toohello impreso con una tarifa fija.

Si desea que la aplicación de hello tooterminate, presione `<Enter>` clave.

> [!IMPORTANT]
> No se recomienda toouse Ctrl + C tooterminate hello borde IoT aplicación de puerta de enlace. Como esto puede provocar Hola proceso tooterminate anormalmente.

