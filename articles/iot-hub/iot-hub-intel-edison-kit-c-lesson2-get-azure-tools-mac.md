---
title: "Connect Intel Edison (C) tooAzure IoT - lección 2: herramientas de Azure (macOS) | Documentos de Microsoft"
description: "Instale Python la interfaz de la línea de comandos de Azure (CLI de Azure) en Mac OS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: CLI de Azure, servicio en la nube de IoT, Arduino en la nube
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0dfc9ff90e879d5fd03040016ac71a9fe4f4a744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obtención de las herramientas de Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 y versiones posteriores][windows]
> * [Ubuntu 16.04][ubuntu]
> * [macOS 10.10][macos]

## <a name="what-you-will-do"></a>Lo que hará
Instalar hello Azure interfaz de línea de comandos (CLI de Azure). Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* ¿Cómo tooinstall CLI de Azure.
* ¿Cómo tooadd un subgrupo de IoT de hello CLI de Azure.

## <a name="what-you-need"></a>Lo que necesita
* Un Mac con conexión a Internet.
* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, puede crear una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.

## <a name="install-python"></a>Instalación de Python
Aunque macOS incluye Python 2.7 fuera del cuadro de hello, se recomienda instalar Python a través de Homebrew. Consulte [Instalación de Python en Mac OS](http://docs.python-guide.org/en/latest/starting/install/osx/).

Instalar Python y pip ejecutando Hola siguiente comando:

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a>Instalar Hola CLI de Azure
Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure. Puede trabaja directamente desde la línea de comandos tooprovision y administrar recursos. 

tooinstall Hola CLI más reciente de Azure, siga estos pasos:

1. Ejecute hello siga los comandos en una ventana de terminal. Es posible que tarde cinco minutos tooinstall Hola CLI de Azure.

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. Comprobar la instalación de hello ejecutando Hola siguiente comando:

   ```bash
   az iot -h
   ```

Debería ver la siguiente Hola de salida si la instalación de hello es correcta.

![Resultado que indica una instalación correcta](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Resumen
Ha instalado Hola CLI de Azure. La siguiente tarea es toocreate su identidad de concentrador y dispositivos de IoT de Azure mediante el uso de Hola CLI de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Creación de una instancia de IoT Hub y registro de Intel Edison][create-your-iot-hub-and-register-intel-edison]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
