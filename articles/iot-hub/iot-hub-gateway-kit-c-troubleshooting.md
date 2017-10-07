---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Solución de problemas | Microsoft Docs"
description: "Página de solución de problemas de la puerta de enlace de Intel NUC"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: problemas con iot, problemas con internet de las cosas
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Solución de problemas

## <a name="hardware-issues"></a>Problemas de hardware

### <a name="ti-sensortag-cannot-be-connected"></a>No se puede conectar SensorTag de TI

problemas de conectividad de tootroubleshoot SensorTag, usar hello [SensorTag aplicación](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Tiene un problema con Intel NUC

tootroubleshoot problemas de arranque, consulte demasiado[solución de problemas de arranque No en Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

tootroubleshoot problemas del sistema operativo, consulte demasiado[solución de problemas del sistema operativo en Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot otros problemas, consulte demasiado[códigos de parpadear y emita un sonido para Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Problemas de paquetes en Node.js

### <a name="no-response-during-gulp-tasks"></a>Sin respuesta durante las tareas de Gulp

Si tiene problemas en las tareas de gulp en ejecución, puede agregar hello `--verbose` opción para la depuración. Intente tooterminate actual gulp tareas mediante el uso de `Ctrl + C`, y, a continuación, Hola ejecución siguiente comando en los mensajes de depuración de toosee de ventana de consola. En la salida de la consola, deberían aparecer mensajes de error detallados.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemas de detección de dispositivos

Para obtener ayuda para solucionar problemas comunes con hello `discover-sensortag` comando, compruebe hello [página wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>problemas de npm

Intente tooupdate el paquete npm ejecutando Hola siguiente comando:

```bash
npm install -g npm
```

Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Depuración remota
> Las siguientes instrucciones están pensadas para depurar los scripts de Node.js utilizados en este tutorial.
### <a name="run-hello-sample-application-in-debug-mode"></a>Ejecutar la aplicación de ejemplo de Hola en modo de depuración

Ejecute la aplicación de ejemplo de Hola en modo de depuración con hello siguiente comando:

```bash
gulp run --debug
```

Cuando el motor de depuración de hello está listo, debería ver `Debugger listening on port 5858` de salida de la consola de Hola.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configurar el dispositivo remoto de Visual Studio Code tooconnect toohello

1. Abra hello **depurar** panel en el lado izquierdo de Hola.
2. Haga clic en hello verde **Iniciar depuración** botón (F5). Visual Studio Code abre un archivo `launch.json`.
3. Hola de actualización `launch.json` archivo con hello siguen contenido. Reemplace `[device hostname or IP address]` con el nombre de host o dirección de la IP del dispositivo real Hola.

   ``` json
   {
     "version": "0.2.0",
     "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Configuración de depuración remota](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Asociar aplicación remota toohello

Haga clic en hello verde **Iniciar depuración** toostart depuración de botón de (F5).

Lectura [JavaScript en VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn más información sobre el depurador de Hola.

![BLE de depuración de ejemplo](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Problemas de la CLI de Azure

Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar. soluciones de tooseek, puede usar hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.

Para obtener ayuda para solucionar problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).

Si se cumplen "No se pudo encontrar una versión que cumple el requisito de hello," por favor, siguiente ejecución Hola comando versión toolastest de tooupgrade pip.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemas de instalación de Python

### <a name="legacy-installation-issues-macos"></a>Problemas de instalación de versiones antiguas (Mac OS)

Al instalar pip, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**. Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo. Algunos paquetes de pip de una instalación anterior se crearon raíz, lo que produce el error de permiso de Hola. Hola solución es tooremove esos paquetes instalados por la raíz. Utilice Hola siguiendo los pasos toocomplete esta tarea:

1. Vaya demasiado`/usr/local/lib/python2.7/site-packages`
2. Muestre los paquetes creados en la raíz: `ls -l | grep root`.
3. Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.
4. Vuelva a instalar Python.

## <a name="azure-iot-hub-issues"></a>Problemas de Azure IoT Hub

Si se ha aprovisionado correctamente el centro de IoT de Azure con hello Azure CLI y necesita una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, intente Hola después de herramientas.

### <a name="device-explorer"></a>Explorador de dispositivos

[El Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure. Se comunica con los siguientes hello [los extremos del centro de IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Tooprovision de administración de identidad de dispositivo y administrar los dispositivos registrados con el centro de IoT.
- Recibir el dispositivo a la nube para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.
- Enviar en la nube al dispositivo para poder enviar mensajes tooyour dispositivos de su centro de IoT.

Configurar la cadena de conexión de base de datos central de IoT dentro de esta herramienta toouse todas sus capacidades.

### <a name="iothub-explorer"></a>iothub-explorer

[el centro de IOT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage los clientes de dispositivos. Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar comandos de nube al dispositivo.

tooinstall Hola versión más reciente (versión preliminar) de herramienta de explorador el centro de IOT hello, ejecute el siguiente comando de hello:

```bash
npm install -g iothub-explorer@latest
```

tooget ayuda adicional acerca de todos los Hola explorador el centro de IOT de comandos y sus parámetros, ejecute el siguiente comando de hello:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Hola portal de Azure

Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure. También podría interesarle hello toouse [portal de Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp aprovisionar, administrar y depurar los recursos de Azure.

## <a name="azure-storage-issues"></a>Problemas de Azure Storage

[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com/) es una aplicación independiente de Microsoft que puede usar toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux. Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella. Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.
