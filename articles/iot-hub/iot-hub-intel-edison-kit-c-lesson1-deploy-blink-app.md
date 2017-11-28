---
title: "Connect Intel Edison (C) tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar aplicación de ejemplo C hello desde GitHub y ejecute gulp toodeploy este panel Intel Edison tooyour de aplicación. Esta aplicación de ejemplo parpadea Hola LED conectado toohello panel cada dos segundos."
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
ms.openlocfilehash: fa84fae812dd742a2ad4997a5e213c8e40e6fcf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="8bf47-105">Crear e implementar la aplicación de hello parpadeo</span><span class="sxs-lookup"><span data-stu-id="8bf47-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8bf47-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8bf47-106">What you will do</span></span>
<span data-ttu-id="8bf47-107">Clonar aplicación de ejemplo C hello desde GitHub y usar el ejemplo hello de aplicación para la herramienta de gulp hello toodeploy, tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="8bf47-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="8bf47-108">aplicación de ejemplo de Hola parpadea Hola LED conectado toohello panel cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="8bf47-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="8bf47-109">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8bf47-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8bf47-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8bf47-110">What you will learn</span></span>
* <span data-ttu-id="8bf47-111">La ejecución hello y toodeploy aplicación en Edison de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8bf47-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8bf47-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8bf47-112">What you need</span></span>
<span data-ttu-id="8bf47-113">Debe haber completado correctamente hello las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="8bf47-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="8bf47-114">[Configuración del dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="8bf47-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="8bf47-115">[Obtener herramientas de Hola][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="8bf47-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="8bf47-116">Aplicación de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="8bf47-116">Open hello sample application</span></span>
<span data-ttu-id="8bf47-117">Hola tooopen aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8bf47-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="8bf47-118">Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bf47-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-edison-getting-started.git
   ```
2. <span data-ttu-id="8bf47-119">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8bf47-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

<span data-ttu-id="8bf47-121">archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.</span><span class="sxs-lookup"><span data-stu-id="8bf47-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="8bf47-122">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8bf47-122">Install application dependencies</span></span>
<span data-ttu-id="8bf47-123">Instalar bibliotecas de Hola y otros módulos que necesita para la aplicación de ejemplo de Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="8bf47-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="8bf47-124">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="8bf47-124">Configure hello device connection</span></span>
<span data-ttu-id="8bf47-125">tooconfigure Hola conexión del dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="8bf47-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="8bf47-126">Generar archivo de configuración de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bf47-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="8bf47-127">archivo de configuración de Hello `config-edison.json` contiene las credenciales de usuario de hello usar toolog en tooEdison.</span><span class="sxs-lookup"><span data-stu-id="8bf47-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="8bf47-128">pérdida de hello tooavoid de credenciales de usuario, se genera el archivo de configuración de hello en subcarpeta hello `.iot-hub-getting-started` de la carpeta particular de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8bf47-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="8bf47-129">Abra el archivo de configuración de dispositivo de hello en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bf47-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="8bf47-130">Reemplace el marcador de posición de hello `[device hostname or IP address]` y `[device password]` con la dirección IP de Hola y la contraseña que ha marcado hacia abajo en la lección anterior.</span><span class="sxs-lookup"><span data-stu-id="8bf47-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="8bf47-132">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="8bf47-132">Congratulations!</span></span> <span data-ttu-id="8bf47-133">Primera aplicación de ejemplo Hola para Edison que ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="8bf47-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="8bf47-134">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8bf47-134">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-edison"></a><span data-ttu-id="8bf47-135">Instalar hello Azure IoT Hub SDK en Edison</span><span class="sxs-lookup"><span data-stu-id="8bf47-135">Install hello Azure IoT Hub SDK on Edison</span></span>
<span data-ttu-id="8bf47-136">Instalar hello Azure IoT Hub SDK en Edison ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bf47-136">Install hello Azure IoT Hub SDK on Edison by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="8bf47-137">Esta tarea puede tardar un toocomplete mucho tiempo, dependiendo de la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="8bf47-137">This task might take a long time toocomplete, depending on your network connection.</span></span> <span data-ttu-id="8bf47-138">Se necesita toobe ejecutar una sola vez para uno Edison.</span><span class="sxs-lookup"><span data-stu-id="8bf47-138">It needs toobe run only once for one Edison.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="8bf47-139">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="8bf47-139">Deploy and run hello sample app</span></span>
<span data-ttu-id="8bf47-140">Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8bf47-140">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="8bf47-141">Compruebe que funciona de la aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="8bf47-141">Verify hello app works</span></span>
<span data-ttu-id="8bf47-142">aplicación de ejemplo de Hola finaliza automáticamente después de hello LED parpadea para 20 veces.</span><span class="sxs-lookup"><span data-stu-id="8bf47-142">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="8bf47-143">Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="8bf47-143">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![Intermitencia del LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="8bf47-145">Resumen</span><span class="sxs-lookup"><span data-stu-id="8bf47-145">Summary</span></span>
<span data-ttu-id="8bf47-146">Ha instalado Hola requerido herramientas toowork con Edison e implementado un Hola de tooblink tooEdison de aplicación de ejemplo LED.</span><span class="sxs-lookup"><span data-stu-id="8bf47-146">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="8bf47-147">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta Edison tooAzure toosend centro de IoT y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="8bf47-147">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bf47-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bf47-148">Next steps</span></span>
<span data-ttu-id="8bf47-149">[Obtener hello Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="8bf47-149">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure_c.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking_c.jpg
[get-the-azure-tools]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
