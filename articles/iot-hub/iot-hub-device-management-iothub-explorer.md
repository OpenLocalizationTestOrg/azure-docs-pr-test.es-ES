---
title: "aaaAzure administración de dispositivos de IoT con el centro de IOT explorador | Documentos de Microsoft"
description: "Usar Hola el centro de IOT-Explorador de CLI para la administración de dispositivos del centro de IoT de Azure, que ofrece métodos directos de Hola y opciones de administración de propiedades deseadas de hello gemelas."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "administración de dispositivos de azure iot, administración de dispositivos de azure iot hub, iot de administración de dispositivos, administración de dispositivos de iot hub"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="b715c-104">Uso de iothub-explorer para la administración de dispositivos de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b715c-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="b715c-106">[el centro de IOT explorador](https://github.com/azure/iothub-explorer) es una herramienta CLI que se ejecute en un identidades de dispositivos de toomanage de equipo de host en el registro de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b715c-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="b715c-107">Se trata con opciones de administración que se puede usar tooperform de varias tareas.</span><span class="sxs-lookup"><span data-stu-id="b715c-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="b715c-108">Opción de administración</span><span class="sxs-lookup"><span data-stu-id="b715c-108">Management option</span></span>          | <span data-ttu-id="b715c-109">Tarea</span><span class="sxs-lookup"><span data-stu-id="b715c-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b715c-110">Métodos directos</span><span class="sxs-lookup"><span data-stu-id="b715c-110">Direct methods</span></span>             | <span data-ttu-id="b715c-111">Hacer que un dispositivo actúan como iniciar o detener el envío de mensajes o reiniciar el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b715c-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="b715c-112">Propiedades deseadas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-112">Twin desired properties</span></span>    | <span data-ttu-id="b715c-113">Poner un dispositivo en determinados Estados, por ejemplo, configurar un toogreen LED o configuración de telemetría de hello interval too30 minutos de envío.</span><span class="sxs-lookup"><span data-stu-id="b715c-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="b715c-114">Propiedades notificadas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-114">Twin reported properties</span></span>   | <span data-ttu-id="b715c-115">Obtener Hola notifica el estado de un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b715c-115">Get hello reported state of a device.</span></span> <span data-ttu-id="b715c-116">Por ejemplo, el dispositivo de Hola informa Hola que LED parpadea ahora.</span><span class="sxs-lookup"><span data-stu-id="b715c-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="b715c-117">Etiquetas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-117">Twin tags</span></span>                  | <span data-ttu-id="b715c-118">Almacenar metadatos específicos del dispositivo en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="b715c-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="b715c-119">Por ejemplo, hello ubicación de implementación de una máquina expendedora.</span><span class="sxs-lookup"><span data-stu-id="b715c-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="b715c-120">Mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="b715c-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="b715c-121">Enviar dispositivo tooa de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="b715c-121">Send notifications tooa device.</span></span> <span data-ttu-id="b715c-122">Por ejemplo, "es muy probable que toorain hoy en día.</span><span class="sxs-lookup"><span data-stu-id="b715c-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="b715c-123">No olvide toobring paraguas."</span><span class="sxs-lookup"><span data-stu-id="b715c-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="b715c-124">Consultas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-124">Device twin queries</span></span>        | <span data-ttu-id="b715c-125">Consultar todos los dispositivos: los gemelos tooretrieve las condiciones arbitrario, como identificar los dispositivos de Hola que están disponibles para su uso.</span><span class="sxs-lookup"><span data-stu-id="b715c-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="b715c-126">Para obtener más explicación acerca de las diferencias de hello e instrucciones sobre el uso de estas opciones, consulte [Guía de comunicación de dispositivos a la nube](iot-hub-devguide-d2c-guidance.md) y [orientación para la comunicación en la nube para dispositivos](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="b715c-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b715c-127">Los dispositivos gemelos son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones).</span><span class="sxs-lookup"><span data-stu-id="b715c-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="b715c-128">Centro de IoT conserva a un gemelas de dispositivo para cada dispositivo que se conecta tooit.</span><span class="sxs-lookup"><span data-stu-id="b715c-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="b715c-129">Para más información acerca de los dispositivos gemelos, consulte [Introducción a los dispositivos gemelos](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="b715c-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b715c-130">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="b715c-130">What you learn</span></span>

<span data-ttu-id="b715c-131">Aprenderá a usar iothub-explorer con distintas opciones de administración en su máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b715c-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b715c-132">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="b715c-132">What you do</span></span>

<span data-ttu-id="b715c-133">Ejecute iothub-explorer con distintas opciones de administración.</span><span class="sxs-lookup"><span data-stu-id="b715c-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b715c-134">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="b715c-134">What you need</span></span>

- <span data-ttu-id="b715c-135">Tutorial [configurar su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde abordan las Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="b715c-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="b715c-136">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b715c-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="b715c-137">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="b715c-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b715c-138">Una aplicación de cliente que envía el centro de IoT de Azure de tooyour de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b715c-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="b715c-139">Asegúrese de que el dispositivo se está ejecutando con la aplicación de cliente de Hola durante este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b715c-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="b715c-140">iothub-explorer, [instale iothub-explorer](https://github.com/azure/iothub-explorer) en la máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="b715c-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="b715c-141">Conectar el centro de IoT tooyour</span><span class="sxs-lookup"><span data-stu-id="b715c-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="b715c-142">Conecte el centro de IoT tooyour mediante la ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="b715c-143">Uso de iothub-explorer con métodos directos</span><span class="sxs-lookup"><span data-stu-id="b715c-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="b715c-144">Invocar hello `start` método en el centro de IoT de hello dispositivo aplicación toosend mensajes tooyour ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="b715c-145">Invocar hello `stop` método hello dispositivo aplicación toostop enviando mensajes centro de IoT tooyour ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="b715c-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="b715c-146">Use iothub-explorer con las propiedades deseadas de los dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="b715c-147">Establecer un intervalo de la propiedad deseada = 3000 ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="b715c-148">El dispositivo puede leer esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="b715c-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="b715c-149">Use iothub-explorer con las propiedades notificadas de los dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="b715c-150">Obtengan hello notificadas propiedades de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="b715c-151">Una de las propiedades de hello es $metadata. $lastUpdated que muestra Hola última hora de este dispositivo envía o recibe un mensaje.</span><span class="sxs-lookup"><span data-stu-id="b715c-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="b715c-152">Uso de iothub-explorer con etiquetas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="b715c-153">Mostrar etiquetas de Hola y las propiedades de dispositivo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="b715c-154">Agregar un rol de campo = dispositivo de toohello de temperatura y humedad ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="b715c-155">Uso de iothub-explorer con mensajes de la nube al dispositivo</span><span class="sxs-lookup"><span data-stu-id="b715c-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="b715c-156">Enviar un dispositivo de toohello de mensaje "¡Hello World" mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="b715c-157">Vea [utilizar el centro de IOT explorador toosend y recibir mensajes entre el dispositivo y el centro de IoT](iot-hub-explorer-cloud-device-messaging.md) para un escenario real del uso de este comando.</span><span class="sxs-lookup"><span data-stu-id="b715c-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="b715c-158">Uso de iothub-explorer con consultas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="b715c-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="b715c-159">Consultar dispositivos con una etiqueta de rol = 'temperatura y humedad' ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="b715c-160">Consultar todos los dispositivos excepto los que tienen una etiqueta de rol = 'temperatura y humedad' ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b715c-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="b715c-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b715c-161">Next steps</span></span>

<span data-ttu-id="b715c-162">Ha aprendido cómo toouse el centro de IOT-explorador con distintas opciones de administración.</span><span class="sxs-lookup"><span data-stu-id="b715c-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
