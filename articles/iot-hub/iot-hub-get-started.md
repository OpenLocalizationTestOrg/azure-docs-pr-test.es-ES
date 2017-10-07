---
title: 'Centro de IoT de Azure: empezar a conectar en la nube IoT dispositivos toohello | Documentos de Microsoft'
description: "Obtenga información acerca de cómo tooconnect los paneles de IoT y starter kits tooAzure centro de IoT. Los dispositivos pueden enviar telemetría tooIoT concentrador y centro de IoT pueden supervisar y administrar los dispositivos."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial de azure iot hub
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a>Tutoriales de introducción de Azure IoT Hub

Puede usar el centro de IoT de Azure y soluciones de hello Azure IoT dispositivos SDK toobuild Internet de las cosas (IoT):

* Centro de IoT de Azure es un servicio completamente administrado en la nube de Hola que se conecta, supervisa y administra los dispositivos de IoT de forma segura. Utilice Hola SDK de dispositivos de IoT de Azure tooimplement los dispositivos de IoT.
* Use una puerta de enlace de IoT en escenarios IoT más complejos. Por ejemplo, donde debe tooconsider factores como los dispositivos heredados, los costos de ancho de banda, las directivas de seguridad y privacidad o procesamiento de datos de borde. En estos casos, utilice Azure IoT borde tooimplement una puerta de enlace que se conecta el centro de IoT tooyour de dispositivos.

## <a name="what-hello-tutorials-cover"></a>Aspectos tratan en tutoriales de Hola

Estos tutoriales presentan tooAzure centro de IoT y el dispositivo de hello SDK. tutoriales de Hola cubren IoT escenarios toodemonstrate hello las funciones comunes de centro de IoT. Hello tutoriales también muestran cómo toocombine centro de IoT con otro Azure servicios y toobuild de las herramientas más eficaces soluciones de IoT. En los tutoriales de hello, puede elegir toouse dispositivos de IoT simulados o reales. Además, puede obtener información sobre cómo toouse un centro de IoT de puerta de enlace tooenable dispositivos tooconnect tooyour.

## <a name="set-up-your-device"></a>Configuración del dispositivo

Conectar un IoT dispositivo o puerta de enlace tooAzure centro de IoT. Puede elegir un tooget de dispositivo físico o simulada iniciado:

| Dispositivo IoT                       | Lenguaje de programación |
|----------------------------------|----------------------|
| Raspberry Pi                     | [Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]  |
| IoT DevKit                       | [Arduino en VSCode][DevKit]     |
| Intel Edison                     | [Node.js][Ed_Nd], [C][Ed_C]    |
| Adafruit Feather HUZZAH ESP8266  | [Arduino][Hu_Ard]              |
| Sparkfun ESP8266 Thing Dev       | [Arduino][Th_Ard]              |
| Adafruit Feather M0              | [Arduino][M0_Ard]              |
| Dispositivo simulado en PC           | [.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd] y [Python][Sim_Pyth] |
| Simulador de dispositivos en línea         | [Raspberry Pi (Node.js)][Ol_Sim] |

Además, puede usar un centro de IoT IoT borde puerta de enlace tooenable dispositivos tooconnect tooyour:

| Dispositivo de puerta de enlace               | Lenguaje de programación | Plataforma         |
|------------------------------|----------------------|------------------|
| Intel NUC (modelo DE3815TYKE) | C                    | [Wind River Linux][NUC_Lnx] |
| Puerta de enlace simulada            | C                    | [Linux][Sim_Lnx], [Windows][Sim_Win] |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
