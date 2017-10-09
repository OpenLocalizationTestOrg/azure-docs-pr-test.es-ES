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
# <a name="troubleshooting"></a><span data-ttu-id="74cbb-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="74cbb-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="74cbb-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="74cbb-105">Hardware issues</span></span>
<span data-ttu-id="74cbb-106">Para obtener información acerca de cómo solucionar problemas comunes en el panel de Adafruit compacto M0 Wi-Fi Arduino, vea hello [página oficial de solución de problemas](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="74cbb-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see hello [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="74cbb-107">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="74cbb-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="74cbb-108">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="74cbb-108">No response during gulp tasks</span></span>
<span data-ttu-id="74cbb-109">Si encuentra problemas al ejecutar gulp tareas, puede agregar hello `--verbose` opción para la depuración.</span><span class="sxs-lookup"><span data-stu-id="74cbb-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="74cbb-110">Intente tooterminate actual gulp tareas mediante el uso de `Ctrl + C`, y, a continuación, Hola ejecución siguiente comando en los mensajes de depuración de toosee de ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="74cbb-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="74cbb-111">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="74cbb-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="74cbb-112">O bien puede agregar `--listen` tooopen información del registro del dispositivo de puerto serie toooutput.</span><span class="sxs-lookup"><span data-stu-id="74cbb-112">Or you can add `--listen` tooopen serial port toooutput device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="74cbb-113">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="74cbb-113">NPM issues</span></span>
<span data-ttu-id="74cbb-114">Intente tooupdate el paquete NPM con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="74cbb-114">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="74cbb-115">Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="74cbb-115">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="74cbb-116">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="74cbb-116">Azure-CLI issues</span></span>
<span data-ttu-id="74cbb-117">Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="74cbb-117">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="74cbb-118">Busque soluciones en hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluciones.</span><span class="sxs-lookup"><span data-stu-id="74cbb-118">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="74cbb-119">Intente tooupgrade cli de Azure toolatest versión cuando comandos no funcionan según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="74cbb-119">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="74cbb-120">Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="74cbb-120">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="74cbb-121">Para obtener ayuda acerca de la solución de problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="74cbb-121">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="74cbb-122">Si se cumplen "No se pudo encontrar una versión que cumple el requisito de hello," por favor, siguiente ejecución Hola comando versión toolastest de tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="74cbb-122">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="74cbb-123">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="74cbb-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="74cbb-124">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="74cbb-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="74cbb-125">Al instalar **pip**, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="74cbb-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="74cbb-126">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="74cbb-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="74cbb-127">Algunos **pip** raíz, lo que provoca el error de permiso de Hola que se crearon paquetes desde una instalación anterior.</span><span class="sxs-lookup"><span data-stu-id="74cbb-127">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="74cbb-128">Hola solución es tooremove esos paquetes instalados por la raíz.</span><span class="sxs-lookup"><span data-stu-id="74cbb-128">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="74cbb-129">Utilice Hola siguiendo los pasos toocomplete esta tarea:</span><span class="sxs-lookup"><span data-stu-id="74cbb-129">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="74cbb-130">Vaya a: /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="74cbb-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="74cbb-131">Muestre los paquetes creados de raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="74cbb-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="74cbb-132">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="74cbb-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="74cbb-133">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="74cbb-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="74cbb-134">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="74cbb-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="74cbb-135">Si ha aprovisionado correctamente el centro de IoT de Azure con `azure-cli`, y necesitan una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, Hola try siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="74cbb-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="74cbb-136">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="74cbb-136">Device Explorer</span></span>
<span data-ttu-id="74cbb-137">[El Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="74cbb-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="74cbb-138">Se comunica con los siguientes hello [los extremos del centro de IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="74cbb-138">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="74cbb-139">*Administración de identidad de dispositivo* tooprovision y administrar los dispositivos registrados con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="74cbb-139">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="74cbb-140">*Dispositivo para la nube de recepción* para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="74cbb-140">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="74cbb-141">*Enviar en la nube al dispositivo* para poder enviar mensajes tooyour dispositivos de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="74cbb-141">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="74cbb-142">Configurar la `IoT hub connection string` dentro de esta herramienta toouse todas sus capacidades.</span><span class="sxs-lookup"><span data-stu-id="74cbb-142">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="74cbb-143">Explorador de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="74cbb-143">IoT hub Explorer</span></span>
<span data-ttu-id="74cbb-144">[Centro de IoT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage los clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="74cbb-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="74cbb-145">Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar comandos de nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="74cbb-145">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="74cbb-146">tooinstall Hola última versión (versión preliminar) de herramienta de explorador el centro de IOT de hello, ejecute el siguiente comando en el entorno de línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="74cbb-146">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="74cbb-147">Puede usar Hola siguiente Hola a tooget ayuda adicional acerca de todos los comandos de explorador el centro de IOT y sus parámetros de comando:</span><span class="sxs-lookup"><span data-stu-id="74cbb-147">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="74cbb-148">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="74cbb-148">Azure portal</span></span>
<span data-ttu-id="74cbb-149">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="74cbb-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="74cbb-150">También podría interesarle hello toouse [portal de Azure](../azure-portal-overview.md) toohelp aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="74cbb-150">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="74cbb-151">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="74cbb-151">Azure storage issues</span></span>
<span data-ttu-id="74cbb-152">[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com) es una aplicación independiente de Microsoft que puede usar toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="74cbb-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="74cbb-153">Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="74cbb-153">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="74cbb-154">Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="74cbb-154">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md