---
title: aaaSimulated frambuesa Pi toocloud (Node.js) - conectar frambuesa Pi web simulador tooAzure centro de IoT | Documentos de Microsoft
description: Conectar frambuesa Pi web simulador tooAzure centro de IoT de frambuesa Pi toosend datos toohello nube de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Centro de iot pi, de pi frambuesas simulador, azure iot frambuesas pi, frambuesas pi frambuesas enviar datos toocloud, frambuesas pi toocloud
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/28/2017
ms.author: xshi
ms.openlocfilehash: 83736caf6ce723a49001058495a780f7f51946a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-online-simulator-tooazure-iot-hub-nodejs"></a><span data-ttu-id="dfebc-104">Conectar frambuesa Pi simulador online tooAzure centro de IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="dfebc-104">Connect Raspberry Pi online simulator tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="dfebc-105">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con el simulador de frambuesa Pi en línea.</span><span class="sxs-lookup"><span data-stu-id="dfebc-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi online simulator.</span></span> <span data-ttu-id="dfebc-106">A continuación, aprenderá cómo tooseamlessly conectarse en la nube Hola Pi simulador toohello mediante [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="dfebc-106">You then learn how tooseamlessly connect hello Pi simulator toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> 

<span data-ttu-id="dfebc-107">Si tiene dispositivos físicos, visite [conectar frambuesa Pi tooAzure centro de IoT](iot-hub-raspberry-pi-kit-node-get-started.md) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="dfebc-107">If you have physical devices, visit [Connect Raspberry Pi tooAzure IoT Hub](iot-hub-raspberry-pi-kit-node-get-started.md) tooget started.</span></span> 

<p>
<div id="diag" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/3_banner.png" alt="Connect Raspberry Pi web simulator tooAzure IoT Hub" width="400">
</div>
<p>
<div id="button" style="width:100%; text-align:center">
<a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#Getstarted" target="_blank">
<img src="media/iot-hub-raspberry-pi-web-simulator/6_button_default.png" alt="Start Raspberry Pi simulator" width="400" onmouseover="this.src='media/iot-hub-raspberry-pi-web-simulator/5_button_click.png';" onmouseout="this.src='media/iot-hub-raspberry-pi-web-simulator/6_button_default.png';">
</div>

## <a name="what-you-do"></a><span data-ttu-id="dfebc-108">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="dfebc-108">What you do</span></span>

* <span data-ttu-id="dfebc-109">Obtenga información acerca de conceptos básicos de Hola de simulador de frambuesa Pi en línea.</span><span class="sxs-lookup"><span data-stu-id="dfebc-109">Learn hello basics of Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="dfebc-110">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="dfebc-110">Create an IoT hub.</span></span>
* <span data-ttu-id="dfebc-111">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dfebc-111">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="dfebc-112">Ejecutar una aplicación de ejemplo en el centro de IoT de Pi toosend simulado sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="dfebc-112">Run a sample application on Pi toosend simulated sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="dfebc-113">Conectar simulada centro de IoT de frambuesa Pi tooan creados por usted.</span><span class="sxs-lookup"><span data-stu-id="dfebc-113">Connect simulated Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="dfebc-114">A continuación, ejecutar una aplicación de ejemplo con datos del sensor de hello simulador toogenerate.</span><span class="sxs-lookup"><span data-stu-id="dfebc-114">Then you run a sample application with hello simulator toogenerate sensor data.</span></span> <span data-ttu-id="dfebc-115">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="dfebc-115">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="dfebc-116">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="dfebc-116">What you learn</span></span>

* <span data-ttu-id="dfebc-117">¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="dfebc-117">How toocreate an Azure IoT hub and get your new device connection string.</span></span> <span data-ttu-id="dfebc-118">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="dfebc-118">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="dfebc-119">¿Cómo toowork con el simulador de frambuesa Pi en línea.</span><span class="sxs-lookup"><span data-stu-id="dfebc-119">How toowork with Raspberry Pi online simulator.</span></span>
* <span data-ttu-id="dfebc-120">Cómo centro de IoT de toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="dfebc-120">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="overview-of-raspberry-pi-web-simulator"></a><span data-ttu-id="dfebc-121">Introducción al simulador web de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="dfebc-121">Overview of Raspberry Pi web simulator</span></span>

<span data-ttu-id="dfebc-122">Haga clic en el simulador en línea de hello botón toolaunch frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="dfebc-122">Click hello button toolaunch Raspberry Pi online simulator.</span></span>

> [!div class="button"]
<span data-ttu-id="dfebc-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Iniciar simulador de Raspberry Pi</a></span><span class="sxs-lookup"><span data-stu-id="dfebc-123"><a href="https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted" target="_blank">Start Raspberry Pi Simulator</a></span></span>

<span data-ttu-id="dfebc-124">Hay tres áreas en el simulador de hello web.</span><span class="sxs-lookup"><span data-stu-id="dfebc-124">There are three areas in hello web simulator.</span></span>
1. <span data-ttu-id="dfebc-125">Área de ensamblado - circuito de hello predeterminada es que una instrucción de procesamiento se conecta con un sensor BME280 y un LED.</span><span class="sxs-lookup"><span data-stu-id="dfebc-125">Assembly area - hello default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="dfebc-126">área de Hello está bloqueada en la versión de vista previa actualmente por lo que no puede realizar la personalización.</span><span class="sxs-lookup"><span data-stu-id="dfebc-126">hello area is locked in preview version so currently you cannot do customization.</span></span>
2. <span data-ttu-id="dfebc-127">Codificación de área, un editor de código en línea para toocode con frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="dfebc-127">Coding area - An online code editor for you toocode with Raspberry Pi.</span></span> <span data-ttu-id="dfebc-128">aplicación de ejemplo de Hola predeterminado ayuda a los datos del sensor toocollect desde BME280 sensor y envía tooyour centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="dfebc-128">hello default sample application helps toocollect sensor data from BME280 sensor and sends tooyour Azure IoT Hub.</span></span> <span data-ttu-id="dfebc-129">aplicación Hello es totalmente compatible con dispositivos reales de Pi.</span><span class="sxs-lookup"><span data-stu-id="dfebc-129">hello application is fully compatible with real Pi devices.</span></span> 
3. <span data-ttu-id="dfebc-130">Ventana de consola integrada - muestra la salida de hello del código.</span><span class="sxs-lookup"><span data-stu-id="dfebc-130">Integrated console window - It shows hello output of your code.</span></span> <span data-ttu-id="dfebc-131">Hola parte superior de esta ventana, hay tres botones.</span><span class="sxs-lookup"><span data-stu-id="dfebc-131">At hello top of this window, there are three buttons.</span></span>
   * <span data-ttu-id="dfebc-132">**Ejecute** -ejecutar aplicación hello en el área de código de hello.</span><span class="sxs-lookup"><span data-stu-id="dfebc-132">**Run** - Run hello application in hello coding area.</span></span>
   * <span data-ttu-id="dfebc-133">**Restablecer** -Hola de restablecimiento de codificación de la aplicación de ejemplo de área toohello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="dfebc-133">**Reset** - Reset hello coding area toohello default sample application.</span></span>
   * <span data-ttu-id="dfebc-134">**Doblar/expandir** - en hello derecho lado existe es un botón para que toofold/expandir Hola ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="dfebc-134">**Fold/Expand** - On hello right side there is a button for you toofold/expand hello console window.</span></span>

> [!NOTE] 
<span data-ttu-id="dfebc-135">simulador de web Pi frambuesa Hola ahora está disponible en versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="dfebc-135">hello Raspberry Pi web simulator is now available in preview version.</span></span> <span data-ttu-id="dfebc-136">Nos gustaría toohear su propia voz hello [salón de chat de Gitter](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="dfebc-136">We'd like toohear your voice in hello [Gitter Chatroom](https://gitter.im/Microsoft/raspberry-pi-web-simulator).</span></span> <span data-ttu-id="dfebc-137">código fuente de Hello es público en [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span><span class="sxs-lookup"><span data-stu-id="dfebc-137">hello source code is public on [Github](https://github.com/Azure-Samples/raspberry-pi-web-simulator).</span></span>

![Introducción al simulador en línea de Pi](media/iot-hub-raspberry-pi-web-simulator/0_overview.png)

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]


## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="dfebc-139">Ejecución de una aplicación de ejemplo en el simulador web de Pi</span><span class="sxs-lookup"><span data-stu-id="dfebc-139">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="dfebc-140">En el área de código, asegúrese de que está trabajando en la aplicación de ejemplo de Hola predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dfebc-140">In coding area, make sure you are working on hello default sample application.</span></span> <span data-ttu-id="dfebc-141">Reemplace el marcador de posición de hello en línea 15 con hello cadena de conexión de dispositivo de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="dfebc-141">Replace hello placeholder in Line 15 with hello Azure IoT hub device connection string.</span></span>
   <span data-ttu-id="dfebc-142">![Reemplace la cadena de conexión de dispositivo de Hola](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span><span class="sxs-lookup"><span data-stu-id="dfebc-142">![Replace hello device connection string](media/iot-hub-raspberry-pi-web-simulator/1_connectionstring.png)</span></span>

2. <span data-ttu-id="dfebc-143">Haga clic en **ejecutar** o tipo `npm start` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="dfebc-143">Click **Run** or type `npm start` toorun hello application.</span></span>


<span data-ttu-id="dfebc-144">Debería ver Hola después de salida que muestra los datos de sensor de Hola y mensajes de saludo que se envían centro de IoT tooyour ![salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span><span class="sxs-lookup"><span data-stu-id="dfebc-144">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub ![Output - sensor data sent from Raspberry Pi tooyour IoT hub](media/iot-hub-raspberry-pi-web-simulator/2_run_application.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="dfebc-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfebc-145">Next steps</span></span>

<span data-ttu-id="dfebc-146">Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="dfebc-146">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
