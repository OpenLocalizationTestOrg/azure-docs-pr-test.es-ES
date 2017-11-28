---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 3: almacenamiento de tablas | Documentos de Microsoft"
description: Supervisar mensajes de dispositivo a la nube de hello tal y como se escriben tooyour almacenamiento de tabla de Azure.
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
ms.openlocfilehash: 307ce2bc595339790db7379cc011fe262c2b8734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-persisted-in-azure-storage"></a><span data-ttu-id="bfd58-104">Lectura de los mensajes que se conservan en Azure Storage</span><span class="sxs-lookup"><span data-stu-id="bfd58-104">Read messages persisted in Azure Storage</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="bfd58-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="bfd58-105">What you will do</span></span>
<span data-ttu-id="bfd58-106">Mensajes de dispositivo para la nube de saludo de monitor que se envían desde el centro de IoT de frambuesa Pi 3 tooyour como mensajes de saludo se escriben tooyour almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd58-106">Monitor hello device-to-cloud messages that are sent from Raspberry Pi 3 tooyour IoT hub as hello messages are written tooyour Azure Table storage.</span></span> <span data-ttu-id="bfd58-107">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="bfd58-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bfd58-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="bfd58-108">What you will learn</span></span>
<span data-ttu-id="bfd58-109">En este artículo, obtendrá información sobre cómo se guardan los mensajes de tooread de toouse Hola gulp tarea de mensaje de lectura en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd58-109">In this article, you will learn how toouse hello gulp read-message task tooread messages persisted in your Azure Table storage.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="bfd58-110">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="bfd58-110">What you need</span></span>
<span data-ttu-id="bfd58-111">Antes de iniciar este proceso, debe haber completado correctamente [ejecutar aplicación de ejemplo de Hola Azure parpadeo en frambuesa Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span><span class="sxs-lookup"><span data-stu-id="bfd58-111">Before starting this process, you must have successfully completed [Run hello Azure blink sample application on Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson3-run-azure-blink.md).</span></span>

## <a name="read-new-messages-from-your-storage-account"></a><span data-ttu-id="bfd58-112">Lectura de mensajes nuevos de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="bfd58-112">Read new messages from your storage account</span></span>
<span data-ttu-id="bfd58-113">En el artículo anterior de hello, ejecutó una aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="bfd58-113">In hello previous article, you ran a sample application on Pi.</span></span> <span data-ttu-id="bfd58-114">aplicación de ejemplo de Hola envía centro de IoT de Azure de tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="bfd58-114">hello sample application sent messages tooyour Azure IoT hub.</span></span> <span data-ttu-id="bfd58-115">mensajes de saludo enviados tooyour centro de IoT se almacenan en el almacenamiento de la tabla de Azure a través de la aplicación de Azure función hello.</span><span class="sxs-lookup"><span data-stu-id="bfd58-115">hello messages sent tooyour IoT hub are stored into your Azure Table storage via hello Azure function app.</span></span> <span data-ttu-id="bfd58-116">Debe tooread mensajes de Hola almacenamiento de Azure conexión cadena desde el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd58-116">You need hello Azure storage connection string tooread messages from your Azure Table storage.</span></span>

<span data-ttu-id="bfd58-117">mensajes de tooread almacenados en el almacenamiento de tabla de Azure, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bfd58-117">tooread messages stored in your Azure Table storage, follow these steps:</span></span>

1. <span data-ttu-id="bfd58-118">Obtener la cadena de conexión de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="bfd58-118">Get hello connection string by running hello following commands:</span></span>

   ```bash
   az storage account list -g iot-sample --query [].name
   az storage account show-connection-string -g iot-sample -n {storage name}
   ```

   <span data-ttu-id="bfd58-119">Hola primer comando recupera hello `storage name` que se usa en hello segunda comando tooget Hola cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="bfd58-119">hello first command retrieves hello `storage name` that is used in hello second command tooget hello connection string.</span></span> <span data-ttu-id="bfd58-120">Use `iot-sample` como valor de Hola de `{resource group name}` si no cambia el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd58-120">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
2. <span data-ttu-id="bfd58-121">Archivo de configuración abierto hello `config-raspberrypi.json` en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bfd58-121">Open hello configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
3. <span data-ttu-id="bfd58-122">Reemplace `[Azure storage connection string]` con la cadena de conexión de Hola que obtuvo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="bfd58-122">Replace `[Azure storage connection string]` with hello connection string you got in step 1.</span></span>
4. <span data-ttu-id="bfd58-123">Guardar hello `config-raspberrypi.json` archivo.</span><span class="sxs-lookup"><span data-stu-id="bfd58-123">Save hello `config-raspberrypi.json` file.</span></span>
5. <span data-ttu-id="bfd58-124">Enviar mensajes de nuevo y leer desde el almacenamiento de tabla de Azure ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="bfd58-124">Send messages again and read them from your Azure Table storage by running hello following command:</span></span>
   
   ```bash
   gulp run --read-storage
   ```
   
   <span data-ttu-id="bfd58-125">Hello lógica para leer del almacenamiento de tabla de Azure está en hello `azure-table.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="bfd58-125">hello logic for reading from Azure Table storage is in hello `azure-table.js` file.</span></span>
   
   ![Ejecución de Gulp: almacenamiento de lectura](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_read_message_c.png)

## <a name="summary"></a><span data-ttu-id="bfd58-127">Resumen</span><span class="sxs-lookup"><span data-stu-id="bfd58-127">Summary</span></span>
<span data-ttu-id="bfd58-128">Ha conectado el centro de IoT tooyour Pi en la nube de hello correctamente y usa mensajes de Hola parpadeo ejemplo aplicación toosend dispositivo a la nube.</span><span class="sxs-lookup"><span data-stu-id="bfd58-128">You've successfully connected Pi tooyour IoT hub in hello cloud and used hello blink sample application toosend device-to-cloud messages.</span></span> <span data-ttu-id="bfd58-129">También utiliza hello Azure función aplicación toostore entrantes IoT hub mensajes tooyour almacenamiento tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd58-129">You also used hello Azure function app toostore incoming IoT hub messages tooyour Azure Table storage.</span></span> <span data-ttu-id="bfd58-130">Ahora puede enviar mensajes de la nube al dispositivo desde la tooPi del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="bfd58-130">You can now send cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfd58-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfd58-131">Next steps</span></span>
[<span data-ttu-id="bfd58-132">Ejecutar un tooreceive de la aplicación de ejemplo en la nube al dispositivo mensajes</span><span class="sxs-lookup"><span data-stu-id="bfd58-132">Run a sample application tooreceive cloud-to-device messages</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md)

