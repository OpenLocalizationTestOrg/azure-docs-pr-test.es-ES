---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 2: Obtención de las herramientas (Ubuntu) | Microsoft Docs"
description: Instalar software de Hola y herramientas de hello en el equipo host ejecuta Ubuntu, crear un centro de IoT y registrar el dispositivo en el centro de IoT Hola.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "desarrollo de iot, software de iot, servicio en la nube de iot, software de internet de las cosas, cli de azure, instalar git en ubuntu, ejecución de gulp, instalar node js ubuntu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cf673154-ce67-4ed7-a9f7-2440301c6270
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 38c4d5d9cceec47758f0641cc26b631a7b19d37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-tools-ubuntu-1604"></a><span data-ttu-id="59226-104">Obtener herramientas de hello (Ubuntu 16.04)</span><span class="sxs-lookup"><span data-stu-id="59226-104">Get hello tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59226-105">Windows 7 o posterior</span><span class="sxs-lookup"><span data-stu-id="59226-105">Windows 7 or later</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
> * [<span data-ttu-id="59226-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="59226-106">Ubuntu 16.04</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-ubuntu.md)
> * [<span data-ttu-id="59226-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="59226-107">macOS 10.10</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="59226-108">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="59226-108">What you will do</span></span>

- <span data-ttu-id="59226-109">Instale Git, Node.js, Gulp y Python.</span><span class="sxs-lookup"><span data-stu-id="59226-109">Install Git, Node.js, Gulp, Python.</span></span>
- <span data-ttu-id="59226-110">Instalar hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="59226-110">Install hello Azure command-line interface (Azure CLI).</span></span> 

<span data-ttu-id="59226-111">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="59226-111">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>
## <a name="what-you-will-learn"></a><span data-ttu-id="59226-112">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="59226-112">What you will learn</span></span>

<span data-ttu-id="59226-113">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="59226-113">In this lesson, you will learn:</span></span>

- <span data-ttu-id="59226-114">¿Cómo tooinstall Git y Node.js.</span><span class="sxs-lookup"><span data-stu-id="59226-114">How tooinstall Git and Node.js.</span></span>
  - <span data-ttu-id="59226-115">Git es un sistema de control de versiones distribuido de código abierto.</span><span class="sxs-lookup"><span data-stu-id="59226-115">Git is an open source distributed version control system.</span></span> <span data-ttu-id="59226-116">aplicación de ejemplo de Hola en esta lección se almacena en Git.</span><span class="sxs-lookup"><span data-stu-id="59226-116">hello sample application for this lesson is stored on Git.</span></span>
  - <span data-ttu-id="59226-117">Node.js es un entorno en tiempo de ejecución de JavaScript con un amplio ecosistema de paquetes.</span><span class="sxs-lookup"><span data-stu-id="59226-117">Node.js is a JavaScript runtime with a rich package ecosystem.</span></span>
- <span data-ttu-id="59226-118">Cómo las herramientas de desarrollo toouse NPM tooinstall Node.js.</span><span class="sxs-lookup"><span data-stu-id="59226-118">How toouse NPM tooinstall Node.js development tools.</span></span>
  - <span data-ttu-id="59226-119">Hola mínima versión requerida del Node.js es 4.5 LTS.</span><span class="sxs-lookup"><span data-stu-id="59226-119">hello minimum required version of Node.js is 4.5 LTS.</span></span>
  - <span data-ttu-id="59226-120">NPM es uno de los administradores de paquetes de saludo para Node.js.</span><span class="sxs-lookup"><span data-stu-id="59226-120">NPM is one of hello package managers for Node.js.</span></span>
- <span data-ttu-id="59226-121">Cómo tooinstall código Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59226-121">How tooinstall Visual Studio Code.</span></span>
  - <span data-ttu-id="59226-122">Visual Studio Code es un editor de código fuente multiplataforma ligero pero eficaz para Windows, Linux y macOS.</span><span class="sxs-lookup"><span data-stu-id="59226-122">Visual Studio Code is a cross platform, lightweight but powerful source code editor for Windows, Linux, and macOS.</span></span> <span data-ttu-id="59226-123">Ofrece un elevado nivel de compatibilidad para la depuración, control de Git insertado, resaltado de sintaxis, función inteligente de autocompletar código, fragmentos de código y refactorización de código.</span><span class="sxs-lookup"><span data-stu-id="59226-123">It has great support for debugging, embedded Git control, syntax highlighting, intelligent code completion, snippets, and code refactoring as well.</span></span>
- <span data-ttu-id="59226-124">¿Cómo tooinstall Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="59226-124">How tooinstall hello Azure CLI</span></span>
  - <span data-ttu-id="59226-125">Hola CLI de Azure proporciona una experiencia de línea de comandos multiplataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="59226-125">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="59226-126">Puede trabaja directamente desde una línea de comandos tooprovision y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="59226-126">You work directly from a command line tooprovision and manage resources.</span></span>
- <span data-ttu-id="59226-127">¿Cómo toouse Hola toocreate de CLI de Azure de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="59226-127">How toouse hello Azure CLI toocreate an IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="59226-128">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="59226-128">What you need</span></span>

- <span data-ttu-id="59226-129">Un toodownload de conexión de Internet Hola herramientas y software.</span><span class="sxs-lookup"><span data-stu-id="59226-129">An Internet connection toodownload hello tools and software.</span></span>
- <span data-ttu-id="59226-130">Un equipo que ejecute Ubuntu 16.04 o posterior</span><span class="sxs-lookup"><span data-stu-id="59226-130">A computer that is running Ubuntu 16.04 or later.</span></span>

## <a name="install-git-and-nodejs"></a><span data-ttu-id="59226-131">Instalación de Git y Node.js</span><span class="sxs-lookup"><span data-stu-id="59226-131">Install Git and Node.js</span></span>

<span data-ttu-id="59226-132">tooinstall Git y Node.js, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="59226-132">tooinstall Git and Node.js, follow these steps:</span></span>

1. <span data-ttu-id="59226-133">Presione `Ctrl + Alt + T` tooopen un terminal.</span><span class="sxs-lookup"><span data-stu-id="59226-133">Press `Ctrl + Alt + T` tooopen a terminal.</span></span>
2. <span data-ttu-id="59226-134">Ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="59226-134">Run hello following commands:</span></span>

   ```bash
   sudo apt-get update
   curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
   sudo apt-get install -y nodejs
   sudo apt-get install git
   ```

## <a name="install-nodejs-development-tools"></a><span data-ttu-id="59226-135">Instalación de herramientas de desarrollo de Node.js</span><span class="sxs-lookup"><span data-stu-id="59226-135">Install Node.js development tools</span></span>

<span data-ttu-id="59226-136">Usa [gulp.js](http://gulpjs.com/) tooautomate implementación y ejecución de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="59226-136">You use [gulp.js](http://gulpjs.com/) tooautomate deployment and execution of scripts.</span></span>

<span data-ttu-id="59226-137">gulp tooinstall, ejecute hello siguiente comando en terminal hello:</span><span class="sxs-lookup"><span data-stu-id="59226-137">tooinstall gulp, run hello following command in hello terminal:</span></span>

```bash
sudo npm install -g gulp
```

<span data-ttu-id="59226-138">Si experimenta problemas con la instalación de hello, vea Hola [Guía de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="59226-138">If you experience issues with hello installation, see hello [troubleshooting guide](iot-hub-gateway-kit-c-sim-troubleshooting.md) for solutions toocommon problems.</span></span>

> [!Note]
> <span data-ttu-id="59226-139">Nodo, NPM y Gulp son scripts de automatización necesarios toorun desarrollados en Node.js.</span><span class="sxs-lookup"><span data-stu-id="59226-139">Node, NPM and Gulp are required toorun automation scripts developed in Node.js.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="59226-140">Instalar Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="59226-140">Install hello Azure CLI</span></span>

<span data-ttu-id="59226-141">Hola tooinstall CLI de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="59226-141">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="59226-142">Ejecute hello siga los comandos de terminal de hello:</span><span class="sxs-lookup"><span data-stu-id="59226-142">Run hello following commands in hello terminal:</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```

   <span data-ttu-id="59226-143">instalación de Hello puede tardar 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="59226-143">hello installation might take 5 minutes.</span></span>

2. <span data-ttu-id="59226-144">Comprobar la instalación de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="59226-144">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```
<span data-ttu-id="59226-145">Debería ver la siguiente Hola de salida si la instalación de hello es correcta.</span><span class="sxs-lookup"><span data-stu-id="59226-145">You should see hello following output if hello installation is successful.</span></span>
<span data-ttu-id="59226-146">![Verificación de la instalación de la CLI de Azure](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="59226-146">![Verify Azure CLI installation](media/iot-hub-gateway-kit-lessons/lesson2/az_iot_help_ubuntu.png)</span></span>

### <a name="install-visual-studio-code"></a><span data-ttu-id="59226-147">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="59226-147">Install Visual Studio Code</span></span>

<span data-ttu-id="59226-148">Usar código de Visual Studio posteriormente en archivos de configuración del tutorial tooedit Hola.</span><span class="sxs-lookup"><span data-stu-id="59226-148">You use Visual Studio Code later in hello tutorial tooedit configuration files.</span></span>

<span data-ttu-id="59226-149">[Descargue](https://code.visualstudio.com/docs/setup/linux) e instale Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="59226-149">[Download](https://code.visualstudio.com/docs/setup/linux) and install Visual Studio Code.</span></span>

## <a name="summary"></a><span data-ttu-id="59226-150">Resumen</span><span class="sxs-lookup"><span data-stu-id="59226-150">Summary</span></span>

<span data-ttu-id="59226-151">Ha instalado todas las herramientas de hello necesario y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="59226-151">You've installed all hello required tools and software on your host computer.</span></span> <span data-ttu-id="59226-152">La siguiente tarea es toouse hello Azure CLI toocreate un centro de IoT y registrar el dispositivo en el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="59226-152">Your next task is toouse hello Azure CLI toocreate an IoT hub and register your device in your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59226-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59226-153">Next steps</span></span>
[<span data-ttu-id="59226-154">Creación de una instancia de IoT Hub y registro del dispositivo</span><span class="sxs-lookup"><span data-stu-id="59226-154">Create an IoT hub and register your device</span></span>](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)
