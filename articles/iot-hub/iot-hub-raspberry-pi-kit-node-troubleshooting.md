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
# <a name="troubleshooting"></a><span data-ttu-id="66b04-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="66b04-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="66b04-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="66b04-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="66b04-106">aplicación de Hello se ejecuta bien pero Hola LED parpadea no</span><span class="sxs-lookup"><span data-stu-id="66b04-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="66b04-107">Este problema es siempre toohardware relacionados circuito conectividad.</span><span class="sxs-lookup"><span data-stu-id="66b04-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="66b04-108">Use los siguientes pasos tooidentify problemas de hello:</span><span class="sxs-lookup"><span data-stu-id="66b04-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="66b04-109">Compruebe que eligió Hola correcto **GPIO** en el panel.</span><span class="sxs-lookup"><span data-stu-id="66b04-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="66b04-110">Hola dos puertos deben ser **GPIO GND (Pin 6)** y **04 GPIO (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="66b04-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="66b04-111">Compruebe que la polaridad Hola de los LED sea correcta.</span><span class="sxs-lookup"><span data-stu-id="66b04-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="66b04-112">autenticación mutua de más de Hello debe indicar hello **positivo**, pin ánodo.</span><span class="sxs-lookup"><span data-stu-id="66b04-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="66b04-113">Hola de uso **anclar 3,3 v** y **GND Pin** frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="66b04-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="66b04-114">Tratar Pi como Hola corriente continua.</span><span class="sxs-lookup"><span data-stu-id="66b04-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="66b04-115">Compruebe que Hola LED funciona bien.</span><span class="sxs-lookup"><span data-stu-id="66b04-115">Check that hello LED works fine.</span></span>

![Especificación del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="66b04-117">Otros problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="66b04-117">Other hardware issues</span></span>
<span data-ttu-id="66b04-118">Para obtener información acerca de cómo solucionar problemas comunes de frambuesa Pi 3, vea hello [página oficial de solución de problemas](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="66b04-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="66b04-119">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="66b04-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="66b04-120">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="66b04-120">No response during gulp tasks</span></span>
<span data-ttu-id="66b04-121">Si tiene problemas en las tareas de gulp en ejecución, puede agregar hello `--verbose` opción para la depuración.</span><span class="sxs-lookup"><span data-stu-id="66b04-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="66b04-122">Probar tooterminate actual gulp tareas, puede usar Ctrl + C y, a continuación, ejecute el siguiente comando en los mensajes de depuración de toosee de ventana de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="66b04-123">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="66b04-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="66b04-124">Problemas de detección de dispositivos</span><span class="sxs-lookup"><span data-stu-id="66b04-124">Device discovery issues</span></span>
<span data-ttu-id="66b04-125">Para obtener ayuda para solucionar problemas comunes con hello `devdisco` comando, compruebe hello [Léame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="66b04-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="66b04-126">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="66b04-126">npm issues</span></span>
<span data-ttu-id="66b04-127">Intente tooupdate el paquete de npm con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="66b04-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="66b04-128">Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="66b04-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="66b04-129">Depuración remota</span><span class="sxs-lookup"><span data-stu-id="66b04-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="66b04-130">Ejecutar la aplicación de ejemplo de Hola en modo de depuración</span><span class="sxs-lookup"><span data-stu-id="66b04-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="66b04-131">Cuando el motor de depuración de hello está listo, debería ver ```Debugger listening on port 5858``` de salida de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="66b04-132">Configurar el dispositivo remoto de Visual Studio Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="66b04-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="66b04-133">Abra hello **depurar** panel en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="66b04-134">Haga clic en hello verde **Iniciar depuración** botón (F5).</span><span class="sxs-lookup"><span data-stu-id="66b04-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="66b04-135">Se abrirá un archivo launch.json en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="66b04-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="66b04-136">Actualizar archivo de hello launch.json con hello siguen contenido.</span><span class="sxs-lookup"><span data-stu-id="66b04-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="66b04-137">Reemplace `[device hostname or IP address]` con el nombre de host o dirección de la IP del dispositivo real Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="66b04-138">toolearn más información acerca de hello depuración de Visual Studio, consulte demasiado[depuración en código de Visual Studio](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="66b04-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="66b04-140">Asociar aplicación remota toohello</span><span class="sxs-lookup"><span data-stu-id="66b04-140">Attach toohello remote application</span></span>
<span data-ttu-id="66b04-141">Haga clic en hello verde **Iniciar depuración** toostart depuración de botón de (F5).</span><span class="sxs-lookup"><span data-stu-id="66b04-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="66b04-142">Lectura [JavaScript en VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn más información sobre el depurador de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Depuración remota interactiva](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="66b04-144">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="66b04-144">Azure CLI issues</span></span>
<span data-ttu-id="66b04-145">Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="66b04-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="66b04-146">soluciones de tooseek, puede usar hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="66b04-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="66b04-147">Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="66b04-148">Para obtener ayuda para solucionar problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="66b04-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="66b04-149">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="66b04-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="66b04-150">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="66b04-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="66b04-151">Al instalar pip, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="66b04-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="66b04-152">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="66b04-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="66b04-153">Algunos paquetes de pip de una instalación anterior se crearon raíz, lo que produce el error de permiso de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b04-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="66b04-154">Hola solución es tooremove esos paquetes instalados por la raíz.</span><span class="sxs-lookup"><span data-stu-id="66b04-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="66b04-155">Utilice Hola siguiendo los pasos toocomplete esta tarea:</span><span class="sxs-lookup"><span data-stu-id="66b04-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="66b04-156">Vaya a: /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="66b04-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="66b04-157">Muestre los paquetes creados en la raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="66b04-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="66b04-158">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="66b04-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="66b04-159">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="66b04-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="66b04-160">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="66b04-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="66b04-161">Si se ha aprovisionado correctamente el centro de IoT de Azure con Azure CLI y necesita una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, intente Hola después de herramientas.</span><span class="sxs-lookup"><span data-stu-id="66b04-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="66b04-162">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="66b04-162">Device explorer</span></span>
<span data-ttu-id="66b04-163">Hola [explorer dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) herramienta se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="66b04-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="66b04-164">Se comunica con los siguientes hello [los extremos del centro de IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="66b04-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="66b04-165">*Administración de identidad de dispositivo* tooprovision y administrar los dispositivos registrados con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="66b04-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="66b04-166">*Dispositivo para la nube de recepción* para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="66b04-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="66b04-167">*Enviar en la nube al dispositivo* para poder enviar mensajes tooyour dispositivos de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="66b04-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="66b04-168">Configurar la cadena de conexión de base de datos central de IoT dentro de esta herramienta toouse todas sus capacidades.</span><span class="sxs-lookup"><span data-stu-id="66b04-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="66b04-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="66b04-169">iothub-explorer</span></span>
<span data-ttu-id="66b04-170">[el centro de IOT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage dispositivos.</span><span class="sxs-lookup"><span data-stu-id="66b04-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="66b04-171">Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar mensajes en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="66b04-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="66b04-172">tooinstall Hola última versión (versión preliminar) de herramienta de explorador el centro de IOT de hello, ejecute el siguiente comando en el entorno de línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="66b04-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="66b04-173">Puede usar Hola siguiente Hola a tooget ayuda adicional acerca de todos los comandos de explorador el centro de IOT y sus parámetros de comando:</span><span class="sxs-lookup"><span data-stu-id="66b04-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="66b04-174">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="66b04-174">Azure portal</span></span>
<span data-ttu-id="66b04-175">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="66b04-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="66b04-176">También podría interesarle hello toouse [portal de Azure](../azure-portal-overview.md) toohelp aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="66b04-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="66b04-177">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="66b04-177">Azure Storage issues</span></span>
<span data-ttu-id="66b04-178">[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com) es una aplicación independiente de Microsoft que puede usar toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="66b04-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="66b04-179">Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="66b04-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="66b04-180">Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="66b04-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

