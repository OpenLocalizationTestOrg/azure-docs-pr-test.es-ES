---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 1: Configurar dispositivo | Documentos de Microsoft"
description: "Configure frambuesa Pi 3 para usarlo por primera vez e instale hello Raspbian OS, un sistema operativo disponible que esté optimizado para hello hardware frambuesa Pi."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "instalación raspbian, descarga raspbian, cómo tooinstall raspbian, raspbian el programa de instalación, frambuesas pi instalación raspbian, frambuesas pi instalar os, frambuesas pi sd tarjeta install, frambuesas pi connect, conectar conectividad de pi de pi, frambuesas tooraspberry"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8ee9b23c-93f7-43ff-8ea1-e7761eb87a6f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ba3466f6d5d46352326a2a63eb011e117da5aca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a>Configuración del dispositivo
## <a name="what-you-will-do"></a>Lo que hará
Configure Pi para usarlos por primera vez e instale el sistema operativo de hello Raspbian. Raspbian es un sistema operativo disponible que esté optimizado para hello hardware frambuesa Pi. Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:

* Cómo tooinstall Raspbian sobre Pi.
* ¿Cómo toopower seguridad Pi mediante un cable USB.
* ¿Cómo tooconnect Pi toohello de red mediante un cable Ethernet o una red inalámbrica.
* Cómo breadboard tooadd un toohello LED y conéctelo tooPi.

## <a name="what-you-need"></a>Lo que necesita
toocomplete esta operación, necesita Hola siguientes partes de los Starter Kit de frambuesa Pi 3:

* Hola placa de frambuesa Pi 3
* tarjeta microSD de 16 GB de Hola
* Hola 5 voltios 2 amp alimentación con cable de hello pie 6 micro USB
* breadboard Hola
* Los cables conectores
* Una resistencia de 560 Ohm
* Un LED difuso de 10 mm
* Hola cable Ethernet

![Los elementos del kit de inicio](media/iot-hub-raspberry-pi-lessons/lesson1/starter_kit.jpg)

También necesita lo siguiente:

* Una conexión con cable o inalámbrica para Pi tooconnect a.
* Un SD USB adaptador o mini SD tooburn Hola SO imagen de la tarjeta a tarjeta microSD de Hola.
* Un equipo con Windows, Mac o Linux. equipo de Hello es usado tooinstall Raspbian en tarjeta microSD de Hola.
* Un toodownload de conexión de Internet Hola software y herramientas que necesitan.

## <a name="install-raspbian-on-hello-microsd-card"></a>Instalar Raspbian en tarjeta MicroSD de Hola
Preparar la tarjeta microSD de hello para la instalación de la imagen de Raspbian Hola.

1. Descargue Raspbian.
   1. [Descargar](https://www.raspberrypi.org/downloads/raspbian/) archivo .zip de hello para Raspbian Jessie con píxeles.
   2. Extraer hello Raspbian imagen tooa carpeta del equipo.
2. Instalar Raspbian toohello microSD tarjeta.
   1. [Descargar](https://www.etcher.io) e instalar la utilidad de grabadora de tarjeta de hello SD de creación.
   2. Ejecute creación y seleccione la imagen de Raspbian Hola que ha extraído en el paso 1.
   3. Seleccione la unidad de tarjeta microSD Hola.
      Tenga en cuenta que creación probablemente ya seleccionó unidad correcta Hola.
   4. Haga clic en **Flash** tooinstall Raspbian toohello microSD tarjeta.
   5. Quitar tarjeta microSD de hello del equipo cuando se completa la instalación.
      Es tarjeta microSD de tooremove seguro Hola directamente porque creación expulsa automáticamente o desmonta tarjeta microSD de hello tras la finalización.
   6. Inserte la tarjeta microSD de hello en el instalador de plataforma.

![Inserte una tarjeta SD Hola](media/iot-hub-raspberry-pi-lessons/lesson1/insert_sdcard.jpg)

## <a name="turn-on-pi"></a>Encendido de la Pi
Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola.

![Encendido](media/iot-hub-raspberry-pi-lessons/lesson1/micro_usb_power_on.jpg)

> [!NOTE]
> Es importante toouse Hola de alimentación en el kit de Hola por lo menos 2A toomake seguro de que su frambuesa tiene suficiente energía toowork correctamente.

## <a name="enable-ssh"></a>Habilite SSH
A partir de la versión de noviembre de 2016 de hello, Raspbian tiene servidor SSH Hola deshabilitada de forma predeterminada. Necesita tooenable lo manualmente. Puede hacer referencia a toohello [oficiales instrucciones](https://www.raspberrypi.org/documentation/remote-access/ssh/) o conectar un monitor y vaya demasiado**Preferencias -> configuración de frambuesa Pi** tooenable SSH.

## <a name="connect-raspberry-pi-3-toohello-network"></a>Conectar red toohello de frambuesa Pi 3
Puede conectarse tooa Pi con el cable de red o red inalámbrica tooa. Asegúrese de que ese Pi está conectado toohello misma red que el equipo. Por ejemplo, puede conectarse toohello Pi a que mismo conmutador que el equipo está conectado.

### <a name="connect-tooa-wired-network"></a>Conectar tooa de red cableada
Utilice Hola Ethernet por cable tooconnect tooyour de Pi de red cableada. Hello dos LED de Pi activar si se establece conexión Hola.

![Conexión mediante un cable Ethernet](media/iot-hub-raspberry-pi-lessons/lesson1/connect_ethernet.jpg)

### <a name="connect-tooa-wireless-network"></a>Conectar red inalámbrica tooa
Siga hello [instrucciones](https://www.raspberrypi.org/learning/software-guide/wifi/) de red inalámbrica de hello frambuesa Pi Foundation tooconnect Pi tooyour. Estas instrucciones requieren toofirst conectar un monitor y un teclado tooPi.

## <a name="connect-hello-led-toopi"></a>Conectar Hola LED tooPi
toocomplete esta tarea, utilice hello [breadboard](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard), Hola cables de conector, LED de Hola y Hola resistencia. Conéctelos toohello [entrada/salida de propósito general](https://www.raspberrypi.org/documentation/usage/gpio/) puertos (GPIO) de Pi.

![Placa de pruebas, LED y resistencia](media/iot-hub-raspberry-pi-lessons/lesson1/breadboard_led_resistor.jpg)

1. Conectar la autenticación mutua más corto de Hola de hello LED demasiado**GPIO GND (Pin 6)**.
2. Conectar la autenticación mutua en más de autenticación mutua de tooone LED de resistencia de Hola Hola Hola.
3. Conectar Hola otra sección de resistencia de hello demasiado**GPIO 4 (Pin 7)**.

Tenga en cuenta que la polaridad Hola LED es importante. Esta opción de polaridad comúnmente se conoce como "bajo activo".

![Diagrama de asignación de pines](media/iot-hub-raspberry-pi-lessons/lesson1/pinout_breadboard.png)

¡Enhorabuena! Ha configurado correctamente la Pi.

## <a name="summary"></a>Resumen
En este artículo, ha aprendido cómo Pi tooconfigure mediante la instalación Raspbian, conexión Pi tooa de la red y conecta un tooPi LED. Tenga en cuenta que Hola que LED aún no ilumina. Hola siguiente tarea es software en preparación para la ejecución de una aplicación de ejemplo sobre Pi y herramientas que necesitan tooinstall Hola.

![El hardware está listo.](media/iot-hub-raspberry-pi-lessons/lesson1/hardware_ready.jpg)

## <a name="next-steps"></a>Pasos siguientes
[Obtener herramientas de Hola](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

