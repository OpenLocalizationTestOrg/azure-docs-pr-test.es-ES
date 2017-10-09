---
title: "Connect Intel Edison (C) tooAzure IoT: solución de problemas | Documentos de Microsoft"
description: "Página de solución de problemas para la experiencia de Intel Edison (C)"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Solución de problemas de Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="1741d-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="1741d-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="1741d-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="1741d-105">Hardware issues</span></span>
<span data-ttu-id="1741d-106">Para obtener información acerca de cómo solucionar problemas comunes de Intel Edison, vea hello [página oficial de solución de problemas](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="1741d-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="1741d-107">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="1741d-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="1741d-108">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="1741d-108">No response during gulp tasks</span></span>
<span data-ttu-id="1741d-109">Si encuentra problemas al ejecutar gulp tareas, puede agregar hello `--verbose` opción para la depuración.</span><span class="sxs-lookup"><span data-stu-id="1741d-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="1741d-110">Intente tooterminate actual gulp tareas mediante el uso de `Ctrl + C`, y, a continuación, Hola ejecución siguiente comando en los mensajes de depuración de toosee de ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="1741d-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="1741d-111">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="1741d-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="1741d-112">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="1741d-112">NPM issues</span></span>
<span data-ttu-id="1741d-113">Intente tooupdate el paquete NPM con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="1741d-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="1741d-114">Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="1741d-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="1741d-115">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1741d-115">Azure-CLI issues</span></span>
<span data-ttu-id="1741d-116">Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="1741d-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="1741d-117">Busque soluciones en hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluciones.</span><span class="sxs-lookup"><span data-stu-id="1741d-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="1741d-118">Intente tooupgrade cli de Azure toolatest versión cuando comandos no funcionan según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="1741d-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="1741d-119">Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="1741d-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="1741d-120">Para obtener ayuda acerca de la solución de problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="1741d-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="1741d-121">Si se cumplen "No se pudo encontrar una versión que cumple el requisito de hello," por favor, siguiente ejecución Hola comando versión toolastest de tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="1741d-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="1741d-122">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="1741d-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="1741d-123">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="1741d-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="1741d-124">Al instalar **pip**, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="1741d-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="1741d-125">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="1741d-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="1741d-126">Algunos **pip** raíz, lo que provoca el error de permiso de Hola que se crearon paquetes desde una instalación anterior.</span><span class="sxs-lookup"><span data-stu-id="1741d-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="1741d-127">Hola solución es tooremove esos paquetes instalados por la raíz.</span><span class="sxs-lookup"><span data-stu-id="1741d-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="1741d-128">Utilice Hola siguiendo los pasos toocomplete esta tarea:</span><span class="sxs-lookup"><span data-stu-id="1741d-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="1741d-129">Vaya a: /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="1741d-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="1741d-130">Muestre los paquetes creados de raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="1741d-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="1741d-131">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="1741d-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="1741d-132">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="1741d-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="1741d-133">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1741d-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="1741d-134">Si ha aprovisionado correctamente el centro de IoT de Azure con `azure-cli`, y necesitan una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, Hola try siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="1741d-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="1741d-135">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="1741d-135">Device Explorer</span></span>
<span data-ttu-id="1741d-136">[El Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="1741d-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="1741d-137">Se comunica con los siguientes hello [los extremos del centro de IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="1741d-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="1741d-138">_Administración de identidad de dispositivo_ tooprovision y administrar los dispositivos registrados con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1741d-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="1741d-139">_Dispositivo para la nube de recepción_ para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1741d-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="1741d-140">_Enviar en la nube al dispositivo_ para poder enviar mensajes tooyour dispositivos de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="1741d-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="1741d-141">Configurar la `IoT hub connection string` dentro de esta herramienta toouse todas sus capacidades.</span><span class="sxs-lookup"><span data-stu-id="1741d-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="1741d-142">Explorador de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="1741d-142">IoT hub Explorer</span></span>
<span data-ttu-id="1741d-143">[Centro de IoT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage los clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1741d-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="1741d-144">Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar comandos de nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1741d-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="1741d-145">tooinstall Hola última versión (versión preliminar) de herramienta de explorador el centro de IOT de hello, ejecute el siguiente comando en el entorno de línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="1741d-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="1741d-146">Puede usar Hola siguiente Hola a tooget ayuda adicional acerca de todos los comandos de explorador el centro de IOT y sus parámetros de comando:</span><span class="sxs-lookup"><span data-stu-id="1741d-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="1741d-147">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1741d-147">Azure portal</span></span>
<span data-ttu-id="1741d-148">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1741d-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="1741d-149">También podría interesarle hello toouse [portal de Azure](../azure-portal-overview.md) toohelp aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1741d-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="1741d-150">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1741d-150">Azure storage issues</span></span>
<span data-ttu-id="1741d-151">[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com) es una aplicación independiente de Microsoft que puede usar toowork con [el almacenamiento de Azure](https://azure.microsoft.com/en-us/services/storage/) datos en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="1741d-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="1741d-152">Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="1741d-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="1741d-153">Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1741d-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1741d-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1741d-154">Next steps</span></span>
<span data-ttu-id="1741d-155">Esta página solo incluye los problemas más comunes de hello del kit de Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="1741d-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="1741d-156">También puede dejar comentarios inferior tooreport problemas para solucionar problemas adicionales.</span><span class="sxs-lookup"><span data-stu-id="1741d-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="1741d-157">Vuelva demasiado[empezar a trabajar con Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1741d-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started