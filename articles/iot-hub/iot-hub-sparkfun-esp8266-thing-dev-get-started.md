---
title: aaaESP8266 toocloud - conectar Sparkfun ESP8266 lo Dev tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse de plataforma de nube de Azure de toosend datos toohello Sparkfun ESP8266 lo Dev tooAzure centro de IoT para ella en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Conectar Sparkfun ESP8266 lo Dev tooAzure centro de IoT en nube Hola

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![conexión entre DHT22, Thing Dev, y IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Lo que hará

Conectar el centro de IoT tooan de desarrollo de Sparkfun ESP8266 lo que creará. A continuación, ejecutar una aplicación de ejemplo en los datos de temperatura y humedad toocollect ESP8266 desde un sensor DHT22. Por último, envíe el centro de IoT de hello sensor datos tooyour.

> [!NOTE]
> Si usa otros paneles ESP8266, aún puede seguir estos pasos tooconnect, centro de IoT tooyour. Dependiendo de la placa de hello ESP8266 que está utilizando, puede que necesite tooreconfigure Hola `LED_PIN`. Por ejemplo, si usas ESP8266 desde Pensador AI, puede cambiarlo de `0` demasiado`2`. ¿Aún no tiene el kit?, haga clic [aquí](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>Lo qué aprenderá

* ¿Cómo toocreate un centro de IoT y registrar un dispositivo para algo de desarrollo
* ¿Cómo tooconnect lo desarrollo con sensor de Hola y el equipo.
* ¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en algo de desarrollo
* ¿Cómo toosend Hola centro de IoT de tooyour de datos de sensor.

## <a name="what-you-will-need"></a>Qué necesita

![Piezas necesarias para el tutorial de Hola](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete esta operación, necesita Hola siguientes partes de los Starter Kit de desarrollo de lo:

* Hola Sparkfun ESP8266 lo Dev panel.
* Un cable USB A Micro USB tooType.

También necesita Hola siguiente para el entorno de desarrollo:

* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
* Un equipo PC o Mac que ejecute Windows o Ubuntu.
* Red inalámbrica para tooconnect Sparkfun ESP8266 lo Dev a.
* Herramienta de configuración de Hola de toodownload de la conexión de Internet.
* [Arduino IDE](https://www.arduino.cc/en/main/software) versión 1.6.8 (o posterior), las versiones anteriores no funcionarán con la biblioteca de AzureIoT Hola.

Hello elementos siguientes son opcionales en caso de que no tiene un sensor. También tiene Hola opción consiste en utilizar datos de sensor simulada.

* Un sensor de temperatura y humedad Adafruit DHT22.
* La placa de pruebas.
* Cables de puente M/M.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Conectar ESP8266 lo desarrollo con sensor de Hola y el equipo

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Conectar un sensor de temperatura y humedad DHT22 tooESP8266 lo desarrollo

Utilice hello breadboard y puentes cables toomake Hola conexión como se indica a continuación. Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.

![referencia de conexiones](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Para el PIN de sensor, usaremos Hola después de conectar:

| Inicio (sensor)           | Fin (placa)           | Color de cable   |
| -----------------------  | ---------------------- | ------------: |
| VDD (patilla 27F)            | 3V (patilla 8A)           | Cable rojo     |
| DATOS (patilla 28F)           | GPIO 2 (patilla 9A)       | Cable blanco    |
| GND (patilla 30F)            | GND (patilla 7J)          | Cable negro   |


- Para obtener más información, consulte [el programa de instalación del sensor DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) y [las especificaciones de Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711).

Ahora su Sparkfun ESP8266 Thing Dev debe estar conectado con un sensor de trabajo.

![conectar dht22 con ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Conectar el equipo de desarrollo de Sparkfun ESP8266 lo tooyour

Utilice Sparkfun ESP8266 lo Dev tooyour equipo de hello Micro USB tooType A USB cable tooconnect como se indica a continuación.

![conectar compacto huzzah tooyour equipo](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Adición de permisos de puerto (solo Ubuntu)

Si usas Ubuntu, asegúrese de que un usuario normal tenga Hola permisos toooperate en hello USB puerto de Sparkfun ESP8266 lo dev. permisos de puerto serie tooadd para un usuario normal, siga estos pasos:

1. Ejecute hello siguientes comandos en un terminal:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Obtener una Hola siguientes salidas:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   En la salida de hello, tenga en cuenta `uucp` o `dialout` decir Hola grupo nombre del propietario de hello puerto USB.

1. Agregar grupo de toohello de hello usuarios ejecutando Hola siguiente comando:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`es el nombre de propietario de grupo de Hola que obtuvo en el paso anterior de Hola. `<username>` es el nombre de usuario de Ubuntu.

1. Cierre sesión Ubuntu y vuelva a iniciar en ella para cambiar tootake efecto de Hola.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Recopilar datos del sensor y enviarla tooyour centro de IoT

En esta sección, implementará y ejecutará una aplicación de ejemplo en Sparkfun ESP8266 Thing Dev. aplicación de ejemplo de Hola parpadea Hola LED en Sparkfun ESP8266 lo Dev y envía la temperatura de Hola y recopilan los datos de humedad de hello DHT22 sensor tooyour centro de IoT.

### <a name="get-hello-sample-application-from-github"></a>Obtener la aplicación de ejemplo de Hola desde GitHub

aplicación de ejemplo de Hola se hospeda en GitHub. Clonar el repositorio de ejemplo de Hola que contiene la aplicación de ejemplo de Hola desde GitHub. repositorio de ejemplo de Hola tooclone, siga estos pasos:

1. Abra un símbolo del sistema o una ventana de terminal.
1. Vaya carpeta tooa donde desea toobe de aplicación de ejemplo de Hola almacenado.
1. Ejecute el siguiente comando de hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Instalar el paquete de Hola para Sparkfun ESP8266 lo Dev en Arduino IDE:

1. Abra la carpeta de Hola donde se almacena la aplicación de ejemplo de Hola.
1. Abra el archivo de app.ino de hello en la carpeta de la aplicación hello en Arduino IDE.

   ![Abra la aplicación de ejemplo de Hola en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. Hola Arduino IDE, haga clic en **archivo** > **preferencias**.
1. Hola **preferencias** diálogo cuadro, haga clic en hello icono siguiente toohello **más direcciones URL del Administrador de paneles** cuadro de texto.
1. En la ventana emergente de hello, escriba Hola después de la dirección URL y, a continuación, haga clic en **Aceptar**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![dirección url del paquete de punto tooa arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. Hola **preferencias** cuadro de diálogo, haga clic en **Aceptar**.
1. Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Boards Manager** (Administrador de placas) y busque esp8266.
   Se instalará ESP8266 con una versión de 2.2.0 o posterior.

   ![Hola esp8266 paquete está instalado](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Sparkfun ESP8266 Thing Dev**.

### <a name="install-necessary-libraries"></a>Instalación de las bibliotecas necesarias

1. Hola Arduino IDE, haga clic en **boceto** > **incluyen biblioteca** > **administrar bibliotecas de**.
1. Busque Hola siguiendo los nombres de las bibliotecas uno por uno. Para cada biblioteca de Hola que encuentre, haga clic en **instalar**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>¿No tiene un sensor DHT22 real?

aplicación de ejemplo de Hola puede simular la temperatura y humedad datos en caso de que no tiene un sensor DHT22 real. datos de toouse simulado de la aplicación de ejemplo de tooenable hello, siga estos pasos:

1. Abra hello `config.h` archivo Hola `app` carpeta.
1. Busque Hola después de la línea de código y cambie el valor de Hola de `false` demasiado`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar datos de toouse simulado de aplicación de ejemplo de Hola](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Guarde con `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Implementar tooSparkfun de aplicación de ejemplo de Hola ESP8266 lo desarrollo

1. Hola Arduino IDE, haga clic en **herramienta** > **puerto**y, a continuación, haga clic en puerto serie Hola para Sparkfun ESP8266 lo dev
1. Haga clic en **boceto** > **cargar** toobuild e implementar tooSparkfun de aplicación de ejemplo de Hola ESP8266 lo dev

> [!Note]
> Si usas macOS probablemente percibirá Hola siguientes mensajes durante la carga. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Abra la ventana de ternimal y finalizar por debajo de acciones toosolve este problema.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Escriba sus credenciales.

Una vez finalizada correctamente la carga de hello, siga Hola pasos tooenter sus credenciales:

1. Hola Arduino IDE, haga clic en **herramientas** > **Monitor serie**.
1. En la ventana del monitor de la serie de hello, observe listas desplegables de hello dos en hello esquina inferior derecha.
1. Seleccione **ningún final de línea** de lista desplegable de la izquierda Hola.
1. Seleccione **115.200 baudios** para la lista desplegable derecha de Hola.
1. En cuadro de entrada de hello situado en parte superior de saludo de la ventana del monitor de la serie de hello, escriba Hola siguiente información si se le solicita tooprovide y, a continuación, haga clic en **enviar**.
   * SSID de Wi-Fi
   * Contraseña de Wi-Fi
   * Cadena de conexión de dispositivo

> [!Note]
> información de credenciales de Hola se almacena en hello EEPROM de Sparkfun ESP8266 lo dev. Si hace clic en botón de restablecimiento de hello en hello Sparkfun ESP8266 lo Dev panel, aplicación de ejemplo de Hola se le preguntará si desea obtener información de hello tooerase. Escriba `Y` toohave Hola información borrado y se le pide información de hello tooprovide nuevo.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Compruebe la aplicación de ejemplo de Hola se esté ejecutando correctamente

Si ve siguiente Hola de salida de la ventana del monitor de la serie de Hola y Hola parpadear LED de Sparkfun ESP8266 lo Dev, aplicación de ejemplo de Hola se está ejecutando correctamente.

![salida final en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Pasos siguientes

Está correctamente conectado un centro de IoT tooyour Sparkfun ESP8266 lo Dev y envía el centro de IoT de hello capturan sensor datos tooyour. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
