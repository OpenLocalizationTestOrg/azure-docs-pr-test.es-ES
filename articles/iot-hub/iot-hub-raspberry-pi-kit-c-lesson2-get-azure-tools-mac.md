---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 2: herramientas de Azure (macOS) | Documentos de Microsoft"
description: "Instale Python la interfaz de la línea de comandos de Azure (CLI de Azure) en Mac OS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio en la nube iot, cli de azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f2d7d584-7734-401c-976c-81788a7282a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a079250fd94fa9bc1c11b6c21de02a8d46f6f3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obtención de las herramientas de Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 y versiones posteriores](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará
Instalar hello Azure interfaz de línea de comandos (CLI de Azure). Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

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

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a>Resumen
Ha instalado Hola CLI de Azure. La siguiente tarea es toocreate su identidad de concentrador y dispositivos de IoT de Azure mediante el uso de Hola CLI de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Creación de un centro de IoT y registro de Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

