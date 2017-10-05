---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Introducción | Microsoft Docs"
description: Comience con el kit de inicio de puerta de enlace de IoT, cree el centro de IoT de Azure y conecte SensorTag y la puerta de enlace al centro de IoT
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot hub, puerta de enlace de iot, introducción con internet de las cosas, kit de herramientas de iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 56d05f4e-f2c1-4b22-8701-f01e14deead6
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 624bdc7877d5048da08897f868272fd8e8f3f7b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="8a691-104">Introducción con el kit de inicio de puerta de enlace de IoT mediante un dispositivo SensorTag</span><span class="sxs-lookup"><span data-stu-id="8a691-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a691-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="8a691-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="8a691-106">Dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="8a691-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="8a691-107">En este tutorial, empiece por aprender los conceptos básicos sobre cómo trabajar con el [kit de inicio de puerta de enlace de IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="8a691-107">In this tutorial, you begin by learning the basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="8a691-108">Va a trabajar con Intel NUC que ejecuta Wind River Linux y [SensorTag de TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="8a691-108">You will be working with Intel NUC that's running Wind River Linux and the [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="8a691-109">Aprenderá a conectar fácilmente los dispositivos a la nube mediante Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8a691-109">You will learn how to seamleesly connect your devices to the cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="8a691-110">**¿Aún no tiene el kit?:** haga clic [aquí](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="8a691-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="8a691-111">**¿No tiene un dispositivo SensorTag?:** [Empiece con un dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) o [compre un dispositivo SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="8a691-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="8a691-112">Lección 1: Configuración de NUC</span><span class="sxs-lookup"><span data-stu-id="8a691-112">Lesson 1: Configure your NUC</span></span>
![Diagrama integral de la lección 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="8a691-114">En esta lección, se configura Intel NUC (Next Unit of Computing) en el kit como una puerta de enlace de IoT de Azure, se instala el paquete de Azure IoT Edge en NUC y se ejecuta una aplicación de ejemplo para comprobar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8a691-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in the Kit as an Azure IoT gateway, install the Azure IoT Edge package on NUC, and run a sample app to verify the gateway functionality.</span></span>

<span data-ttu-id="8a691-115">*Tiempo estimado para completar el tutorial: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-115">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="8a691-116">Vaya a [Configuración de Intel NUC como puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) (Configuración de Intel NUC como una puerta de enlace de IoT).</span><span class="sxs-lookup"><span data-stu-id="8a691-116">Go to [Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="8a691-117">Lección 2: Creación de la instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="8a691-117">Lesson 2: Create your IoT Hub</span></span>
![Diagrama integral de la lección 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="8a691-119">En esta lección, se instalan las herramientas y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="8a691-119">In this lesson, you install the tools and software on your host computer.</span></span> <span data-ttu-id="8a691-120">Debe crear una cuenta gratuita de Azure, aprovisionar la instancia de IoT Hub de Azure y crear el primer dispositivo en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8a691-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in the IoT hub.</span></span>

<span data-ttu-id="8a691-121">Complete la lección 1 antes de iniciar esta.</span><span class="sxs-lookup"><span data-stu-id="8a691-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-the-tools"></a><span data-ttu-id="8a691-122">Obtener las herramientas</span><span class="sxs-lookup"><span data-stu-id="8a691-122">Get the tools</span></span>
<span data-ttu-id="8a691-123">Instale las herramientas y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="8a691-123">Install the tools and software on your host computer.</span></span>

<span data-ttu-id="8a691-124">*Tiempo estimado para completar el tutorial: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-124">*Estimated time to complete: 20 minutes*</span></span>

<span data-ttu-id="8a691-125">Vaya a [Obtener las herramientas](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md).</span><span class="sxs-lookup"><span data-stu-id="8a691-125">Go to [Get the tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="8a691-126">Cree una instancia de IoT Hub y registre el dispositivo</span><span class="sxs-lookup"><span data-stu-id="8a691-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="8a691-127">Cree el grupo de recursos, aprovisione la primera instancia de IoT Hub de Azure y agregue el primer dispositivo a dicha instancia mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8a691-127">Create your resource group, provision your first Azure IoT hub, and add your first device to the IoT hub using the Azure CLI.</span></span>

<span data-ttu-id="8a691-128">*Tiempo estimado para completar el tutorial: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-128">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="8a691-129">Vaya a [Creación de un IoT Hub y registro del dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md).</span><span class="sxs-lookup"><span data-stu-id="8a691-129">Go to [Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="8a691-130">Lección 3: Recibir mensajes de SensorTag y leerlos en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="8a691-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="8a691-131">En esta lección, usará scripts para automatizar la configuración y ejecución de una aplicación de ejemplo BLE en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8a691-131">In this lesson, you will use scripts to automate the configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="8a691-132">Dichas aplicaciones utilizan una colección de módulos para agregar y transformar datos, procesar comandos o realizar una serie de tareas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="8a691-132">Such applications use a collection of modules to aggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="8a691-133">Los módulos se comunican entre sí a través de un agente de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8a691-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="8a691-134">La aplicación de ejemplo tiene un módulo de BLE y un módulo de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8a691-134">The sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="8a691-135">El módulo BLE recibe datos de SensorTag para BLE.</span><span class="sxs-lookup"><span data-stu-id="8a691-135">The BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="8a691-136">El módulo de IoT Hub empaqueta los datos recibidos y los envía a su IoT Hub a través del marco de la puerta de enlace proporcionado en Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="8a691-136">The IoT hub module packages the data received and sends it to your IoT hub through the gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama integral de la lección 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-the-ble-sample-app"></a><span data-ttu-id="8a691-138">Configuración y ejecución de la aplicación de ejemplo BLE</span><span class="sxs-lookup"><span data-stu-id="8a691-138">Configure and run the BLE sample app</span></span>
<span data-ttu-id="8a691-139">Configure la conectividad entre SensorTag y la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8a691-139">Set up the connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="8a691-140">Complete la configuración y ejecute la aplicación de ejemplo BLE.</span><span class="sxs-lookup"><span data-stu-id="8a691-140">Then finish the configuration and run the BLE sample application.</span></span>

<span data-ttu-id="8a691-141">*Tiempo estimado para completar el tutorial: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-141">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="8a691-142">Vaya a [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md) (Configuración y ejecución de la aplicación de ejemplo BLE).</span><span class="sxs-lookup"><span data-stu-id="8a691-142">Go to [Configure and run the BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="8a691-143">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="8a691-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="8a691-144">Ejecute el código de ejemplo en el equipo host para leer los mensajes en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8a691-144">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="8a691-145">*Tiempo estimado para completar el tutorial: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-145">*Estimated time to complete: 15 minutes*</span></span>

<span data-ttu-id="8a691-146">Vaya a [Lectura de mensajes en IoT Hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="8a691-146">Go to [Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-to-azure-table-storage"></a><span data-ttu-id="8a691-147">Lección 4: Almacenamiento de mensajes en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="8a691-147">Lesson 4: Save messages to Azure Table storage</span></span>
<span data-ttu-id="8a691-148">Cree una instancia de Azure Function App que recopile los mensajes entrantes de la instancia de IoT Hub y los escriba en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8a691-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them to Azure Table storage.</span></span>

![Diagrama integral de la lección 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="8a691-150">Creación de una cuenta de Azure Storage y una aplicación de Azure Function</span><span class="sxs-lookup"><span data-stu-id="8a691-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="8a691-151">Use una plantilla de Azure Resource Manager para crear una aplicación de Azure Function y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8a691-151">Use an Azure Resource Manager template to create an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="8a691-152">*Tiempo estimado para completar el tutorial: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-152">*Estimated time to complete: 10 minutes*</span></span>

<span data-ttu-id="8a691-153">Vaya a [Creación de una instancia de Azure Function App y una cuenta de Azure Storage](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="8a691-153">Go to [Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="8a691-154">Lectura de los mensajes que se conservan en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="8a691-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="8a691-155">Supervise los mensajes de la puerta de enlace a la nube a medida que se escriben en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="8a691-155">Monitor the gateway-to-cloud messages as they are written to Azure Table storage.</span></span>

<span data-ttu-id="8a691-156">*Tiempo estimado para completar el tutorial: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="8a691-156">*Estimated time to complete: 5 minutes*</span></span>

<span data-ttu-id="8a691-157">Vaya a [Lectura de los mensajes que se conservan en Azure Table Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md) (Lectura de los mensajes que se conservan en Azure Table Storage).</span><span class="sxs-lookup"><span data-stu-id="8a691-157">Go to [Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8a691-158">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8a691-158">Troubleshooting</span></span>
<span data-ttu-id="8a691-159">Si tiene algún problema durante las lecciones, puede encontrar soluciones en el artículo [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) (Solución de problemas).</span><span class="sxs-lookup"><span data-stu-id="8a691-159">If you have any problems during the lessons, look for solutions in the [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="8a691-160">Explorar más</span><span class="sxs-lookup"><span data-stu-id="8a691-160">Explore more</span></span>
<span data-ttu-id="8a691-161">Visite la [zona de desarrollador del Kit de puerta de enlace de IoT de Intel](http://software.intel.com/iot/microsoft-azure) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8a691-161">Visit the [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) to learn more.</span></span>