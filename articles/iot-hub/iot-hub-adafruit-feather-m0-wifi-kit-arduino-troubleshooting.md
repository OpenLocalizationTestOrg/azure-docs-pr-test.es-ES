---
title: Connect Arduino (C) tooAzure IoT - solucionar | Documentos de Microsoft
description: "Página de solución de problemas de experiencia de Adafruit Feather M0 WiFi Arduino"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Solución de problemas de Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Solución de problemas
## <a name="hardware-issues"></a>Problemas de hardware
Para obtener información acerca de cómo solucionar problemas comunes en el panel de Adafruit compacto M0 Wi-Fi Arduino, vea hello [página oficial de solución de problemas](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).

## <a name="nodejs-package-issues"></a>Problemas de paquetes en Node.js
### <a name="no-response-during-gulp-tasks"></a>Sin respuesta durante las tareas de Gulp
Si encuentra problemas al ejecutar gulp tareas, puede agregar hello `--verbose` opción para la depuración. Intente tooterminate actual gulp tareas mediante el uso de `Ctrl + C`, y, a continuación, Hola ejecución siguiente comando en los mensajes de depuración de toosee de ventana de consola. En la salida de la consola, deberían aparecer mensajes de error detallados.

```bash
gulp --verbose
```

O bien puede agregar `--listen` tooopen información del registro del dispositivo de puerto serie toooutput.

```bash
gulp --listen
``` 

### <a name="npm-issues"></a>Problemas de NPM
Intente tooupdate el paquete NPM con hello siguiente comando:

```bash
npm install -g npm
```

Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo][sample-repository].

## <a name="azure-cli-issues"></a>Problemas de la CLI de Azure
Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar. Busque soluciones en hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluciones. Intente tooupgrade cli de Azure toolatest versión cuando comandos no funcionan según lo previsto.

Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.

Para obtener ayuda acerca de la solución de problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).

Si se cumplen "No se pudo encontrar una versión que cumple el requisito de hello," por favor, siguiente ejecución Hola comando versión toolastest de tooupgrade pip.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemas de instalación de Python
### <a name="legacy-installation-issues-macos"></a>Problemas de instalación de versiones antiguas (Mac OS)
Al instalar **pip**, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**. Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo. Algunos **pip** raíz, lo que provoca el error de permiso de Hola que se crearon paquetes desde una instalación anterior. Hola solución es tooremove esos paquetes instalados por la raíz. Utilice Hola siguiendo los pasos toocomplete esta tarea:

1. Vaya a: /usr/local/lib/python2.7/site-packages.
2. Muestre los paquetes creados de raíz: `ls -l | grep root`.
3. Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.
4. Vuelva a instalar Python.

## <a name="azure-iot-hub-issues"></a>Problemas de Azure IoT Hub
Si ha aprovisionado correctamente el centro de IoT de Azure con `azure-cli`, y necesitan una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, Hola try siguientes herramientas:

### <a name="device-explorer"></a>Explorador de dispositivos
[El Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure. Se comunica con los siguientes hello [los extremos del centro de IoT](iot-hub-devguide.md):

* *Administración de identidad de dispositivo* tooprovision y administrar los dispositivos registrados con el centro de IoT.
* *Dispositivo para la nube de recepción* para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.
* *Enviar en la nube al dispositivo* para poder enviar mensajes tooyour dispositivos de su centro de IoT.

Configurar la `IoT hub connection string` dentro de esta herramienta toouse todas sus capacidades.

### <a name="iot-hub-explorer"></a>Explorador de IoT Hub
[Centro de IoT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage los clientes de dispositivos. Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar comandos de nube al dispositivo.


tooinstall Hola última versión (versión preliminar) de herramienta de explorador el centro de IOT de hello, ejecute el siguiente comando en el entorno de línea de comandos de hello:

```bash
npm install -g iothub-explorer@latest
```

Puede usar Hola siguiente Hola a tooget ayuda adicional acerca de todos los comandos de explorador el centro de IOT y sus parámetros de comando:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure Portal
Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure. También podría interesarle hello toouse [portal de Azure](../azure-portal-overview.md) toohelp aprovisionar, administrar y depurar los recursos de Azure.

## <a name="azure-storage-issues"></a>Problemas de Azure Storage
[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com) es una aplicación independiente de Microsoft que puede usar toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux. Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella. Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md