---
title: "Connect Intel Edison (C) tooAzure IoT - lección 1: Configurar dispositivo | Documentos de Microsoft"
description: Configure Intel Edison para usarlo por primera vez.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurar, conectar arduino toopc, el programa de instalación arduino, panel de arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a>Configuración de Intel Edison
## <a name="what-you-will-do"></a>Lo que hará
Configurar a Intel Edison para usarlos por primera vez ensamblando panel hello, activando la e instalación tooyour de herramienta de configuración de escritorio tooflash de SO firmware Edison, establecer su contraseña y conéctelo tooWi-Fi. Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* ¿Cómo tooassemble Edison del panel y enciéndalo.
* Cómo firmware tooflash Edison, establecer contraseña y conectarse Wi-Fi.

## <a name="what-you-need"></a>Lo que necesita
toocomplete esta operación, necesita Hola siguientes partes de su Intel Edison Starter Kit:

* El módulo Intel® Edison.
* La placa de expansión de Arduino.
* Las barras de separación o tornillos incluidos en el empaquetado de hello, incluida la tarjeta de expansión de dos tornillos toofasten Hola módulo toohello y cuatro conjuntos de tornillos y separadores de plástico.
* Un cable USB A tooType de Micro B
* Una fuente de alimentación de corriente continua (CC). La fuente de alimentación debe ser del siguiente tipo:
  - 7-15 V CC.
  - Un mínimo de 1500 mA.
  - pin de Hello center o interna debe ser polo positivo de Hola Hola de fuente de alimentación

  ![Los elementos del kit de inicio](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

También necesita lo siguiente:

* Un equipo con Windows, Mac o Linux.
* Una conexión inalámbrica para tooconnect Edison a.
* Una herramienta de configuración de toodownload de conexión de Internet.

## <a name="assemble-your-board"></a>Ensamblaje de la placa

Esta sección contiene pasos tooattach su tarjeta de expansión de Intel® Edison módulo tooyour.

1. Coloque el módulo de Intel® Edison de hello en esquema Hola blanco en su tarjeta de expansión, se alinea vulnerabilidades de hello en el módulo de hello con tornillos de hello en la tarjeta de expansión de Hola.

2. Mantenga presionada en módulo de hello justo debajo de palabras de hello `What will you make?` hasta que cree un complemento.

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. Utilice Hola dos frutos hexadecimal (incluidos en el paquete de hello) toosecure Hola módulo toohello expansión placa.

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Inserte un tornillo en uno de cuatro agujeros de esquina hello en la tarjeta de expansión de Hola. Retorcer y apriete uno de los separadores de plástico blanco hello en tornillo Hola.

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Repita este paso para Hola otros separadores de esquina de tres.

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Ya ha ensamblado la placa.

   ![Placa ensamblada](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Encendido de Edison

1. Conecte en fuente de alimentación de Hola.

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. Un LED verde (con la etiqueta DS1 en hello tarjeta de expansión Arduino *) debe encenderse y permanecer encendido.

3. Espere un minuto para hello panel toofinish arrancado.

   > [!NOTE]
   > Si no tiene una fuente de alimentación de controlador de dominio, puede placa de Hola de alimentación a través de un puerto USB. Consulte la sección `Connect Edison tooyour computer` para más información. La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.

## <a name="connect-edison-tooyour-computer"></a>Conectar Edison tooyour equipo

1. Alternar hacia abajo Hola microconmutador hacia Hola dos micro puertos USB para que Edison está en modo de dispositivo. Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Alternar hacia abajo microconmutador Hola](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Enchufe cable USB micro de hello en puerto USB de micro superior Hola.

   ![Puerto microUSB superior](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Plug Hola otro extremo del cable USB en el equipo.

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

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

¡Enhorabuena! Ha configurado correctamente Edison.

## <a name="summary"></a>Resumen
En este artículo, ha aprendido cómo tooassemble Hola panel Edison, flash su firmware, la contraseña de la instalación y conéctelo tooWi-Fi mediante la herramienta de configuración. Tenga en cuenta que Hola que LED aún no ilumina. Hola siguiente tarea es software como preparación para ejecutar una aplicación de ejemplo en Edison y herramientas que necesitan tooinstall Hola.

## <a name="next-steps"></a>Pasos siguientes
[Obtener herramientas de Hola][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md