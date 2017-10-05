---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 3: Table Storage | Microsoft Docs"
description: Supervise los mensajes del dispositivo a la nube a medida que se escriben en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: recuperar datos de la nube, servicio en la nube de iot
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 8c5558bb-3c31-4445-90e6-b1a978738545
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 16b7f2e38bfe3b40d199cb6e07976433aa54ea32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="ae7ed-104">Lectura de los mensajes que se conservan en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ae7ed-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="ae7ed-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="ae7ed-105">What you will do</span></span>
<span data-ttu-id="ae7ed-106">Va a supervisar los mensajes del dispositivo a la nube que se envían desde Raspberry Pi 3 a IoT Hub a medida que se escriben en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-106">Monitor the device-to-cloud messages that are sent from Raspberry Pi 3 to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="ae7ed-107">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ae7ed-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ae7ed-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="ae7ed-108">What you will learn</span></span>
<span data-ttu-id="ae7ed-109">En este artículo, aprenderá a utilizar la tarea read-message de Gulp para leer los mensajes guardados en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ae7ed-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="ae7ed-110">What you need</span></span>
<span data-ttu-id="ae7ed-111">Antes de comenzar este procedimiento, debe de haber completado correctamente el tutorial sobre la [ejecución de una aplicación de ejemplo de Azure para activar el parpadeo en Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="ae7ed-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="ae7ed-112">Lectura de mensajes nuevos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="ae7ed-112">Read new messages from your storage account</span></span>
<span data-ttu-id="ae7ed-113">En el artículo anterior, ejecutó una aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-113">In the previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="ae7ed-114">La aplicación de ejemplo envío mensajes a IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="ae7ed-115">Los mensajes enviados a IoT Hub se almacenan en Azure Table Storage a través de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="ae7ed-116">Para poder leer los mensajes de Azure Table Storage, necesita la cadena de conexión de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="ae7ed-117">Para leer los mensajes almacenados en Azure Table Storage, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ae7ed-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="ae7ed-118">Obtenga la cadena de conexión ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ae7ed-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="ae7ed-119">El primer comando recupera el elemento `storage name` que se utiliza en el segundo comando para obtener la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="ae7ed-120">Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="ae7ed-121">Abra el archivo de configuración `config-raspberrypi.json` en Visual Studio Code con este comando:</span><span class="sxs-lookup"><span data-stu-id="ae7ed-121">Open the configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="ae7ed-122">Reemplace `[Azure storage connection string]` por la cadena de conexión que obtuvo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="ae7ed-123">Guarde el archivo `config-raspberrypi.json`.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-123">Save the `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="ae7ed-124">Vuelva a enviar los mensajes y léalos en Azure Table Storage mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ae7ed-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="ae7ed-125">La lógica para leer mensajes de Azure Table Storage se encuentra en el archivo `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>
   
   ![Ejecución de Gulp: almacenamiento de lectura](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="ae7ed-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="ae7ed-127">Summary</span></span>
<span data-ttu-id="ae7ed-128">Ha conseguido conectar Pi a IoT Hub en la nube y utilizar la aplicación de ejemplo de activación del parpadeo para enviar mensajes del dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-128">You've successfully connected Pi to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="ae7ed-129">También ha utilizado Azure Function App para almacenar los mensajes entrantes de IoT Hub en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="ae7ed-130">Ahora, puede enviar a Pi mensajes del dispositivo a la nube desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ae7ed-130">You can now send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae7ed-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ae7ed-131">Next steps</span></span>
[<span data-ttu-id="ae7ed-132">Ejecución de una aplicación de ejemplo para recibir mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="ae7ed-132">Run a sample application to receive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

