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
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="8bd9d-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8bd9d-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="8bd9d-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="8bd9d-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="8bd9d-106">No se puede conectar SensorTag de TI</span><span class="sxs-lookup"><span data-stu-id="8bd9d-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="8bd9d-107">Para solucionar los problemas de conectividad de SensorTag, utilice la [aplicación SensorTag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="8bd9d-108">Tiene un problema con Intel NUC</span><span class="sxs-lookup"><span data-stu-id="8bd9d-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="8bd9d-109">Para solucionar problemas de arranque, vea [Troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html) (Solución de problemas de no arranque en Intel NUC).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="8bd9d-110">Para solucionar problemas del sistema operativo, vea [Troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html) (Solución de problemas del sistema operativo en Intel NUC).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="8bd9d-111">Para solucionar otros problemas, vea [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html) (Códigos intermitentes y sonoros para Intel NUC).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="8bd9d-112">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="8bd9d-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="8bd9d-113">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="8bd9d-113">No response during gulp tasks</span></span>

<span data-ttu-id="8bd9d-114">Si tiene problemas para ejecutar tareas de Gulp, puede agregar la opción `--verbose` para depurar el código.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="8bd9d-115">Trate de finalizar las tareas actuales de Gulp con `Ctrl + C` y ejecute el comando siguiente en la ventana de consola para ver los mensajes de depuración.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="8bd9d-116">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="8bd9d-117">Problemas de detección de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8bd9d-117">Device discovery issues</span></span>

<span data-ttu-id="8bd9d-118">Si necesita ayuda para solucionar problemas habituales con el comando `discover-sensortag`, vea la [página de la wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="8bd9d-119">problemas de npm</span><span class="sxs-lookup"><span data-stu-id="8bd9d-119">npm issues</span></span>

<span data-ttu-id="8bd9d-120">Intente actualizar el paquete de NPM mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bd9d-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="8bd9d-121">Si el problema persiste, deje sus comentarios al final de este artículo o cree un problema de GitHub en el [repositorio de ejemplos](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="8bd9d-122">Depuración remota</span><span class="sxs-lookup"><span data-stu-id="8bd9d-122">Remote Debugging</span></span>
> <span data-ttu-id="8bd9d-123">Las siguientes instrucciones están pensadas para depurar los scripts de Node.js utilizados en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="8bd9d-124">Ejecución de la aplicación de ejemplo en el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="8bd9d-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="8bd9d-125">Ejecute la aplicación de ejemplo en el modo de depuración mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bd9d-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="8bd9d-126">Cuando el motor de depuración esté preparado, debería ver `Debugger listening on port 5858` en la salida de la consola.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="8bd9d-127">Configuración de Visual Studio Code para establecer conexión con el dispositivo remoto</span><span class="sxs-lookup"><span data-stu-id="8bd9d-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="8bd9d-128">Abra el panel **Depurar** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="8bd9d-129">Haga clic en el botón **Iniciar depuración** de color verde (F5).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="8bd9d-130">Visual Studio Code abre un archivo `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="8bd9d-131">Actualice el archivo `launch.json` con el siguiente contenido.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="8bd9d-132">Reemplace `[device hostname or IP address]` por la dirección IP o el nombre de host reales del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="8bd9d-134">Asociación a la aplicación remota</span><span class="sxs-lookup"><span data-stu-id="8bd9d-134">Attach to the remote application</span></span>

<span data-ttu-id="8bd9d-135">Haga clic en el color verde **Iniciar depuración** botón (F5) para iniciar la depuración.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="8bd9d-136">Lea el documento de [JavaScript de VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) para obtener más información sobre el depurador.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![BLE de depuración de ejemplo](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="8bd9d-138">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8bd9d-138">Azure CLI issues</span></span>

<span data-ttu-id="8bd9d-139">La interfaz de la línea de comandos de Azure (CLI de Azure ) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="8bd9d-140">Puede consultar la [guía de instalación de la versión preliminar](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) para buscar soluciones.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="8bd9d-141">Si detecta los errores con la herramienta, envíe un [problema](https://github.com/Azure/azure-cli/issues) en la sección de **problemas** del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="8bd9d-142">Si necesita ayuda para solucionar problemas comunes, consulte el archivo [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="8bd9d-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="8bd9d-143">Si se encuentra un error que indica que no se ha podido encontrar una versión que satisfaga los requisitos, ejecute el siguiente comando para actualizar pip a la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="8bd9d-144">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="8bd9d-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="8bd9d-145">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="8bd9d-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="8bd9d-146">Al instalar pip, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="8bd9d-147">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="8bd9d-148">Algunos paquetes de pip se crearon en la raíz en una versión anterior, lo que produce este error de permisos.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="8bd9d-149">La solución es quitar dichos paquetes instalados de raíz.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="8bd9d-150">Realice los pasos siguientes para completar esta tarea:</span><span class="sxs-lookup"><span data-stu-id="8bd9d-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="8bd9d-151">Vaya a `/usr/local/lib/python2.7/site-packages`.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="8bd9d-152">Muestre los paquetes creados en la raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="8bd9d-153">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="8bd9d-154">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="8bd9d-155">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="8bd9d-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="8bd9d-156">Si la instancia de Azure IoT Hub se ha aprovisionado correctamente con la CLI de Azure y necesita una herramienta que administre los dispositivos que se conectan a su IoT Hub, puede probar las siguientes herramientas.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="8bd9d-157">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8bd9d-157">Device Explorer</span></span>

<span data-ttu-id="8bd9d-158">El [Explorador de dispositivos](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) se ejecuta en el equipo local Windows y se conecta a IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="8bd9d-159">Además, se comunica con los siguientes [puntos de conexión de IoT Hub](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="8bd9d-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="8bd9d-160">Administración de identidades de dispositivo para aprovisionar y administrar los dispositivos registrados con su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="8bd9d-161">Recepción de mensajes del dispositivo a la nube, para poder supervisar mensajes enviados desde el dispositivo a la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="8bd9d-162">Envío de mensajes de la nube al dispositivo, para poder enviar mensajes a los dispositivos desde la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="8bd9d-163">Configure la cadena de conexión de IoT Hub con esta herramienta para que pueda utilizar todas las funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="8bd9d-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="8bd9d-164">iothub-explorer</span></span>

<span data-ttu-id="8bd9d-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) es una sencilla herramienta multiplataforma de CLI que se utiliza para administrar los clientes de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="8bd9d-166">Esta herramienta puede usarse para administrar los dispositivos en el registro de identidad, supervisar los mensajes del dispositivo a la nube y enviar comandos de la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="8bd9d-167">Para instalar la última versión (preliminar) de la herramienta iothub-explorer, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bd9d-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="8bd9d-168">Para obtener más ayuda sobre todos los comandos del explorador de IoT Hub y sus parámetros, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bd9d-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="8bd9d-169">El Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8bd9d-169">The Azure portal</span></span>

<span data-ttu-id="8bd9d-170">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="8bd9d-171">También puede utilizar [Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) para ayudar a aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="8bd9d-172">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8bd9d-172">Azure Storage issues</span></span>

<span data-ttu-id="8bd9d-173">El [Explorador de Microsoft Azure Storage (versión preliminar)](http://storageexplorer.com/) es una aplicación independiente de Microsoft que permite trabajar con datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="8bd9d-174">Con esta herramienta, puede conectarse a la tabla y ver los datos que contiene.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="8bd9d-175">Puede utilizar esta herramienta para solucionar los problemas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8bd9d-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
