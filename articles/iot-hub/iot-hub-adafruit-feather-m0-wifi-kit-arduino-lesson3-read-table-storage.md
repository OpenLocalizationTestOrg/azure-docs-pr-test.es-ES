---
title: "Conexión de Arduino (C) a Azure IoT: Lección 3: Table Storage | Microsoft Docs"
description: Supervise los mensajes del dispositivo a la nube a medida que se escriben en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube, recopilación de datos en la nube, servicio en la nube de IoT, datos de IoT"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 386083e0-0dbb-48c0-9ac2-4f8fb4590772
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 29fb97f5cf0669acb9e68d8a829294ee64c9cf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="15b79-104">Lectura de los mensajes que se conservan en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="15b79-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="15b79-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="15b79-105">What you will do</span></span>
<span data-ttu-id="15b79-106">Supervise los mensajes de dispositivo a nube que se envían desde la placa Adafruit Feather M0 WiFi Arduino a IoT Hub a medida que se escriben en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="15b79-106">Monitor the device-to-cloud messages that are sent from your Adafruit Feather M0 WiFi Arduino board to your IoT hub as the messages are written to your Azure Table storage.</span></span>

<span data-ttu-id="15b79-107">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="15b79-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="15b79-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="15b79-108">What you will learn</span></span>
<span data-ttu-id="15b79-109">En este artículo, aprenderá a utilizar la tarea read-message de Gulp para leer los mensajes guardados en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="15b79-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="15b79-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="15b79-110">What you need</span></span>
<span data-ttu-id="15b79-111">Antes de comenzar este procedimiento, debe de haber completado correctamente el tutorial sobre la [ejecución de una aplicación de ejemplo de Azure para activar el parpadeo en la placa de Arduino][run-blink-application].</span><span class="sxs-lookup"><span data-stu-id="15b79-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on your Arduino board][run-blink-application].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="15b79-112">Lectura de mensajes nuevos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="15b79-112">Read new messages from your storage account</span></span>
<span data-ttu-id="15b79-113">En el artículo anterior, ejecutó una aplicación de ejemplo en la placa de Arduino.</span><span class="sxs-lookup"><span data-stu-id="15b79-113">In the previous article, you ran a sample application on your Arduino board.</span></span> <span data-ttu-id="15b79-114">La aplicación de ejemplo envío mensajes a IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="15b79-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="15b79-115">Los mensajes enviados a IoT Hub se almacenan en Azure Table Storage a través de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="15b79-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="15b79-116">Para poder leer los mensajes de Azure Table Storage, necesita la cadena de conexión de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="15b79-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="15b79-117">Para leer los mensajes almacenados en Azure Table Storage, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="15b79-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="15b79-118">Obtenga la cadena de conexión ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="15b79-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="15b79-119">El primer comando recupera el elemento `storage name` que se utiliza en el segundo comando para obtener la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="15b79-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="15b79-120">Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="15b79-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="15b79-121">Abra el archivo de configuración `config-arduino.json` en Visual Studio Code con este comando:</span><span class="sxs-lookup"><span data-stu-id="15b79-121">Open the configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```
3. <span data-ttu-id="15b79-122">Reemplace `[Azure storage connection string]` por la cadena de conexión que obtuvo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="15b79-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="15b79-123">Guarde el archivo `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="15b79-123">Save the `config-arduino.json` file.</span></span>
5. <span data-ttu-id="15b79-124">Vuelva a enviar los mensajes y léalos en Azure Table Storage mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="15b79-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage

   # You can monitor the serial port by running listen task:
   gulp listen

   # Or you can combine above two gulp tasks into one:
   gulp run --read-storage --listen
   ```

   <span data-ttu-id="15b79-125">La lógica para leer mensajes de Azure Table Storage se encuentra en el archivo `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="15b79-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![Ejecución de Gulp: almacenamiento de lectura][gulp-run]

## <a name="summary"></a><span data-ttu-id="15b79-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="15b79-127">Summary</span></span>
<span data-ttu-id="15b79-128">Ha conectado la placa de Arduino a IoT Hub en la nube y utilizado la aplicación de ejemplo de intermitencia correctamente para enviar mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="15b79-128">You've successfully connected your Arduino board to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="15b79-129">También ha utilizado Azure Function App para almacenar los mensajes entrantes de IoT Hub en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="15b79-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="15b79-130">Ahora, puede enviar a la placa de Arduino mensajes de dispositivo a nube desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="15b79-130">You can now send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15b79-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="15b79-131">Next steps</span></span>
<span data-ttu-id="15b79-132">[Envío de mensajes de nube a dispositivo][send-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="15b79-132">[Send cloud-to-device messages][send-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[run-blink-application]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-run-azure-blink.md
[gulp-run]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_read_message_arduino.png
[send-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md