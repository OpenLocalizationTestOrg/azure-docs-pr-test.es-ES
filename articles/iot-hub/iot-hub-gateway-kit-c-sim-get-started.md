---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Introducción | Microsoft Docs"
description: Comience con el kit de inicio de puerta de enlace de IoT, cree la instancia de IoT Hub de Azure y conecte la puerta de enlace a la instancia de IoT Hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "iot hub de azure, puerta de enlace de iot, introducción con internet de las cosas, kit de herramientas de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 0c110b8b-bee4-4aec-a18a-dfc292aa17a3
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 916fa40d9ac857dfa72197b40c232834593d3891
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="cd933-104">Introducción con el kit de inicio de puerta de enlace de IoT con un dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="cd933-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd933-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="cd933-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="cd933-106">Dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="cd933-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="cd933-107">En este tutorial, empezará por aprender los conceptos básicos sobre cómo trabajar con el [kit de inicio de puerta de enlace de IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="cd933-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="cd933-108">Va a trabajar con Intel NUC que ejecuta Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="cd933-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="cd933-109">Aprenderá a conectar fácilmente los dispositivos a la nube mediante IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd933-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="cd933-110">**¿Aún no tiene el kit?:** haga clic [aquí](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="cd933-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="cd933-111">Lección 1: Configuración de NUC</span><span class="sxs-lookup"><span data-stu-id="cd933-111">Lesson 1: Configure your NUC</span></span>
![Diagrama integral de la lección 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="cd933-113">En esta lección, se configura Intel NUC (Next Unit of Computing) en el kit como una puerta de enlace de IoT de Azure, se instala el paquete de Azure IoT Edge en NUC y se ejecuta una aplicación de ejemplo para comprobar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="cd933-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="cd933-114">*Tiempo estimado para completar el tutorial: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-114">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="cd933-115">Vaya a [Configuración de Intel NUC como puerta de enlace de IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md) (Configuración de Intel NUC como una puerta de enlace de IoT).</span><span class="sxs-lookup"><span data-stu-id="cd933-115">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="cd933-116">Lección 2: Creación de la instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cd933-116">Lesson 2: Create your IoT Hub</span></span>
![Diagrama integral de la lección 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="cd933-118">En esta lección, se instalan las herramientas y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="cd933-118">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="cd933-119">Debe crear una cuenta gratuita de Azure, aprovisionar la instancia de IoT Hub de Azure y crear el primer dispositivo en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cd933-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="cd933-120">Complete la lección 1 antes de iniciar esta.</span><span class="sxs-lookup"><span data-stu-id="cd933-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="cd933-121">Obtener las herramientas</span><span class="sxs-lookup"><span data-stu-id="cd933-121">Get the tools</span></span>
<span data-ttu-id="cd933-122">Instale las herramientas y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="cd933-122">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="cd933-123">*Tiempo estimado para completar el tutorial: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-123">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="cd933-124">Vaya a [Obtener las herramientas](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md).</span><span class="sxs-lookup"><span data-stu-id="cd933-124">Go to [Get the tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="cd933-125">Cree una instancia de IoT Hub y registre el dispositivo</span><span class="sxs-lookup"><span data-stu-id="cd933-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="cd933-126">Cree el grupo de recursos, aprovisione la primera instancia de IoT Hub de Azure y agregue el primer dispositivo a dicha instancia mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="cd933-126">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="cd933-127">*Tiempo estimado para completar el tutorial: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-127">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="cd933-128">Vaya a [Creación de una instancia de IoT Hub y registro del dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md).</span><span class="sxs-lookup"><span data-stu-id="cd933-128">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-the-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="cd933-129">Lección 3: Recepción de mensajes del dispositivo simulado y lectura de estos en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cd933-129">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="cd933-130">En esta lección, usará scripts para automatizar la configuración y la ejecución de una aplicación de dispositivo simulado en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="cd933-130">In this lesson, you will use scripts to automate the configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="cd933-131">La aplicación de dispositivo simulado genera datos de temperatura de ejemplo y los envía a un módulo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cd933-131">The simulated device app generates sample temperature data and sends it to an IoT hub module.</span></span> <span data-ttu-id="cd933-132">El módulo de IoT Hub empaqueta los datos recibidos y los envía a su IoT Hub a través del marco de la puerta de enlace proporcionado en Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="cd933-132">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama integral de la lección 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="cd933-134">Configuración y ejecución de un dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="cd933-134">Configure and run a simulated device</span></span>
<span data-ttu-id="cd933-135">Prepare los códigos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cd933-135">Prepare the sample codes.</span></span> <span data-ttu-id="cd933-136">Luego, configure y ejecute la aplicación de ejemplo del dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="cd933-136">Then configure and run the simulated device sample application.</span></span>

<span data-ttu-id="cd933-137">*Tiempo estimado para completar el tutorial: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-137">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="cd933-138">Vaya a [Configuración y ejecución de un dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="cd933-138">Go to [Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="cd933-139">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="cd933-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="cd933-140">Ejecute el código de ejemplo en el equipo host para leer los mensajes en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cd933-140">Run a sample code on your host computer to read the messages from your IoT hub.</span></span>

<span data-ttu-id="cd933-141">*Tiempo estimado para completar el tutorial: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="cd933-142">Vaya a [Lectura de mensajes en IoT Hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="cd933-142">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="cd933-143">Lección 4: Almacenamiento de mensajes en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="cd933-143">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="cd933-144">Cree una instancia de Azure Function App que recopile los mensajes entrantes de la instancia de IoT Hub y los escriba en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="cd933-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagrama integral de la lección 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="cd933-146">Creación de una cuenta de Azure Storage y una aplicación de Azure Function</span><span class="sxs-lookup"><span data-stu-id="cd933-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="cd933-147">Use una plantilla de Azure Resource Manager para crear una aplicación de Azure Function y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cd933-147">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="cd933-148">*Tiempo estimado para completar el tutorial: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-148">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="cd933-149">Vaya a [Creación de una instancia de Azure Function App y una cuenta de Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="cd933-149">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="cd933-150">Lectura de los mensajes que se conservan en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="cd933-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="cd933-151">Supervise los mensajes de la puerta de enlace a la nube a medida que se escriben en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="cd933-151">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="cd933-152">*Tiempo estimado para completar el tutorial: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="cd933-152">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="cd933-153">Vaya a [Lectura de los mensajes que se conservan en Azure Table Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md) (Lectura de los mensajes que se conservan en Azure Table Storage).</span><span class="sxs-lookup"><span data-stu-id="cd933-153">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cd933-154">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cd933-154">Troubleshooting</span></span>
<span data-ttu-id="cd933-155">Si tiene algún problema durante las lecciones, puede encontrar soluciones en el artículo [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) (Solución de problemas).</span><span class="sxs-lookup"><span data-stu-id="cd933-155">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="cd933-156">Explorar más</span><span class="sxs-lookup"><span data-stu-id="cd933-156">Explore more</span></span>
<span data-ttu-id="cd933-157">Visite la [zona de desarrollador del Kit de puerta de enlace de IoT de Intel](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="cd933-157">Visit the [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) to learn more.</span></span>