---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 4: Creación de Function App | Microsoft Docs"
description: "Guardar mensajes Intel NUC tooyour centro de IoT, escribirlos tooAzure el almacenamiento de tabla y, a continuación, leerlos desde la nube de Hola."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f84f9a85-e2c4-4a92-8969-f65eb34c194e
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: efee3bdc15ced104651f4a500311a5fe614267c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="4c95b-104">Creación de una cuenta de Azure Storage y una aplicación de Azure Function</span><span class="sxs-lookup"><span data-stu-id="4c95b-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="4c95b-105">Las funciones de Azure es una solución para ejecutar fácilmente _funciones_ (pequeños fragmentos de código) en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="4c95b-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="4c95b-106">Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c95b-106">An Azure function app hosts hello execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="4c95b-107">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="4c95b-107">What you will do</span></span>

- <span data-ttu-id="4c95b-108">Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c95b-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="4c95b-109">aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="4c95b-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span>

<span data-ttu-id="4c95b-110">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4c95b-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="4c95b-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="4c95b-111">What you will learn</span></span>

<span data-ttu-id="4c95b-112">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4c95b-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="4c95b-113">Cómo toouse toodeploy de administrador de recursos de Azure recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c95b-113">How toouse Azure Resource Manager toodeploy Azure resources.</span></span>
- <span data-ttu-id="4c95b-114">¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c95b-114">How toouse an Azure function app tooprocess IoT Hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4c95b-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="4c95b-115">What you need</span></span>

<span data-ttu-id="4c95b-116">Debe haber completado correctamente lecciones anteriores de hello:</span><span class="sxs-lookup"><span data-stu-id="4c95b-116">You must have successfully completed hello previous lessons:</span></span>

- [<span data-ttu-id="4c95b-117">Lección 1: Configuración de Intel NUC como puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="4c95b-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
- [<span data-ttu-id="4c95b-118">Lección 2: Preparación del equipo host y de IoT Hub de Azure</span><span class="sxs-lookup"><span data-stu-id="4c95b-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="4c95b-119">Lección 3: Recepción de mensajes de SensorTag y lectura en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="4c95b-119">Lesson 3: Receive messages from SensorTag and read messages from IoT hub</span></span>](iot-hub-gateway-kit-c-lesson3-configure-ble-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="4c95b-120">Apertura de una aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4c95b-120">Open a sample app</span></span>

<span data-ttu-id="4c95b-121">Vaya tooyour `iot-hub-c-intel-nuc-gateway-getting-started` carpeta repo, archivos de configuración de inicializar hello y proyecto de ejemplo de Hola, a continuación, abrir en Visual Studio Code ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="4c95b-121">Go tooyour `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize hello configuration files, and then open hello sample project in Visual Studio Code by running hello following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![estructura del repositorio](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="4c95b-123">Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="4c95b-123">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="4c95b-124">Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4c95b-124">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
- <span data-ttu-id="4c95b-125">Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.</span><span class="sxs-lookup"><span data-stu-id="4c95b-125">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="4c95b-126">Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="4c95b-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="4c95b-127">Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c95b-127">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm template json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="4c95b-129">Sustituya `[your IoT Hub name]` por el valor `{my hub name}` que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="4c95b-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="4c95b-130">Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4c95b-130">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="4c95b-131">Use `iot-gateway` como valor de Hola de `{resource group name}` si no cambia el valor de hello en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="4c95b-131">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="4c95b-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="4c95b-132">Summary</span></span>

<span data-ttu-id="4c95b-133">Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="4c95b-133">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="4c95b-134">Ahora puede leer los mensajes enviados por el centro de IoT tooyour de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4c95b-134">You can now read messages that are sent by your gateway tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c95b-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4c95b-135">Next steps</span></span>
<span data-ttu-id="4c95b-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md) (Lectura de los mensajes que se conservan en Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="4c95b-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-lesson4-read-table-storage.md).</span></span>
