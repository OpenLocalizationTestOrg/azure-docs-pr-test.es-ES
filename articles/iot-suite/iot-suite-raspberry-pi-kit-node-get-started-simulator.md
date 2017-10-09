---
title: "un conjunto de IoT de frambuesa Pi tooAzure aaaConnect con Node.js simulada telemetría | Documentos de Microsoft"
description: "Utilice hello IoT Starter Kit de Microsoft Azure para hello frambuesa Pi 3 y conjunto de IoT de Azure. Usar Node.js tooconnect la solución de supervisión remota toohello de frambuesa Pi, enviar telemetría simulada toohello en la nube y responder toomethods invocado desde el panel de la solución de Hola."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: node.js
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: f65eeaa6e83fd89cdedae8fa8386a3e9ef8417d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-nodejs"></a>Conectar la solución de supervisión remota toohello de frambuesa Pi 3 y enviar telemetría simulada mediante Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Este tutorial muestra cómo toouse Hola frambuesa Pi 3 toosimulate temperatura y humedad datos toosend toohello en la nube. tutorial de Hello usa:

- SO Raspbian, Hola Node.js lenguaje de programación y hello IoT de Microsoft Azure SDK para Node.js tooimplement un dispositivo de ejemplo.
- supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure. implementación de Hello refleja una arquitectura empresarial real. tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él. Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Descargar y configurar el ejemplo hello

Ahora puede descargar y configurar la aplicación de cliente de supervisión remota de hello en el instalador de plataforma de frambuesa.

### <a name="install-nodejs"></a>Instalación de Node.js

Si aún no lo ha hecho, instale Node.js en su Raspberry Pi. Hola IoT SDK para Node.js requiere la versión 0.11.5 de Node.js o una versión posterior. Hello pasos siguientes muestran cómo tooinstall Node.js v6.10.2 en el instalador de plataforma de frambuesa:

1. Usar hello después tooupdate de comando su Pi frambuesa:

    ```sh
    sudo apt-get update
    ```

1. Usar hello después comando toodownload hello Node.js binarios tooyour frambuesa Pi:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Usar hello siguiendo los archivos binarios de comando tooinstall hello:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Usar hello después tooverify comando v6.10.2 Node.js se ha instalado correctamente:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Clonar repositorios de Hola

Si aún no lo ha hecho, Hola clon necesario repositorios ejecutando Hola siguiente comandos en un terminal de su Pi:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Actualizar la cadena de conexión de dispositivo de Hola

Archivo de código fuente de ejemplo de Hola abierto en hello **nano** editor mediante Hola siguiente comando:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Busque la línea de saludo:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Reemplace los valores de marcador de posición de Hola por hello información de dispositivos y centro de IoT creado y guardado en el inicio de Hola de este tutorial. Guarde los cambios (**O Ctrl**, **ENTRAR**) y salga del editor hello (**Ctrl-X**).

## <a name="run-hello-sample"></a>Ejecutar el ejemplo hello

Siguiente ejecución Hola comandos paquetes de requisitos previos de hello tooinstall de ejemplo de Hola:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator
npm install
```

Ahora puede ejecutar el programa de ejemplo de Hola en hello frambuesa Pi. Escriba el comando de hello:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/simulator/remote_monitoring.js
```

Hello resultados del ejemplo siguiente es un ejemplo de salida de hello, vea en línea de comandos de hello en hello frambuesa Pi:

![Salida de la aplicación Raspberry Pi][img-raspberry-output]

Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Pasos siguientes

Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-simulator/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
