---
title: un conjunto de IoT mediante un NUC de Intel de puerta de enlace tooAzure aaaConnect | Documentos de Microsoft
description: "Utilice Hola hello y Kit de puerta de enlace de Microsoft IoT comercial remoto preconfigurada solución de supervisión. Usar una solución de supervisión remota de toohello de tooconnect de dispositivo de SensorTag de tooenable de puerta de enlace de borde de IoT de Azure de hello, enviar en la nube toohello telemetría y responder toomethods invocado desde el panel de la solución de Hola."
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
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Conectar su toohello de puerta de enlace de borde de IoT de Azure remoto solución preconfigurada de supervisión y enviar telemetría desde un SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Este tutorial muestra cómo toouse los datos de temperatura y humedad de toosend borde de IoT de Azure de supervisión remota de SensorTag dispositivo toohello había preconfigurado solución. Hola SensorTag conecta la puerta de enlace de toohello NUC de Intel con Bluetooth. tutorial de Hello usa:

- Azure IoT borde tooimplement una puerta de enlace de ejemplo.
- supervisión remota de Hello IoT conjunto había preconfigurado solución como back-end de hello en la nube.

## <a name="overview"></a>Información general

En este tutorial, se realizará Hola pasos:

- Implemente una instancia de hello remoto supervisión solución preconfigurada tooyour suscripción de Azure. Este paso implementa y configura varios servicios de Azure automáticamente.
- Configure su toocommunicate de dispositivo de puerta de enlace de Intel NUC con el equipo y la solución de supervisión remota de Hola.
- Configurar la telemetría de tooreceive de puerta de enlace de Intel NUC desde un dispositivo de SensorTag y envíelo toohello panel de supervisión remoto.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[SensorTag de Texas Instruments BLE][lnk-sensortag]. Este tutorial recupera los datos de telemetría a través de Bluetooth del dispositivo de SensorTag Hola.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hola disposiciones de solución de supervisión remoto un conjunto de servicios de Azure en su suscripción de Azure. implementación de Hello refleja una arquitectura empresarial real. tooavoid cargos de consumo innecesario de Azure, elimine la instancia de la solución de hello preconfigurado en azureiotsuite.com cuando haya terminado con él. Si necesita hello solución preconfigurada de nuevo, puede crearla fácilmente. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Configurar la conectividad de Bluetooth

Configurar el Bluetooth en hello NUC Intel tooenable hello SensorTag dispositivo tooconnect y enviar telemetría.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>Buscar la dirección MAC de Hola de hello SensorTag

1. En el shell de hello en hello NUC de Intel, ejecute hello después de comando toounblock Hola Bluetooth servicio:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Siguiente ejecución Hola comandos del servicio de Bluetooth toostart hello en hello NUC de Intel y escriba shell de hello Bluetooth:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Ejecute hello después toopower de comando en el controlador de hello Bluetooth:

    ```bash
    power on
    ```

    Cuando el controlador de hello está activada, verá un mensaje **cambiar power en se realizó correctamente**.

1. Ejecute hello después tooscan de comando para dispositivos Bluetooth cercanos:

    ```bash
    scan on
    ```

1. Presione Hola del botón de encendido en hello SensorTag toomake se puede detectar. Hola verde LED parpadea.

1. Cuando vea un mensaje en el shell de hello ese controlador Hola descubrió hello SensorTag, tome nota de la dirección MAC del dispositivo de Hola Hola. Hola dirección MAC es similar a **A0:E6:F8:B5:F6:00**. Necesita dirección MAC de hello más adelante en el tutorial Hola al configurar la puerta de enlace de Hola.

1. Ejecute hello después tooturn comando desactivado el análisis de Bluetooth:

    ```bash
    scan off
    ```

1. Ejecute hello después tooverify de comandos que puede conectarse toohello SensorTag dispositivo:

    ```bash
    connect <SensorTag MAC address>
    ```

    Si se conecta correctamente, el shell de hello muestra mensajes de bienvenida **conexión correcta** y se imprime información acerca del dispositivo de SensorTag Hola. Si no puede conectarse, compruebe hello que sensortag todavía está encendida.

1. Ahora puede desconectarse de hello SensorTag y ejecutar salir del shell de Bluetooth Hola Hola siguientes comandos:

    ```bash
    disconnect
    exit
    ```

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

script de compilación de Hello coloca módulo personalizado de borde de IoT de hello libsensor2remotemonitoring.so en la carpeta de compilación de Hola.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configurar y ejecutar Hola puerta de enlace de borde de IoT

Ahora puede configurar Hola telemetría de toosend de puerta de enlace de IoT borde de su tooyour de dispositivo SensorTag panel de supervisión remoto. Para obtener más información sobre cómo configurar una puerta de enlace y los módulos de IoT Edge, consulte [Conceptos de Azure IoT Edge][lnk-gateway-concepts].

> [!TIP]
> En este tutorial, utilice estándar hello `vi` editor de texto en hello NUC de Intel. Si no ha usado `vi` antes, debe completar un tutorial introductorio, como [Unix - Hola vi Editor Tutorial] [ lnk-vi-tutorial] toofamiliarize usted mismo con este editor. Como alternativa, puede instalar más fácil de usar hello [nano](https://www.nano-editor.org/) editor mediante el comando hello `smart install nano -y`.

Archivo de configuración de ejemplo de Hola abierto en hello **vi** editor mediante Hola siguiente comando:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
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
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Reemplace hello **macAddress** marcador de posición con hello dirección MAC de su SensorTag se ha indicado anteriormente. Reemplace hello **deviceID** y **deviceKey** marcadores de posición con identificadores de Hola y claves para dispositivos de hello dos que se creó anteriormente en la solución de supervisión remota Hola.

Busque Hola siguiendo las líneas en la configuración de hello para el módulo de Hola SensorTag:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Reemplace hello **dispositivo\_mac\_dirección** marcador de posición con hello dirección MAC de su SensorTag se ha indicado anteriormente.

Guarde los cambios.

Ahora puede ejecutar la puerta de enlace de hello con hello siguientes comandos:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Hola puerta de enlace de IoT borde comienza en hello NUC de Intel y envía la telemetría de hello SensorTag toohello solución de supervisión remota:

![Puerta de enlace de IoT borde envía telemetría de hello SensorTag][img-telemetry]

Presione **Ctrl-C** programa Hola de tooexit en cualquier momento.

## <a name="view-hello-telemetry"></a>Vista Hola telemetría

puerta de enlace de Hello ahora está enviando telemetría de hello SensorTag dispositivo toohello solución de supervisión. Puede ver la telemetría de hello en el panel de la solución de Hola. También puede enviar el dispositivo de SensorTag tooyour de comandos a través de puerta de enlace de Hola desde el panel de la solución de Hola.

- Vaya a Panel de solución toohello.
- Dispositivo Hola SELECT que configuró en la puerta de enlace de Hola que representa hello SensorTag Hola **tooView dispositivo** lista desplegable.
- telemetría Hello de dispositivo de SensorTag Hola se muestra en el panel de Hola.

![Mostrar la telemetría de hello SensorTag dispositivos][img-telemetry-display]

> [!WARNING]
> Si deja Hola supervisión de solución que se ejecuta en su cuenta de Azure remota, se le facturará por vez Hola que se ejecuta. Para obtener más información acerca de cómo reducir el consumo de Hola se ejecuta la solución de supervisión remota, consulte [configurar Azure IoT conjunto preconfigurado soluciones para fines de demostración][lnk-demo-config]. Eliminar soluciones Hola preconfigurado de su cuenta de Azure cuando termine de usarlo.


## <a name="next-steps"></a>Pasos siguientes

Visite hello [centro de desarrollo de Azure IoT](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y documentación sobre IoT de Azure.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started