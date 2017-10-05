---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 4: Solución de problemas | Microsoft Docs"
description: "Página de solución de problemas para la experiencia con Node.js de Intel Edison"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "solución de problemas de arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="5a944-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5a944-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="5a944-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="5a944-105">Hardware issues</span></span>
<span data-ttu-id="5a944-106">Para obtener más información sobre cómo solucionar problemas comunes en Intel Edison, consulte la [página oficial de solución de problemas](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="5a944-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="5a944-107">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="5a944-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="5a944-108">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="5a944-108">No response during gulp tasks</span></span>
<span data-ttu-id="5a944-109">Si tiene problemas para ejecutar tareas de Gulp, puede agregar la opción `--verbose` para realizar una depuración.</span><span class="sxs-lookup"><span data-stu-id="5a944-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="5a944-110">Trate de finalizar las tareas actuales de Gulp con `Ctrl + C` y, luego, ejecute el comando siguiente en la ventana de consola para ver los mensajes de depuración.</span><span class="sxs-lookup"><span data-stu-id="5a944-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="5a944-111">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="5a944-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="5a944-112">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="5a944-112">NPM issues</span></span>
<span data-ttu-id="5a944-113">Pruebe a ejecutar el paquete de NPM con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5a944-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="5a944-114">Si el problema persiste, deje sus comentarios al final de este artículo o cree un problema en GitHub dentro del [repositorio de ejemplos][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="5a944-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="5a944-115">Depuración remota</span><span class="sxs-lookup"><span data-stu-id="5a944-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="5a944-116">Ejecución de la aplicación de ejemplo en el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="5a944-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="5a944-117">Cuando el motor de depuración esté preparado, debería poder ver ```Debugger listening on port 5858``` en la salida de la consola.</span><span class="sxs-lookup"><span data-stu-id="5a944-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="5a944-118">Configuración de VS Code para conectarse al dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="5a944-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="5a944-119">Abra el panel **Depurar** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="5a944-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="5a944-120">Haga clic en el botón **Iniciar depuración** de color verde (F5).</span><span class="sxs-lookup"><span data-stu-id="5a944-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="5a944-121">VS Code debería abrir un archivo **launch.json**, que debe actualizar.</span><span class="sxs-lookup"><span data-stu-id="5a944-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="5a944-122">Actualice el archivo **launch.json** con el contenido siguiente. Reemplace `[device hostname or IP address]` con la dirección IP del dispositivo real o el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="5a944-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

![Configuración de depuración remota](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="5a944-124">Asociación a la aplicación remota</span><span class="sxs-lookup"><span data-stu-id="5a944-124">Attach to the remote application</span></span>

<span data-ttu-id="5a944-125">Haga clic en el botón de color verde **Iniciar depuración** (F5) para iniciar la depuración.</span><span class="sxs-lookup"><span data-stu-id="5a944-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="5a944-126">Puede leer el documento de [JavaScript de VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) para obtener más información sobre el depurador.</span><span class="sxs-lookup"><span data-stu-id="5a944-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Depuración remota interactiva](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="5a944-128">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5a944-128">Azure-CLI issues</span></span>
<span data-ttu-id="5a944-129">La interfaz de la línea de comandos de Azure (CLI de Azure ) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="5a944-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="5a944-130">Busque soluciones en la [Guía de instalación de la versión preliminar](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="5a944-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="5a944-131">Trate de actualizar la CLI de Azure a la versión más reciente cuando los comandos no funcionen según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="5a944-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="5a944-132">Si detecta los errores con la herramienta, envíe un [problema](https://github.com/Azure/azure-cli/issues) en la sección de **problemas** del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a944-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="5a944-133">Para obtener ayuda sobre la solución de problemas comunes, consulte el archivo [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="5a944-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="5a944-134">Si se encuentra un error que indica que no se ha podido encontrar una versión que satisfaga los requisitos, ejecute el siguiente comando para actualizar pip a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="5a944-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="5a944-135">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="5a944-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="5a944-136">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="5a944-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="5a944-137">Al instalar **pip**, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="5a944-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="5a944-138">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="5a944-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="5a944-139">Algunos paquetes **pip** de una instalación anterior se crearon de raíz, lo que provoca el error de permiso.</span><span class="sxs-lookup"><span data-stu-id="5a944-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="5a944-140">La solución es quitar dichos paquetes instalados de raíz.</span><span class="sxs-lookup"><span data-stu-id="5a944-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="5a944-141">Realice los pasos siguientes para completar esta tarea:</span><span class="sxs-lookup"><span data-stu-id="5a944-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="5a944-142">Vaya a: /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="5a944-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="5a944-143">Muestre los paquetes creados de raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="5a944-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="5a944-144">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="5a944-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="5a944-145">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="5a944-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="5a944-146">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a944-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="5a944-147">Si el centro de IoT Hub de Azure se ha aprovisionado correctamente con `azure-cli` y necesita una herramienta que administre los dispositivos que se conectan a este centro, puede probar las siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="5a944-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="5a944-148">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="5a944-148">Device Explorer</span></span>
<span data-ttu-id="5a944-149">El [Explorador de dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) se ejecuta en el equipo local Windows y se conecta a IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a944-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="5a944-150">Además, se comunica con los siguientes [puntos de conexión de IoT Hub](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="5a944-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="5a944-151">_Administración de identidades de dispositivo_ para aprovisionar y administrar los dispositivos registrados con su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a944-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="5a944-152">_Recepción de mensajes del dispositivo a la nube_, para poder supervisar mensajes enviados desde el dispositivo al centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a944-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="5a944-153">_Envío de mensajes de la nube al dispositivo_, para poder enviar mensajes a los dispositivos desde el centro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a944-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="5a944-154">Configurar `IoT hub connection string` dentro de esta herramienta para usar todas sus funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="5a944-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="5a944-155">Explorador de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5a944-155">IoT hub Explorer</span></span>
<span data-ttu-id="5a944-156">El [Explorador de IoT Hub](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo para administrar clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="5a944-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="5a944-157">Esta herramienta puede usarse para administrar los dispositivos en el registro de identidad, supervisar los mensajes del dispositivo a la nube y enviar comandos de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5a944-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="5a944-158">Para instalar la última versión (versión preliminar) de la herramienta iothub-explorer, ejecute el siguiente comando en el entorno de la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="5a944-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="5a944-159">Puede utilizar el siguiente comando para obtener más ayuda sobre todos los comandos del Explorador de IoT Hub y sus parámetros:</span><span class="sxs-lookup"><span data-stu-id="5a944-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="5a944-160">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="5a944-160">Azure portal</span></span>
<span data-ttu-id="5a944-161">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a944-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="5a944-162">También puede utilizar [Azure Portal](../azure-portal-overview.md) para ayudar a aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5a944-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="5a944-163">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5a944-163">Azure storage issues</span></span>
<span data-ttu-id="5a944-164">El [Explorador de Microsoft Azure Storage (versión preliminar)](http://storageexplorer.com) es una aplicación independiente de Microsoft que permite trabajar con datos de [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="5a944-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="5a944-165">Con esta herramienta, puede conectarse a la tabla y ver los datos que contiene.</span><span class="sxs-lookup"><span data-stu-id="5a944-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="5a944-166">Puede utilizar esta herramienta para solucionar los problemas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5a944-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a944-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5a944-167">Next steps</span></span>
<span data-ttu-id="5a944-168">Esta página solo incluye los problemas más comunes del kit de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="5a944-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="5a944-169">También puede dejar comentarios en la parte inferior para que podamos solucionar problemas adicionales.</span><span class="sxs-lookup"><span data-stu-id="5a944-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="5a944-170">Volver a [Introducción a Intel Edison (C)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5a944-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started