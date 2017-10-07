---
title: Connect Raspberry PI (C) tooAzure IoT - solucionar | Documentos de Microsoft
description: "Solución de problemas de página de la experiencia de frambuesa Pi Node.js Hola"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: problemas con iot, problemas con internet de las cosas
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Solución de problemas
## <a name="hardware-issues"></a>Problemas de hardware
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>aplicación de Hello se ejecuta bien pero Hola LED parpadea no
Este problema es siempre toohardware relacionados circuito conectividad. Use los siguientes pasos tooidentify problemas de hello:

1. Compruebe que eligió Hola correcto **GPIO** en el panel. Hola dos puertos deben ser **GPIO GND (Pin 6)** y **04 GPIO (Pin 7)**.
2. Compruebe que la polaridad Hola de los LED sea correcta. autenticación mutua de más de Hello debe indicar hello **positivo**, pin ánodo.
3. Hola de uso **anclar 3,3 v** y **GND Pin** frambuesa Pi 3. Tratar Pi como Hola corriente continua. Compruebe que Hola LED funciona bien.

![Especificación del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Otros problemas de hardware
Para obtener información acerca de cómo solucionar problemas comunes de frambuesa Pi 3, vea hello [página oficial de solución de problemas](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemas de paquetes en Node.js
### <a name="no-response-during-gulp-tasks"></a>Sin respuesta durante las tareas de Gulp
Si tiene problemas en las tareas de gulp en ejecución, puede agregar hello `--verbose` opción para la depuración. Probar tooterminate actual gulp tareas, puede usar Ctrl + C y, a continuación, ejecute el siguiente comando en los mensajes de depuración de toosee de ventana de consola de Hola. En la salida de la consola, deberían aparecer mensajes de error detallados.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemas de detección de dispositivos
Para obtener ayuda para solucionar problemas comunes con hello `devdisco` comando, compruebe hello [Léame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>problemas de npm
Intente tooupdate el paquete de npm con hello siguiente comando:

```bash
npm install -g npm
```

Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Depuración remota
### <a name="run-hello-sample-application-in-debug-mode"></a>Ejecutar la aplicación de ejemplo de Hola en modo de depuración
```bash
gulp run --debug
```

Cuando el motor de depuración de hello está listo, debería ver ```Debugger listening on port 5858``` de salida de la consola de Hola.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Configurar el dispositivo remoto de Visual Studio Code tooconnect toohello
1. Abra hello **depurar** panel en el lado izquierdo de Hola.
2. Haga clic en hello verde **Iniciar depuración** botón (F5). Se abrirá un archivo launch.json en Visual Studio Code.
3. Actualizar archivo de hello launch.json con hello siguen contenido. Reemplace `[device hostname or IP address]` con el nombre de host o dirección de la IP del dispositivo real Hola.

> [!NOTE]
> toolearn más información acerca de hello depuración de Visual Studio, consulte demasiado[depuración en código de Visual Studio](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


```json
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
            "remoteRoot": null
        }
    ]
}
```

![Configuración de depuración remota](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Asociar aplicación remota toohello
Haga clic en hello verde **Iniciar depuración** toostart depuración de botón de (F5).

Lectura [JavaScript en VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn más información sobre el depurador de Hola.

![Depuración remota interactiva](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemas de la CLI de Azure
Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar. soluciones de tooseek, puede usar hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.

Para obtener ayuda para solucionar problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problemas de instalación de Python
### <a name="legacy-installation-issues-macos"></a>Problemas de instalación de versiones antiguas (Mac OS)
Al instalar pip, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**. Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo. Algunos paquetes de pip de una instalación anterior se crearon raíz, lo que produce el error de permiso de Hola. Hola solución es tooremove esos paquetes instalados por la raíz. Utilice Hola siguiendo los pasos toocomplete esta tarea:

1. Vaya a: /usr/local/lib/python2.7/site-packages.
2. Muestre los paquetes creados en la raíz: `ls -l | grep root`.
3. Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.
4. Vuelva a instalar Python.

## <a name="azure-iot-hub-issues"></a>Problemas de Azure IoT Hub
Si se ha aprovisionado correctamente el centro de IoT de Azure con Azure CLI y necesita una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, intente Hola después de herramientas.

### <a name="device-explorer"></a>Explorador de dispositivos
Hola [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) herramienta se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure. Se comunica con los siguientes hello [los extremos del centro de IoT](iot-hub-devguide.md):


* *Administración de identidad de dispositivo* tooprovision y administrar los dispositivos registrados con el centro de IoT.
* *Dispositivo para la nube de recepción* para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.
* *Enviar en la nube al dispositivo* para poder enviar mensajes tooyour dispositivos de su centro de IoT.

Configurar la cadena de conexión de base de datos central de IoT dentro de esta herramienta toouse todas sus capacidades.

### <a name="iothub-explorer"></a>iothub-explorer
[el centro de IOT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage dispositivos. Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar mensajes en la nube al dispositivo.

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

