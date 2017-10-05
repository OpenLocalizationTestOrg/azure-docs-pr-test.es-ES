---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 4: Guardado de mensajes | Microsoft Docs"
description: "Guarde mensajes de Intel NUC en su IoT Hub, escríbalos en una tabla de Azure Table Storage y, después, léalos desde la nube."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube, datos almacenados en la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: ffed0c2e-b092-40e1-9113-8196ec057d67
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c7fc47b07acede28ffe790debca7e38521726011
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-storage-account"></a><span data-ttu-id="39d7a-104">Creación de una cuenta de Azure Storage y una aplicación de Azure Function</span><span class="sxs-lookup"><span data-stu-id="39d7a-104">Create an Azure function app and storage account</span></span>

<span data-ttu-id="39d7a-105">Azure Functions es una solución que permite ejecutar _funciones_ (pequeños fragmentos de código) en la nube fácilmente.</span><span class="sxs-lookup"><span data-stu-id="39d7a-105">Azure Functions is a solution for easily running _functions_ (small pieces of code) in the cloud.</span></span> <span data-ttu-id="39d7a-106">Una aplicación de Azure Function hospeda la ejecución de sus funciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="39d7a-106">An Azure function app hosts the execution of your functions in Azure.</span></span> 

## <a name="what-you-will-do"></a><span data-ttu-id="39d7a-107">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="39d7a-107">What you will do</span></span>

- <span data-ttu-id="39d7a-108">Va a utilizar una plantilla de Azure Resource Manager para crear una instancia de Azure Function App y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="39d7a-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="39d7a-109">La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="39d7a-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span>

<span data-ttu-id="39d7a-110">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="39d7a-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>


## <a name="what-you-will-learn"></a><span data-ttu-id="39d7a-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="39d7a-111">What you will learn</span></span>

<span data-ttu-id="39d7a-112">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="39d7a-112">In this lesson, you will learn:</span></span>

- <span data-ttu-id="39d7a-113">Uso de Azure Resource Manager para implementar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="39d7a-113">How to use Azure Resource Manager to deploy Azure resources.</span></span>
- <span data-ttu-id="39d7a-114">Uso de una instancia de Azure Function App para procesar mensajes de IoT Hub y escribirlos en una tabla de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="39d7a-114">How to use an Azure function app to process IoT Hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="39d7a-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="39d7a-115">What you need</span></span>

<span data-ttu-id="39d7a-116">Debe haber completado correctamente las lecciones anteriores:</span><span class="sxs-lookup"><span data-stu-id="39d7a-116">You must have successfully completed the previous lessons:</span></span>

- [<span data-ttu-id="39d7a-117">Lección 1: Configuración de Intel NUC como puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="39d7a-117">Lesson 1: Set up your Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-sim-lesson1-set-up-nuc.md)
- [<span data-ttu-id="39d7a-118">Lección 2: Preparación del equipo host y de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="39d7a-118">Lesson 2: Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
- [<span data-ttu-id="39d7a-119">Lección 3: Recepción de mensajes del dispositivo simulado y lectura de estos desde el IoT Hub</span><span class="sxs-lookup"><span data-stu-id="39d7a-119">Lesson 3: Receive messages from the simulated device and read messages from your IoT hub</span></span>](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md)

## <a name="open-a-sample-app"></a><span data-ttu-id="39d7a-120">Apertura de una aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="39d7a-120">Open a sample app</span></span>

<span data-ttu-id="39d7a-121">Vaya a su carpeta del repositorio `iot-hub-c-intel-nuc-gateway-getting-started`, inicialice los archivos de configuración y, después, abra el proyecto de ejemplo en Visual Studio Code ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="39d7a-121">Go to your `iot-hub-c-intel-nuc-gateway-getting-started` repo folder, initialize the configuration files, and then open the sample project in Visual Studio Code by running the following command:</span></span>

```bash
cd Lesson4
npm install
gulp init
code .
```

![estructura del repositorio](media/iot-hub-gateway-kit-lessons/lesson4/arm_template.png)

- <span data-ttu-id="39d7a-123">El archivo `arm-template.json` es una plantilla de Azure Resource Manager que contiene una instancia de Azure Function App y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="39d7a-123">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
- <span data-ttu-id="39d7a-124">El archivo `arm-template-param.json` es el archivo de configuración que utiliza la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39d7a-124">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
- <span data-ttu-id="39d7a-125">La subcarpeta `ReceiveDeviceMessages` contiene el código de Node.js para la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="39d7a-125">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="39d7a-126">Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="39d7a-126">Configure Azure Resource Manager templates and create resources in Azure</span></span>

<span data-ttu-id="39d7a-127">Actualice el archivo `arm-template-param.json` en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="39d7a-127">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![arm template json](media/iot-hub-gateway-kit-lessons/lesson4/arm_template_param.png)

- <span data-ttu-id="39d7a-129">Sustituya `[your IoT Hub name]` por el valor `{my hub name}` que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="39d7a-129">Replace `[your IoT Hub name]` with `{my hub name}` that you specified in Lesson 2.</span></span>

<span data-ttu-id="39d7a-130">Después de actualizar el archivo `arm-template-param.json`, implemente los recursos en Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="39d7a-130">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-gateway
```

<span data-ttu-id="39d7a-131">Use `iot-gateway` como el valor de `{resource group name}` si no lo cambió en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="39d7a-131">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value in Lesson 2.</span></span>

## <a name="summary"></a><span data-ttu-id="39d7a-132">Resumen</span><span class="sxs-lookup"><span data-stu-id="39d7a-132">Summary</span></span>

<span data-ttu-id="39d7a-133">Ha creado una instancia de Azure Function App para procesar mensajes de IoT Hub, así como una cuenta de Azure Storage para almacenar estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="39d7a-133">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="39d7a-134">Ahora puede leer los mensajes que envía su puerta de enlace al IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="39d7a-134">You can now read messages that are sent by your gateway to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39d7a-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39d7a-135">Next steps</span></span>
<span data-ttu-id="39d7a-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md) (Lectura de los mensajes que se conservan en Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="39d7a-136">[Read messages persisted in Azure Storage](iot-hub-gateway-kit-c-sim-lesson4-read-table-storage.md).</span></span>
