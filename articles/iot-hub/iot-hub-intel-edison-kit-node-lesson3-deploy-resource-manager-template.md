---
title: "Conectar Intel Edison (nodo) tooAzure IoT - lección 3: crear la aplicación de la función | Documentos de Microsoft"
description: "aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: almacenar datos en la nube de hello, los datos almacenados en la nube, el servicio de nube de iot
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
ms.openlocfilehash: 8ea0a4cdf978158d70e47eaed57e3de378b638d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-app-and-azure-storage-account"></a><span data-ttu-id="55362-104">Creación de una instancia de Azure Function App y una cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="55362-104">Create an Azure function app and Azure storage account</span></span>
<span data-ttu-id="55362-105">[Las funciones de Azure](../../articles/azure-functions/functions-overview.md) es una solución para ejecutar fácilmente *funciones* (pequeños fragmentos de código) en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="55362-105">[Azure Functions](../../articles/azure-functions/functions-overview.md) is a solution for easily running *functions* (small pieces of code) in hello cloud.</span></span> <span data-ttu-id="55362-106">Una aplicación de Azure función hospeda ejecución Hola de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="55362-106">An Azure function app hosts hello execution of your functions in Azure.</span></span>

## <a name="what-will-you-do"></a><span data-ttu-id="55362-107">Qué hará</span><span class="sxs-lookup"><span data-stu-id="55362-107">What will you do</span></span>
<span data-ttu-id="55362-108">Utilice un toocreate de plantilla de Azure Resource Manager una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="55362-108">Use an Azure Resource Manager template toocreate an Azure function app and an Azure storage account.</span></span> <span data-ttu-id="55362-109">aplicación de Azure función Hello escucha eventos de centro de IoT tooAzure, procesa los mensajes entrantes y los escribe tooAzure el almacenamiento de tabla.</span><span class="sxs-lookup"><span data-stu-id="55362-109">hello Azure function app listens tooAzure IoT hub events, processes incoming messages, and writes them tooAzure Table storage.</span></span> <span data-ttu-id="55362-110">cuenta de almacenamiento Hello se usa una para su lectura Hola conserva copias de los mensajes de la tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="55362-110">hello storage account is used for reading hello persisted copies of messages from Azure table.</span></span> <span data-ttu-id="55362-111">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="55362-111">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-will-you-learn"></a><span data-ttu-id="55362-112">Qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="55362-112">What will you learn</span></span>
<span data-ttu-id="55362-113">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="55362-113">In this article, you will learn:</span></span>
* <span data-ttu-id="55362-114">Cómo toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure recursos.</span><span class="sxs-lookup"><span data-stu-id="55362-114">How toouse [Azure Resource Manager](../../articles/azure-resource-manager/resource-group-overview.md) toodeploy Azure resources.</span></span>
* <span data-ttu-id="55362-115">¿Cómo toouse un Azure función tooprocess aplicación mensajes del centro de IoT y escribirlos tooa tabla en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="55362-115">How toouse an Azure function app tooprocess IoT hub messages and write them tooa table in Azure Table storage.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="55362-116">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="55362-116">What do you need</span></span>
<span data-ttu-id="55362-117">Debe haber completado correctamente los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="55362-117">You must have successfully completed:</span></span>
- <span data-ttu-id="55362-118">[Introducción a Intel Edison][get-started-with-your-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="55362-118">[Get started with your Intel Edison][get-started-with-your-intel-edison]</span></span>
- <span data-ttu-id="55362-119">[Create your Azure IoT hub][create-your-azure-iot-hub] (Creación de un Azure IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="55362-119">[Create your Azure IoT hub][create-your-azure-iot-hub]</span></span>

## <a name="open-hello-sample-app"></a><span data-ttu-id="55362-120">Aplicación de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="55362-120">Open hello sample app</span></span>
<span data-ttu-id="55362-121">Abra el proyecto de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="55362-121">Open hello sample project in Visual Studio Code by running hello following commands:</span></span>

```bash
cd Lesson3
code .
```

![Estructura del repositorio][repo-structure]

* <span data-ttu-id="55362-123">archivo de Hello en hello `app` subcarpeta es el archivo de origen de la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="55362-123">hello file in hello `app` subfolder is hello key source file.</span></span> <span data-ttu-id="55362-124">Este archivo de origen contiene código de hello toosend un mensaje 20 veces tooyour IoT hub- and blink Hola LED para cada mensaje que envía.</span><span class="sxs-lookup"><span data-stu-id="55362-124">This source file contains hello code toosend a message 20 times tooyour IoT hub and blink hello LED for each message it sends.</span></span>
* <span data-ttu-id="55362-125">Hola `arm-template.json` archivo es hello Azure Resource Manager plantilla que contiene una aplicación de Azure de función y una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="55362-125">hello `arm-template.json` file is hello Azure Resource Manager template that contains an Azure function app and an Azure storage account.</span></span>
* <span data-ttu-id="55362-126">Hola `arm-template-param.json` archivo es el archivo de configuración de hello utilizado por la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="55362-126">hello `arm-template-param.json` file is hello configuration file used by hello Azure Resource Manager template.</span></span>
* <span data-ttu-id="55362-127">Hola `ReceiveDeviceMessages` subcarpeta contiene código de Node.js de Hola para hello Azure función.</span><span class="sxs-lookup"><span data-stu-id="55362-127">hello `ReceiveDeviceMessages` subfolder contains hello Node.js code for hello Azure function.</span></span>

## <a name="configure-azure-resource-manager-templates-and-create-resources-in-azure"></a><span data-ttu-id="55362-128">Configuración de las plantillas de Azure Resource Manager y creación de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="55362-128">Configure Azure Resource Manager templates and create resources in Azure</span></span>
<span data-ttu-id="55362-129">Hola de actualización `arm-template-param.json` archivo de código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="55362-129">Update hello `arm-template-param.json` file in Visual Studio Code.</span></span>

![Parámetros de plantilla de Azure Resource Manager][arm-template-parameters]

* <span data-ttu-id="55362-131">Sustituya **[su nombre de centro de IoT Hub]** por **{mi nombre de centro}** que especificó cuando [creó el centro de IoT Hub y registró Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="55362-131">Replace **[your IoT Hub name]** with **{my hub name}** that you specified when you [created your IoT hub and registered Intel Edison][created-your-iot-hub-and-registered-intel-edison].</span></span>
* <span data-ttu-id="55362-132">Reemplace **[prefix string for new resources]** por el prefijo que desee.</span><span class="sxs-lookup"><span data-stu-id="55362-132">Replace **[prefix string for new resources]** with any prefix you want.</span></span> <span data-ttu-id="55362-133">prefijo de Hola garantiza que el nombre de recurso hello es globalmente único tooavoid conflicto.</span><span class="sxs-lookup"><span data-stu-id="55362-133">hello prefix ensures that hello resource name is globally unique tooavoid conflict.</span></span> <span data-ttu-id="55362-134">No use un guión o un número inicial de prefijo de Hola.</span><span class="sxs-lookup"><span data-stu-id="55362-134">Do not use a dash or number initial in hello prefix.</span></span>

<span data-ttu-id="55362-135">Después de actualizar hello `arm-template-param.json` de archivos, implementar Hola recursos tooAzure ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="55362-135">After you update hello `arm-template-param.json` file, deploy hello resources tooAzure by running hello following command:</span></span>

```bash
az group deployment create --template-file arm-template.json --parameters @arm-template-param.json -g iot-sample
```

<span data-ttu-id="55362-136">Tarda aproximadamente cinco minutos toocreate estos recursos.</span><span class="sxs-lookup"><span data-stu-id="55362-136">It takes about five minutes toocreate these resources.</span></span> <span data-ttu-id="55362-137">Mientras la creación de recursos de hello está en curso, puede mover en el artículo siguiente de toohello.</span><span class="sxs-lookup"><span data-stu-id="55362-137">While hello resource creation is in progress, you can move on toohello next article.</span></span>

## <a name="summary"></a><span data-ttu-id="55362-138">Resumen</span><span class="sxs-lookup"><span data-stu-id="55362-138">Summary</span></span>
<span data-ttu-id="55362-139">Ha creado su tooprocess de aplicación de Azure función mensajes de centro de IoT y el almacenamiento de Azure cuenta toostore estos mensajes.</span><span class="sxs-lookup"><span data-stu-id="55362-139">You've created your Azure function app tooprocess IoT hub messages and an Azure storage account toostore these messages.</span></span> <span data-ttu-id="55362-140">Ahora puede implementar y ejecutar mensajes de dispositivo a la nube de toosend de ejemplo de Hola en Edison.</span><span class="sxs-lookup"><span data-stu-id="55362-140">You can now deploy and run hello sample toosend device-to-cloud messages on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55362-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55362-141">Next steps</span></span>
<span data-ttu-id="55362-142">[Ejecutar un toosend de la aplicación de ejemplo mensajes del dispositivo a la nube en Intel Edison][send-device-to-cloud-messages].</span><span class="sxs-lookup"><span data-stu-id="55362-142">[Run a sample application toosend device-to-cloud messages on Intel Edison][send-device-to-cloud-messages].</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-started-with-your-intel-edison]: iot-hub-intel-edison-kit-node-get-started.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-get-started.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson3/repo_structure.png
[arm-template-parameters]: media/iot-hub-intel-edison-lessons/lesson3/arm_para.png
[created-your-iot-hub-and-registered-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[send-device-to-cloud-messages]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md