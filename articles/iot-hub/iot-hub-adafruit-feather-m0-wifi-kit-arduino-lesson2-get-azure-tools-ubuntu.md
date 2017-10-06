---
title: "Conectar Arduino tooAzure IoT - lección 2: herramientas de Azure (Ubuntu) | Documentos de Microsoft"
description: "Instale Python y la interfaz de la línea de comandos de Azure (CLI de Azure) en Ubuntu."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: CLI de Azure, servicio en la nube de IoT, Arduino en la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7eb9c891a6340fee018894883583022d740ecb6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a>Obtención de las herramientas de Azure (Ubuntu 16.04)

> [!div class="op_single_selector"]
> * [Windows 7 o posterior][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Lo que hará

Instalar hello Azure interfaz de línea de comandos (CLI de Azure). Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) de su placa Adafruit compacto M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* ¿Cómo tooinstall Hola CLI de Azure.
* ¿Cómo tooadd un subgrupo de IoT de hello CLI de Azure.

## <a name="what-you-need"></a>Lo que necesita
* Un equipo con Ubuntu con conexión a Internet.
* Una suscripción de Azure activa. Si no tiene ninguna, puede crear una [cuenta de evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) en tan solo unos minutos.

## <a name="install-hello-azure-cli"></a>Instalar Hola CLI de Azure
Hola CLI de Azure proporciona una experiencia multiplataforma de línea de comandos de Azure, permitiéndole toowork directamente desde la línea de comandos tooprovision y administrar los recursos.

tooinstall Hola CLI más reciente de Azure, siga estos pasos:

1. Ejecute hello siga los comandos en una ventana de terminal. Es posible que tarde cinco minutos tooinstall Hola CLI de Azure.

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. Comprobar la instalación de hello ejecutando Hola siguiente comando:

   ```bash
   az iot -h
   ```

Debería ver la siguiente Hola de salida si la instalación de hello es correcta.

![Resultado que indica una instalación correcta][output]

## <a name="summary"></a>Resumen
Ha instalado Hola CLI de Azure. La siguiente tarea es toocreate su centro de IoT de Azure y la identidad del dispositivo a través Hola CLI de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Creación de la instancia de IoT Hub y registro de Raspberry Pi][create-your-iot-hub-and-register-your-arduino-board]
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md