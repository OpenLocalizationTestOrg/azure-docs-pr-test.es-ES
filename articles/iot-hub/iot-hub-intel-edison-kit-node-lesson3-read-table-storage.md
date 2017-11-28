---
title: "Conexión de Intel Edison (Node) a Azure IoT: Lección 3: Supervisión de mensajes | Microsoft Docs"
description: Supervise los mensajes del dispositivo a la nube a medida que se escriben en Azure Table Storage.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "datos en la nube, recopilación de datos en la nube, servicio en la nube de IoT, datos de IoT"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: fa2c7efe-7e34-4e39-bb70-015c15ac69ed
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c1a59227cd2bf9d2c9bcaa4212dd5127a95e2779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="09b76-104">Lectura de los mensajes que se conservan en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="09b76-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="09b76-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="09b76-105">What you will do</span></span>
<span data-ttu-id="09b76-106">Va a supervisar los mensajes de dispositivo a nube que se envían desde Intel Edison a IoT Hub a medida que se escriben en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="09b76-106">Monitor the device-to-cloud messages that are sent from Intel Edison to your IoT hub as the messages are written to your Azure Table storage.</span></span> <span data-ttu-id="09b76-107">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="09b76-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="09b76-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="09b76-108">What you will learn</span></span>
<span data-ttu-id="09b76-109">En este artículo, aprenderá a utilizar la tarea read-message de Gulp para leer los mensajes guardados en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="09b76-109">In this article, you will learn how to use the gulp read-message task to read messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="09b76-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="09b76-110">What you need</span></span>
<span data-ttu-id="09b76-111">Antes de comenzar este procedimiento, debe de haber completado correctamente el tutorial sobre la [ejecución de una aplicación de ejemplo de Azure para activar el parpadeo en Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span><span class="sxs-lookup"><span data-stu-id="09b76-111">Before starting this process, you must have successfully completed [Run the Azure blink sample application on Intel Edison][run-the-azure-blink-sample-application-on-intel-edison].</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="09b76-112">Lectura de mensajes nuevos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="09b76-112">Read new messages from your storage account</span></span>
<span data-ttu-id="09b76-113">En el artículo anterior, ejecutó una aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="09b76-113">In the previous article, you ran a sample application on Edison.</span></span> <span data-ttu-id="09b76-114">La aplicación de ejemplo envío mensajes a IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="09b76-114">The sample application sent messages to your Azure IoT hub.</span></span> <span data-ttu-id="09b76-115">Los mensajes enviados a IoT Hub se almacenan en Azure Table Storage a través de Azure Function App.</span><span class="sxs-lookup"><span data-stu-id="09b76-115">The messages sent to your IoT hub are stored into your Azure Table storage via the Azure function app.</span></span> <span data-ttu-id="09b76-116">Para poder leer los mensajes de Azure Table Storage, necesita la cadena de conexión de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="09b76-116">You need the Azure storage connection string to read messages from your Azure Table storage.</span></span>

<span data-ttu-id="09b76-117">Para leer los mensajes almacenados en Azure Table Storage, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="09b76-117">To read messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="09b76-118">Obtenga la cadena de conexión ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="09b76-118">Get the connection string by running the following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="09b76-119">El primer comando recupera el elemento `storage name` que se utiliza en el segundo comando para obtener la cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="09b76-119">The first command retrieves the `storage name` that is used in the second command to get the connection string.</span></span> <span data-ttu-id="09b76-120">Use `iot-sample` como valor de `{resource group name}`, si no lo modificó previamente.</span><span class="sxs-lookup"><span data-stu-id="09b76-120">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>
2. <span data-ttu-id="09b76-121">Abra el archivo de configuración `config-edison.json` en Visual Studio Code con este comando:</span><span class="sxs-lookup"><span data-stu-id="09b76-121">Open the configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```
3. <span data-ttu-id="09b76-122">Reemplace `[Azure storage connection string]` por la cadena de conexión que obtuvo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="09b76-122">Replace `[Azure storage connection string]` with the connection string you got in step 1.</span></span>
4. <span data-ttu-id="09b76-123">Guarde el archivo `config-edison.json`.</span><span class="sxs-lookup"><span data-stu-id="09b76-123">Save the `config-edison.json` file.</span></span>
5. <span data-ttu-id="09b76-124">Vuelva a enviar los mensajes y léalos en Azure Table Storage mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="09b76-124">Send messages again and read them from your Azure Table storage by running the following command:</span></span>

   ```bash
   gulp run --read-storage
   ```

   <span data-ttu-id="09b76-125">La lógica para leer mensajes de Azure Table Storage se encuentra en el archivo `azure-table.js`.</span><span class="sxs-lookup"><span data-stu-id="09b76-125">The logic for reading from Azure Table storage is in the `azure-table.js` file.</span></span>

   ![Ejecución de Gulp: almacenamiento de lectura][gulp run]

## <a name="summary"></a><span data-ttu-id="09b76-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="09b76-127">Summary</span></span>
<span data-ttu-id="09b76-128">Ha conseguido conectar Edison a IoT Hub en la nube y utilizar la aplicación de ejemplo de activación del parpadeo para enviar mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="09b76-128">You've successfully connected Edison to your IoT hub in the cloud and used the blink sample application to send device-to-cloud messages.</span></span> <span data-ttu-id="09b76-129">También ha utilizado Azure Function App para almacenar los mensajes entrantes de IoT Hub en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="09b76-129">You also used the Azure function app to store incoming IoT hub messages to your Azure Table storage.</span></span> <span data-ttu-id="09b76-130">Ahora, puede enviar a Edison mensajes de dispositivo a nube desde IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09b76-130">You can now send cloud-to-device messages from your IoT hub to Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09b76-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09b76-131">Next steps</span></span>
<span data-ttu-id="09b76-132">[Ejecución de la aplicación de ejemplo para recibir mensajes de nube a dispositivo][receive-cloud-to-device-messages]</span><span class="sxs-lookup"><span data-stu-id="09b76-132">[Run a sample application to receive cloud-to-device messages][receive-cloud-to-device-messages]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[run-the-azure-blink-sample-application-on-intel-edison]: iot-hub-intel-edison-kit-node-lesson3-run-azure-blink.md
[gulp run]: media/iot-hub-intel-edison-lessons/lesson3/gulp_read_message.png
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md