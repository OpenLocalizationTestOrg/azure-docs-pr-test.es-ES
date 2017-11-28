---
title: Connect Raspberry PI (C) tooAzure IoT - solucionar | Documentos de Microsoft
description: "Página de solución de problemas de Node.js en Raspberry Pi"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: problemas con iot, problemas con internet de las cosas
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="79950-104">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="79950-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="79950-105">Problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="79950-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="79950-106">aplicación de Hello se ejecuta bien pero Hola LED parpadea no</span><span class="sxs-lookup"><span data-stu-id="79950-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="79950-107">Este problema es siempre toohello relacionados hardware circuito conectividad.</span><span class="sxs-lookup"><span data-stu-id="79950-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="79950-108">Utilice los siguientes pasos tooidentify problemas de Hola.</span><span class="sxs-lookup"><span data-stu-id="79950-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="79950-109">Compruebe que eligió Hola correcto **GPIO** en el panel.</span><span class="sxs-lookup"><span data-stu-id="79950-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="79950-110">Hola dos puertos deben ser **GPIO GND (Pin 6)** y **04 GPIO (Pin 7)**.</span><span class="sxs-lookup"><span data-stu-id="79950-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="79950-111">Compruebe que la polaridad Hola de los LED sea correcta.</span><span class="sxs-lookup"><span data-stu-id="79950-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="79950-112">autenticación mutua de más de Hello debe indicar hello **positivo**, pin ánodo.</span><span class="sxs-lookup"><span data-stu-id="79950-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="79950-113">Hola de uso **anclar 3,3 v** y **GND Pin** frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="79950-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="79950-114">Tratar Pi como Hola corriente continua.</span><span class="sxs-lookup"><span data-stu-id="79950-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="79950-115">Compruebe que Hola LED funciona bien.</span><span class="sxs-lookup"><span data-stu-id="79950-115">Check that hello LED works fine.</span></span>

![Especificación del LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="79950-117">Otros problemas de hardware</span><span class="sxs-lookup"><span data-stu-id="79950-117">Other hardware issues</span></span>
<span data-ttu-id="79950-118">Para obtener información acerca de cómo solucionar problemas comunes de frambuesa Pi 3, vea hello [página oficial de solución de problemas](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="79950-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="79950-119">Problemas de paquetes en Node.js</span><span class="sxs-lookup"><span data-stu-id="79950-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="79950-120">Sin respuesta durante las tareas de Gulp</span><span class="sxs-lookup"><span data-stu-id="79950-120">No response during gulp tasks</span></span>
<span data-ttu-id="79950-121">Si encuentra problemas al ejecutar gulp tareas, puede agregar hello `--verbose` opción para la depuración.</span><span class="sxs-lookup"><span data-stu-id="79950-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="79950-122">Intente tooterminate actual gulp tareas mediante el uso de `Ctrl + C`, y, a continuación, Hola ejecución siguiente comando en los mensajes de depuración de toosee de ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="79950-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="79950-123">En la salida de la consola, deberían aparecer mensajes de error detallados.</span><span class="sxs-lookup"><span data-stu-id="79950-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="79950-124">Problemas de detección de dispositivos</span><span class="sxs-lookup"><span data-stu-id="79950-124">Device discovery issues</span></span>
<span data-ttu-id="79950-125">Para obtener ayuda para solucionar problemas comunes con hello `devdisco` comando, compruebe hello [Léame](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="79950-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="79950-126">Problemas de NPM</span><span class="sxs-lookup"><span data-stu-id="79950-126">NPM issues</span></span>
<span data-ttu-id="79950-127">Intente tooupdate el paquete NPM con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="79950-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="79950-128">Si aún existe el problema de hello, deje sus comentarios al final de Hola de este artículo o crear un problema de GitHub en nuestra [repositorio de ejemplo](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="79950-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="79950-129">Depuración remota</span><span class="sxs-lookup"><span data-stu-id="79950-129">Remote debugging</span></span>

<span data-ttu-id="79950-130">La compatibilidad con la depuración remota estará disponible próximamente en la extensión de código C o C++ de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="79950-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="79950-131">Mientras tanto, puede utilizar GDB a través de su terminal SSH favorito:</span><span class="sxs-lookup"><span data-stu-id="79950-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="79950-132">Problemas de la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="79950-132">Azure-CLI issues</span></span>
<span data-ttu-id="79950-133">Hello Azure interfaz de línea de comandos (CLI de Azure) es una versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="79950-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="79950-134">Busque soluciones en hello [Guía de instalación de vista previa](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek soluciones.</span><span class="sxs-lookup"><span data-stu-id="79950-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="79950-135">Intente tooupgrade cli de Azure toolatest versión cuando comandos no funcionan según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="79950-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="79950-136">Si se producen los errores con la herramienta de hello, archivo un [problema](https://github.com/Azure/azure-cli/issues) en hello **problemas** sección del repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="79950-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="79950-137">Para obtener ayuda acerca de la solución de problemas comunes, consulte hello [Léame](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="79950-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="79950-138">Si se cumplen "No se pudo encontrar una versión que cumple el requisito de hello," por favor, siguiente ejecución Hola comando versión toolastest de tooupgrade pip.</span><span class="sxs-lookup"><span data-stu-id="79950-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="79950-139">Problemas de instalación de Python</span><span class="sxs-lookup"><span data-stu-id="79950-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="79950-140">Problemas de instalación de versiones antiguas (Mac OS)</span><span class="sxs-lookup"><span data-stu-id="79950-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="79950-141">Al instalar **pip**, se produce un error de permisos si hay paquetes antiguos instalados con permisos **su**.</span><span class="sxs-lookup"><span data-stu-id="79950-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="79950-142">Esto se debe a que hay una instalación anterior de Python con Brew (macOS) que no se ha desinstalado por completo.</span><span class="sxs-lookup"><span data-stu-id="79950-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="79950-143">Algunos **pip** raíz, lo que provoca el error de permiso de Hola que se crearon paquetes desde una instalación anterior.</span><span class="sxs-lookup"><span data-stu-id="79950-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="79950-144">Hola solución es tooremove esos paquetes instalados por la raíz.</span><span class="sxs-lookup"><span data-stu-id="79950-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="79950-145">Utilice Hola siguiendo los pasos toocomplete esta tarea:</span><span class="sxs-lookup"><span data-stu-id="79950-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="79950-146">Vaya a: /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="79950-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="79950-147">Muestre los paquetes creados de raíz: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="79950-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="79950-148">Desinstale los paquetes mostrados en el paso 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="79950-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="79950-149">Vuelva a instalar Python.</span><span class="sxs-lookup"><span data-stu-id="79950-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="79950-150">Problemas de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="79950-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="79950-151">Si ha aprovisionado correctamente el centro de IoT de Azure con `azure-cli`, y necesitan una herramienta toomanage Hola los dispositivos que se conectan tooyour centro de IoT, Hola try siguientes herramientas:</span><span class="sxs-lookup"><span data-stu-id="79950-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="79950-152">Explorador de dispositivos</span><span class="sxs-lookup"><span data-stu-id="79950-152">Device Explorer</span></span>
<span data-ttu-id="79950-153">[El Explorador de dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) se ejecuta en el equipo local de Windows y se conecta tooyour centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="79950-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="79950-154">Se comunica con los siguientes hello [los extremos del centro de IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="79950-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="79950-155">*Administración de identidad de dispositivo* tooprovision y administrar los dispositivos registrados con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="79950-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="79950-156">*Dispositivo para la nube de recepción* para que pueda supervisar mensajes enviados desde el centro de IoT tooyour de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79950-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="79950-157">*Enviar en la nube al dispositivo* para poder enviar mensajes tooyour dispositivos de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="79950-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="79950-158">Configurar la `IoT hub connection string` dentro de esta herramienta toouse todas sus capacidades.</span><span class="sxs-lookup"><span data-stu-id="79950-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="79950-159">Explorador de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="79950-159">IoT hub Explorer</span></span>
<span data-ttu-id="79950-160">[Centro de IoT explorador](https://github.com/Azure/iothub-explorer) es una herramienta CLI multiplataforma de ejemplo toomanage los clientes de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="79950-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="79950-161">Puede usar dispositivos de Hola de toomanage de herramienta de hello en el registro de la identidad de hello, supervisar los mensajes del dispositivo a la nube y enviar comandos de nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="79950-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="79950-162">tooinstall Hola última versión (versión preliminar) de herramienta de explorador el centro de IOT de hello, ejecute el siguiente comando en el entorno de línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="79950-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="79950-163">Puede usar Hola siguiente Hola a tooget ayuda adicional acerca de todos los comandos de explorador el centro de IOT y sus parámetros de comando:</span><span class="sxs-lookup"><span data-stu-id="79950-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="79950-164">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="79950-164">Azure portal</span></span>
<span data-ttu-id="79950-165">Puede aprovechar todas las capacidades que brinda CLI para crear y administrar todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="79950-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="79950-166">También podría interesarle hello toouse [portal de Azure](../azure-portal-overview.md) toohelp aprovisionar, administrar y depurar los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="79950-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="79950-167">Problemas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="79950-167">Azure storage issues</span></span>
<span data-ttu-id="79950-168">[Explorador de almacenamiento de Microsoft Azure (vista previa)](http://storageexplorer.com) es una aplicación independiente de Microsoft que puede usar toowork con datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="79950-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="79950-169">Mediante esta herramienta, puede conectarse tooyour tabla y ver datos de hello en ella.</span><span class="sxs-lookup"><span data-stu-id="79950-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="79950-170">Puede usar esta herramienta tootroubleshoot los problemas de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="79950-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
