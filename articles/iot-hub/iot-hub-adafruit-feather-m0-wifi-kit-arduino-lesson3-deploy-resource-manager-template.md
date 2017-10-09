---
title: "Connect Arduino (C) tooAzure IoT - lección 3: implementación de plantilla | Documentos de Microsoft"
description: "aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9c8f4cd1-9511-4601-ad7e-51761a986753
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6a84a6d3c5263a85c8997cf69fe446d73ab7a5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="082da-104">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="082da-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="082da-105">[Las funciones de Azure](../../articles/azure-functions/functions-overview.md) es una solución para ejecutar fácilmente *funciones* (pequeños fragmentos de código) en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="082da-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="082da-106">Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="082da-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="082da-107">Qué hará</span><span class="sxs-lookup"><span data-stu-id="082da-107">What will you do</span></span>
<span data-ttu-id="082da-108">Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="082da-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="082da-109">aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="082da-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="082da-110">Si tiene problemas, buscar soluciones en hello [solución de problemas de la página de su placa Adafruit compacto M0 Wi-Fi Arduino](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="082da-110">If you have any problems, look for solutions on hello [troubleshooting page for your Adafruit Feather M0 WiFi Arduino board](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="082da-111">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="082da-111">What will you learn</span></span>
<span data-ttu-id="082da-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="082da-112">In this article, you will learn:</span></span>
* <span data-ttu-id="082da-113">Cómo toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="082da-113">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="082da-114">¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="082da-114">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="082da-115">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="082da-115">What do you need</span></span>
<span data-ttu-id="082da-116">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="082da-116">You must have successfully completed:</span></span>
- <span data-ttu-id="082da-117">[Get started with your Arduino board][get-started] (Introducción a la placa de Arduino)</span><span class="sxs-lookup"><span data-stu-id="082da-117">[Get started with your Arduino board][get-started]</span></span>
- <span data-ttu-id="082da-118">[Creación de una instancia de Azure IoT Hub][create-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="082da-118">[Create your Azure IoT hub][create-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="082da-119">Aplicación de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="082da-119">Open hello sample app</span></span>
<span data-ttu-id="082da-120">Abra el proyecto de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="082da-120">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estructura del repositorio][repo-structure]

* <span data-ttu-id="082da-122">Hola `app.ino` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="082da-122">hello `app.ino` file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="082da-123">Este archivo de origen contiene código de hello toosend un mensaje 20 veces tooyour IoT hub- and blink Hola LED para cada mensaje que envía.</span><span class="sxs-lookup"><span data-stu-id="082da-123">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="082da-124">Hola `config.json` contiene valores de configuración necesarios.</span><span class="sxs-lookup"><span data-stu-id="082da-124">hello `config.json` contains required configuration settings.</span></span>
* <span data-ttu-id="082da-125">Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="082da-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="082da-126">Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="082da-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="082da-127">Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.</span><span class="sxs-lookup"><span data-stu-id="082da-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="082da-128">Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="082da-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="082da-129">Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="082da-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parámetros de plantilla de Azure Resource Manager][arm-template-params]

* <span data-ttu-id="082da-131">Sustituya **[su nombre de IoT Hub]** por el valor **{mi nombre de centro}** que especificó cuando [creó el IoT Hub y registró la placa de Arduino][created-iot-hub-and-registered-arduino-board].</span><span class="sxs-lookup"><span data-stu-id="082da-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered your Arduino board][created-iot-hub-and-registered-arduino-board].</span></span>
* <span data-ttu-id="082da-132">Reemplace **[prefix string for new resources]** por el prefijo que desee.</span><span class="sxs-lookup"><span data-stu-id="082da-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="082da-133">prefijo de Hola garantiza que el nombre de recurso hello es globalmente único tooavoid conflicto.</span><span class="sxs-lookup"><span data-stu-id="082da-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="082da-134">No use un guión o un número inicial de prefijo de Hola.</span><span class="sxs-lookup"><span data-stu-id="082da-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="082da-135">Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="082da-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="082da-136">Tarda aproximadamente cinco minutos toocreate estos recursos.</span><span class="sxs-lookup"><span data-stu-id="082da-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="082da-137">Mientras la creación de recursos de hello está en curso, puede mover en el artículo siguiente de toohello.</span><span class="sxs-lookup"><span data-stu-id="082da-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="082da-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="082da-138">Summary</span></span>
<span data-ttu-id="082da-139">Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="082da-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="082da-140">Ahora puede implementar y ejecutar mensajes de dispositivo a la nube de toosend de ejemplo de Hola en el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="082da-140">You can now deploy and run hello sample toosend device-to-cloud messages on your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="082da-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="082da-141">Next steps</span></span>
<span data-ttu-id="082da-142">[Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube en el panel de Arduino][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="082da-142">[Run a sample application toosend device-to-cloud messages on your Arduino board][send-device-to-cloud-messages]</span></span>

<!-- Images and links -->

[get-started]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[create-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/repo_structure_c.png
[arm-template-params]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/arm_para_arduino.png
[created-iot-hub-and-registered-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md