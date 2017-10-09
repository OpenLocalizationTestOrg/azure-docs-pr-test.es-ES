---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (macOS) | Microsoft Docs"
description: Instalar las herramientas en el equipo Mac, crear un centro de IoT y registrar el dispositivo en el centro de IoT Hola.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar python mac, instalar git en mac, ejecutar gulp, instalar node js mac
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 42f9d186-e20c-4ef9-98cc-71d39e058b06
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 391d60f3cbb209698cae53098efed360ac0f5fad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-macos"></a><span data-ttu-id="10fc6-104">Obtener herramientas de hello (macOS)</span><span class="sxs-lookup"><span data-stu-id="10fc6-104">Get hello tools (macOS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10fc6-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="10fc6-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="10fc6-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="10fc6-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="10fc6-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="10fc6-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="10fc6-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="10fc6-108">What you will do</span></span>

- <span data-ttu-id="10fc6-109">Instale Git, Node.js, Gulp y Python.</span><span class="sxs-lookup"><span data-stu-id="10fc6-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="10fc6-110">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="10fc6-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="10fc6-111">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="10fc6-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="10fc6-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="10fc6-112">What you will learn</span></span>

<span data-ttu-id="10fc6-113">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="10fc6-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="10fc6-114">Cómo tooinstall [Git](https://git-scm.com/) y [Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="10fc6-114">How tooinstall [Git](https://git-scm.com/) and [Node.js](https://nodejs.org/en/).</span></span>
  - <span data-ttu-id="10fc6-115">Git es un sistema de control de versiones distribuido de código abierto.</span><span class="sxs-lookup"><span data-stu-id="10fc6-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="10fc6-116">aplicación de ejemplo de Hola en esta lección se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="10fc6-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="10fc6-117">Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="10fc6-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="10fc6-118">Cómo toouse [NPM](https://www.npmjs.com/) tooinstall Node.js las herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="10fc6-118">How toouse [NPM](https://www.npmjs.com/) tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="10fc6-119">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="10fc6-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="10fc6-120">NPM es uno de los administradores de paquetes de saludo para Node.js.</span><span class="sxs-lookup"><span data-stu-id="10fc6-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="10fc6-121">Cómo tooinstall código Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10fc6-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="10fc6-122">Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="10fc6-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="10fc6-123">Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.</span><span class="sxs-lookup"><span data-stu-id="10fc6-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="10fc6-124">¿Cómo tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="10fc6-124">How tooinstall Python.</span></span>
  - <span data-ttu-id="10fc6-125">Python es un lenguaje de programación general, muy usado, destinado a fines genéricos, interpretado y dinámico.</span><span class="sxs-lookup"><span data-stu-id="10fc6-125">Python is a widely used high-level, general-purpose, interpreted and dynamic programming language.</span></span>
- <span data-ttu-id="10fc6-126">¿Cómo tooinstall Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="10fc6-126">How tooinstall hello Azure CLI.</span></span>
  - <span data-ttu-id="10fc6-127">Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="10fc6-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="10fc6-128">Puede trabaja directamente desde una línea de comandos tooprovision y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="10fc6-128">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="10fc6-129">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="10fc6-129">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="10fc6-130">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="10fc6-130">What you need</span></span>

- <span data-ttu-id="10fc6-131">Un toodownload de conexión de Internet Hola herramientas y software.</span><span class="sxs-lookup"><span data-stu-id="10fc6-131">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="10fc6-132">Un equipo Mac con OS X Yosemite (10.10) o posterior.</span><span class="sxs-lookup"><span data-stu-id="10fc6-132">A Mac computer that’s running OS X Yosemite (10.10) or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="10fc6-133">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="10fc6-133">Install Git and Node.js</span></span>

<span data-ttu-id="10fc6-134">tooinstall Git y Node.js, use la utilidad de administración de paquetes de Homebrew Hola siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="10fc6-134">tooinstall Git and Node.js, use hello Homebrew package management utility by following these steps:</span></span>

1. <span data-ttu-id="10fc6-135">[Descargue](http://brew.sh/) e instale Homebrew.</span><span class="sxs-lookup"><span data-stu-id="10fc6-135">[Download](http://brew.sh/) and install Homebrew.</span></span> <span data-ttu-id="10fc6-136">Si ya ha instalado Homebrew, vaya toostep 2.</span><span class="sxs-lookup"><span data-stu-id="10fc6-136">If you’ve already installed Homebrew, go toostep 2.</span></span>
   1. <span data-ttu-id="10fc6-137">Presione `Cmd + Space` y escriba `Terminal` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="10fc6-137">Press `Cmd + Space` and enter `Terminal` tooopen a terminal.</span></span>
   2. <span data-ttu-id="10fc6-138">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="10fc6-138">Run hello following command:</span></span>

      ```bash
      /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
      ```

2. <span data-ttu-id="10fc6-139">Instale Git y Node.js con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="10fc6-139">Install Git and Node.js by running hello following command:</span></span>

    ```bash
    brew install node git
    ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="10fc6-140">Instalación de herramientas de desarrollo de Node.js</span><span class="sxs-lookup"><span data-stu-id="10fc6-140">Install Node.js development tools</span></span>

<span data-ttu-id="10fc6-141">Usa [gulp.js](http://gulpjs.com/) tooautomate implementación y ejecución de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="10fc6-141">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="10fc6-142">gulp tooinstall, ejecute hello siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="10fc6-142">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
npm install -g gulp
```

<span data-ttu-id="10fc6-143">Si experimenta problemas con la instalación de hello, vea Hola [Guía de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="10fc6-143">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="10fc6-144">Nodo, NPM y Gulp son scripts de automatización necesarios toorun desarrollados en Node.js.</span><span class="sxs-lookup"><span data-stu-id="10fc6-144">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-python"></a><span data-ttu-id="10fc6-145">Instalación de Python</span><span class="sxs-lookup"><span data-stu-id="10fc6-145">Install Python</span></span>

<span data-ttu-id="10fc6-146">Aunque Mac OS X incluye Python 2.7 de serie, se recomienda instalar Python mediante Homebrew.</span><span class="sxs-lookup"><span data-stu-id="10fc6-146">Although Mac OS X comes with Python 2.7, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="10fc6-147">Consulte [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/) (Instalación de Python en Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="10fc6-147">See [Installing Python on Mac OS X](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="10fc6-148">Instalar Python y pip ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="10fc6-148">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="10fc6-149">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="10fc6-149">Install hello Azure CLI</span></span>

<span data-ttu-id="10fc6-150">Hola tooinstall CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="10fc6-150">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="10fc6-151">Ejecute hello siga los comandos de terminal de hello:</span><span class="sxs-lookup"><span data-stu-id="10fc6-151">Run hello following commands in hello terminal:</span></span>
   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
   <span data-ttu-id="10fc6-152">instalación de Hello puede tardar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="10fc6-152">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="10fc6-153">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="10fc6-153">Verify hello installation by running hello following command:</span></span>
   ```bash
   az iot -h
   ```
   <span data-ttu-id="10fc6-154">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="10fc6-154">You should see hello following output if hello installation is successful.</span></span>

   ![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_osx.png)

## <a name="install-visual-studio-code"></a><span data-ttu-id="10fc6-156">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="10fc6-156">Install Visual Studio Code</span></span>

<span data-ttu-id="10fc6-157">Usar código de Visual Studio posteriormente en archivos de configuración del tutorial tooedit Hola.</span><span class="sxs-lookup"><span data-stu-id="10fc6-157">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="10fc6-158">[Descargue](https://code.visualstudio.com/docs/setup/osx) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="10fc6-158">[Download](https://code.visualstudio.com/docs/setup/osx) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="10fc6-159">Resumen</span><span class="sxs-lookup"><span data-stu-id="10fc6-159">Summary</span></span>

<span data-ttu-id="10fc6-160">Ha instalado todas las herramientas de hello necesario y el software en el equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="10fc6-160">You’ve installed all hello required tools and software on your Mac computer.</span></span> <span data-ttu-id="10fc6-161">La siguiente tarea es toouse hello Azure CLI toocreate un centro de IoT y registrar el dispositivo en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="10fc6-161">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10fc6-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10fc6-162">Next steps</span></span>
[<span data-ttu-id="10fc6-163">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="10fc6-163">Create an IoT hub and register Device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
