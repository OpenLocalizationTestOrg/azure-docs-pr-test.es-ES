---
title: aaaESP8266 toocloud - conectar compacto HUZZAH ESP8266 tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conéctese de plataforma de nube de Azure de toosend datos toohello Adafruit compacto HUZZAH ESP8266 tooAzure centro de IoT para él en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Conectar Adafruit compacto HUZZAH ESP8266 tooAzure centro de IoT en nube Hola

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexión entre DHT22, Feather HUZZAH ESP8266 e IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Qué debe hacer


Conectar el centro de IoT de tooan Adafruit compacto HUZZAH ESP8266 creados por usted. A continuación, ejecutar una aplicación de ejemplo en ESP8266 toocollect Hola temperatura y humedad los datos de un sensor DHT22. Por último, envíe centro de IoT de hello sensor datos tooyour.

> [!NOTE]
> Si usa otros paneles ESP8266, aún puede seguir estos pasos tooconnect, centro de IoT tooyour. Función que está usando el panel de hello ESP8266, podría necesitar tooreconfigure Hola `LED_PIN`. Por ejemplo, si usa ESP8266 de AI Pensador, puede cambiar de `0` demasiado`2`. ¿Aún no tiene un kit? Obtener de hello [sitio Web de Azure](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Conocimientos que adquirirá

* ¿Cómo toocreate un centro de IoT y registrar un dispositivo de desvanecimiento HUZZAH ESP8266
* ¿Cómo tooconnect compacto HUZZAH ESP8266 con sensor de Hola y el equipo
* ¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en compacto HUZZAH ESP8266
* ¿Cómo toosend Hola centro de IoT de sensor datos tooyour

## <a name="what-you-need"></a>Lo que necesita

![Piezas necesarias para el tutorial de Hola](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete esta operación, necesita Hola siguientes partes de su compacto HUZZAH ESP8266 Starter Kit:

* Hola compacto HUZZAH ESP8266 panel
* Un cable USB A tooType de Micro USB

También necesita Hola después cosas para el entorno de desarrollo:

* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
* Un equipo PC o Mac que ejecute Windows o Ubuntu.
* Red inalámbrica para compacto HUZZAH ESP8266 tooconnect a.
* Herramienta de configuración de Hola de toodownload de la conexión de Internet.
* [IDE de Arduino](https://www.arduino.cc/en/main/software) versión 1.6.8 o posterior. Las versiones anteriores no funcionan con la biblioteca de AzureIoT Hola.

Hello elementos siguientes son opcionales en caso de que no tiene un sensor. También tiene Hola opción consiste en utilizar datos de sensor simulada.

* Un sensor de temperatura y humedad Adafruit DHT22
* Una placa de pruebas
* Cables de puente M/M


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Conectar compacto HUZZAH ESP8266 con sensor de Hola y el equipo
En esta sección, se conecta tooyour placa de hello sensores. A continuación, conectar el equipo de tooyour de dispositivo para su uso posterior.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Conectar un tooFeather de sensor DHT22 temperatura y humedad HUZZAH ESP8266

Utilice hello breadboard y puentes cables toomake Hola conexión como se indica a continuación. Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.

![Referencia de conexiones](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Para el PIN de sensor, use Hola después de conectar:


| Inicio (sensor)           | Fin (placa)           | Color de cable   |
| -----------------------  | ---------------------- | ------------: |
| VDD (patilla 31F)            | 3V (patilla 58H)           | Cable rojo     |
| DATOS (patilla 32F)           | GPIO 2 (patilla 46)       | Cable azul    |
| GND (patilla 34F)            | GND (patilla 56I)          | Cable negro   |

Para más información, consulte la [instalación del sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) y el [patillaje de Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Ahora su Feather Huzzah ESP8266 debe estar conectado con un sensor de trabajo.

![Conectar DHT22 con Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Conectar compacto HUZZAH ESP8266 tooyour equipo

Tal y como se muestra a continuación, usar compacto HUZZAH ESP8266 tooyour equipo de hello Micro USB tooType A USB cable tooconnect.

![Conectar compacto Huzzah tooyour equipo](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Agregar permisos de puerto serie (solo Ubuntu)


Si usas Ubuntu, asegúrese de que tiene Hola permisos toooperate en hello USB puerto de desvanecimiento HUZZAH ESP8266. permisos de puerto serie tooadd, siga estos pasos:


1. Ejecute hello siguientes comandos en un terminal:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Obtener una Hola siguientes salidas:

   * crw-rw---- 1 root uucp xxxxxxxx
   * crw-rw---- 1 root dialout xxxxxxxx

   En la salida de hello, tenga en cuenta que `uucp` o `dialout` es nombre de propietario del grupo de Hola de hello puerto USB.

1. Agregar grupo de toohello de hello usuarios ejecutando Hola siguiente comando:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`es el nombre de propietario de grupo de Hola que obtuvo en el paso anterior de Hola. `<username>` es el nombre de usuario de Ubuntu.

1. Cierre la sesión de Ubuntu y, a continuación, inicie la sesión para tooappear de cambio de Hola.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Recopilar datos del sensor y enviarla tooyour centro de IoT

En esta sección, implementará y ejecutará una aplicación de ejemplo en Feather HUZZAH ESP8266. aplicación de ejemplo de Hola parpadea Hola LED de desvanecimiento HUZZAH ESP8266 y envía la temperatura de Hola y recopilan los datos de humedad de hello DHT22 sensor tooyour centro de IoT.

### <a name="get-hello-sample-application-from-github"></a>Obtener la aplicación de ejemplo de Hola desde GitHub

aplicación de ejemplo de Hola se hospeda en GitHub. Clonar el repositorio de ejemplo de Hola que contiene la aplicación de ejemplo de Hola desde GitHub. repositorio de ejemplo de Hola tooclone, siga estos pasos:

1. Abra un símbolo del sistema o una ventana de terminal.
1. Vaya carpeta tooa donde desea toobe de aplicación de ejemplo de Hola almacenado.
1. Ejecute el siguiente comando de hello:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Instalar el paquete de Hola para compacto HUZZAH ESP8266 Hola Arduino IDE:

1. Abra la carpeta de Hola donde se almacena la aplicación de ejemplo de Hola.
1. Abra el archivo de app.ino de hello en la carpeta de la aplicación Hola Hola Arduino IDE.

   ![Abra la aplicación de ejemplo de Hola en Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. Hola Arduino IDE, haga clic en **archivo** > **preferencias**.
1. Hola **preferencias** diálogo cuadro, haga clic en hello icono siguiente toohello **más direcciones URL del Administrador de paneles** cuadro.
1. En la ventana emergente de hello, escriba Hola después de la dirección URL y, a continuación, haga clic en **Aceptar**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Dirección url del paquete de punto tooa Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. Hola **preferencias** cuadro de diálogo, haga clic en **Aceptar**.
1. Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Boards Manager** (Administrador de placas) y busque esp8266.

   El administrador de placas indica que está instalado ESP8266 con la versión 2.2.0 o posterior.

   ![Hola esp8266 paquete está instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Instalación de las bibliotecas necesarias

1. Hola Arduino IDE, haga clic en **boceto** > **incluyen biblioteca** > **administrar bibliotecas de**.
1. Busque Hola siguiendo los nombres de las bibliotecas uno por uno. Para cada biblioteca que encuentre, haga clic en **Install** (Instalar).
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>¿No tiene un sensor DHT22 real?

aplicación de ejemplo de Hola puede simular la temperatura y humedad datos en caso de que no tiene un sensor DHT22 real. tooset los datos de toouse simulado de aplicación de ejemplo Hola, siga estos pasos:

1. Abra hello `config.h` archivo Hola `app` carpeta.
1. Busque Hola después de la línea de código y cambie el valor de Hola de `false` demasiado`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar datos de toouse simulado de aplicación de ejemplo de Hola](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Guardar archivo de hello con `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Implementar tooFeather de aplicación de ejemplo de Hola HUZZAH ESP8266

1. Hola Arduino IDE, haga clic en **herramienta** > **puerto**y, a continuación, haga clic en puerto serie Hola de desvanecimiento HUZZAH ESP8266.
1. Haga clic en **boceto** > **cargar** toobuild e implementar tooFeather de aplicación de ejemplo de Hola HUZZAH ESP8266.

### <a name="enter-your-credentials"></a>Escriba sus credenciales.

Una vez finalizada correctamente la carga de hello, siga estos pasos tooenter sus credenciales:

1. Hola Arduino IDE, haga clic en **herramientas** > **Monitor serie**.
1. En la ventana del monitor de la serie de hello, tenga en cuenta listas desplegables de hello dos en la esquina inferior derecha de Hola.
1. Seleccione **ningún final de línea** de lista desplegable de la izquierda Hola.
1. Seleccione **115.200 baudios** para la lista desplegable derecha de Hola.
1. En cuadro de entrada de hello situado en parte superior de saludo de la ventana del monitor de la serie de hello, escriba Hola siguiente información si se le solicita tooprovide y, a continuación, haga clic en **enviar**.
   * SSID de Wi-Fi
   * Contraseña de Wi-Fi
   * Cadena de conexión de dispositivo

> [!Note]
> información de credenciales de Hola se almacena en hello EEPROM de desvanecimiento HUZZAH ESP8266. Si hace clic en botón de restablecimiento de hello en Hola panel compacto HUZZAH ESP8266, aplicación de ejemplo de Hola le preguntará si desea que tooerase información de Hola. Escriba `Y` información de hello toohave borrado. Se le pide información de hello tooprovide una segunda vez.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Compruebe la aplicación de ejemplo de Hola se esté ejecutando correctamente

Si ve siguiente Hola de salida de la ventana del monitor de la serie de Hola y Hola parpadear LED de desvanecimiento HUZZAH ESP8266, aplicación de ejemplo de Hola se está ejecutando correctamente.

![Salida final en el IDE de Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Pasos siguientes

Está correctamente conectado un centro de IoT de desvanecimiento HUZZAH ESP8266 tooyour y envía el centro de IoT de hello capturan sensor datos tooyour. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

