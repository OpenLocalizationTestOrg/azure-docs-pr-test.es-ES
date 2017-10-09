---
title: "Conectar frambuesa Pi (nodo) tooAzure IoT - lección 2: obtener herramientas (Ubuntu) | Documentos de Microsoft"
description: "Instalar Python y hello Azure interfaz de línea de comandos (CLI de Azure) en Mac OS."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: servicio en la nube iot, cli de azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3f35fae53a360a758bc8f61ed2063f7e2f2dc067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a>Obtención de las herramientas de Azure (macOS 10.10)
> [!div class="op_single_selector"]
> * [Windows 7 y versiones posteriores](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará
Instalar hello Azure interfaz de línea de comandos (CLI de Azure). Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

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
[Creación de un centro de IoT y registro de Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

