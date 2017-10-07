---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 2: herramientas de Azure (Windows) | Documentos de Microsoft"
description: "Instalar Python y hello Azure interfaz de línea de comandos (CLI de Azure) en Windows 7 y versiones posteriores."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: servicio en la nube iot, cli de azure
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: a3c083b5-0d76-46af-bc77-2ad7d8aadc1e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1819d61fafbee6ac42a1bea5c16437cd8bf43af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a>Obtención de las herramientas de Azure (Windows 7 o posterior)
> [!div class="op_single_selector"]
> * [Windows 7 y versiones posteriores](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)
> * [Ubuntu 16.04](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-ubuntu.md)
> * [macOS 10.10](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a>Lo que hará
Instalar Python y hello Azure interfaz de línea de comandos (CLI de Azure). Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Lo qué aprenderá
En este artículo, aprenderá lo siguiente:
* ¿Cómo tooinstall Python.
* ¿Cómo tooinstall Hola CLI de Azure.

## <a name="what-you-need"></a>Lo que necesita
* Un equipo Windows con conexión a Internet.
* Una suscripción de Azure activa. Si no tiene ninguna cuenta de Azure, cree una [cuenta de evaluación gratuita de Azure](http://azure.microsoft.com/pricing/free-trial/) en solo unos minutos.

## <a name="install-python"></a>Instalación de Python
[Instale Python](https://www.python.org/downloads/) en el equipo Windows. Puede instalar Python 2.7, 3.4 o 3.5. Este tutorial se basa en Python 2.7. Si ya ha instalado Python, vaya toohello próxima sección e instale Hola CLI de Azure.

También necesita ruta de acceso de tooadd Hola de carpetas de Hola donde python.exe y pip.exe son toohello instalado system `PATH` variable de entorno. De forma predeterminada, se instala python.exe en `C:\Python27` y pip.exe en `C:\Python27\Scripts`.

## <a name="install-hello-azure-cli"></a>Instalar Hola CLI de Azure
Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure. Puede trabaja directamente desde la línea de comandos tooprovision y administrar recursos.

Hola tooinstall CLI de Azure, siga estos pasos:

1. Abra una ventana de símbolo del sistema como administrador.
2. Ejecute hello siguientes comandos:

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. Comprobar la instalación de hello ejecutando Hola siguiente comando:

   ```bash
   az iot -h
   ```

Vea la siguiente Hola de salida si la instalación de hello es correcta.

![Resultado que indica una instalación correcta](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a>Resumen
Ha instalado Hola CLI de Azure. Su próximo tareas toocreate su identidad de concentrador y dispositivos de IoT de Azure mediante el uso de hello CLI de Azure.

## <a name="next-steps"></a>Pasos siguientes
[Creación de un centro de IoT y registro de Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md)

