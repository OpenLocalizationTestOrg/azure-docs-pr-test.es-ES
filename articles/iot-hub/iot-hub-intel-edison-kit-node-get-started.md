---
title: aaaIntel Edison toocloud (Node.js) - conectar Intel Edison tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse Intel Edison tooAzure centro de IoT para la plataforma de nube de Azure de Intel Edison toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel centro de iot edison, intel edison enviar datos toocloud, intel edison toocloud
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a>Conectar Intel Edison tooAzure centro de IoT (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con Edison de Intel. A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).

¿Aún no tiene un kit? Comience [aquí](https://azure.microsoft.com/develop/iot/starter-kits)

## <a name="what-you-do"></a>Qué debe hacer

* Configure Intel Edison y los módulos de Grove.
* Cree un IoT Hub.
* Registre un dispositivo para Edison en IoT Hub.
* Ejecutar una aplicación de ejemplo en el centro de IoT Edison toosend sensor datos tooyour.

Conectar el centro de IoT de tooan Edison de Intel que cree. A continuación, ejecutar una aplicación de ejemplo en Edison toocollect temperatura y humedad datos de un sensor de temperatura de arboleda. Por último, envíe centro de IoT de hello sensor datos tooyour.

## <a name="what-you-learn"></a>Conocimientos que adquirirá

* ¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.
* ¿Cómo tooconnect Edison con un sensor de temperatura de arboleda.
* ¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en Edison.
* Cómo centro de IoT de toosend sensor datos tooyour.

## <a name="what-you-need"></a>Lo que necesita

![Lo que necesita](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* Hola panel Edison de Intel
* La placa de expansión de Arduino.
* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
* Un equipo PC o Mac con Windows o Linux.
* Una conexión a Internet.
* Un cable USB A tooType de Micro B
* Una fuente de alimentación de corriente continua (CC). La fuente de alimentación debe ser del siguiente tipo:
  - 7-15 V CC.
  - Un mínimo de 1500 mA.
  - pin de Hello center o interna debe ser polo positivo de Hola Hola de fuente de alimentación

Hola siguientes elementos es opcional:

* Grove Base Shield V2
* Grove: sensor de temperatura
* Cable de Grove
* Las barras de separación o tornillos incluidos en el empaquetado de hello, incluida la tarjeta de expansión de dos tornillos toofasten Hola módulo toohello y cuatro conjuntos de tornillos y separadores de plástico.

> [!NOTE] 
Estos elementos son opcionales, porque la compatibilidad de ejemplo de código de hello había simulado los datos de sensor.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a>Configurar Intel Edison

### <a name="assemble-your-board"></a>Ensamblaje de la placa

Esta sección contiene pasos tooattach su tarjeta de expansión de Intel® Edison módulo tooyour.

1. Coloque el módulo de Intel® Edison de hello en esquema Hola blanco en su tarjeta de expansión, se alinea vulnerabilidades de hello en el módulo de hello con tornillos de hello en la tarjeta de expansión de Hola.

2. Mantenga presionada en módulo de hello justo debajo de palabras de hello `What will you make?` hasta que cree un complemento.

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. Utilice Hola dos frutos hexadecimal (incluidos en el paquete de hello) toosecure Hola módulo toohello expansión placa.

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. Inserte un tornillo en uno de cuatro agujeros de esquina hello en la tarjeta de expansión de Hola. Retorcer y apriete uno de los separadores de plástico blanco hello en tornillo Hola.

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. Repita este paso para Hola otros separadores de esquina de tres.

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

Ya ha ensamblado la placa.

   ![Placa ensamblada](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a>Conectar hello arboleda Base escudo y sensor de temperatura de Hola

1. Coloque hello arboleda Base escudo en panel de tooyour. Asegúrese de que todas las patillas estén bien conectadas a la placa.
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. Sensor de temperatura de uso arboleda Cable tooconnect arboleda en hello escudo de Base de arboleda **A0** puerto.

   ![Conecte sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Conexión de Edison y el sensor](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

Ahora el sensor está listo.

### <a name="power-up-edison"></a>Encendido de Edison

1. Conecte en fuente de alimentación de Hola.

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. Un LED verde (con la etiqueta DS1 en hello tarjeta de expansión Arduino *) debe encenderse y permanecer encendido.

3. Espere un minuto para hello panel toofinish arrancado.

   > [!NOTE]
   > Si no tiene una fuente de alimentación de controlador de dominio, puede placa de Hola de alimentación a través de un puerto USB. Consulte la sección `Connect Edison tooyour computer` para más información. La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.

### <a name="connect-edison-tooyour-computer"></a>Conectar Edison tooyour equipo

1. Alternar hacia abajo Hola microconmutador hacia Hola dos micro puertos USB para que Edison está en modo de dispositivo. Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Alternar hacia abajo microconmutador Hola](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. Enchufe cable USB micro de hello en puerto USB de micro superior Hola.

   ![Puerto microUSB superior](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. Plug Hola otro extremo del cable USB en el equipo.

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. Sabrá que la placa se ha terminado de inicializar cuando en el equipo aparezca una unidad nueva (es muy parecido a cuando se inserta una tarjeta SD en el equipo).

## <a name="download-and-run-hello-configuration-tool"></a>Descargue y ejecute la herramienta de configuración de Hola
Obtener la herramienta de configuración más reciente de Hola de [este vínculo](https://software.intel.com/en-us/iot/hardware/edison/downloads) aparecen en hello `Installers` encabezado. Ejecutar la herramienta de Hola y siga su pantalla instrucciones, hacer clic en siguiente cuando sea necesario

### <a name="flash-firmware"></a>Actualización del firmware
1. En hello `Set up options` página, haga clic en `Flash Firmware`.
2. Seleccione tooflash de imagen de hello en el panel, realice uno de los siguientes hello:
   - toodownload y flash, seleccione el panel con la imagen de firmware más reciente de hello disponible de Intel, `Download hello latest image version xxxx`.
   - Seleccione el panel con una imagen que ya se ha guardado en el equipo de tooflash `Select hello local image`. Busque la imagen de hello seleccione tooand desea tooflash tooyour panel.
3. herramienta de configuración de Hello intentará tooflash el panel. todo el proceso intermitente Hola puede tardar minutos too10.

### <a name="set-password"></a>Establecimiento de la contraseña
1. En hello `Set up options` página, haga clic en `Enable Security`.
2. Puede establecer un nombre personalizado para la placa Intel® Edison. Esto es opcional.
3. Escriba una contraseña para la placa y, luego, haga clic en `Set password`.
4. Marcar como inactiva la contraseña de hello, que se utiliza más adelante.

### <a name="connect-wi-fi"></a>Conexión a una red Wi-Fi
1. En hello `Set up options` página, haga clic en `Connect Wi-Fi`. Espera tooone minuto como los análisis del equipo para las redes Wi-Fi disponibles.
2. De hello `Detected Networks` lista desplegable, seleccione la red.
3. De hello `Security` lista desplegable, tipo de seguridad de la red de hello select.
4. Proporcione los datos de inicio de sesión y contraseña. Después, haga clic en `Configure Wi-Fi`.
5. Marcar como inactiva Hola dirección IP, que se utiliza más adelante.

> [!NOTE]
> Asegúrese de que ese Edison está conectado toohello misma red que el equipo. El equipo conecta tooyour Edison utilizando la dirección IP de Hola.

   ![Conecte sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

¡Enhorabuena! Ha configurado correctamente Edison.

## <a name="run-a-sample-application-on-intel-edison"></a>Ejecutar una aplicación de ejemplo en Intel Edison

### <a name="prepare-hello-azure-iot-device-sdk"></a>Preparar Hola SDK de dispositivos de IoT de Azure

1. Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host Edison de Intel. dirección IP de Hello procede de la herramienta de configuración de Hola y contraseña de hello es Hola uno que haya establecido en esa herramienta.
    - [PuTTY](http://www.putty.org/) para Windows.
    - cliente SSH integrado de Hello en Ubuntu o macOS.

2. Dispositivo de tooyour de la aplicación de cliente de ejemplo con clonación Hola. 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. A continuación, navegue Hola de toorun de carpeta toohello repositorio después comando tooinstall todos los paquetes, puede tardar serval minutos toocomplete.
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a>Configurar y ejecutar la aplicación de ejemplo de Hola

1. Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:

   ```bash
   nano config.json
   ```

   ![Archivo config](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   Hay dos macros en este archivo que se pueden configurar. Hello primero uno es `INTERVAL`, que define el intervalo de tiempo de hello entre dos mensajes que envían toocloud. Hola otra `simulatedData`, que es un valor booleano para si toouse simulado los datos de sensor o no.

   Si se **no tiene el sensor de hello**, hello establezca `simulatedData` valor demasiado`true` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.

1. Guarde y salga al presionar Control-O > Entrar > Control-X.


1. Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola.

Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.

![Salida: datos de sensor enviados desde el centro de IoT de Intel Edison tooyour](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a>Pasos siguientes

Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
