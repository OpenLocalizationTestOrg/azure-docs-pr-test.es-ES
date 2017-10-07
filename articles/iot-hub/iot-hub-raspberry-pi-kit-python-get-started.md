---
title: aaaRaspberry Pi toocloud (Python) - conectar frambuesa Pi tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse frambuesa Pi tooAzure centro de IoT para la plataforma de nube de Azure de frambuesa Pi toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot frambuesas pi, frambuesas pi iot hub, frambuesas pi envío datos toocloud, frambuesas pi toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a>Conectar frambuesa Pi tooAzure centro de IoT (Python)

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

## <a name="set-up-raspberry-pi"></a>Configuración de Raspberry Pi

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

### <a name="enable-ssh-and-i2c"></a>Habilitar SSH e I2C

1. Conecte el monitor de toohello de Pi, teclado y mouse (ratón), inicie Pi y, a continuación, inicie sesión en Raspbian con `pi` como nombre de usuario de Hola y `raspberry` como contraseña de Hola.
1. Haga clic en icono frambuesas hello > **preferencias** > **frambuesa Pi configuración**.

   ![menú de Hello Raspbian preferencias](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. En hello **Interfaces** pestaña, establezca **I2C** y **SSH** demasiado**habilitar**y, a continuación, haga clic en **Aceptar**. Si no tiene sensores físicos y desea que los datos de sensor toouse simulado, este paso es opcional.

   ![Habilitar I2C y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH y I2C, puede encontrar varios documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Conectar Hola sensor tooPi

Utilice hello breadboard y puentes cables tooconnect un LED y un tooPi BME280 como se indica a continuación. Si no dispone de sensor hello, [omitir esta sección](#connect-pi-to-the-network).

![Hola frambuesa Pi y sensor de conexión](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

sensor de Hello BME280 puede recopilar datos de temperatura y humedad. Y Hola LED parpadea si se produce una comunicación entre el dispositivo y hello en la nube. 

Para el PIN de sensor, use Hola después de conectar:

| Inicio (sensor y LED)     | Fin (placa)            | Color de cable   |
| -----------------------  | ---------------------- | ------------: |
| VDD (patilla 5G)             | Potencia 3,3 V (patilla 1)       | Cable blanco   |
| GND (patilla 7G)             | GND (patilla 6)            | Cable marrón   |
| SDI (patilla 10G)            | I2C1 SDA (patilla 3)       | Cable rojo     |
| SCK (patilla 8G)             | I2C1 SCL (patilla 5)       | Cable naranja  |
| LED VDD (patilla 18F)        | GPIO 24 (patilla 18)       | Cable blanco   |
| LED GND (patilla 17F)        | GND (patilla 20)           | Cable negro   |

Haga clic en tooview [frambuesa Pi 2 y 3 asignaciones de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.

Una vez se haya conectado correctamente BME280 tooyour frambuesa Pi, debería ser como debajo de imagen.

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Conectar red toohello de Pi

Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola. Use Hola Ethernet por cable tooconnect Pi tooyour con cable de red o siga hello [las instrucciones de hello frambuesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) red inalámbrica de tooconnect Pi tooyour. Después de que el instalador de plataforma ha sido red toohello conectado correctamente, deberá tootake una nota de hello [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Red toowired conectado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Asegúrese de que ese Pi está conectado toohello misma red que el equipo. Por ejemplo, si el equipo está conectado tooa red inalámbrica mientras Pi es tooa conectado por cable de red, no verá Hola IP dirección en la salida de hello devdisco.

## <a name="run-a-sample-application-on-pi"></a>Ejecutar una aplicación de ejemplo en Pi

### <a name="install-hello-prerequisite-packages"></a>Instalar paquetes de requisitos previos de Hola

Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host frambuesa Pi.
   
   **Usuarios de Windows**
   1. Descargue e instale [PuTTY](http://www.putty.org/) para Windows. 
   1. Copie la dirección IP de saludo de la sección de Pi en nombre de Host de hello (o dirección IP) y seleccione SSH como tipo de conexión de Hola.
   
   
   **Usuarios de Mac y Ubuntu**
   
   Use el cliente SSH integrado de hello en Ubuntu o macOS. Es posible que tenga toorun `ssh pi@<ip address of pi>` tooconnect Pi mediante SSH.
   > [!NOTE] 
   el nombre de usuario de Hello predeterminada es `pi` , y es la contraseña de hello `raspberry`.


### <a name="configure-hello-sample-application"></a>Configurar la aplicación de ejemplo de Hola

1. Clonar aplicación de ejemplo de Hola ejecutando Hola siguiente comando:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   Hay cinco macros en este archivo que se pueden configurar. Hello primero uno es `MESSAGE_TIMESPAN`, que define el intervalo de tiempo de hello (en milisegundos) entre los dos mensajes que envían toocloud. Hola otra `SIMULATED_DATA`, que es un valor booleano para si toouse simulado los datos de sensor o no. `I2C_ADDRESS`es la dirección de hello I2C que está conectado el sensor BME280. `GPIO_PIN_ADDRESS`es la dirección GPIO de hello para el LED. Hello en último lugar uno es `BLINK_TIMESPAN`, que define el intervalo de tiempo de hello cuando se activa el LED en milisegundos.

   Si se **no tiene el sensor de hello**, hello establezca `SIMULATED_DATA` valor demasiado`True` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.

1. Guarde y salga al presionar Control-O > Entrar > Control-X.

### <a name="build-and-run-hello-sample-application"></a>Compilar y ejecutar la aplicación de ejemplo de Hola

1. Compile la aplicación de ejemplo de Hola ejecutando el siguiente comando de Hola. Como hello Azure IoT SDK para Python son contenedores que funcionan sobre Hola SDK de C de dispositivos de IoT de Azure, necesitará bibliotecas de hello C toocompile si desea o necesita bibliotecas de Python toogenerate Hola desde el código fuente.

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   También puede especificar la versión de Hola que desee mediante la ejecución de `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`. Si ejecuta el script sin el parámetro, el script de Hola detectará automáticamente versión Hola de python instalado (secuencia de búsqueda 2.7 -> 3.4 -> 3.5). Asegúrese de que su versión de Python mantenga la coherencia durante la compilación y la ejecución. 
   
   > [!NOTE] 
   En la creación de biblioteca de cliente de Python de hello (iothub_client.so) en dispositivos de Linux que tienen menos de 1GB de RAM, verá compilar acumulando en 98% durante la creación de iothub_client_python.cpp tal y como se muestra a continuación `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`. Si experimenta este problema, compruebe el consumo de memoria de hello de dispositivo de hello mediante `free -m command` en otra ventana de terminal durante ese tiempo. Si se está quedando sin memoria mientras se estaba compilando el archivo iothub_client_python.cpp, puede que tenga tootemporarily aumentar tooget de espacio de intercambio de hello toosuccessfully de memoria insuficiente compilar biblioteca del SDK de dispositivo de Hola de cliente de Python.
   
1. Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola. Y si usar python Hola 3, puede usar Hola comando `python3 app.py '<your Azure IoT hub device connection string>'`.


   Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.

   ![Salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a>Pasos siguientes

Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT. mensajes de saludo de toosee que el instalador de plataforma de frambuesa ha enviado IoT de tooyour concentrador o envío tooyour de mensajes frambuesa Pi en una interfaz de línea de comandos, vea hello [administrar nube dispositivo mensajería con el centro de IOT explorer, tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
