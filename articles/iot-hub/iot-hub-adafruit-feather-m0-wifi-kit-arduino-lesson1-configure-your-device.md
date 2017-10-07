---
title: "Connect Arduino (C) tooAzure IoT - lección 1: Configurar dispositivo | Documentos de Microsoft"
description: Configure Adafruit Feather M0 WiFi por primera vez.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurar, conectar arduino toopc, el programa de instalación arduino, panel de arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configuración del dispositivo
## <a name="what-you-will-do"></a>Lo que hará
Configurar el panel de Adafruit compacto M0 Wi-Fi Arduino para usarlos por primera vez ensamblando panel hello, activando una. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).

## <a name="what-you-need"></a>Lo que necesita
toocomplete esta operación, necesita Hola siguientes piezas el Starter Kit de Adafruit compacto M0 Wi-Fi:

* Hola panel Adafruit compacto M0 Wi-Fi
* Un cable USB A tooType de Micro B

![USB Micro B a Tipo A][kit]

También necesita lo siguiente:

* Un equipo con Windows, Mac o Linux.
* Una conexión inalámbrica para su tooconnect de panel Arduino a.
* Una herramienta de configuración de toodownload de conexión de Internet.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* Cómo tooassemble su panel de Arduino y la energía se hacia arriba para hello siguiendo lecciones.
* ¿Cómo tooadd permisos de puerto serie en Ubuntu.

## <a name="connect-your-arduino-board-tooyour-computer"></a>Conectar el equipo de tooyour Arduino panel

1. Enchufe cable USB micro de hello en puerto USB de micro superior Hola.

   ![Puerto microUSB superior][top-micro-usb-port]

2. Plug Hola otro extremo del cable USB en el equipo.

   ![Cable USB conectado a un equipo][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a>Adición de permisos de puerto serie en Ubuntu

Puede omitir esta sección si utiliza Windows o Mac OS. Para Ubuntu, deberá Hola siguiendo los pasos toomake usuario de linux normal de hello tenga toooperate de permisos de hello en el puerto USB de hello de la placa de Arduino.

1. Ahora como usuario normal del terminal:

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   Verá algo parecido a lo siguiente:

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   Hola "0" puede ser un número diferente, o se podrían devolver varias entradas. En los primeros datos de casos Hola Hola necesitamos es `uucp`, Hola en segundo lugar es `dialout`, que es propietario del grupo de Hola de archivo hello.

2. Agregar grupo de usuarios toohello toohello:

   ```bash
   sudo usermod -a -G group-name username
   ```

   Donde `group-name` es Hola se encontraron datos en el primer paso de Hola y `username` es el nombre de usuario de linux.

3. Necesitará toolog y de nuevo para este cambio tootake efecto y el programa de instalación de hello completa.

## <a name="summary"></a>Resumen
En este artículo, ha aprendido cómo tooconfigure el panel de Arduino. Hola siguiente tarea es software como preparación para ejecutar una aplicación de ejemplo en el panel de Arduino y herramientas que necesitan tooinstall Hola.

![El hardware está listo.][hardware-is-ready]

## <a name="next-steps"></a>Pasos siguientes
[Obtener herramientas de Hola][get-the-tools]
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md