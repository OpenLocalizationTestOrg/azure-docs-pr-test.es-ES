---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Introducción | Microsoft Docs"
description: "Introducción a la puerta de enlace de IoT Starter Kit, crea el centro de IoT de Azure y conectar el centro de IoT toohello SensorTag y puerta de enlace"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Centro de iot de Azure, puerta de enlace de iot, introducción a Hola internet de las cosas, el Kit de herramientas de iot"
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
ms.openlocfilehash: d8e4057e7774e43c069dd3f2f2e03f098c1ac844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-iot-gateway-starter-kit-with-a-sensortag"></a><span data-ttu-id="e97dc-104">Introducción con el kit de inicio de puerta de enlace de IoT mediante un dispositivo SensorTag</span><span class="sxs-lookup"><span data-stu-id="e97dc-104">Get started with IoT Gateway Starter Kit with a SensorTag</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e97dc-105">SensorTag</span><span class="sxs-lookup"><span data-stu-id="e97dc-105">SensorTag</span></span>](iot-hub-gateway-kit-c-get-started.md)
> * [<span data-ttu-id="e97dc-106">Dispositivo simulado</span><span class="sxs-lookup"><span data-stu-id="e97dc-106">Simulated Device</span></span>](iot-hub-gateway-kit-c-sim-get-started.md)

<span data-ttu-id="e97dc-107">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con [Starter Kit de puerta de enlace de IoT](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="e97dc-107">In this tutorial, you begin by learning hello basics of working with [IoT Gateway Starter Kit](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="e97dc-108">Se va a trabajar con NUC de Intel que ejecuta Linux demarcación de viento y hello [SensorTag de TI](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span><span class="sxs-lookup"><span data-stu-id="e97dc-108">You will be working with Intel NUC that's running Wind River Linux and hello [TI SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html#main).</span></span> <span data-ttu-id="e97dc-109">Obtendrá información sobre cómo tooseamleesly conectar la nube de toohello de dispositivos mediante el uso de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="e97dc-109">You will learn how tooseamleesly connect your devices toohello cloud by using Azure IoT Hub.</span></span>

***
<span data-ttu-id="e97dc-110">**¿Aún no tiene el kit?:** haga clic [aquí](https://aka.ms/gateway-kit).</span><span class="sxs-lookup"><span data-stu-id="e97dc-110">**Don't have a kit yet?:** Click [here](https://aka.ms/gateway-kit).</span></span> <span data-ttu-id="e97dc-111">**¿No tiene un dispositivo SensorTag?:**[Empiece con un dispositivo simulado](iot-hub-gateway-kit-c-sim-get-started.md) o [compre un dispositivo SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span><span class="sxs-lookup"><span data-stu-id="e97dc-111">**Don't have a SensorTag?:** [Start with a simulated device](iot-hub-gateway-kit-c-sim-get-started.md) or [buy a SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/?INTC=SensorTag&HQS=sensortag)</span></span>
***

## <a name="lesson-1-configure-your-nuc"></a><span data-ttu-id="e97dc-112">Lección 1: Configuración de NUC</span><span class="sxs-lookup"><span data-stu-id="e97dc-112">Lesson 1: Configure your NUC</span></span>
![Diagrama integral de la lección 1](media/iot-hub-gateway-kit-lessons/e2e-lesson1.png)

<span data-ttu-id="e97dc-114">En esta lección, configurar NUC de Intel (siguiente unidad de "informática") en hello Kit como una puerta de enlace de IoT de Azure, instalar paquetes de hello borde de IoT de Azure en NUC y ejecutar una funcionalidad de la puerta de enlace de la aplicación tooverify ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="e97dc-114">In this lesson, you set up Intel NUC (Next Unit of Computing) in hello Kit as an Azure IoT gateway, install hello Azure IoT Edge package on NUC, and run a sample app tooverify hello gateway functionality.</span></span>

<span data-ttu-id="e97dc-115">*Estimado toocomplete de tiempo: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-115">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="e97dc-116">Vaya demasiado[configurar Intel NUC como una puerta de enlace de IoT](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span><span class="sxs-lookup"><span data-stu-id="e97dc-116">Go too[Set up Intel NUC as an IoT gateway](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)</span></span>

## <a name="lesson-2-create-your-iot-hub"></a><span data-ttu-id="e97dc-117">Lección 2: Creación de la instancia de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e97dc-117">Lesson 2: Create your IoT Hub</span></span>
![Diagrama integral de la lección 2](media/iot-hub-gateway-kit-lessons/e2e-lesson2.png)

<span data-ttu-id="e97dc-119">En esta lección, instale herramientas de Hola y el software en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="e97dc-119">In this lesson, you install hello tools and software on your host computer.</span></span> <span data-ttu-id="e97dc-120">A continuación, crear su cuenta de Azure gratuita, aprovisionar el centro de IoT de Azure y crear su primer dispositivo en el centro de IoT Hola.</span><span class="sxs-lookup"><span data-stu-id="e97dc-120">Then you create your free Azure account, provision your Azure IoT hub and create your first device in hello IoT hub.</span></span>

<span data-ttu-id="e97dc-121">Complete la lección 1 antes de iniciar esta.</span><span class="sxs-lookup"><span data-stu-id="e97dc-121">Complete Lesson 1 before you start this lesson.</span></span>

### <a name="get-hello-tools"></a><span data-ttu-id="e97dc-122">Obtener herramientas de Hola</span><span class="sxs-lookup"><span data-stu-id="e97dc-122">Get hello tools</span></span>
<span data-ttu-id="e97dc-123">Instalar software y herramientas de hello en el equipo host.</span><span class="sxs-lookup"><span data-stu-id="e97dc-123">Install hello tools and software on your host computer.</span></span>

<span data-ttu-id="e97dc-124">*Estimado toocomplete de tiempo: 20 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-124">*Estimated time toocomplete: 20 minutes*</span></span>

<span data-ttu-id="e97dc-125">Vaya demasiado[obtener herramientas Hola](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span><span class="sxs-lookup"><span data-stu-id="e97dc-125">Go too[Get hello tools](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)</span></span>

### <a name="create-an-iot-hub-and-register-your-device"></a><span data-ttu-id="e97dc-126">Cree una instancia de IoT Hub y registre el dispositivo</span><span class="sxs-lookup"><span data-stu-id="e97dc-126">Create an IoT hub and register your device</span></span>
<span data-ttu-id="e97dc-127">Crear el grupo de recursos, aprovisionar el primer centro de IoT de Azure y agregar el primer centro de IoT de toohello de dispositivo mediante Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="e97dc-127">Create your resource group, provision your first Azure IoT hub, and add your first device toohello IoT hub using hello Azure CLI.</span></span>

<span data-ttu-id="e97dc-128">*Estimado toocomplete de tiempo: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-128">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="e97dc-129">Vaya demasiado[crear un centro de IoT y registrar el dispositivo](iot-hub-gateway-kit-c-lesson2-register-device.md)</span><span class="sxs-lookup"><span data-stu-id="e97dc-129">Go too[Create an IoT hub and register your device](iot-hub-gateway-kit-c-lesson2-register-device.md)</span></span>

## <a name="lesson-3-receive-messages-from-sensortag-and-read-messages-from-your-iot-hub"></a><span data-ttu-id="e97dc-130">Lección 3: Recibir mensajes de SensorTag y leerlos en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e97dc-130">Lesson 3: Receive messages from SensorTag and read messages from your IoT hub</span></span>
<span data-ttu-id="e97dc-131">En esta lección, usará configuración de las secuencias de comandos tooautomate hello y ejecución de una aplicación de ejemplo Bilitar en la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e97dc-131">In this lesson, you will use scripts tooautomate hello configuration and execution of a BLE sample application in your gateway.</span></span> <span data-ttu-id="e97dc-132">Dichas aplicaciones utiliza una colección de módulos tooaggregate y transformación de datos, procesan los comandos o realizan una serie de tareas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e97dc-132">Such applications use a collection of modules tooaggregate and transform data, process commands, or perform any number of related tasks.</span></span> <span data-ttu-id="e97dc-133">Los módulos se comunican entre sí a través de un agente de mensajes.</span><span class="sxs-lookup"><span data-stu-id="e97dc-133">Modules communicate with one another via a message broker.</span></span> <span data-ttu-id="e97dc-134">aplicación de ejemplo de Hola tiene un módulo de Bilitar y un módulo de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e97dc-134">hello sample application has a BLE module and an IoT hub module.</span></span> <span data-ttu-id="e97dc-135">módulo de Hello Bilitar recibe datos de Bilitar SensorTag.</span><span class="sxs-lookup"><span data-stu-id="e97dc-135">hello BLE module receives data from BLE SensorTag.</span></span> <span data-ttu-id="e97dc-136">Hola paquetes de módulo de centro de IoT datos Hola reciben y envía el centro de IoT tooyour a través del marco de puerta de enlace de hello proporcionado en el borde de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="e97dc-136">hello IoT hub module packages hello data received and sends it tooyour IoT hub through hello gateway framework provided in Azure IoT Edge.</span></span>

![Diagrama integral de la lección 3](media/iot-hub-gateway-kit-lessons/e2e-lesson3.png)

### <a name="configure-and-run-hello-ble-sample-app"></a><span data-ttu-id="e97dc-138">Configurar y ejecutar la aplicación de ejemplo de Hola BLE</span><span class="sxs-lookup"><span data-stu-id="e97dc-138">Configure and run hello BLE sample app</span></span>
<span data-ttu-id="e97dc-139">Configurar la conectividad de hello entre SensorTag y la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e97dc-139">Set up hello connectivity between SensorTag and your gateway.</span></span> <span data-ttu-id="e97dc-140">A continuación, finalice la configuración de Hola y ejecutar la aplicación de ejemplo de Hola Bilitar.</span><span class="sxs-lookup"><span data-stu-id="e97dc-140">Then finish hello configuration and run hello BLE sample application.</span></span>

<span data-ttu-id="e97dc-141">*Estimado toocomplete de tiempo: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-141">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="e97dc-142">Vaya demasiado[ejecución hello habilitar y configurar aplicación de ejemplo](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span><span class="sxs-lookup"><span data-stu-id="e97dc-142">Go too[Configure and run hello BLE sample app](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)</span></span>

### <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="e97dc-143">Lectura de mensajes en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e97dc-143">Read messages from your IoT hub</span></span>
<span data-ttu-id="e97dc-144">Ejecutar código de ejemplo en el host de equipo tooread mensajes desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e97dc-144">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="e97dc-145">*Estimado toocomplete de tiempo: 15 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-145">*Estimated time toocomplete: 15 minutes*</span></span>

<span data-ttu-id="e97dc-146">Vaya demasiado[leer los mensajes de su centro de IoT](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span><span class="sxs-lookup"><span data-stu-id="e97dc-146">Go too[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>

## <a name="lesson-4-save-messages-tooazure-table-storage"></a><span data-ttu-id="e97dc-147">Lección 4: Guardar mensajes tooAzure el almacenamiento de tabla</span><span class="sxs-lookup"><span data-stu-id="e97dc-147">Lesson 4: Save messages tooAzure Table storage</span></span>
<span data-ttu-id="e97dc-148">Crear una aplicación de Azure de función que obtiene los mensajes entrantes desde el centro de IoT y los escribe tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="e97dc-148">Create an Azure function app that gets incoming messages from your IoT hub and writes them tooAzure Table storage.</span></span>

![Diagrama integral de la lección 4](media/iot-hub-gateway-kit-lessons/e2e-lesson4.png)

### <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="e97dc-150">Creación de una cuenta de Azure Storage y una aplicación de Azure Function</span><span class="sxs-lookup"><span data-stu-id="e97dc-150">Create an Azure function app and Azure Storage account</span></span>
<span data-ttu-id="e97dc-151">Utilice un toocreate de plantilla de Azure Resource Manager, una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e97dc-151">Use an Azure Resource Manager template toocreate an Azure function app and an Azure Storage account.</span></span>

<span data-ttu-id="e97dc-152">*Estimado toocomplete de tiempo: 10 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-152">*Estimated time toocomplete: 10 minutes*</span></span>

<span data-ttu-id="e97dc-153">Vaya demasiado[crear una cuenta de almacenamiento de Azure y la aplicación de Azure (función)](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="e97dc-153">Go too[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>

### <a name="read-messages-persisted-in-azure-table-storage"></a><span data-ttu-id="e97dc-154">Lectura de los mensajes que se conservan en Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="e97dc-154">Read messages persisted in Azure Table storage</span></span>
<span data-ttu-id="e97dc-155">Supervisar mensajes de puerta de enlace a la nube de hello tal y como se escriben tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="e97dc-155">Monitor hello gateway-to-cloud messages as they are written tooAzure Table storage.</span></span>

<span data-ttu-id="e97dc-156">*Estimado toocomplete de tiempo: 5 minutos*</span><span class="sxs-lookup"><span data-stu-id="e97dc-156">*Estimated time toocomplete: 5 minutes*</span></span>

<span data-ttu-id="e97dc-157">Vaya demasiado[leer los mensajes de guardado en el almacenamiento de Azure Table](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e97dc-157">Go too[Read messages persisted in Azure Table storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e97dc-158">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="e97dc-158">Troubleshooting</span></span>
<span data-ttu-id="e97dc-159">Si tiene problemas durante las lecciones de hello, buscar soluciones en hello [solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="e97dc-159">If you have any problems during hello lessons, look for solutions in hello [Troubleshooting](iot-hub-gateway-kit-c-troubleshooting.md) article.</span></span>

## <a name="explore-more"></a><span data-ttu-id="e97dc-160">Explorar más</span><span class="sxs-lookup"><span data-stu-id="e97dc-160">Explore more</span></span>
<span data-ttu-id="e97dc-161">Visite hello [zona de desarrollador de Kit de puerta de enlace de IoT de Intel](http://software.intel.com/iot/microsoft-azure) toolearn más.</span><span class="sxs-lookup"><span data-stu-id="e97dc-161">Visit hello [Intel IoT Gateway Kit developer zone](http://software.intel.com/iot/microsoft-azure) toolearn more.</span></span>
