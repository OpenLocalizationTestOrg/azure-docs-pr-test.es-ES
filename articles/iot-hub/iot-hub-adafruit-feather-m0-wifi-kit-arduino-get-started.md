---
title: "M0 toocloud: conexión Wi-Fi de desvanecimiento M0 tooAzure centro de IoT | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset una copia de seguridad y conectarse Adafruit compacto M0 Wi-Fi tooAzure plataforma de nube de Azure de centro de IoT toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Conectar Adafruit compacto M0 Wi-Fi tooAzure centro de IoT en nube Hola
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexión entre BME280, Feather M0 WiFi e IoT Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con el panel de Arduino. A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>Qué debe hacer

Conectar el centro de IoT de tooan Adafruit compacto M0 Wi-Fi que cree. A continuación, ejecutar una aplicación de ejemplo en M0 Wi-Fi toocollect Hola temperatura y humedad los datos desde un BME280. Por último, envíe centro de IoT de hello sensor datos tooyour.


## <a name="what-you-learn"></a>Conocimientos que adquirirá

* ¿Cómo toocreate un centro de IoT y registrar un dispositivo de Wi-Fi de desvanecimiento M0
* ¿Cómo tooconnect Wi-Fi de desvanecimiento M0 con sensor de Hola y el equipo
* ¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en Wi-Fi de desvanecimiento M0
* ¿Cómo toosend Hola centro de IoT de sensor datos tooyour

## <a name="what-you-need"></a>Lo que necesita

![Piezas necesarias para el tutorial de Hola](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete esta operación, necesita Hola siguientes partes de los Starter Kit de desvanecimiento M0 Wi-Fi:

* Hola Wi-Fi de desvanecimiento M0 panel
* Un cable USB A tooType de Micro USB

También necesita Hola después cosas para el entorno de desarrollo:

* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
* Un equipo PC o Mac que ejecute Windows o Ubuntu.
* Una red inalámbrica para Wi-Fi de desvanecimiento M0 tooconnect a.
* Una herramienta de configuración de Internet conexión toodownload Hola.
* [IDE de Arduino](https://www.arduino.cc/en/main/software) versión 1.6.8 o posterior. Las versiones anteriores no funcionan con la biblioteca de centro de IoT de Azure Hola.

Si no dispone de un sensor, Hola siguientes elementos es opcional. También tiene Hola opción consiste en utilizar datos de sensor simulada:

* Un sensor de temperatura y humedad BME280
* Una placa de pruebas
* Cables de puente M/M

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Conexión Wi-Fi de desvanecimiento M0 con sensor Hola y el equipo
En esta sección, se conecta tooyour placa de hello sensores. A continuación, conectar el equipo de tooyour de dispositivo para su uso posterior.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Conectar un tooFeather de sensor DHT22 temperatura y humedad M0 Wi-Fi

Usar hello breadboard y puentes cables toomake Hola conexión. Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.

![Referencia de conexiones](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Para el PIN de sensor, use Hola después de conectar:


| Inicio (sensor)           | Fin (placa)            | Color del cable   |
| -----------------------  | ---------------------- | ------------: |
| VDD (patilla 27A)            | 3V (patilla 3A)            | Cable rojo     |
| GND (patilla 29A)            | GND (patilla 6A)           | Cable negro   |
| SCK (patilla 30A)            | SCK (patilla 12A)          | Cable amarillo  |
| SDO (patilla 31A)            | MI (patilla 14A)           | Cable blanco   |
| SDI (patilla 32A)            | M0 (patilla 13A)           | Cable azul    |
| CS (patilla 33A)             | GPIO 5 (patilla 15J)       | Cable naranja  |

Para más información, consulte la [introducción al sensor de presión atmosférica, temperatura y humedad Adafruit BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) y el artículo sobre el [patillaje de Adafruit Feather M0 WiFi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).



Ahora Feather M0 WiFi debe estar conectado con un sensor en funcionamiento.

![Conectar DHT22 con Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Conectar Wi-Fi de desvanecimiento M0 tooyour equipo

Usar Hola Micro USB tooType A USB cable tooconnect Wi-Fi de desvanecimiento M0 tooyour equipo, como se muestra:

![Conectar compacto Huzzah tooyour equipo](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Agregar permisos de puerto serie (solo Ubuntu)

Si usas Ubuntu, asegúrese de que tiene Hola permisos toooperate en hello USB puerto de desvanecimiento M0 Wi-Fi. permisos de puerto serie tooadd, siga estos pasos:


1. En un terminal, ejecute hello siguientes comandos:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Obtener una Hola siguientes salidas:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   En la salida de hello, tenga en cuenta que `uucp` o `dialout` es nombre de propietario del grupo de Hola de hello puerto USB.

2. tooadd hello toohello grupo de usuarios, ejecute el siguiente comando de hello:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   En el paso anterior de hello, obtiene el nombre de propietario del grupo de hello `<group-owner-name>`. `<username>` es el nombre de usuario de Ubuntu.

3. Para tooappear de cambio de hello, cierre la sesión de Ubuntu y, a continuación, inicie una sesión.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Recopilar datos del sensor y enviarla tooyour centro de IoT

En esta sección, implementará y ejecutará una aplicación de ejemplo en Feather M0 WiFi. aplicación de ejemplo de Hola hace Hola parpadear LED en Wi-Fi de desvanecimiento M0. A continuación, envía temperatura de Hola y recopilan los datos de humedad de hello BME280 sensor tooyour centro de IoT.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Obtener la aplicación de ejemplo de Hola desde GitHub y preparar hello Arduino IDE

aplicación de ejemplo de Hola se hospeda en GitHub. Clonar el repositorio de ejemplo de Hola que contiene la aplicación de ejemplo de Hola desde GitHub. repositorio de ejemplo de Hola tooclone, siga estos pasos:

1. Abra un símbolo del sistema o una ventana de terminal.

2. Vaya carpeta tooa donde desea toobe de aplicación de ejemplo de Hola almacenado.
3. Ejecute el siguiente comando de hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Instalar el paquete de Hola para Wi-Fi de desvanecimiento M0 Hola Arduino IDE

1. Abra la carpeta de Hola donde se almacena la aplicación de ejemplo de Hola.

2. Abra el archivo de app.ino de hello en la carpeta de la aplicación Hola Hola Arduino IDE.

   ![Abra la aplicación de ejemplo de Hola en Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Haga clic en **archivo** > **preferencias** (Windows o Linux) o **Arduino** > **preferencias** (Mac) y copie y Pegar Hola vínculo en hello **más direcciones URL del Administrador de paneles** opción Hola preferencias Arduino IDE.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Haga clic en **herramientas** > **panel** > **paneles Manager**y, a continuación, instalar hello `Arduino SAMD Boards` versión `1.6.2` o posterior. 

1. A continuación, en Hola la misma ventana, instale `Adafruit SAMD Boards` las definiciones de tooadd Hola panel archivo de paquete.

   ![Hola esp8266 paquete está instalado](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Adafruit M0 WiFi**.

5. Instale los controladores (solo para Windows). Cuando se conecta Wi-Fi de desvanecimiento M0, tendrá que tooinstall un controlador. Haga clic en [vínculo de descarga de hello en la página Web de hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) instalador del controlador toodownload Hola. Siga los controladores de Hola Hola pasos tooinstall que desee.

### <a name="install-necessary-libraries"></a>Instalación de las bibliotecas necesarias

1. Hola Arduino IDE, haga clic en **boceto** > **incluyen biblioteca** > **administrar bibliotecas de**.

2. Busque Hola siguiendo los nombres de las bibliotecas uno por uno. Para cada biblioteca que encuentre, haga clic en **Install** (Instalar):

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Instale manualmente `Adafruit_WINC1500`. Vaya demasiado[este sitio Web](https://github.com/adafruit/Adafruit_WINC1500) y haga clic en **clon o una descarga** > **Download ZIP**. A continuación, en el IDE Arduino, vaya demasiado**boceto** > **incluyen biblioteca** > **agregar .zip biblioteca** y agregue el archivo zip de Hola.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Usar la aplicación de ejemplo de Hola si no tienes un sensor BME280 real

Si no dispone de un sensor BME280 real, aplicación de ejemplo de Hola puede simular los datos de temperatura y humedad. tooset los datos de toouse simulado de aplicación de ejemplo Hola, siga estos pasos:

1. Abra hello `config.h` archivo Hola `app` carpeta.

2. Busque Hola después de la línea de código y cambie el valor de Hola de `false` demasiado`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar datos de toouse simulado de aplicación de ejemplo de Hola](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Guardar archivo de hello con `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Implementar tooFeather de aplicación de ejemplo de Hola M0 Wi-Fi

1. Hola Arduino IDE, haga clic en **herramienta** > **puerto**y, a continuación, haga clic en puerto serie Hola de Wi-Fi de desvanecimiento M0.

2. Haga clic en **boceto** > **cargar** toobuild e implementar tooFeather de aplicación de ejemplo de Hola M0 Wi-Fi.

### <a name="enter-your-credentials"></a>Escriba sus credenciales.

Una vez finalizada correctamente la carga de hello, siga estos pasos tooenter sus credenciales:

1. Hola Arduino IDE, haga clic en **herramientas** > **Monitor serie**.

2. En la esquina inferior derecha de saludo de la ventana del monitor de la serie de hello, seleccione **ningún final de línea** en lista de desplegable Hola Hola izquierda.
3. Seleccione **115.200 baudios** en lista desplegable Hola Hola derecho.
4. En el cuadro de entrada de hello en la parte superior de hello, escriba Hola siguiente información si le pide tooprovide y haga clic en **enviar**:

   * SSID de Wi-Fi
   * Contraseña de Wi-Fi
   * Cadena de conexión de dispositivo

> [!Note]
> información de credenciales de Hola se almacena en hello EEPROM de desvanecimiento M0 Wi-Fi. Si hace clic en botón de reinicio de hello en hello placa de Wi-Fi de desvanecimiento M0, aplicación de ejemplo de Hola le preguntará si desea que tooerase información de Hola. Escriba `Y` información de hello tooerase. Se le pide información de hello tooprovide una segunda vez.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Compruebe que la aplicación de ejemplo de Hola se ejecuta correctamente

Si ve siguiente Hola de salida de ventana del monitor de la serie de Hola y Hola parpadear LED de desvanecimiento M0 Wi-Fi, aplicación de ejemplo de Hola se esté ejecutando correctamente:

![Salida final en el IDE de Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Pasos siguientes

Está correctamente conectado centro de IoT de Wi-Fi de desvanecimiento M0 tooyour y envía el centro de IoT de hello capturan sensor datos tooyour. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

