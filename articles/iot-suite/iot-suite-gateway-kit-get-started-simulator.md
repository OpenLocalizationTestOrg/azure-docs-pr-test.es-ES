---
title: un conjunto de IoT mediante un NUC de Intel de puerta de enlace tooAzure aaaConnect | Documentos de Microsoft
description: "Utilice Hola hello y Kit de puerta de enlace de Microsoft IoT comercial remoto preconfigurada solución de supervisión. Hola utilice Azure IoT borde puerta de enlace tooconnect toohello solución de supervisión, enviar telemetría simulada toohello en la nube y responder toomethods invoca desde el panel de la solución de Hola."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Conectar su toohello de puerta de enlace de borde de IoT de Azure remoto solución preconfigurada de supervisión y enviar telemetría simulada

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Este tutorial muestra cómo toosimulate temperatura de toouse borde de IoT de Azure y la supervisión remota de humedad datos toosend toohello preconfigurado solución. tutorial de Hello usa:

- Azure IoT borde tooimplement una puerta de enlace de ejemplo.
- supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.

## <a name="overview"></a>Información general

En este tutorial, se realizará Hola pasos:

- Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure. Este paso implementa y configura varios servicios de Azure automáticamente.
- Configure su toocommunicate de dispositivo de puerta de enlace de Intel NUC con el equipo y la solución de supervisión remota de Hola.
- Configurar hello toosend de puerta de enlace de IoT borde simulados telemetría que se puede ver en el panel de la solución de Hola.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure. implementación de Hello refleja una arquitectura empresarial real. tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él. Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Repita Hola anteriores pasos tooadd un segundo dispositivo con un Id. de dispositivo como **device02**. ejemplo de Hola envía datos de dos dispositivos simulados en la solución de supervisión remota toohello Hola puerta de enlace.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Crear el módulo personalizado de borde de IoT de Hola

Ahora puede compilar módulo IoT borde personalizado Hola que permite Hola puerta de enlace toosend mensajes toohello solución de supervisión. Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].

Descargar código de fuente de Hola para módulos personalizados de borde de IoT de Hola desde GitHub con hello siguientes comandos:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Crear el módulo de IoT borde personalizado de hello mediante Hola siguientes comandos:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilación de Hello coloca módulo personalizado de borde de IoT de hello libsimulator.so en la carpeta de compilación de Hola.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurar y ejecutar Hola puerta de enlace de borde de IoT

Ahora puede configurar hello borde IoT puerta de enlace toosend telemetría simulada tooyour remoto panel de supervisión. Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> En este tutorial, utilice estándar hello `vi` editor de texto en hello NUC de Intel. Si no ha usado `vi` antes, debe completar un tutorial introductorio, como [Unix - Hola vi Editor Tutorial] [ lnk-vi-tutorial] toofamiliarize usted mismo con este editor. Como alternativa, puede instalar más fácil de usar hello [nano](https://www.nano-editor.org/) editor mediante el comando hello `smart install nano -y`.

Archivo de configuración de ejemplo de Hola abierto en hello **vi** editor mediante Hola siguiente comando:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
```

Busque Hola siguiendo las líneas en la configuración de hello para el módulo de hello el centro de IOT:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Reemplace el marcador de posición de hello valores con información de centro de IoT creado y guardado en Hola Hola inicio de este tutorial. valor de Hola para IoTHubName es similar a **yourrmsolution37e08**, y valor hello IoTSuffix es normalmente **devices.net azure**.

Busque Hola siguiendo las líneas en la configuración de hello para el módulo de asignación de hello:

```json
args": [
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Reemplace hello **deviceID** y **deviceKey** marcadores de posición con identificadores de Hola y claves para dispositivos de hello dos que se creó anteriormente en la solución de supervisión remota Hola.

Guarde los cambios.

Ahora puede ejecutar Hola comandos de puerta de enlace de IoT borde con hello siguientes:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

puerta de enlace de Hello comienza en hello NUC de Intel y envía la solución de supervisión remota de telemetría simulada toohello:

![La puerta de enlace de IoT Edge genera telemetría simulada.][img-simulated telemetry]

Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.

## <a name="view-hello-telemetry"></a>Vista Hola telemetría

Hola puerta de enlace de IoT borde ahora está enviando telemetría simulada toohello solución de supervisión remoto. Puede ver la telemetría de hello en el panel de la solución de Hola.

- Vaya a Panel de solución toohello.
- Seleccione uno de los dispositivos de hello dos que configuró en la puerta de enlace de Hola Hola **tooView dispositivo** lista desplegable.
- telemetría Hola desde dispositivos de puerta de enlace de Hola se muestra en el panel de Hola.

![Mostrar la telemetría de dispositivos de puerta de enlace de hello simulada][img-telemetry-display]

> [!WARNING]
> Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config]. Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.

## <a name="next-steps"></a>Pasos siguientes

Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started