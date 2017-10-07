---
title: "Connect Intel Edison (C) tooAzure IoT - lección 4: recibir mensajes | Documentos de Microsoft"
description: "Una aplicación de ejemplo se ejecuta en Edison y supervisa los mensajes entrantes provenientes desde su instancia de IoT Hub. Una nueva tarea de gulp envía mensajes tooEdison desde su hello tooblink de centro de IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "control de led de arduino desde web, control de led de arduino a través de web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="aef55-105">Ejecutar un tooreceive de la aplicación de ejemplo en la nube al dispositivo mensajes</span><span class="sxs-lookup"><span data-stu-id="aef55-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="aef55-106">En este artículo se implementará una aplicación de ejemplo en Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="aef55-106">In this article, you deploy a sample application on Intel Edison.</span></span> <span data-ttu-id="aef55-107">aplicación de ejemplo de Hola supervisa los mensajes entrantes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="aef55-108">También permite ejecutar una tarea de gulp en su tooEdison de mensajes de toosend de equipo, el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-108">You also run a gulp task on your computer toosend messages tooEdison from your IoT hub.</span></span> <span data-ttu-id="aef55-109">Cuando la aplicación de ejemplo de Hola recibe mensajes de Hola, parpadea Hola LED.</span><span class="sxs-lookup"><span data-stu-id="aef55-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="aef55-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="aef55-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="aef55-111">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="aef55-111">What you will do</span></span>
* <span data-ttu-id="aef55-112">Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef55-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="aef55-113">Implemente y ejecute la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef55-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="aef55-114">Enviar mensajes desde su Hola de IoT hub tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="aef55-114">Send messages from your IoT hub tooEdison tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="aef55-115">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="aef55-115">What you will learn</span></span>
<span data-ttu-id="aef55-116">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="aef55-116">In this article, you will learn:</span></span>
* <span data-ttu-id="aef55-117">Cómo los mensajes entrantes de toomonitor desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="aef55-118">¿Cómo toosend en la nube al dispositivo mensajes desde su tooEdison de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-118">How toosend cloud-to-device messages from your IoT hub tooEdison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aef55-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="aef55-119">What you need</span></span>
* <span data-ttu-id="aef55-120">Intel Edison, configurado para su uso.</span><span class="sxs-lookup"><span data-stu-id="aef55-120">Intel Edison, set up for use.</span></span> <span data-ttu-id="aef55-121">toolearn tooset seguridad Edison, vea [configurar su dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="aef55-121">toolearn how tooset up Edison, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="aef55-122">Una instancia de IoT Hub creada en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="aef55-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="aef55-123">toolearn cómo toocreate su centro de IoT, consulte [crea el centro de IoT de Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="aef55-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="aef55-124">Conectar el centro de IoT de tooyour de aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="aef55-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="aef55-125">Asegúrese de que se encuentra en la carpeta de repositorio de hello `iot-hub-c-edison-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="aef55-125">Make sure that you're in hello repo folder `iot-hub-c-edison-getting-started`.</span></span> <span data-ttu-id="aef55-126">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="aef55-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="aef55-127">archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola que contiene código de hello toomonitor mensajes entrantes Hola centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-127">hello file in hello `app` subfolder is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="aef55-128">Hola `blinkLED` función parpadea Hola LED.</span><span class="sxs-lookup"><span data-stu-id="aef55-128">hello `blinkLED` function blinks hello LED.</span></span>

   ![Estructura de repositorio en la aplicación de ejemplo de Hola][repo-structure]
2. <span data-ttu-id="aef55-130">Inicializar el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="aef55-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="aef55-131">Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en este equipo, se heredan todas las configuraciones de hello, por lo que puede omitir la tarea de toohello hello paso de la implementación de y ejecutar la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef55-131">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="aef55-132">Si completó los pasos de hello en [crear una cuenta de aplicación y el almacenamiento de Azure función] [ create-an-azure-function-app-and-storage-account] en un equipo diferente, deberá marcadores de posición de tooreplace Hola Hola `config-edison.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="aef55-132">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-edison.json` file.</span></span> <span data-ttu-id="aef55-133">Hola `config-edison.json` archivo se encuentra en la subcarpeta de Hola de su carpeta principal.</span><span class="sxs-lookup"><span data-stu-id="aef55-133">hello `config-edison.json` file is in hello subfolder of your home folder.</span></span>

   ![Contenido del archivo de configuración edison.json Hola](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * <span data-ttu-id="aef55-135">Reemplace **[nombre de host de dispositivo o dirección IP]** con la dirección IP del dispositivo Hola marcados como inactivos cuando se configura el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aef55-135">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="aef55-136">Reemplace **[cadena de conexión de dispositivos de IoT]** con cadena de conexión de dispositivo de Hola que obtiene mediante la ejecución de hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="aef55-136">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="aef55-137">Reemplace **[cadena de conexión de base de datos central de IoT]** con la cadena de conexión de base de datos central de IoT que obtiene mediante la ejecución de Hola Hola `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="aef55-137">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aef55-138">Ejecute también **gulp install-tools** si no lo hizo en la lección 1.</span><span class="sxs-lookup"><span data-stu-id="aef55-138">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="aef55-139">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="aef55-139">Deploy and run hello sample application</span></span>
<span data-ttu-id="aef55-140">Implementar y ejecutar la aplicación de ejemplo de Hola en Edison ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="aef55-140">Deploy and run hello sample application on Edison by running hello following commands:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="aef55-141">comando de Hello gulp implementa tooEdison de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aef55-141">hello gulp command deploys hello sample application tooEdison.</span></span> <span data-ttu-id="aef55-142">A continuación, se ejecuta aplicación hello en Edison y una tarea independiente en su host de equipo toosend 20 parpadeo mensajes tooEdison desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-142">Then, it runs hello application on Edison and a separate task on your host computer toosend 20 blink messages tooEdison from your IoT hub.</span></span>

<span data-ttu-id="aef55-143">Después de ejecuta la aplicación de ejemplo de Hola, empieza a escuchar toomessages desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-143">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="aef55-144">Mientras tanto, hello gulp tarea puede enviar varios mensajes "blink" de su tooEdison de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-144">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="aef55-145">Para cada mensaje de intermitencia Edison recibe, aplicación de ejemplo de Hola llama hello `blinkLED` hello de la función tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="aef55-145">For each blink message that Edison receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="aef55-146">Verá parpadear LED de hello cada dos segundos como hello gulp tarea envía 20 mensajes desde su tooEdison de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="aef55-146">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooEdison.</span></span> <span data-ttu-id="aef55-147">Hello en último lugar uno es un mensaje de "stop" que detiene la aplicación hello se ejecute.</span><span class="sxs-lookup"><span data-stu-id="aef55-147">hello last one is a "stop" message that stops hello application from running.</span></span>

![Aplicación de ejemplo con comandos de Gulp y mensajes de parpadeo][gulp-command-and-blink-messages]

## <a name="summary"></a><span data-ttu-id="aef55-149">Resumen</span><span class="sxs-lookup"><span data-stu-id="aef55-149">Summary</span></span>
<span data-ttu-id="aef55-150">Ha enviado correctamente los mensajes desde su Hola de IoT hub tooEdison tooblink LED.</span><span class="sxs-lookup"><span data-stu-id="aef55-150">You’ve successfully sent messages from your IoT hub tooEdison tooblink hello LED.</span></span> <span data-ttu-id="aef55-151">Hola siguiente tarea es opcional: cambie Hola activar y desactivar el comportamiento de hello LED.</span><span class="sxs-lookup"><span data-stu-id="aef55-151">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aef55-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aef55-152">Next steps</span></span>
<span data-ttu-id="aef55-153">[Cambiar Hola activar y desactivar el comportamiento de hello LED][change-the-on-and-off-behavior-of-the-led]</span><span class="sxs-lookup"><span data-stu-id="aef55-153">[Change hello on and off behavior of hello LED][change-the-on-and-off-behavior-of-the-led]</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md