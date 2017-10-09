---
title: aaaSimulated frambuesa Pi toocloud (Node.js) - conectar frambuesa Pi web simulador tooAzure centro de IoT | Documentos de Microsoft
description: Conectar frambuesa Pi web simulador tooAzure centro de IoT de frambuesa Pi toosend datos toohello nube de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centro de iot pi, de pi frambuesas simulador, azure iot frambuesas pi, frambuesas pi frambuesas enviar datos toocloud, frambuesas pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/7/2017
ms.author: xshi
ms.openlocfilehash: 0ebe1004e96ff4e64fdd1b05b7e35192ec42f7d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a>Conectar frambuesa Pi simulador online tooAzure centro de IoT (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con el simulador de frambuesa Pi en línea. A continuación, aprenderá cómo tooseamlessly conectarse en la nube Hola Pi simulador toohello mediante [centro de IoT de Azure](iot-hub-what-is-iot-hub.md). 

Si tiene dispositivos físicos, visite [conectar frambuesa Pi tooAzure centro de IoT](iot-hub-raspberry-pi-kit-node-get-started.md) tooget iniciado. 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a>Qué debe hacer

* Obtenga información acerca de conceptos básicos de Hola de simulador de frambuesa Pi en línea.
* Cree un Centro de IoT.
* Registre un dispositivo para Pi en IoT Hub.
* Ejecutar una aplicación de ejemplo en el centro de IoT de Pi toosend simulado sensor datos tooyour.

Conectar simulada centro de IoT de frambuesa Pi tooan creados por usted. A continuación, ejecutar una aplicación de ejemplo con datos del sensor de hello simulador toogenerate. Por último, envíe centro de IoT de hello sensor datos tooyour.

## <a name="what-you-learn"></a>Conocimientos que adquirirá

* ¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo. Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.
* ¿Cómo toowork con el simulador de frambuesa Pi en línea.
* Cómo centro de IoT de toosend sensor datos tooyour.

## <a name="overview-of-raspberry-pi-web-simulator"></a>Introducción al simulador web de Raspberry Pi

Haga clic en el simulador en línea de hello botón toolaunch frambuesa Pi.

> [!div class="button"]
[Iniciar simulador de Raspberry Pi](https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted)

Hay tres áreas en el simulador de hello web.
* Área de ensamblado - circuito de hello predeterminada es que una instrucción de procesamiento se conecta con un sensor BME280 y un LED. área de Hello está bloqueada en la versión de vista previa actualmente por lo que no puede realizar la personalización.
* Codificación de área, un editor de código en línea para toocode con frambuesa Pi. aplicación de ejemplo de Hola predeterminado ayuda a los datos del sensor toocollect desde BME280 sensor y envía tooyour centro de IoT de Azure. aplicación Hello es totalmente compatible con dispositivos reales de Pi. 
* Ventana de consola integrada - muestra la salida de hello del código. Hola parte superior de esta ventana, hay tres botones.
   * **Ejecute** -ejecutar aplicación hello en el área de código de hello.
   * **Restablecer** -Hola de restablecimiento de codificación de la aplicación de ejemplo de área toohello predeterminado.
   * **Doblar/expandir** - en hello derecho lado existe es un botón para que toofold/expandir Hola ventana de la consola.

> [!NOTE] 
simulador de web Pi frambuesa Hola ahora está disponible en versión preliminar. Nos gustaría toohear su propia voz hello [salón de chat de Gitter](https://gitter.im/Microsoft/raspberry-pi-web-simulator). código fuente de Hello es público en [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).

![Introducción al simulador en línea de Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a>Ejecución de una aplicación de ejemplo en el simulador web de Pi

1. En el área de código, asegúrese de que está trabajando en la aplicación de ejemplo de Hola predeterminada. Reemplace el marcador de posición de hello en línea 15 con hello cadena de conexión de dispositivo de centro de IoT de Azure.
   ![Reemplace la cadena de conexión de dispositivo de Hola](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)

2. Haga clic en **ejecutar** o tipo `npm start` aplicación de hello toorun.


Debería ver Hola después de salida que muestra los datos de sensor de Hola y mensajes de saludo que se envían centro de IoT tooyour ![salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)


## <a name="next-steps"></a>Pasos siguientes

Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
