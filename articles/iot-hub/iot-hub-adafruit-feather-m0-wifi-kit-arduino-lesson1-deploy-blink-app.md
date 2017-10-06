---
title: "Conectar Arduino tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar Arduino aplicación de ejemplo de Hola desde GitHub y ejecutar gulp toodeploy esta tooyour aplicación Adafruit compacto M0 Wi-Fi. Esta aplicación de ejemplo parpadea Hola GPIO"
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
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="73199-105">Crear e implementar la aplicación de hello parpadeo</span><span class="sxs-lookup"><span data-stu-id="73199-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="73199-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="73199-106">What you will do</span></span>
<span data-ttu-id="73199-107">Clonar Arduino aplicación de ejemplo de Hola desde GitHub y usar hello gulp herramienta toodeploy Hola ejemplo aplicación tooyour Adafruit compacto M0 Wi-Fi Arduino panel.</span><span class="sxs-lookup"><span data-stu-id="73199-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="73199-108">aplicación de ejemplo Hola Hola parpadea GPIO número 13 en barod LED cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="73199-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="73199-109">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="73199-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="73199-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="73199-110">What you will learn</span></span>
* <span data-ttu-id="73199-111">La ejecución hello y toodeploy aplicación en el panel de Arduino de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="73199-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="73199-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="73199-112">What you need</span></span>
<span data-ttu-id="73199-113">Debe haber completado correctamente hello las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="73199-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="73199-114">[Configuración del dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="73199-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="73199-115">[Obtener herramientas de Hola][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="73199-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="73199-116">Aplicación de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="73199-116">Open hello sample application</span></span>
<span data-ttu-id="73199-117">Hola tooopen aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="73199-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="73199-118">Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="73199-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="73199-119">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="73199-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

<span data-ttu-id="73199-121">Hola `app.ino` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.</span><span class="sxs-lookup"><span data-stu-id="73199-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="73199-122">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="73199-122">Install application dependencies</span></span>
<span data-ttu-id="73199-123">Instalar bibliotecas de Hola y otros módulos que necesita para la aplicación de ejemplo de Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="73199-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="73199-124">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="73199-124">Configure hello device connection</span></span>
<span data-ttu-id="73199-125">tooconfigure Hola conexión del dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="73199-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="73199-126">Obtener el puerto serie de hello de dispositivo de hello con cli de detección de dispositivos de hello:</span><span class="sxs-lookup"><span data-stu-id="73199-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="73199-127">Debe ver un resultado que es similar siguiente toohello y encontrar Hola usb puerto COM de su placa de Arduino: ![detección de dispositivos][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="73199-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="73199-128">Archivo abierto hello `config.json` en Hola carpeta lección y agregar valor Hola de hello encuentra el número de puerto COM:</span><span class="sxs-lookup"><span data-stu-id="73199-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="73199-130">Para el puerto de hello COM, en la plataforma Windows, tiene un formato de hello `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="73199-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="73199-131">En macOS o Ubuntu, empieza por `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="73199-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="73199-132">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="73199-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="73199-133">Instalar las herramientas de hello necesario para el panel de Arduino</span><span class="sxs-lookup"><span data-stu-id="73199-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="73199-134">Instale hello centro de IoT de Azure SDK para el panel de Arduino con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="73199-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="73199-135">Esta tarea puede tardar un toocomplete mucho tiempo, dependiendo de la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="73199-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="73199-136">Salga de Hola que ejecuta la instancia de Arduino IDE cuando se ejecuta tareas gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="73199-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="73199-137">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="73199-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="73199-138">Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="73199-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="73199-139">Compruebe que funciona de la aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="73199-139">Verify hello app works</span></span>
<span data-ttu-id="73199-140">Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas] [ troubleshooting-page] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="73199-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![Intermitencia del LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="73199-142">Resumen</span><span class="sxs-lookup"><span data-stu-id="73199-142">Summary</span></span>
<span data-ttu-id="73199-143">Ha instalado Hola requerido herramientas toowork con el panel de Arduino e implementado un Hola ejemplo aplicación tooyour Arduino panel tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="73199-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="73199-144">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta su tooAzure de panel Arduino toosend centro de IoT y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="73199-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73199-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73199-145">Next steps</span></span>
<span data-ttu-id="73199-146">[Obtener hello Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="73199-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md