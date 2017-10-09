---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Solución de problemas | Microsoft Docs"
description: "Página de solución de problemas de la puerta de enlace de Intel NUC"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: problemas con iot, problemas con internet de las cosas
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="7afb4-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7afb4-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="7afb4-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="7afb4-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="7afb4-106">No se puede conectar SensorTag de TI</span><span class="sxs-lookup"><span data-stu-id="7afb4-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="7afb4-107">problemas de conectividad de tootroubleshoot SensorTag, usar hello [SensorTag aplicación](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="7afb4-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="7afb4-108">Tiene un problema con Intel NUC</span><span class="sxs-lookup"><span data-stu-id="7afb4-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="7afb4-109">tootroubleshoot problemas de arranque, consulte demasiado[solución de problemas de arranque No en Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="7afb4-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="7afb4-110">tootroubleshoot problemas del sistema operativo, consulte demasiado[solución de problemas del sistema operativo en Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="7afb4-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="7afb4-111">tootroubleshoot otros problemas, consulte demasiado[códigos de parpadear y emita un sonido para Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="7afb4-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="7afb4-112">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="7afb4-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="7afb4-113">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="7afb4-113">No response during gulp tasks</span></span>

<span data-ttu-id="7afb4-114">Si tiene problemas en las tareas de gulp en ejecución, puede agregar hello `--verbose` opción para la depuración.</span><span class="sxs-lookup"><span data-stu-id="7afb4-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="7afb4-115">Intente tooterminate actual gulp tareas mediante el uso de `Ctrl + C`, y, a continuación, Hola ejecución siguiente comando en los mensajes de depuración de toosee de ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="7afb4-116">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="7afb4-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="7afb4-117">Problemas de detección de dispositivos</span><span class="sxs-lookup"><span data-stu-id="7afb4-117">Device discovery issues</span></span>

<span data-ttu-id="7afb4-118">Para obtener ayuda para solucionar problemas comunes con hello `discover-sensortag` comando, compruebe hello [página wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="7afb4-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="7afb4-119">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="7afb4-119">npm issues</span></span>

<span data-ttu-id="7afb4-120">Intente tooupdate el paquete npm ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7afb4-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="7afb4-121">Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7afb4-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="7afb4-122">Depuración remota</span><span class="sxs-lookup"><span data-stu-id="7afb4-122">Remote Debugging</span></span>
> <span data-ttu-id="7afb4-123">Las siguientes instrucciones están pensadas para depurar los scripts de Node.js utilizados en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7afb4-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="7afb4-124">Ejecutar la aplicación de ejemplo de Hola en modo de depuración</span><span class="sxs-lookup"><span data-stu-id="7afb4-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="7afb4-125">Ejecute la aplicación de ejemplo de Hola en modo de depuración con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7afb4-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="7afb4-126">Cuando el motor de depuración de hello está listo, debería ver `Debugger listening on port 5858` de salida de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="7afb4-127">Configurar el dispositivo remoto de Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="7afb4-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="7afb4-128">Abra hello **depurar** panel en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="7afb4-129">Haga clic en hello verde **Iniciar depuración** botón (F5).</span><span class="sxs-lookup"><span data-stu-id="7afb4-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="7afb4-130">Visual Studio Code abre un archivo `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="7afb4-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="7afb4-131">Hola de actualización `launch.json` archivo con hello siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="7afb4-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="7afb4-132">Reemplace `[device hostname or IP address]` con el nombre de host o dirección de la IP del dispositivo real Hola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

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

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="7afb4-134">Asociar aplicación remota toohello</span><span class="sxs-lookup"><span data-stu-id="7afb4-134">Attach toohello remote application</span></span>

<span data-ttu-id="7afb4-135">Haga clic en hello verde **Iniciar depuración** toostart depuración de botón de (F5).</span><span class="sxs-lookup"><span data-stu-id="7afb4-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="7afb4-136">Lectura [JavaScript en VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn más información sobre el depurador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![BLE de depuración de ejemplo](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="7afb4-138">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="7afb4-138">Azure CLI issues</span></span>

<span data-ttu-id="7afb4-139">Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="7afb4-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="7afb4-140">soluciones de tooseek, puede usar hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="7afb4-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="7afb4-141">Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="7afb4-142">Para obtener ayuda para solucionar problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="7afb4-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="7afb4-143">Si se cumplen "No se pudo encontrar una versión que cumple el requisito de hello," por favor, siguiente ejecución Hola comando versión toolastest de tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="7afb4-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="7afb4-144">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="7afb4-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="7afb4-145">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="7afb4-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="7afb4-146">Al instalar pip, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="7afb4-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="7afb4-147">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="7afb4-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="7afb4-148">Algunos paquetes de pip de una instalación anterior se crearon raíz, lo que produce el error de permiso de Hola.</span><span class="sxs-lookup"><span data-stu-id="7afb4-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="7afb4-149">Hola solución es tooremove esos paquetes instalados por la raíz.</span><span class="sxs-lookup"><span data-stu-id="7afb4-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="7afb4-150">Utilice Hola siguiendo los pasos toocomplete esta tarea:</span><span class="sxs-lookup"><span data-stu-id="7afb4-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="7afb4-151">Vaya demasiado`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="7afb4-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="7afb4-152">Muestre los paquetes creados en la raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="7afb4-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="7afb4-153">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="7afb4-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="7afb4-154">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="7afb4-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="7afb4-155">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7afb4-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="7afb4-156">Si se ha aprovisionado correctamente el centro de IoT de Azure con hello Azure CLI y necesita una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, intente Hola después de herramientas.</span><span class="sxs-lookup"><span data-stu-id="7afb4-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="7afb4-157">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="7afb4-157">Device Explorer</span></span>

<span data-ttu-id="7afb4-158">[El Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="7afb4-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="7afb4-159">Se comunica con los siguientes hello [los extremos del centro de IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="7afb4-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="7afb4-160">Tooprovision de administración de identidad de dispositivo y administrar los dispositivos registrados con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7afb4-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="7afb4-161">Recibir el dispositivo a la nube para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7afb4-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="7afb4-162">Enviar en la nube al dispositivo para poder enviar mensajes tooyour dispositivos de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7afb4-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="7afb4-163">Configurar la cadena de conexión de base de datos central de IoT dentro de esta herramienta toouse todas sus capacidades.</span><span class="sxs-lookup"><span data-stu-id="7afb4-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="7afb4-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="7afb4-164">iothub-explorer</span></span>

<span data-ttu-id="7afb4-165">[el centro de IOT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage los clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7afb4-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="7afb4-166">Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar comandos de nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7afb4-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="7afb4-167">tooinstall Hola versión más reciente (versión preliminar) de herramienta de explorador el centro de IOT hello, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7afb4-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="7afb4-168">tooget ayuda adicional acerca de todos los Hola explorador el centro de IOT de comandos y sus parámetros, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="7afb4-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="7afb4-169">Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7afb4-169">hello Azure portal</span></span>

<span data-ttu-id="7afb4-170">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7afb4-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="7afb4-171">También podría interesarle hello toouse [portal de Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7afb4-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="7afb4-172">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7afb4-172">Azure Storage issues</span></span>

<span data-ttu-id="7afb4-173">[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com/) es una aplicación independiente de Microsoft que puede usar toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="7afb4-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="7afb4-174">Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="7afb4-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="7afb4-175">Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="7afb4-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
