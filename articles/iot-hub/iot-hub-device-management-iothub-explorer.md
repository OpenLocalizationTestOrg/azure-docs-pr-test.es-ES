---
title: "Administración de dispositivos de Azure IoT con iothub-explorer | Microsoft Docs"
description: "Use la herramienta de la CLI iothub-explorer para la administración de dispositivos de Azure IoT Hub, herramienta que incluye métodos directos y opciones de administración de las propiedades deseadas de los dispositivos gemelos."
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
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="620f6-104">Uso de iothub-explorer para la administración de dispositivos de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="620f6-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagrama integral](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="620f6-106">[iothub-explorer](https://github.com/azure/iothub-explorer) es una herramienta de la CLI que se ejecuta en un equipo host para administrar identidades de dispositivo en el registro de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="620f6-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="620f6-107">Incluye opciones de administración que puede usar para realizar varias tareas.</span><span class="sxs-lookup"><span data-stu-id="620f6-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="620f6-108">Opción de administración</span><span class="sxs-lookup"><span data-stu-id="620f6-108">Management option</span></span>          | <span data-ttu-id="620f6-109">Tarea</span><span class="sxs-lookup"><span data-stu-id="620f6-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="620f6-110">Métodos directos</span><span class="sxs-lookup"><span data-stu-id="620f6-110">Direct methods</span></span>             | <span data-ttu-id="620f6-111">Hacer que un dispositivo actúe, por ejemplo, para iniciar o detener el envío de mensajes o reiniciar el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="620f6-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="620f6-112">Propiedades deseadas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-112">Twin desired properties</span></span>    | <span data-ttu-id="620f6-113">Poner un dispositivo en determinados estados, como establecer un indicador LED en verde o establecer el intervalo de envío de telemetría en 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="620f6-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="620f6-114">Propiedades notificadas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-114">Twin reported properties</span></span>   | <span data-ttu-id="620f6-115">Obtener el estado notificado de un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="620f6-115">Get the reported state of a device.</span></span> <span data-ttu-id="620f6-116">Por ejemplo, el dispositivo informa de que el LED está parpadeando.</span><span class="sxs-lookup"><span data-stu-id="620f6-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="620f6-117">Etiquetas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-117">Twin tags</span></span>                  | <span data-ttu-id="620f6-118">Almacenar metadatos específicos de dispositivo en la nube.</span><span class="sxs-lookup"><span data-stu-id="620f6-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="620f6-119">Por ejemplo, la ubicación de implementación de una máquina expendedora.</span><span class="sxs-lookup"><span data-stu-id="620f6-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="620f6-120">Mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="620f6-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="620f6-121">Enviar notificaciones a un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="620f6-121">Send notifications to a device.</span></span> <span data-ttu-id="620f6-122">Por ejemplo, "Es muy probable que llueva hoy.</span><span class="sxs-lookup"><span data-stu-id="620f6-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="620f6-123">No olvide traerse un paraguas".</span><span class="sxs-lookup"><span data-stu-id="620f6-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="620f6-124">Consultas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-124">Device twin queries</span></span>        | <span data-ttu-id="620f6-125">Consultar todos los dispositivos gemelos para recuperar aquellos con condiciones arbitrarias como, por ejemplo, identificar los dispositivos que están disponibles para su uso.</span><span class="sxs-lookup"><span data-stu-id="620f6-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="620f6-126">Para obtener una explicación más detallada acerca de las diferencias y orientación sobre el uso de estas opciones, consulte la [Guía de comunicación de dispositivo a nube](iot-hub-devguide-d2c-guidance.md) y la [Guía de comunicación de nube a dispositivo](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="620f6-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="620f6-127">Los dispositivos gemelos son documentos JSON que almacenan información sobre el estado de los dispositivos (metadatos, configuraciones y condiciones).</span><span class="sxs-lookup"><span data-stu-id="620f6-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="620f6-128">IoT Hub conserva un dispositivo gemelo por cada dispositivo que se conecta a él.</span><span class="sxs-lookup"><span data-stu-id="620f6-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="620f6-129">Para más información acerca de los dispositivos gemelos, consulte [Introducción a los dispositivos gemelos](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="620f6-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="620f6-130">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="620f6-130">What you learn</span></span>

<span data-ttu-id="620f6-131">Aprenderá a usar iothub-explorer con distintas opciones de administración en su máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="620f6-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="620f6-132">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="620f6-132">What you do</span></span>

<span data-ttu-id="620f6-133">Ejecute iothub-explorer con distintas opciones de administración.</span><span class="sxs-lookup"><span data-stu-id="620f6-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="620f6-134">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="620f6-134">What you need</span></span>

- <span data-ttu-id="620f6-135">Tutorial [Instalación de su dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) completado donde se abordan los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="620f6-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="620f6-136">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="620f6-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="620f6-137">Un centro de Azure IoT en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="620f6-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="620f6-138">Una aplicación cliente que envía mensajes a su centro de Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="620f6-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="620f6-139">Asegúrese de que el dispositivo se está ejecutando con la aplicación de cliente durante este tutorial.</span><span class="sxs-lookup"><span data-stu-id="620f6-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="620f6-140">iothub-explorer, [instale iothub-explorer](https://github.com/azure/iothub-explorer) en la máquina de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="620f6-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="620f6-141">Conexión a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="620f6-141">Connect to your IoT hub</span></span>

<span data-ttu-id="620f6-142">Conéctese a su instancia de IoT Hub mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="620f6-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="620f6-143">Uso de iothub-explorer con métodos directos</span><span class="sxs-lookup"><span data-stu-id="620f6-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="620f6-144">Invoque el método `start` en la aplicación de dispositivo para enviar mensajes a su instancia de IoT Hub mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="620f6-145">Invoque el método `stop` en la aplicación de dispositivo para dejar de enviar mensajes a su instancia de IoT Hub mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="620f6-146">Use iothub-explorer con las propiedades deseadas de los dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="620f6-147">Establezca un intervalo de propiedad deseada = 3000 mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="620f6-148">El dispositivo puede leer esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="620f6-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="620f6-149">Use iothub-explorer con las propiedades notificadas de los dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="620f6-150">Obtenga las propiedades notificadas del dispositivo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="620f6-151">Una de las propiedades es $metadata.$lastUpdated que muestra la última vez que este dispositivo envía o recibe un mensaje.</span><span class="sxs-lookup"><span data-stu-id="620f6-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="620f6-152">Uso de iothub-explorer con etiquetas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="620f6-153">Muestre las etiquetas y las propiedades del dispositivo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="620f6-154">Agregue un rol de campo = temperatura y humedad al dispositivo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="620f6-155">Uso de iothub-explorer con mensajes de la nube al dispositivo</span><span class="sxs-lookup"><span data-stu-id="620f6-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="620f6-156">Envíe un mensaje "Hello World" al dispositivo mediante la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="620f6-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="620f6-157">Consulte [Uso de iothub-explorer para enviar y recibir mensajes entre el dispositivo y la instancia de IoT Hub](iot-hub-explorer-cloud-device-messaging.md) para ver un escenario real de uso de este comando.</span><span class="sxs-lookup"><span data-stu-id="620f6-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="620f6-158">Uso de iothub-explorer con consultas de dispositivos gemelos</span><span class="sxs-lookup"><span data-stu-id="620f6-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="620f6-159">Consulte los dispositivos con una etiqueta de rol = "temperatura y humedad" mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="620f6-160">Consulte todos los dispositivos excepto aquellos con una etiqueta de rol = "temperatura y humedad" mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="620f6-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="620f6-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="620f6-161">Next steps</span></span>

<span data-ttu-id="620f6-162">Ha aprendido a usar iothub-explorer con distintas opciones de administración.</span><span class="sxs-lookup"><span data-stu-id="620f6-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
