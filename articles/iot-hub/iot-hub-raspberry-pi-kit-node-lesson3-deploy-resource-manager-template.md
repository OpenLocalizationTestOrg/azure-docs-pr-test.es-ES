---
title: "Conexión de Raspberry Pi (Node) a Azure IoT: Lección 3: Implementación de plantillas | Microsoft Docs"
description: La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: almacenar datos en la nube, datos almacenados en la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6c58de85-c5c4-4989-bb5e-08c45c549966
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 44901faea37a847a418e6d2b4097302cdb610495
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="629fa-104">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="629fa-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="629fa-105">[Azure Functions](../azure-functions/functions-overview.md) es una solución que permite ejecutar *funciones* (pequeños fragmentos de código) en la nube fácilmente.</span><span class="sxs-lookup"><span data-stu-id="629fa-105">[Azure Functions](../azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="629fa-106">Una aplicación de Azure Function hospeda la ejecución de sus funciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="629fa-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="629fa-107">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="629fa-107">What you will do</span></span>
<span data-ttu-id="629fa-108">Va a utilizar una plantilla de Azure Resource Manager para crear una instancia de Azure Function App y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="629fa-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="629fa-109">La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="629fa-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="629fa-110">Si tiene problemas, puede encontrar soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="629fa-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="629fa-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="629fa-111">What you will learn</span></span>
<span data-ttu-id="629fa-112">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="629fa-112">In this article, you will learn:</span></span>

* <span data-ttu-id="629fa-113">Cómo utilizar [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) para implementar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="629fa-113">How to use [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="629fa-114">Cómo utilizar una instancia de Azure Function App para procesar mensajes de IoT Hub y escribirlos en una tabla de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="629fa-114">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="629fa-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="629fa-115">What you need</span></span>
<span data-ttu-id="629fa-116">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="629fa-116">You must have successfully completed:</span></span>
* <span data-ttu-id="629fa-117">[Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md) (Introducción a Raspberry Pi 3)</span><span class="sxs-lookup"><span data-stu-id="629fa-117">[Get started with Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-get-started.md)</span></span>
* <span data-ttu-id="629fa-118">[Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md) (Creación de un centro de IoT de Azure)</span><span class="sxs-lookup"><span data-stu-id="629fa-118">[Create your Azure IoT hub](iot-hub-raspberry-pi-kit-node-get-started.md)</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="629fa-119">Apertura de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="629fa-119">Open the sample app</span></span>
<span data-ttu-id="629fa-120">Abra el proyecto de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="629fa-120">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estructura del repositorio](media/iot-hub-raspberry-pi-lessons/lesson3/repo_structure.png)

* <span data-ttu-id="629fa-122">El archivo `app.js` de la subcarpeta `app` es el archivo de origen de la clave.</span><span class="sxs-lookup"><span data-stu-id="629fa-122">The `app.js` file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="629fa-123">Este archivo de origen contiene el código para enviar un mensaje 20 veces en su instancia de IoT Hub y hacer parpadear el LED para cada mensaje que envía.</span><span class="sxs-lookup"><span data-stu-id="629fa-123">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="629fa-124">El archivo `arm-template.json` es una plantilla de Azure Resource Manager que contiene una instancia de Azure Function App y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="629fa-124">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="629fa-125">El archivo `arm-template-param.json` es el archivo de configuración que utiliza la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="629fa-125">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="629fa-126">La subcarpeta `ReceiveDeviceMessages` contiene el código de Node.js para la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="629fa-126">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="629fa-127">Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="629fa-127">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="629fa-128">Actualice el archivo `arm-template-param.json` en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="629fa-128">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parámetros de plantilla de Azure Resource Manager](media/iot-hub-raspberry-pi-lessons/lesson3/arm_para.png)

* <span data-ttu-id="629fa-130">Sustituya **[su nombre de centro IoT]** por **{mi nombre de centro}** que especificó cuando [creó el centro de IoT y registró Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="629fa-130">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>
* <span data-ttu-id="629fa-131">Reemplace **[prefix string for new resources]** por el prefijo que desee.</span><span class="sxs-lookup"><span data-stu-id="629fa-131">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="629fa-132">El prefijo garantiza que el nombre del recurso sea globalmente único para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="629fa-132">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="629fa-133">No utilice guiones ni números al comienzo del prefijo.</span><span class="sxs-lookup"><span data-stu-id="629fa-133">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="629fa-134">Después de actualizar el archivo `arm-template-param.json`, implemente los recursos en Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="629fa-134">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="629fa-135">Este proceso tarda aproximadamente cinco minutos en crear estos recursos.</span><span class="sxs-lookup"><span data-stu-id="629fa-135">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="629fa-136">Mientras espera a que se ejecute la creación de recursos, puede pasar al siguiente artículo.</span><span class="sxs-lookup"><span data-stu-id="629fa-136">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="629fa-137">Resumen</span><span class="sxs-lookup"><span data-stu-id="629fa-137">Summary</span></span>
<span data-ttu-id="629fa-138">Ha creado una instancia de Azure Function App para procesar mensajes de IoT Hub, así como una cuenta de Azure Storage para almacenar estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="629fa-138">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="629fa-139">Ahora puede implementar y ejecutar el ejemplo para enviar mensajes del dispositivo a la nube en Pi.</span><span class="sxs-lookup"><span data-stu-id="629fa-139">You can now deploy and run the sample to send device-to-cloud messages on Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="629fa-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="629fa-140">Next steps</span></span>
<span data-ttu-id="629fa-141">[Run a sample application to send device-to-cloud messages on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md) (Ejecución de una aplicación de ejemplo para enviar mensajes de dispositivo a nube en Raspberry Pi 3)</span><span class="sxs-lookup"><span data-stu-id="629fa-141">[Run a sample application to send device-to-cloud messages on Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson3-run-azure-blink.md)</span></span>

