---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Introducción | Microsoft Docs"
description: "Introducción a la puerta de enlace de IoT Starter Kit, crea el centro de IoT de Azure y conectar el centro de IoT de puerta de enlace toohello"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Centro de iot de Azure, puerta de enlace de iot, introducción a Hola internet de las cosas, el Kit de herramientas de iot"
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
ms.openlocfilehash: 1a54a5e5f1c1d9b2e657c9e4448274256e2533f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-simulated-device"></a><span data-ttu-id="0cb16-104">Introducción con el kit de inicio de puerta de enlace de IoT con un dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="0cb16-104">Get started with IoT Gateway Starter Kit with a simulated device</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cb16-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="0cb16-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="0cb16-106">Dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="0cb16-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="0cb16-107">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con [Starter Kit de puerta de enlace de IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="0cb16-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="0cb16-108">Va a trabajar con Intel NUC que ejecuta Wind River Linux.</span><span class="sxs-lookup"><span data-stu-id="0cb16-108">You will be working with Intel NUC that's running Wind River Linux.</span></span> <span data-ttu-id="0cb16-109">Obtendrá información sobre cómo tooseamleesly conectar la nube de toohello de dispositivos mediante el uso de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb16-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="0cb16-110">**¿Aún no tiene el kit?:** haga clic [aquí](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="0cb16-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="0cb16-111">Lección 1: Configuración de NUC</span><span class="sxs-lookup"><span data-stu-id="0cb16-111">Lesson 1: Configure your NUC</span></span>
![Diagrama integral de la lección 1](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson1.png)

<span data-ttu-id="0cb16-113">En esta lección, configurar NUC de Intel (siguiente unidad de "informática") en hello Kit como una puerta de enlace de IoT de Azure, instalar paquetes de hello borde de IoT de Azure en NUC y ejecutar una funcionalidad de la puerta de enlace de la aplicación tooverify ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="0cb16-113">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="0cb16-114">*Estimado toocomplete de tiempo: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-114">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="0cb16-115">Vaya demasiado[configurar Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="0cb16-115">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="0cb16-116">Lección 2: Creación de la instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0cb16-116">Lesson 2: Create your IoT Hub</span></span>
![Diagrama integral de la lección 2](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson2.png)

<span data-ttu-id="0cb16-118">En esta lección, instale herramientas de Hola y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="0cb16-118">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="0cb16-119">A continuación, crear su cuenta de Azure gratuita, aprovisionar el centro de IoT de Azure y crear su primer dispositivo en el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="0cb16-119">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="0cb16-120">Complete la lección 1 antes de iniciar esta.</span><span class="sxs-lookup"><span data-stu-id="0cb16-120">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="0cb16-121">Obtener herramientas de Hola</span><span class="sxs-lookup"><span data-stu-id="0cb16-121">Get hello tools</span></span>
<span data-ttu-id="0cb16-122">Instalar software y herramientas de hello en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="0cb16-122">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="0cb16-123">*Estimado toocomplete de tiempo: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-123">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="0cb16-124">Vaya demasiado[obtener herramientas Hola](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="0cb16-124">Go too[Get hello tools](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="0cb16-125">Cree una instancia de IoT Hub y registre el dispositivo</span><span class="sxs-lookup"><span data-stu-id="0cb16-125">Create an IoT hub and register your device</span></span>
<span data-ttu-id="0cb16-126">Crear el grupo de recursos, aprovisionar el primer centro de IoT de Azure y agregar el primer centro de IoT de toohello de dispositivo mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb16-126">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="0cb16-127">*Estimado toocomplete de tiempo: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-127">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="0cb16-128">Vaya demasiado[crear un centro de IoT y registrar el dispositivo](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="0cb16-128">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-hello-simulated-device-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="0cb16-129">Lección 3: Recibir mensajes de dispositivo simulado de Hola y leer los mensajes de su centro de IoT</span><span class="sxs-lookup"><span data-stu-id="0cb16-129">Lesson 3: Receive messages from hello simulated device and read messages from your IoT hub</span></span>
<span data-ttu-id="0cb16-130">En esta lección, usará configuración de las secuencias de comandos tooautomate hello y ejecución de una aplicación de dispositivo simulado en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="0cb16-130">In this lesson, you will use scripts tooautomate hello configuration and execution of a simulated device app in your gateway.</span></span> <span data-ttu-id="0cb16-131">aplicación de dispositivo simulado de Hello genera datos de temperatura de ejemplo y lo envía el módulo de centro de IoT tooan.</span><span class="sxs-lookup"><span data-stu-id="0cb16-131">hello simulated device app generates sample temperature data and sends it tooan IoT hub module.</span></span> <span data-ttu-id="0cb16-132">Hola paquetes de módulo de centro de IoT datos Hola reciben y envía el centro de IoT tooyour a través del marco de puerta de enlace de hello proporcionado en el borde de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb16-132">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama integral de la lección 3](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson3.png)

### <a name="configure-and-run-a-simulated-device"></a><span data-ttu-id="0cb16-134">Configuración y ejecución de un dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="0cb16-134">Configure and run a simulated device</span></span>
<span data-ttu-id="0cb16-135">Preparar los códigos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0cb16-135">Prepare hello sample codes.</span></span> <span data-ttu-id="0cb16-136">A continuación, configure y ejecute la aplicación de ejemplo de Hola simulada dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0cb16-136">Then configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="0cb16-137">*Estimado toocomplete de tiempo: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-137">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="0cb16-138">Vaya demasiado[configurar y ejecutar un dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span><span class="sxs-lookup"><span data-stu-id="0cb16-138">Go too[Configure and run a simulated device](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="0cb16-139">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0cb16-139">Read messages from your IoT hub</span></span>
<span data-ttu-id="0cb16-140">Ejecutar código de ejemplo en los mensajes de saludo de tooread de equipo de host desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0cb16-140">Run a sample code on your host computer tooread hello messages from your IoT hub.</span></span>

<span data-ttu-id="0cb16-141">*Estimado toocomplete de tiempo: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="0cb16-142">Vaya demasiado[leer los mensajes de su centro de IoT](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="0cb16-142">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="0cb16-143">Lección 4: Guardar mensajes tooAzure el almacenamiento de tabla</span><span class="sxs-lookup"><span data-stu-id="0cb16-143">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="0cb16-144">Crear una aplicación de Azure de función que obtiene los mensajes entrantes desde el centro de IoT y los escribe tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="0cb16-144">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagrama integral de la lección 4](media/iot-hub-gateway-kit-lessons/e2e-sim-Lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="0cb16-146">Creación de una cuenta de Azure Storage y una aplicación de Azure Function</span><span class="sxs-lookup"><span data-stu-id="0cb16-146">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="0cb16-147">Utilice un toocreate de plantilla de Azure Resource Manager, una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb16-147">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="0cb16-148">*Estimado toocomplete de tiempo: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-148">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="0cb16-149">Vaya demasiado[crear una cuenta de almacenamiento de Azure y la aplicación de Azure (función)](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="0cb16-149">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="0cb16-150">Lectura de los mensajes que se conservan en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="0cb16-150">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="0cb16-151">Supervisar mensajes de puerta de enlace a la nube de hello tal y como se escriben tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="0cb16-151">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="0cb16-152">*Estimado toocomplete de tiempo: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="0cb16-152">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="0cb16-153">Vaya demasiado[leer los mensajes de guardado en el almacenamiento de Azure Table](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0cb16-153">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0cb16-154">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="0cb16-154">Troubleshooting</span></span>
<span data-ttu-id="0cb16-155">Si tiene problemas durante las lecciones de hello, buscar soluciones en hello [solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="0cb16-155">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-sim-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="0cb16-156">Explorar más</span><span class="sxs-lookup"><span data-stu-id="0cb16-156">Explore more</span></span>
<span data-ttu-id="0cb16-157">Visite hello [zona de desarrollador de Kit de puerta de enlace de IoT de Intel](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="0cb16-157">Visit hello [Intel IoT Gateway Kit developer zone](https://software.intel.com/en-us/iot/hardware/gateways/dev-kit) toolearn more.</span></span>
