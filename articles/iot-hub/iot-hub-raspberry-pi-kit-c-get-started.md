---
title: aaaRaspberry Pi toocloud (C) - conectar frambuesa Pi tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse frambuesa Pi tooAzure centro de IoT para la plataforma de nube de Azure de frambuesa Pi toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot frambuesas pi, frambuesas pi iot hub, frambuesas pi envío datos toocloud, frambuesas pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>Conectar frambuesa Pi tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con frambuesa Pi que se está ejecutando Raspbian. A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md). Para obtener ejemplos de Windows 10 IoT Core, vaya toohello [centro de desarrollo de Windows](http://www.windowsondevices.com/).

¿Aún no tiene un kit? Pruebe el [simulador en línea de Rapsberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md). También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Qué debe hacer

* Cree un Centro de IoT.
* Registre un dispositivo para Pi en IoT Hub.
* Configure Raspberry Pi.
* Ejecutar una aplicación de ejemplo en el centro de IoT de Pi toosend sensor datos tooyour.

Conectar el centro de IoT de frambuesa Pi tooan creados por usted. A continuación, ejecutar una aplicación de ejemplo en los datos de temperatura y humedad toocollect Pi de un sensor BME280. Por último, envíe centro de IoT de hello sensor datos tooyour.

## <a name="what-you-learn"></a>Conocimientos que adquirirá

* ¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.
* ¿Cómo tooconnect Pi con un sensor BME280.
* ¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo de Pi.
* Cómo centro de IoT de toosend sensor datos tooyour.

## <a name="what-you-need"></a>Lo que necesita

![Lo que necesita](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* Hola frambuesa Pi 2 o 3 de Pi de frambuesa al panel.
* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
* Un monitor, un teclado USB y mouse (ratón) que se conectan tooPi.
* Un equipo PC o Mac con Windows o Linux.
* Una conexión a Internet.
* Una tarjeta microSD de 16 GB o más.
* Un SD USB adaptador o microSD tarjeta tooburn Hola imagen de sistema operativo en tarjeta microSD de Hola.
* Alimentación de amp 2 de 5 voltios con cable de hello pie 6 micro USB.

Hola siguientes elementos es opcional:

* Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.
* La placa de pruebas.
* Cables de puente M/6 F.
* Un LED difuso de 10 mm.


> [!NOTE] 
Estos elementos son opcionales, porque la compatibilidad de ejemplo de código de hello había simulado los datos de sensor.


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Configurar Raspberry Pi

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Instalar el sistema operativo de hello Raspbian de Pi

Preparar la tarjeta microSD de hello para la instalación de la imagen de Raspbian Hola.

1. Descargue Raspbian.
   1. [Descargar Raspbian Jessie con el escritorio](https://www.raspberrypi.org/downloads/raspbian/) (archivo .zip de hello).
   1. Extraer hello Raspbian imagen tooa carpeta del equipo.
1. Instalar Raspbian toohello microSD tarjeta.
   1. [Descargar e instalar la utilidad de grabadora de tarjeta de SD de creación de hello](https://etcher.io/).
   1. Ejecute creación y seleccione la imagen de Raspbian Hola que ha extraído en el paso 1.
   1. Seleccione la unidad de tarjeta microSD Hola. Tenga en cuenta que creación probablemente ya seleccionó unidad correcta Hola.
   1. Haga clic en Flash tooinstall Raspbian toohello microSD tarjeta.
   1. Quitar tarjeta microSD de hello del equipo cuando se completa la instalación. Es tarjeta microSD de tooremove seguro Hola directamente porque creación expulsa automáticamente o desmonta tarjeta microSD de hello tras la finalización.
   1. Inserte la tarjeta microSD de hello en Pi.

### <a name="enable-ssh-and-spi"></a>Habilitar SSH y SPI

1. Conecte el monitor de toohello de Pi, teclado y mouse (ratón), inicie Pi y, a continuación, inicie sesión en Raspbian con `pi` como nombre de usuario de Hola y `raspberry` como contraseña de Hola.
1. Haga clic en icono frambuesas hello > **preferencias** > **frambuesa Pi configuración**.

   ![menú de Hello Raspbian preferencias](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. En hello **Interfaces** pestaña, establezca **SPI** y **SSH** demasiado**habilitar**y, a continuación, haga clic en **Aceptar**. Si no tiene sensores físicos y desea que los datos de sensor toouse simulado, este paso es opcional.

   ![Habilitar SPI y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH y SPI, puede encontrar varios documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Conectar Hola sensor tooPi

Utilice hello breadboard y puentes cables tooconnect un LED y un tooPi BME280 como se indica a continuación. Si no dispone de sensor hello, [omitir esta sección](#connect-pi-to-the-network).

![Hola frambuesa Pi y sensor de conexión](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

sensor de Hello BME280 puede recopilar datos de temperatura y humedad. Y Hola LED parpadea si se produce una comunicación entre el dispositivo y hello en la nube. 

Para el PIN de sensor, use Hola después de conectar:

| Inicio (sensor y LED)     | Fin (placa)            | Color de cable   |
| -----------------------  | ---------------------- | ------------: |
| LED VDD (patilla 5G)         | GPIO 4 (patilla 7)         | Cable blanco   |
| LED GND (patilla 6G)         | GND (patilla 6)            | Cable negro   |
| VDD (patilla 18F)            | Potencia 3,3 V (patilla 17)      | Cable blanco   |
| GND (patilla 20F)            | GND (patilla 20)           | Cable negro   |
| SCK (patilla 21F)            | SPI0 SCLK (patilla 23)     | Cable naranja  |
| SDO (patilla 22F)            | SPI0 MISO (patilla 21)     | Cable amarillo  |
| SDI (patilla 23F)            | SPI0 MOSI (patilla 19)     | Cable verde   |
| CS (patilla 24F)             | SPI0 CS (patilla 24)       | Cable azul    |

Haga clic en tooview [frambuesa Pi 2 y 3 asignaciones de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.

Una vez se haya conectado correctamente BME280 tooyour frambuesa Pi, debería ser como debajo de imagen.

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Conectar red toohello de Pi

Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola. Use Hola Ethernet por cable tooconnect Pi tooyour con cable de red o siga hello [las instrucciones de hello frambuesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) red inalámbrica de tooconnect Pi tooyour. Después de que el instalador de plataforma ha sido red toohello conectado correctamente, deberá tootake una nota de hello [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Red toowired conectado](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>Ejecutar una aplicación de ejemplo en Pi

### <a name="install-hello-prerequisite-packages"></a>Instalar paquetes de requisitos previos de Hola

1. Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host frambuesa Pi.
   
   **Usuarios de Windows**
   1. Descargue e instale [PuTTY](http://www.putty.org/) para Windows. 
   1. Copie la dirección IP de saludo de la sección de Pi en nombre de Host de hello (o dirección IP) y seleccione SSH como tipo de conexión de Hola.
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Usuarios de Mac y Ubuntu**
   
   Use el cliente SSH integrado de hello en Ubuntu o macOS. Es posible que tenga toorun `ssh pi@<ip address of pi>` tooconnect Pi mediante SSH.
   > [!NOTE] 
   el nombre de usuario de Hello predeterminada es `pi` , y es la contraseña de hello `raspberry`.

1. Instalar paquetes de requisitos previos de Hola para hello SDK de dispositivos de IoT de Azure de Microsoft para C y Cmake ejecutando Hola siguientes comandos:

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Configurar la aplicación de ejemplo de Hola

1. Clonar aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Archivo config](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   Hay dos macros en este archivo que se pueden configurar. Hello primero uno es `INTERVAL`, que define el intervalo de tiempo de hello (en milisegundos) entre los dos mensajes que envían toocloud. Hola otra `SIMULATED_DATA`, que es un valor booleano para si toouse simulado los datos de sensor o no.

   Si se **no tiene el sensor de hello**, hello establezca `SIMULATED_DATA` valor demasiado`1` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.

1. Guarde y salga al presionar Control-O > Entrar > Control-X.

### <a name="build-and-run-hello-sample-application"></a>Compilar y ejecutar la aplicación de ejemplo de Hola

1. Crear aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

   ```bash
   cmake . && make
   ```
   ![Resultado de la compilación](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola.


Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.

![Salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>Pasos siguientes

Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT. mensajes de saludo de toosee que el instalador de plataforma de frambuesa ha enviado IoT de tooyour concentrador o envío tooyour de mensajes frambuesa Pi en una interfaz de línea de comandos, vea hello [administrar nube dispositivo mensajería con el centro de IOT explorer, tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
