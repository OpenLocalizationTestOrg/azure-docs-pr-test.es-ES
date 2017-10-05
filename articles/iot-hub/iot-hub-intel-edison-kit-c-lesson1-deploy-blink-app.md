---
title: "Conexión de Intel Edison (C) a Azure IoT: Lección 1: Implementación de la aplicación | Microsoft Docs"
description: "Clone la aplicación de C de ejemplo de GitHub y ejecute Gulp para implementar esta aplicación en la placa Intel Edison. Esta aplicación de ejemplo hace parpadear el LED conectado a la placa cada dos segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "proyectos de LED de Arduino, intermitencia del LED de Arduino, código de intermitencia del LED de Arduino, programa de intermitencia del LED de Arduino, ejemplo de intermitencia en Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: b02dfd3f-28fd-4b52-8775-eb0eaf74d707
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c45ff5f41bdbc78da8532ffdcaaeec15c695f531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="76f6f-105">Creación e implementación de la aplicación de intermitencia</span><span class="sxs-lookup"><span data-stu-id="76f6f-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="76f6f-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="76f6f-106">What you will do</span></span>
<span data-ttu-id="76f6f-107">Clone la aplicación de C de ejemplo de GitHub y use la herramienta Gulp para implementar la aplicación de ejemplo en Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="76f6f-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Intel Edison.</span></span> <span data-ttu-id="76f6f-108">La aplicación de ejemplo hace parpadear el LED conectado a la placa cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="76f6f-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="76f6f-109">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="76f6f-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="76f6f-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="76f6f-110">What you will learn</span></span>
* <span data-ttu-id="76f6f-111">Cómo implementar y ejecutar la aplicación de ejemplo en Edison</span><span class="sxs-lookup"><span data-stu-id="76f6f-111">How to deploy and run the sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="76f6f-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="76f6f-112">What you need</span></span>
<span data-ttu-id="76f6f-113">Debe haber completado correctamente las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="76f6f-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="76f6f-114">[Configuración del dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="76f6f-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="76f6f-115">[Obtención de las herramientas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="76f6f-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="76f6f-116">Apertura de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="76f6f-116">Open the sample application</span></span>
<span data-ttu-id="76f6f-117">Para abrir la aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="76f6f-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="76f6f-118">Clone el repositorio de ejemplo de GitHub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f6f-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="76f6f-119">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="76f6f-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

<span data-ttu-id="76f6f-121">El archivo de la subcarpeta `app` es el archivo de origen de la clave que contiene el código para controlar el LED.</span><span class="sxs-lookup"><span data-stu-id="76f6f-121">The file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="76f6f-122">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="76f6f-122">Install application dependencies</span></span>
<span data-ttu-id="76f6f-123">Instale las bibliotecas y otros módulos que necesite para la aplicación de ejemplo ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f6f-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="76f6f-124">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="76f6f-124">Configure the device connection</span></span>
<span data-ttu-id="76f6f-125">Para configurar la conexión de dispositivos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="76f6f-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="76f6f-126">Genere el archivo de configuración de dispositivos mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f6f-126">Generate the device configuration file by running the following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="76f6f-127">El archivo de configuración `config-edison.json` contiene las credenciales de usuario que use para iniciar sesión en Edison.</span><span class="sxs-lookup"><span data-stu-id="76f6f-127">The configuration file `config-edison.json` contains the user credentials you use to log in to Edison.</span></span> <span data-ttu-id="76f6f-128">Para evitar la pérdida de las credenciales de usuario, se genera el archivo de configuración en la subcarpeta `.iot-hub-getting-started` de la carpeta principal del equipo.</span><span class="sxs-lookup"><span data-stu-id="76f6f-128">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="76f6f-129">Abra el archivo de configuración de dispositivos en Visual Studio Code ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f6f-129">Open the device configuration file in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="76f6f-130">Reemplace el marcador de posición `[device hostname or IP address]` y `[device password]` por la dirección IP y contraseña que ha anotado en la lección anterior.</span><span class="sxs-lookup"><span data-stu-id="76f6f-130">Replace the placeholder `[device hostname or IP address]` and `[device password]` with the IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="76f6f-132">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="76f6f-132">Congratulations!</span></span> <span data-ttu-id="76f6f-133">Ha creado correctamente la primera aplicación de ejemplo para Edison.</span><span class="sxs-lookup"><span data-stu-id="76f6f-133">You've successfully created the first sample application for Edison.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="76f6f-134">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="76f6f-134">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="76f6f-135">Instalación del SDK de IoT de Azure en Edison</span><span class="sxs-lookup"><span data-stu-id="76f6f-135">Install the Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="76f6f-136">Instale el SDK de IoT de Azure en Edison ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76f6f-136">Install the Azure IoT Hub SDK on Edison by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="76f6f-137">Esta tarea podría tardar mucho tiempo en completarse; depende de la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="76f6f-137">This task might take a long time to complete, depending on your network connection.</span></span> <span data-ttu-id="76f6f-138">Debe ejecutarse una sola vez para una placa de Edison.</span><span class="sxs-lookup"><span data-stu-id="76f6f-138">It needs to be run only once for one Edison.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="76f6f-139">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="76f6f-139">Deploy and run the sample app</span></span>
<span data-ttu-id="76f6f-140">Implemente y ejecute la aplicación de ejemplo usando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="76f6f-140">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="76f6f-141">Comprobación del funcionamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="76f6f-141">Verify the app works</span></span>
<span data-ttu-id="76f6f-142">La aplicación de ejemplo se finaliza automáticamente después de que el LED parpadee 20 veces.</span><span class="sxs-lookup"><span data-stu-id="76f6f-142">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="76f6f-143">En caso contrario, consulte [esta guía][troubleshooting] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="76f6f-143">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting] for solutions to common problems.</span></span>

![Intermitencia del LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="76f6f-145">Resumen</span><span class="sxs-lookup"><span data-stu-id="76f6f-145">Summary</span></span>
<span data-ttu-id="76f6f-146">Ha instalado las herramientas necesarias para usar Edison e implementado una aplicación de ejemplo para que Edison haga parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="76f6f-146">You've installed the required tools to work with Edison and deployed a sample application to Edison to blink the LED.</span></span> <span data-ttu-id="76f6f-147">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que conecte Edison a IoT Hub de Azure para enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="76f6f-147">You can now create, deploy, and run another sample application that connects Edison to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76f6f-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76f6f-148">Next steps</span></span>
<span data-ttu-id="76f6f-149">[Obtención de las herramientas de Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="76f6f-149">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
