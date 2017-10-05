---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Solución de problemas | Microsoft Docs"
description: "Página de solución de problemas de Node.js para Raspberry Pi"
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
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="0baec-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="0baec-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="0baec-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="0baec-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="0baec-106">La aplicación se ejecuta correctamente, pero no el LED no está parpadeando.</span><span class="sxs-lookup"><span data-stu-id="0baec-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="0baec-107">Este problema siempre está relacionado con la conectividad del circuito de hardware.</span><span class="sxs-lookup"><span data-stu-id="0baec-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="0baec-108">Para identificar los problemas, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0baec-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="0baec-109">Compruebe si seleccionó el pin **GPIO** correcto en la placa.</span><span class="sxs-lookup"><span data-stu-id="0baec-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="0baec-110">Los dos puertos deberían ser **GPIO GND (pin 6)** y **GPIO 04 (pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="0baec-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="0baec-111">Compruebe que la polaridad de los LED es correcta.</span><span class="sxs-lookup"><span data-stu-id="0baec-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="0baec-112">La pata más larga debe indicar el pin ánodo **positivo**.</span><span class="sxs-lookup"><span data-stu-id="0baec-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="0baec-113">Utilice el **pin de 3,3 v** y el **pin GND** de Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="0baec-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="0baec-114">Trate Pi como si tuviera corriente continua.</span><span class="sxs-lookup"><span data-stu-id="0baec-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="0baec-115">Compruebe que el LED funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="0baec-115">Check that the LED works fine.</span></span>

![Especificación del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="0baec-117">Otros problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="0baec-117">Other hardware issues</span></span>
<span data-ttu-id="0baec-118">Para más información acerca de cómo solucionar problemas comunes en Raspberry Pi 3, consulte la [página oficial de solución de problemas](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="0baec-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="0baec-119">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="0baec-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="0baec-120">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="0baec-120">No response during gulp tasks</span></span>
<span data-ttu-id="0baec-121">Si tiene problemas para ejecutar tareas de Gulp, puede agregar la opción `--verbose` para depurar el código.</span><span class="sxs-lookup"><span data-stu-id="0baec-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="0baec-122">Trate de finalizar las tareas actuales de Gulp con Ctrl + C y ejecute el comando siguiente en la ventana de consola para ver los mensajes de depuración.</span><span class="sxs-lookup"><span data-stu-id="0baec-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="0baec-123">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="0baec-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="0baec-124">Problemas de detección de dispositivos</span><span class="sxs-lookup"><span data-stu-id="0baec-124">Device discovery issues</span></span>
<span data-ttu-id="0baec-125">Si necesita ayuda para solucionar problemas comunes con el comando `devdisco`, consulte el archivo [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="0baec-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="0baec-126">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="0baec-126">npm issues</span></span>
<span data-ttu-id="0baec-127">Intente actualizar el paquete de NPM con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0baec-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="0baec-128">Si el problema persiste, deje sus comentarios al final de este artículo o cree un problema de GitHub en el [repositorio de ejemplos](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0baec-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="0baec-129">Depuración remota</span><span class="sxs-lookup"><span data-stu-id="0baec-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="0baec-130">Ejecución de la aplicación de ejemplo en el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="0baec-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="0baec-131">Cuando el motor de depuración esté preparado, debería ver ```Debugger listening on port 5858``` en la salida de la consola.</span><span class="sxs-lookup"><span data-stu-id="0baec-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="0baec-132">Configuración de Visual Studio Code para establecer conexión con el dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="0baec-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="0baec-133">Abra el panel **Depurar** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="0baec-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="0baec-134">Haga clic en el botón **Iniciar depuración** de color verde (F5).</span><span class="sxs-lookup"><span data-stu-id="0baec-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="0baec-135">Se abrirá un archivo launch.json en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="0baec-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="0baec-136">Actualice este archivo con el siguiente contenido.</span><span class="sxs-lookup"><span data-stu-id="0baec-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="0baec-137">Reemplace `[device hostname or IP address]` por la dirección IP o el nombre de host reales del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0baec-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="0baec-138">Para más información sobre la depuración en Visual Studio, consulte [este artículo sobre la depuración en Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="0baec-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="0baec-140">Asociación a la aplicación remota</span><span class="sxs-lookup"><span data-stu-id="0baec-140">Attach to the remote application</span></span>
<span data-ttu-id="0baec-141">Haga clic en el color verde **Iniciar depuración** botón (F5) para iniciar la depuración.</span><span class="sxs-lookup"><span data-stu-id="0baec-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="0baec-142">Lea el documento de [JavaScript de VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) para obtener más información sobre el depurador.</span><span class="sxs-lookup"><span data-stu-id="0baec-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Depuración remota interactiva](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="0baec-144">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0baec-144">Azure CLI issues</span></span>
<span data-ttu-id="0baec-145">La interfaz de la línea de comandos de Azure (CLI de Azure ) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="0baec-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="0baec-146">Puede consultar la [guía de instalación de la versión preliminar](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) para buscar soluciones.</span><span class="sxs-lookup"><span data-stu-id="0baec-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="0baec-147">Si detecta los errores con la herramienta, envíe un [problema](https://github.com/Azure/azure-cli/issues) en la sección de **problemas** del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="0baec-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="0baec-148">Si necesita ayuda para solucionar problemas comunes, consulte el archivo [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="0baec-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="0baec-149">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="0baec-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="0baec-150">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="0baec-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="0baec-151">Al instalar pip, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="0baec-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="0baec-152">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="0baec-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="0baec-153">Algunos paquetes de pip se crearon en la raíz en una versión anterior, lo que produce este error de permisos.</span><span class="sxs-lookup"><span data-stu-id="0baec-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="0baec-154">La solución es quitar dichos paquetes instalados de raíz.</span><span class="sxs-lookup"><span data-stu-id="0baec-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="0baec-155">Realice los pasos siguientes para completar esta tarea:</span><span class="sxs-lookup"><span data-stu-id="0baec-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="0baec-156">Vaya a: /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="0baec-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="0baec-157">Muestre los paquetes creados en la raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="0baec-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="0baec-158">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="0baec-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="0baec-159">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="0baec-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="0baec-160">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0baec-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="0baec-161">Si el centro de Azure IoT Hub se ha aprovisionado correctamente con la CLI de Azure y necesita una herramienta que administre los dispositivos que se conectan a este centro, puede probar las siguientes herramientas.</span><span class="sxs-lookup"><span data-stu-id="0baec-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="0baec-162">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="0baec-162">Device explorer</span></span>
<span data-ttu-id="0baec-163">El [Explorador de dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) se ejecuta en el equipo local Windows y se conecta a IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="0baec-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="0baec-164">Además, se comunica con los siguientes [puntos de conexión de IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="0baec-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="0baec-165">*Administración de identidades de dispositivo* para aprovisionar y administrar los dispositivos registrados con su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0baec-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="0baec-166">*Recepción de mensajes del dispositivo a la nube*, para poder supervisar mensajes enviados desde el dispositivo al centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0baec-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="0baec-167">*Envío de mensajes de la nube al dispositivo*, para poder enviar mensajes a los dispositivos desde el centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0baec-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="0baec-168">Configure la cadena de conexión de IoT Hub con esta herramienta para que pueda utilizar todas las funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="0baec-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="0baec-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="0baec-169">iothub-explorer</span></span>
<span data-ttu-id="0baec-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) es una sencilla herramienta multiplataforma de CLI que se utiliza para administrar los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0baec-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="0baec-171">Esta herramienta puede usarse para administrar los dispositivos en el registro de identidad, supervisar los mensajes de dispositivo a nube y enviar mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0baec-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="0baec-172">Para instalar la última versión (versión preliminar) de la herramienta iothub-explorer, ejecute el siguiente comando en el entorno de la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="0baec-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="0baec-173">Puede utilizar el siguiente comando para obtener más ayuda sobre todos los comandos del Explorador de IoT Hub y sus parámetros:</span><span class="sxs-lookup"><span data-stu-id="0baec-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="0baec-174">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0baec-174">Azure portal</span></span>
<span data-ttu-id="0baec-175">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0baec-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="0baec-176">También puede utilizar [Azure Portal](../azure-portal-overview.md) para ayudar a aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="0baec-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="0baec-177">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0baec-177">Azure Storage issues</span></span>
<span data-ttu-id="0baec-178">El [Explorador de Microsoft Azure Storage (versión preliminar)](http://storageexplorer.com) es una aplicación independiente de Microsoft que permite trabajar con datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="0baec-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="0baec-179">Con esta herramienta, puede conectarse a la tabla y ver los datos que contiene.</span><span class="sxs-lookup"><span data-stu-id="0baec-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="0baec-180">Puede utilizar esta herramienta para solucionar los problemas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0baec-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

