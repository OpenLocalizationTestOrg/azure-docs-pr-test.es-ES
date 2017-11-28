---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar aplicación de ejemplo C hello desde GitHub y ejecute gulp toodeploy este panel Intel Edison tooyour de aplicación. Esta aplicación de ejemplo parpadea Hola LED conectado toohello panel cada dos segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "proyectos de LED de Arduino, intermitencia del LED de Arduino, código de intermitencia del LED de Arduino, programa de intermitencia del LED de Arduino, ejemplo de intermitencia en Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: ed2c21d0-c72c-4ac2-9e70-347e9a0711c0
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc03c7e45bd1ba9e9b2c8f2fec70a1be647e96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="fe3ed-105">Crear e implementar la aplicación de hello parpadeo</span><span class="sxs-lookup"><span data-stu-id="fe3ed-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="fe3ed-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="fe3ed-106">What you will do</span></span>
<span data-ttu-id="fe3ed-107">Clonar aplicación de ejemplo C hello desde GitHub y usar el ejemplo hello de aplicación para la herramienta de gulp hello toodeploy, tooIntel Edison.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooIntel Edison.</span></span> <span data-ttu-id="fe3ed-108">aplicación de ejemplo de Hola parpadea Hola LED conectado toohello panel cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="fe3ed-109">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="fe3ed-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fe3ed-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="fe3ed-110">What you will learn</span></span>
* <span data-ttu-id="fe3ed-111">La ejecución hello y toodeploy aplicación en Edison de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-111">How toodeploy and run hello sample application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fe3ed-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="fe3ed-112">What you need</span></span>
<span data-ttu-id="fe3ed-113">Debe haber completado correctamente hello las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="fe3ed-114">[Configuración del dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="fe3ed-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="fe3ed-115">[Obtener herramientas de Hola][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="fe3ed-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="fe3ed-116">Aplicación de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="fe3ed-116">Open hello sample application</span></span>
<span data-ttu-id="fe3ed-117">Hola tooopen aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="fe3ed-118">Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-edison-getting-started.git
   ```
2. <span data-ttu-id="fe3ed-119">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-node-edison-getting-started
   cd Lesson1
   code .
   ```

   ![Estructura del repositorio][repo-structure]

<span data-ttu-id="fe3ed-121">archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-121">hello file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="fe3ed-122">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="fe3ed-122">Install application dependencies</span></span>
<span data-ttu-id="fe3ed-123">Instalar bibliotecas de Hola y otros módulos que necesita para la aplicación de ejemplo de Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="fe3ed-124">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="fe3ed-124">Configure hello device connection</span></span>
<span data-ttu-id="fe3ed-125">tooconfigure Hola conexión del dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="fe3ed-126">Generar archivo de configuración de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-126">Generate hello device configuration file by running hello following command:</span></span>

   ```bash
   gulp init
   ```

   <span data-ttu-id="fe3ed-127">archivo de configuración de Hello `config-edison.json` contiene las credenciales de usuario de hello usar toolog en tooEdison.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-127">hello configuration file `config-edison.json` contains hello user credentials you use toolog in tooEdison.</span></span> <span data-ttu-id="fe3ed-128">pérdida de hello tooavoid de credenciales de usuario, se genera el archivo de configuración de hello en subcarpeta hello `.iot-hub-getting-started` de la carpeta particular de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-128">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="fe3ed-129">Abra el archivo de configuración de dispositivo de hello en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-129">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

3. <span data-ttu-id="fe3ed-130">Reemplace el marcador de posición de hello `[device hostname or IP address]` y `[device password]` con la dirección IP de Hola y la contraseña que ha marcado hacia abajo en la lección anterior.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-130">Replace hello placeholder `[device hostname or IP address]` and `[device password]` with hello IP address and password that you marked down in previous lesson.</span></span>

   ![Config.json](media/iot-hub-intel-edison-lessons/lesson1/vscode-config-mac.png)

<span data-ttu-id="fe3ed-132">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="fe3ed-132">Congratulations!</span></span> <span data-ttu-id="fe3ed-133">Primera aplicación de ejemplo Hola para Edison que ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-133">You've successfully created hello first sample application for Edison.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="fe3ed-134">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="fe3ed-134">Deploy and run hello sample application</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="fe3ed-135">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="fe3ed-135">Deploy and run hello sample app</span></span>
<span data-ttu-id="fe3ed-136">Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fe3ed-136">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="fe3ed-137">Compruebe que funciona de la aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="fe3ed-137">Verify hello app works</span></span>
<span data-ttu-id="fe3ed-138">aplicación de ejemplo de Hola finaliza automáticamente después de hello LED parpadea para 20 veces.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-138">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="fe3ed-139">Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas] [ troubleshooting] para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-139">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting] for solutions toocommon problems.</span></span>

![Intermitencia del LED][led-blinking]

## <a name="summary"></a><span data-ttu-id="fe3ed-141">Resumen</span><span class="sxs-lookup"><span data-stu-id="fe3ed-141">Summary</span></span>
<span data-ttu-id="fe3ed-142">Ha instalado Hola requerido herramientas toowork con Edison e implementado un Hola de tooblink tooEdison de aplicación de ejemplo LED.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-142">You've installed hello required tools toowork with Edison and deployed a sample application tooEdison tooblink hello LED.</span></span> <span data-ttu-id="fe3ed-143">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta Edison tooAzure toosend centro de IoT y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="fe3ed-143">You can now create, deploy, and run another sample application that connects Edison tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe3ed-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe3ed-144">Next steps</span></span>
<span data-ttu-id="fe3ed-145">[Obtener hello Azure tools][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="fe3ed-145">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[Configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson1/repo_structure.png
[led-blinking]: media/iot-hub-intel-edison-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
