---
title: "Conexión de Arduino a Azure IoT: Lección 1: Implementación de la aplicación | Microsoft Docs"
description: "Clone la aplicación de Arduino de ejemplo de GitHub y ejecute gulp para implementar esta aplicación en Adafruit Feather M0 WiFi. Esta aplicación de ejemplo hace parpadear la GPIO."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "proyectos de LED de Arduino, intermitencia del LED de Arduino, código de intermitencia del LED de Arduino, programa de intermitencia del LED de Arduino, ejemplo de intermitencia en Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="88d69-105">Creación e implementación de la aplicación de intermitencia</span><span class="sxs-lookup"><span data-stu-id="88d69-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="88d69-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="88d69-106">What you will do</span></span>
<span data-ttu-id="88d69-107">Clone la aplicación de Arduino de ejemplo de GitHub y use la herramienta gulp para implementar la aplicación de ejemplo en la placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="88d69-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="88d69-108">La aplicación de ejemplo hace parpadear el LED 13 de la GPIO cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="88d69-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="88d69-109">Si tiene problemas, busque soluciones en [esta página][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="88d69-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="88d69-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="88d69-110">What you will learn</span></span>
* <span data-ttu-id="88d69-111">Cómo implementar y ejecutar la aplicación de ejemplo en la placa de Arduino</span><span class="sxs-lookup"><span data-stu-id="88d69-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="88d69-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="88d69-112">What you need</span></span>
<span data-ttu-id="88d69-113">Debe haber completado correctamente las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="88d69-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="88d69-114">[Configuración del dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="88d69-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="88d69-115">[Obtención de las herramientas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="88d69-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="88d69-116">Apertura de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="88d69-116">Open the sample application</span></span>
<span data-ttu-id="88d69-117">Para abrir la aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="88d69-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="88d69-118">Clone el repositorio de ejemplo de GitHub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="88d69-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="88d69-119">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="88d69-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

<span data-ttu-id="88d69-121">El archivo `app.ino` de la subcarpeta `app` es el archivo de origen de la clave que contiene el código para controlar el LED.</span><span class="sxs-lookup"><span data-stu-id="88d69-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="88d69-122">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="88d69-122">Install application dependencies</span></span>
<span data-ttu-id="88d69-123">Instale las bibliotecas y otros módulos que necesite para la aplicación de ejemplo ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="88d69-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="88d69-124">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="88d69-124">Configure the device connection</span></span>
<span data-ttu-id="88d69-125">Para configurar la conexión de dispositivos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="88d69-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="88d69-126">Obtenga el puerto serie del dispositivo con la CLI de detección de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="88d69-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="88d69-127">Debería ver un resultado similar al siguiente y localizar el puerto COM USB de la placa de Arduino: ![Detección de dispositivos][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="88d69-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="88d69-128">Abra el archivo `config.json` de la carpeta lesson y agregue el valor del número de puerto COM encontrado:</span><span class="sxs-lookup"><span data-stu-id="88d69-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="88d69-130">Para el puerto COM, en la plataforma Windows tiene el formato de `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="88d69-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="88d69-131">En macOS o Ubuntu, empieza por `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="88d69-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="88d69-132">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="88d69-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="88d69-133">Instalación de las herramientas necesarias para la placa de Arduino</span><span class="sxs-lookup"><span data-stu-id="88d69-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="88d69-134">Instale el SDK de IoT Hub de Azure de su placa de Arduino ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="88d69-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="88d69-135">Esta tarea podría tardar mucho tiempo en completarse; depende de la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="88d69-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="88d69-136">Salga de la instancia en ejecución del IDE de Arduino cuando se ejecuten las tareas de gulp: `install-tools` y `run`.</span><span class="sxs-lookup"><span data-stu-id="88d69-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="88d69-137">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="88d69-137">Deploy and run the sample app</span></span>
<span data-ttu-id="88d69-138">Implemente y ejecute la aplicación de ejemplo usando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="88d69-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="88d69-139">Comprobación del funcionamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="88d69-139">Verify the app works</span></span>
<span data-ttu-id="88d69-140">En caso contrario, consulte [esta guía][troubleshooting-page] para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="88d69-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![Intermitencia del LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="88d69-142">Resumen</span><span class="sxs-lookup"><span data-stu-id="88d69-142">Summary</span></span>
<span data-ttu-id="88d69-143">Ha instalado las herramientas necesarias para usar la placa de Arduino e implementado una aplicación de ejemplo para que dicha placa haga parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="88d69-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="88d69-144">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que conecte la placa de Arduino a IoT Hub de Azure para enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="88d69-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88d69-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88d69-145">Next steps</span></span>
<span data-ttu-id="88d69-146">[Obtención de las herramientas de Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="88d69-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md