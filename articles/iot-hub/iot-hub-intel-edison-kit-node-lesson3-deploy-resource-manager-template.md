---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 3: Creación de Function App | Microsoft Docs"
description: La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube, datos almacenados en la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 37ee5962-95ce-40e8-8162-17e735eaec21
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 6ada1cbbb560f1373346eca561dceb28d7ca7242
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="79a69-104">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="79a69-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="79a69-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) es una solución que permite ejecutar *funciones* (pequeños fragmentos de código) en la nube fácilmente.</span><span class="sxs-lookup"><span data-stu-id="79a69-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in the cloud.</span></span> <span data-ttu-id="79a69-106">Una aplicación de Azure Function hospeda la ejecución de sus funciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="79a69-106">An Azure function app hosts the execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="79a69-107">Qué hará</span><span class="sxs-lookup"><span data-stu-id="79a69-107">What will you do</span></span>
<span data-ttu-id="79a69-108">Va a utilizar una plantilla de Azure Resource Manager para crear una instancia de Azure Function App y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="79a69-108">Use an Azure Resource Manager template to create an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="79a69-109">La instancia de Azure Function App escucha los eventos de Azure IoT Hub, procesa los mensajes entrantes y los escribe en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="79a69-109">The Azure function app listens to Azure IoT hub events, processes incoming messages, and writes them to Azure Table storage.</span></span> <span data-ttu-id="79a69-110">La cuenta de almacenamiento se usa para leer las copias conservadas de mensajes de la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="79a69-110">The storage account is used for reading the persisted copies of messages from Azure table.</span></span> <span data-ttu-id="79a69-111">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="79a69-111">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="79a69-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="79a69-112">What will you learn</span></span>
<span data-ttu-id="79a69-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79a69-113">In this article, you will learn:</span></span>
* <span data-ttu-id="79a69-114">Cómo utilizar [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) para implementar recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="79a69-114">How to use [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) to deploy Azure resources.</span></span>
* <span data-ttu-id="79a69-115">Cómo utilizar una instancia de Azure Function App para procesar mensajes de IoT Hub y escribirlos en una tabla de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="79a69-115">How to use an Azure function app to process IoT hub messages and write them to a table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="79a69-116">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="79a69-116">What do you need</span></span>
<span data-ttu-id="79a69-117">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="79a69-117">You must have successfully completed:</span></span>
- <span data-ttu-id="79a69-118">[Introducción a Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="79a69-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="79a69-119">[Creación de un centro de IoT Hub de Azure][create-your-azure-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="79a69-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-the-sample-app"></a><span data-ttu-id="79a69-120">Apertura de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="79a69-120">Open the sample app</span></span>
<span data-ttu-id="79a69-121">Abra el proyecto de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="79a69-121">Open the sample project in Visual Studio Code by running the following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estructura del repositorio][repo-structure]

* <span data-ttu-id="79a69-123">El archivo de la subcarpeta `app` es el archivo de origen de la clave.</span><span class="sxs-lookup"><span data-stu-id="79a69-123">The file in the `app` subfolder is the key source file.</span></span> <span data-ttu-id="79a69-124">Este archivo de origen contiene el código para enviar un mensaje 20 veces en su instancia de IoT Hub y hacer parpadear el LED para cada mensaje que envía.</span><span class="sxs-lookup"><span data-stu-id="79a69-124">This source file contains the code to send a message 20 times to your IoT hub and blink the LED for each message it sends.</span></span>
* <span data-ttu-id="79a69-125">El archivo `arm-template.json` es una plantilla de Azure Resource Manager que contiene una instancia de Azure Function App y una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="79a69-125">The `arm-template.json` file is the Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="79a69-126">El archivo `arm-template-param.json` es el archivo de configuración que utiliza la plantilla de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="79a69-126">The `arm-template-param.json` file is the configuration file used by the Azure Resource Manager template.</span></span>
* <span data-ttu-id="79a69-127">La subcarpeta `ReceiveDeviceMessages` contiene el código de Node.js para la función de Azure.</span><span class="sxs-lookup"><span data-stu-id="79a69-127">The `ReceiveDeviceMessages` subfolder contains the Node.js code for the Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="79a69-128">Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="79a69-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="79a69-129">Actualice el archivo `arm-template-param.json` en Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="79a69-129">Update the `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parámetros de plantilla de Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="79a69-131">Sustituya **[su nombre de centro de IoT Hub]** por **{mi nombre de centro}** que especificó cuando [creó el centro de IoT Hub y registró Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="79a69-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="79a69-132">Reemplace **[prefix string for new resources]** por el prefijo que desee.</span><span class="sxs-lookup"><span data-stu-id="79a69-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="79a69-133">El prefijo garantiza que el nombre del recurso sea globalmente único para evitar conflictos.</span><span class="sxs-lookup"><span data-stu-id="79a69-133">The prefix ensures that the resource name is globally unique to avoid conflict.</span></span> <span data-ttu-id="79a69-134">No utilice guiones ni números al comienzo del prefijo.</span><span class="sxs-lookup"><span data-stu-id="79a69-134">Do not use a dash or number initial in the prefix.</span></span>

<span data-ttu-id="79a69-135">Después de actualizar el archivo `arm-template-param.json`, implemente los recursos en Azure ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="79a69-135">After you update the `arm-template-param.json` file, deploy the resources to Azure by running the following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="79a69-136">Este proceso tarda aproximadamente cinco minutos en crear estos recursos.</span><span class="sxs-lookup"><span data-stu-id="79a69-136">It takes about five minutes to create these resources.</span></span> <span data-ttu-id="79a69-137">Mientras espera a que se ejecute la creación de recursos, puede pasar al siguiente artículo.</span><span class="sxs-lookup"><span data-stu-id="79a69-137">While the resource creation is in progress, you can move on to the next article.</span></span>

## <a name="summary"></a><span data-ttu-id="79a69-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="79a69-138">Summary</span></span>
<span data-ttu-id="79a69-139">Ha creado una instancia de Azure Function App para procesar mensajes de IoT Hub, así como una cuenta de Azure Storage para almacenar estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="79a69-139">You've created your Azure function app to process IoT hub messages and an Azure storage account to store these messages.</span></span> <span data-ttu-id="79a69-140">Ahora puede implementar y ejecutar el ejemplo para enviar mensajes de dispositivo a nube en Edison.</span><span class="sxs-lookup"><span data-stu-id="79a69-140">You can now deploy and run the sample to send device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79a69-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79a69-141">Next steps</span></span>
<span data-ttu-id="79a69-142">[Ejecución de una aplicación de ejemplo para enviar mensajes de dispositivo a nube en Intel Edison][send-device-to-cloud-messages]</span><span class="sxs-lookup"><span data-stu-id="79a69-142">[Run a sample application to send device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md