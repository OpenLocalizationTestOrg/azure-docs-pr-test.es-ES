---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (Windows) | Microsoft Docs"
description: Instalar software de Hola y herramientas de hello en el equipo host que ejecuta Windows, crear un centro de IoT y registrar el dispositivo en el centro de IoT Hola.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar git en windows, ejecución de gulp, instalar node js windows, instalar npm en windows, instalar python en windows"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 18ae6ee4-574a-4d5f-9838-ca2a78165628
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3b30b60a0115413394992061a88dde4cd442ac19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-windows-7-and-later"></a><span data-ttu-id="5466a-104">Obtener herramientas de hello (Windows 7 y versiones posteriores)</span><span class="sxs-lookup"><span data-stu-id="5466a-104">Get hello tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5466a-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="5466a-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="5466a-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="5466a-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="5466a-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="5466a-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="5466a-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="5466a-108">What you will do</span></span>

- <span data-ttu-id="5466a-109">Instale Git, Node.js, Gulp y Python.</span><span class="sxs-lookup"><span data-stu-id="5466a-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="5466a-110">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="5466a-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="5466a-111">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5466a-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5466a-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="5466a-112">What you will learn</span></span>

<span data-ttu-id="5466a-113">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5466a-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="5466a-114">Cómo tooinstall [Git](https://git-scm.com/) y [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="5466a-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="5466a-115">Git es un sistema de control de versiones distribuido de código abierto.</span><span class="sxs-lookup"><span data-stu-id="5466a-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="5466a-116">aplicación de ejemplo de Hola en esta lección se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="5466a-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="5466a-117">Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="5466a-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="5466a-118">Cómo toouse [NPM](https://www.npmjs.com/) tooinstall Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="5466a-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="5466a-119">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="5466a-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="5466a-120">NPM es uno de los administradores de paquetes de saludo para Node.js.</span><span class="sxs-lookup"><span data-stu-id="5466a-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="5466a-121">Cómo tooinstall código Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5466a-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="5466a-122">Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="5466a-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="5466a-123">Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.</span><span class="sxs-lookup"><span data-stu-id="5466a-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="5466a-124">¿Cómo tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="5466a-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="5466a-125">Python es un lenguaje de programación general, muy usado, destinado a fines genéricos, interpretado y dinámico.</span><span class="sxs-lookup"><span data-stu-id="5466a-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="5466a-126">¿Cómo tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="5466a-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="5466a-127">Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="5466a-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="5466a-128">Puede trabaja directamente desde una línea de comandos tooprovision y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="5466a-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="5466a-129">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="5466a-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5466a-130">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5466a-130">What you need</span></span>

- <span data-ttu-id="5466a-131">Un toodownload de conexión de Internet Hola herramientas y software.</span><span class="sxs-lookup"><span data-stu-id="5466a-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="5466a-132">Un equipo Windows.</span><span class="sxs-lookup"><span data-stu-id="5466a-132">A Windows computer.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="5466a-133">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="5466a-133">Install Git and Node.js</span></span>

<span data-ttu-id="5466a-134">Haga clic en hello después toodownload vínculos e instale Git y LTS de Node.js para Windows.</span><span class="sxs-lookup"><span data-stu-id="5466a-134">Click hello following links toodownload and install Git and Node.js LTS for Windows.</span></span>

- [<span data-ttu-id="5466a-135">Obtención de Git para Windows</span><span class="sxs-lookup"><span data-stu-id="5466a-135">Get Git for Windows</span></span>](https://git-scm.com/download/win/)
- [<span data-ttu-id="5466a-136">Obtención de Node.js LTS para Windows</span><span class="sxs-lookup"><span data-stu-id="5466a-136">Get Node.js LTS for Windows</span></span>](https://nodejs.org/en/)

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="5466a-137">Instalación de herramientas de desarrollo de Node.js</span><span class="sxs-lookup"><span data-stu-id="5466a-137">Install Node.js development tools</span></span>

<span data-ttu-id="5466a-138">Usa [gulp.js](http://gulpjs.com/) tooautomate implementación y ejecución de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="5466a-138">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="5466a-139">Presione `Windows + R`, tipo `cmd` y presione `Enter` tooopen una ventana del símbolo del sistema, y, a continuación, Hola ejecución siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5466a-139">Press `Windows + R`, type `cmd` and press `Enter` tooopen a Command Prompt window, and then run hello following command:</span></span>

```cmd
npm install -g gulp
```

<span data-ttu-id="5466a-140">Si experimenta problemas con la instalación de hello, vea Hola [Guía de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="5466a-140">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="5466a-141">Nodo, NPM y Gulp son scripts de automatización necesarios toorun desarrollados en Node.js.</span><span class="sxs-lookup"><span data-stu-id="5466a-141">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="5466a-142">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="5466a-142">Install Python</span></span>

<span data-ttu-id="5466a-143">Puede elegir entre Python 2.7, 3.4 o 3.5.</span><span class="sxs-lookup"><span data-stu-id="5466a-143">You can choose from Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="5466a-144">En este tutorial, se usa Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="5466a-144">In this tutorial, we use Python 2.7.</span></span> <span data-ttu-id="5466a-145">Si ya ha instalado python, vaya toohello próxima sección.</span><span class="sxs-lookup"><span data-stu-id="5466a-145">If you've already installed python, go toohello next section.</span></span>

[<span data-ttu-id="5466a-146">Obtención de Python para Windows</span><span class="sxs-lookup"><span data-stu-id="5466a-146">Get Python for Windows</span></span>](https://www.python.org/downloads/)

<span data-ttu-id="5466a-147">También necesita ruta de acceso de tooadd Hola de carpetas de Hola donde Python.exe y pip.exe son toohello instalado system `PATH` variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="5466a-147">You also need tooadd hello path of hello folders where Python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="5466a-148">De forma predeterminada, se instala python.exe en `C:\Python27` y pip.exe en `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="5466a-148">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="5466a-149">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5466a-149">Install hello Azure CLI</span></span>

<span data-ttu-id="5466a-150">Hola tooinstall CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5466a-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="5466a-151">Abra una ventana de símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="5466a-151">Open a Command Prompt window as an administrator.</span></span>

2. <span data-ttu-id="5466a-152">Instale Hola CLI de Azure con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="5466a-152">Install hello Azure CLI by running hello following commands:</span></span>

   ```cmd
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="5466a-153">instalación de Hello puede tardar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="5466a-153">hello installation might take 5 minutes.</span></span>

3. <span data-ttu-id="5466a-154">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5466a-154">Verify hello installation by running hello following command:</span></span>

   ```cmd
   az iot -h
   ```

   <span data-ttu-id="5466a-155">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="5466a-155">You should see hello following output if hello installation is successful.</span></span>

   ![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_win.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="5466a-157">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5466a-157">Install Visual Studio Code</span></span>

<span data-ttu-id="5466a-158">Usar código de Visual Studio posteriormente en archivos de configuración del tutorial tooedit Hola.</span><span class="sxs-lookup"><span data-stu-id="5466a-158">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="5466a-159">[Descargue](https://code.visualstudio.com/docs/setup/windows) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="5466a-159">[Download](https://code.visualstudio.com/docs/setup/windows) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="5466a-160">Resumen</span><span class="sxs-lookup"><span data-stu-id="5466a-160">Summary</span></span>

<span data-ttu-id="5466a-161">Ha instalado todas las herramientas de hello necesario y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="5466a-161">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="5466a-162">La siguiente tarea es toouse hello Azure CLI toocreate un centro de IoT y registrar el dispositivo en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="5466a-162">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5466a-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5466a-163">Next steps</span></span>
[<span data-ttu-id="5466a-164">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5466a-164">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)
