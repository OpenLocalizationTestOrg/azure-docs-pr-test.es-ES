---
title: "dispositivo de nube de Azure IoT Hub aaaManage mensajería con el centro de IOT explorador | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola mensajes toocloud (D2C) de dispositivo de toomonitor de herramienta de explorador el centro de IOT CLI y enviar mensajes de toodevice (C2D) de nube en el centro de IoT de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "el centro de IOT explorador, mensajería, de nube dispositivo toodevice de nube del centro de iot, toodevice de mensajería en la nube"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="49f77-104">Usar el centro de IOT explorador toosend y recibir mensajes entre el dispositivo y el centro de IoT</span><span class="sxs-lookup"><span data-stu-id="49f77-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="49f77-106">[iothub-explorer](https://github.com/azure/iothub-explorer) tiene una serie de comandos que facilitan la administración de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="49f77-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="49f77-107">Este tutorial se centra en cómo toouse el centro de IOT explorador toosend y recibir mensajes entre el dispositivo y el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="49f77-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="49f77-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="49f77-108">What you will learn</span></span>

<span data-ttu-id="49f77-109">Aprenderá cómo toouse mensajes de dispositivo para la nube de explorador el centro de IOT toomonitor y toosend en la nube al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="49f77-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="49f77-110">Mensajes del dispositivo a la nube pudieron ser datos de sensor que el dispositivo se recopila y, a continuación, envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="49f77-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="49f77-111">Mensajes de la nube al dispositivo pudieron ser comandos que el centro de IoT envía tooyour dispositivo tooblink un LED que está conectado tooyour dispositivo.</span><span class="sxs-lookup"><span data-stu-id="49f77-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="49f77-112">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="49f77-112">What you will do</span></span>

- <span data-ttu-id="49f77-113">Utilizar el centro de IOT explorador toomonitor dispositivo a la nube mensajes.</span><span class="sxs-lookup"><span data-stu-id="49f77-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="49f77-114">Utilizar el centro de IOT explorador toosend en la nube al dispositivo mensajes.</span><span class="sxs-lookup"><span data-stu-id="49f77-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="49f77-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="49f77-115">What you need</span></span>

- <span data-ttu-id="49f77-116">Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="49f77-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="49f77-117">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="49f77-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="49f77-118">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="49f77-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="49f77-119">Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="49f77-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="49f77-120">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="49f77-120">iothub-explorer.</span></span> <span data-ttu-id="49f77-121">([instalación de iothub-explorer](https://github.com/azure/iothub-explorer)).</span><span class="sxs-lookup"><span data-stu-id="49f77-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="49f77-122">Supervisión de mensajes de dispositivo a nube</span><span class="sxs-lookup"><span data-stu-id="49f77-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="49f77-123">toomonitor mensajes que se envían desde el centro de IoT tooyour de dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="49f77-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="49f77-124">Abra una ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="49f77-124">Open a console window.</span></span>
1. <span data-ttu-id="49f77-125">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="49f77-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="49f77-126">Obtenga `<device-id>` y `<IoTHubConnectionString>` desde el IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="49f77-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="49f77-127">Asegúrese de que haya terminado de tutorial anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="49f77-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="49f77-128">O bien puede intentar toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` si tienes `HostName`, `SharedAccessKeyName` y `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="49f77-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="49f77-129">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="49f77-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="49f77-130">toosend un mensaje desde su dispositivo tooyour del centro de IoT, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="49f77-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="49f77-131">Abra una ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="49f77-131">Open a console window.</span></span>
1. <span data-ttu-id="49f77-132">Iniciar una sesión en el centro de IoT ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="49f77-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="49f77-133">Enviar un dispositivo de tooyour de mensaje mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="49f77-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="49f77-134">comando Hello parpadea Hola LED que está conectado tooyour dispositivo y envía el dispositivo de tooyour de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="49f77-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="49f77-135">No es necesario para hello dispositivo toosend un centro de IoT de confirmación independiente comando tooyour atrás tras la recepción de mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="49f77-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49f77-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49f77-136">Next steps</span></span>

<span data-ttu-id="49f77-137">Ahora sabe cómo toomonitor dispositivo a la nube mensajes y enviar mensajes en la nube al dispositivo entre los dispositivos de IoT y el centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="49f77-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
