---
title: "aaaUse un dispositivo físico con borde de IoT de Azure | Documentos de Microsoft"
description: "¿Cómo toouse un centro de IoT Texas instrumentos SensorTag dispositivo toosend datos tooan a través de una puerta de enlace de IoT borde ejecutando en un dispositivo de frambuesa Pi 3. puerta de enlace de Hola se basa en el borde de IoT de Azure."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Usar Azure IoT arista en un tooIoT de mensajes del dispositivo a la nube de frambuesa Pi tooforward concentrador

En este tutorial de hello [ejemplo de baja energía Bluetooth] [ lnk-ble-samplecode] muestra cómo toouse [Azure IoT borde] [ lnk-sdk] para:

* Reenviar tooIoT concentrador de telemetría de dispositivo para la nube desde un dispositivo físico.
* Comandos de la ruta de dispositivo físico de centro de IoT tooa.

En este tutorial, se describen los siguientes procedimientos:

* **Arquitectura**: información de arquitectura importante acerca de los ejemplos de hello Bluetooth baja energía.
* **Compile y ejecute**: Hola pasos necesarios toobuild y ejemplo de Hola de ejecución.

## <a name="architecture"></a>Arquitectura

Hola tutorial muestra cómo toobuild y ejecutar una puerta de enlace de IoT borde con frambuesa Pi 3 que ejecuta Raspbian Linux. puerta de enlace de Hola se basa en el borde de IoT. ejemplo de Hola usa una Texas instrumentos SensorTag Bluetooth baja energía (n) dispositivo toocollect temperatura de datos.

Cuando ejecute hello puerta de enlace de IoT borde:

* Conecta tooa SensorTag dispositivo mediante Protocolo de hello Bluetooth baja energía (n).
* Se conecta tooIoT concentrador mediante Protocolo de hello HTTP.
* Reenvía la telemetría de hello SensorTag dispositivo tooIoT concentrador.
* Enruta los comandos de dispositivo de centro de IoT toohello SensorTag.

puerta de enlace de Hello contiene Hola después módulos IoT borde:

* A *módulo Bilitar* que interactúa con una Bilitar dispositivo tooreceive temperatura de datos del dispositivo de Hola y enviar comandos toohello.
* A *módulo de Bilitar nube toodevice* que convierte los mensajes JSON enviados desde el centro de IoT en las instrucciones de BLE de Hola *módulo Bilitar*.
* A *módulo registrador* que registra todos los archivos locales de puerta de enlace mensajes tooa.
* Un *módulo de asignación de identidad* que traduce entre direcciones MAC de los dispositivos BLE y las identidades de los dispositivos de Azure IoT Hub.
* Un *módulo Centro de IoT* que carga centro de IoT de tooan de datos de telemetría y recibe los comandos de dispositivo de un centro de IoT.
* A *módulo de impresora Bilitar* que interprete la telemetría de dispositivo de hello Bilitar e imprime datos con formato toohello consola tooenable problemas y depuración.

### <a name="how-data-flows-through-hello-gateway"></a>Cómo fluyen los datos a través de puerta de enlace de Hola

Hello después de diagrama de bloques muestra la canalización de flujo de datos de carga de telemetría de hello:

![Canalización de puerta de enlace de carga de telemetría](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

pasos de Hola que un elemento de telemetría toma desplazan desde un tooIoT de dispositivo Bilitar concentrador son:

1. dispositivo de Hello Bilitar genera una muestra de temperatura y lo envía a través del módulo de Bluetooth toohello BLE en puerta de enlace de Hola.
1. módulo BLE de Hello recibe el ejemplo hello y publica a broker toohello junto con la dirección MAC de hello de dispositivo de Hola.
1. módulo de asignación de identidad de Hello toma este mensaje y utiliza un Hola de tootranslate tabla interna dirección MAC del dispositivo de hello en una identidad de dispositivo del centro de IoT. Una identidad de dispositivo de IoT Hub consta de un identificador de dispositivo y una clave de dispositivo.
1. módulo de asignación de identidad de Hello publica un mensaje nuevo que contiene datos de ejemplo de Hola temperatura, dirección MAC de hello de dispositivo de hello, Id. de dispositivo de Hola y clave de dispositivo de Hola.
1. Hola módulo Centro de IoT recibe este mensaje nuevo (generado por el módulo de asignación de identidad de hello) y lo publica tooIoT concentrador.
1. módulo de registrador Hola registra todos los mensajes de archivo local de hello broker tooa.

Hello después de diagrama de bloques muestra la canalización de flujo de datos de hello dispositivo comandos:

![Canalización de puerta de enlace de comandos de dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Hola módulo sondea periódicamente el centro de IoT Hola centro de IoT para nuevos mensajes de comando.
1. Cuando Hola módulo Centro de IoT recibe un nuevo mensaje de comando, publica a toohello broker.
1. módulo de asignación de identidad de Hello recoge el mensaje de bienvenida de comando y usa un Hola de tabla interna tootranslate dispositivo de tooa de Id. de dispositivo de centro de IoT dirección MAC. A continuación, publica un mensaje nuevo que incluye la dirección MAC de hello de dispositivo de destino de hello en mapa de propiedades de hello del mensaje de bienvenida.
1. módulo BLE en la nube al dispositivo de Hello toma este mensaje y lo convierte en la instrucción de Bilitar apropiado hello para el módulo de Bilitar Hola. Luego publica un mensaje nuevo.
1. módulo BLE de Hello toma este mensaje y ejecuta la instrucción de E/S de hello mediante la comunicación con dispositivos de Bilitar Hola.
1. módulo de registrador Hola registra todos los mensajes de archivo de disco de hello broker tooa.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial, necesita una suscripción activa de Azure.

> [!NOTE]
> En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].

Se necesita al cliente SSH en su tooenable de máquina de escritorio tooremotely acceso Hola la línea de comandos en hello frambuesa Pi.

- Windows no incluye ningún cliente SSH. Se recomienda usar [PuTTY](http://www.putty.org/).
- La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad SSH de línea de comandos de Hola. Para más información, consulte [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH cuando se usa Linux o Mac OS).

## <a name="prepare-your-hardware"></a>Preparar el hardware

Este tutorial se supone que usa un [SensorTag de instrumentos Texas](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo conectado tooa frambuesa Pi 3 ejecutando Raspbian.

### <a name="install-raspbian"></a>Instalación de Raspbian

Puede utilizar cualquiera de hello después opciones tooinstall Raspbian en el dispositivo de frambuesa Pi 3.

* versión más reciente de hello tooinstall de Raspbian, use hello [NOOBS] [ lnk-noobs] interfaz gráfica de usuario.
* Manualmente [descargar] [ lnk-raspbian] y escribir la imagen más reciente de Hola de tarjeta de hello Raspbian sistema operativo tooan SD.

### <a name="sign-in-and-access-hello-terminal"></a>Inicio de sesión y terminal Hola

Tiene dos tooaccess de opciones un entorno de terminal en su Pi frambuesa:

* Si tiene un teclado y supervisar tooyour conectado frambuesa Pi, puede usar hello Raspbian GUI tooaccess una ventana de terminal.

* Línea de comandos de acceso hello en el instalador de plataforma de frambuesa mediante SSH desde el equipo de escritorio.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Usar una ventana de terminal en hello GUI

las credenciales predeterminadas de Hola para Raspbian son nombre de usuario **pi** y la contraseña **frambuesa**. En la barra de tareas de Hola Hola GUI, puede iniciar hello **Terminal** utilidad mediante el icono de Hola que parece un monitor.

#### <a name="sign-in-with-ssh"></a>Inicio de sesión con SSH

Puede utilizar SSH para acceso de línea de comandos tooyour frambuesa Pi. artículo de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] describe cómo tooconfigure SSH en el instalador de plataforma de frambuesa y cómo tooconnect de [Windows] [ lnk-ssh-windows] o [Linux y Mac OS][lnk-ssh-linux].

Inicie sesión con el nombre de usuario **pi** y la contraseña **raspberry**.

### <a name="install-bluez-537"></a>Instalación de BlueZ 5.37

módulos de Hello Bilitar hable toohello Bluetooth hardware a través de la pila de BlueZ Hola. Necesita la versión 5.37 de BlueZ para hello módulos toowork correctamente. Estas instrucciones Asegúrese de que está instalada la versión correcta de Hola de BlueZ.

1. Detener el demonio de hello actual bluetooth:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Instalar las dependencias de Hola BlueZ:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Descargar código fuente de hello BlueZ desde bluez.org:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Descomprima el código fuente de hello:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Cambiar la carpeta de directorios toohello recién creado:

    ```sh
    cd bluez-5.37
    ```

1. Configurar hello BlueZ código toobe integrada:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Cree BlueZ:

    ```sh
    make
    ```

1. Una vez que ha terminado la creación, instale BlueZ:

    ```sh
    sudo make install
    ```

1. Cambiar la configuración de servicio systemd Bluetooth de forma que apunte toohello nuevo demonio de bluetooth en el archivo hello `/lib/systemd/system/bluetooth.service`. Reemplace la línea de 'ExecStart' de hello con hello siguiente texto:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Habilitar conectividad toohello SensorTag dispositivo desde el dispositivo de frambuesa Pi 3

Antes de ejemplo Hola en ejecución, debe tooverify que el 3 de Pi frambuesa puede conectarse toohello SensorTag dispositivo.

1. Asegúrese de hello `rfkill` utilidad se instala:

    ```sh
    sudo apt-get install rfkill
    ```

1. Desbloquear bluetooth en hello frambuesa Pi 3 y compruebe que es el número de versión de hello **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. shell de tooenter Hola bluetooth interactivo, iniciar el servicio de bluetooth hello y ejecute hello **bluetoothctl** comando:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Escriba el comando hello **encendido** toopower controlador de hello bluetooth. comando de Hello devuelve siguiente toohello similar de salida:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. En el shell de hello bluetooth interactiva, escriba el comando de hello **analizar en** tooscan para los dispositivos bluetooth. comando de Hello devuelve siguiente toohello similar de salida:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Asegúrese de dispositivo de hello SensorTag reconocible presionando botón pequeño hello (Hola debe parpadear LED verde). Hola frambuesa Pi 3 debe detectar dispositivos de hello SensorTag:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    En este ejemplo, puede ver esa dirección MAC de hello SensorTag dispositivo hello **A0:E6:F8:B5:F6:00**.

1. Desactivar el análisis mediante la especificación de hello **examinar desactivar** comando:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Conecte tooyour SensorTag dispositivo con su dirección MAC escribiendo **conectar \<dirección MAC\>**. Después de la salida de ejemplo de Hola se abrevia para mayor claridad:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Puede enumerar las características de GATT hello de dispositivo de hello utilizando Hola de nuevo **atributos de lista** comando.

1. Ahora puede desconectarse de dispositivo de hello mediante hello **desconectar** comando y, a continuación, salir del shell de bluetooth hello mediante hello **salir** comando:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

Ahora está muestra Bilitar IoT borde de Hola a toorun listo en el 3 de frambuesa Pi.

## <a name="run-hello-iot-edge-ble-sample"></a>Ejecutar ejemplo de Hola IoT borde BLE

ejemplo de Hola IoT borde Bilitar a toorun, necesita toocomplete tres tareas:

* Configurar dos dispositivos de ejemplo en IoT Hub.
* Compile IoT Edge en el dispositivo Raspberry Pi 3.
* Configurar y ejecutar el ejemplo de Hola a habilitar en el dispositivo de frambuesa Pi 3.

En tiempo de Hola de escritura, IoT borde sólo admite módulos BLE en puertas de enlace que se ejecutan en Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Configuración de dos dispositivos de ejemplo en IoT Hub

* [Crear un centro de IoT] [ lnk-create-hub] en su suscripción de Azure, se necesita Hola nombre de su toocomplete de base de datos central en este tutorial. Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.
* Agregar un dispositivo denominado **SensorTag_01** tooyour centro de IoT y tome nota de su clave de identificador y el dispositivo. Puede usar hello [explorador del dispositivo o el centro de IOT explorador] [ lnk-explorer-tools] herramientas tooadd este centro de IoT de toohello de dispositivo que creó en el paso anterior de Hola y tooretrieve su clave. Asignar este dispositivo toohello SensorTag dispositivo al configurar la puerta de enlace de Hola.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Compilar Azure IoT Edge en Raspberry Pi 3

Instale las dependencias para Azure IoT Edge:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Siguiente de hello use comandos tooclone IoT borde y todos su submodules tooyour directorio particular de:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Si tiene una copia completa de hello repositorio IoT borde en el 3 de Pi de frambuesa, puede compilar mediante Hola siguiente comando de carpeta de Hola que contiene Hola SDK:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Configurar y ejecutar el ejemplo de Hola a habilitar sobre frambuesa Pi 3

toobootstrap y ejemplo de Hola de ejecución, debe configurar cada módulo IoT borde que participa en la puerta de enlace de Hola. Esta configuración se proporciona en un archivo JSON y debe configurar los cinco módulos de IoT Edge participantes. Hay un archivo JSON de ejemplo en el repositorio, Hola denominado **puerta de enlace\_sample.json** que puede usar como punto de partida para crear su propio archivo de configuración de Hola. Este archivo se encuentra en hello **ble_gateway/samples/src** carpeta en la copia local de hello repositorio IoT borde.

Hello las secciones siguientes describen cómo tooedit esta configuración de archivos de ejemplo de Hola Bilitar y asumir ese repositorio IoT borde hello es Hola **/home/pi/iot-edge /** carpeta frambuesa Pi 3. Si el repositorio de hello está en otra parte, ajustar las rutas de acceso de hello según corresponda.

#### <a name="logger-configuration"></a>Configuración del registrador

Suponiendo que el repositorio de puerta de enlace de Hola se encuentra en hello **/home/pi/iot-edge /** carpeta, configurar el módulo de registrador de hello como sigue:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>Configuración del módulo BLE

configuración de ejemplo de Hola para dispositivos de hello Bilitar supone un dispositivo SensorTag de instrumentos Texas. Todos los dispositivos Bilitar estándar que pueden funcionar como un GATT periférico debe funcionan, pero puede que necesite característica GATT de hello tooupdate identificadores y los datos. Agregue la dirección MAC de hello de dispositivo SensorTag:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Si no usa un dispositivo SensorTag, revise la documentación de Hola de su toodetermine de dispositivo habilitar si necesita característica GATT de hello tooupdate identificadores y valores de datos.

#### <a name="iot-hub-module"></a>módulo de IoT Hub

Agregar nombre de Hola de su centro de IoT. suele ser el valor de sufijo de Hello **devices.net azure**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Configuración del módulo de asignación de identidad

Agregar dirección MAC de Hola de su dispositivo SensorTag y el Id. de dispositivo de Hola y la clave de hello **SensorTag_01** dispositivo agregado tooyour centro de IoT:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Configuración de la impresora BLE

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>Configuración del módulo BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Configuración de enrutamiento

configuración siguiente Hello garantiza siguiente Hola enrutamiento entre módulos IoT borde:

* Hola **registrador** módulo recibe y registra todos los mensajes.
* Hola **SensorTag** módulo envía Hola de mensajes tooboth **asignación** y **Bilitar impresora** módulos.
* Hola **asignación** módulo envía mensajes toohello **el centro de IOT** toobe módulo enviada tooyour centro de IoT.
* Hola **el centro de IOT** módulo envía mensajes realizar copia de toohello **asignación** módulo.
* Hola **asignación** módulo envía mensajes toohello **BLEC2D** módulo.
* Hola **BLEC2D** módulo envía mensajes realizar copia de toohello **Sensor etiqueta** módulo.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

ejemplo de Hola a toorun, archivo de configuración de JSON toohello ruta de acceso de hello pasada como un parámetro toohello **bilitar\_puerta de enlace** binario. Hello siguiente comando presupone que usa hello **gateway_sample.json** archivo de configuración. Ejecute este comando desde hello **iot borde** carpeta Hola frambuesa Pi:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Puede que necesite toopress Hola pequeño situado en hello SensorTag dispositivo toomake se puede detectar antes de ejecutar el ejemplo hello.

Al ejecutar el ejemplo hello, puede usar hello [explorador del dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [el centro de IOT explorador](https://github.com/Azure/iothub-explorer) herramienta toomonitor Hola mensajes Hola puerta de enlace de IoT borde reenvía del dispositivo de SensorTag Hola. Por ejemplo, mediante el centro de IOT explorador puede supervisar mensajes de dispositivo a la nube mediante el siguiente comando de hello:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Envío de mensajes de nube a dispositivo

módulo de Hello Bilitar también admite comandos envío del dispositivo toohello de centro de IoT. Puede usar hello [explorador del dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [el centro de IOT explorador](https://github.com/Azure/iothub-explorer) mensajes JSON de herramienta toosend ese módulo de puerta de enlace de hello Bilitar reenvía en dispositivo de Bilitar toohello.

Si usa Hola Texas instrumentos SensorTag dispositivo, puede activar LED rojo hello, LED verde o timbre mediante el envío de comandos desde el centro de IoT. Antes de enviar comandos desde el centro de IoT, en primer lugar enviar Hola siguientes dos mensajes JSON en orden. A continuación, puede enviar cualquiera de hello tooturn de comandos en las luces de Hola o timbre.

1. Restablecer todos los LED y timbre hello (desactivarlas):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. Configure E/S como "remoto":

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

Ahora puede enviar cualquiera de hello siguiente tooturn de comandos de las luces de Hola o timbre en dispositivo de Hola SensorTag:

* Activar LED Hola rojo:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Activar LED verde hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Activar el timbre hello:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Pasos siguientes

Si desea toogain conocimientos avanzados del borde de IoT y experimentar con algunos ejemplos de código, visite la página siguiente de hello tutoriales de desarrollador y recursos:

* [Azure IoT Edge][lnk-sdk]

toofurther explorar las capacidades de Hola de centro de IoT, vea:

* [Guía para desarrolladores de IoT Hub][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
