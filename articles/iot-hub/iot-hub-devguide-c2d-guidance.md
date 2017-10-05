---
title: Opciones de nube a dispositivo de IoT Hub de Azure | Microsoft Docs
description: "Guía del desarrollador: una guía sobre cuándo usar métodos directos, propiedades notificadas del dispositivo gemelo o mensajes de nube a dispositivo para comunicaciones de este mismo tipo."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: e6cd4880c9bfcc670bd116d3dd8e5245d70f85cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-to-device-communications-guidance"></a><span data-ttu-id="bbd1d-103">Guía de comunicación de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="bbd1d-103">Cloud-to-device communications guidance</span></span>
<span data-ttu-id="bbd1d-104">IoT Hub proporciona tres opciones para aplicaciones de dispositivo que exponen funcionalidades a una aplicación de back-end:</span><span class="sxs-lookup"><span data-stu-id="bbd1d-104">IoT Hub provides three options for device apps to expose functionality to a back-end app:</span></span>

* <span data-ttu-id="bbd1d-105">[Métodos directos][lnk-methods], para las comunicaciones que requieren confirmación inmediata del resultado.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-105">[Direct methods][lnk-methods] for communications that require immediate confirmation of the result.</span></span> <span data-ttu-id="bbd1d-106">Los métodos directos se utilizan frecuentemente para el control interactivo de dispositivos, como la activación de un ventilador.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-106">Direct methods are often used for interactive control of devices such as turning on a fan.</span></span>
* <span data-ttu-id="bbd1d-107">[Propiedades deseadas del dispositivo gemelo][lnk-twins], para comandos de ejecución prolongada destinados a poner el dispositivo en un determinado estado deseado.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-107">[Twin's desired properties][lnk-twins] for long-running commands intended to put the device into a certain desired state.</span></span> <span data-ttu-id="bbd1d-108">Por ejemplo, establecer el intervalo de envío de telemetría en 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-108">For example, set the telemetry send interval to 30 minutes.</span></span>
* <span data-ttu-id="bbd1d-109">[Mensajes de nube a dispositivo][lnk-c2d], para notificaciones unidireccionales a la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-109">[Cloud-to-device messages][lnk-c2d] for one-way notifications to the device app.</span></span>

<span data-ttu-id="bbd1d-110">Esta es una comparación detallada de las distintas opciones de comunicación de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-110">Here is a detailed comparison of the various cloud-to-device communication options.</span></span>

|  | <span data-ttu-id="bbd1d-111">Métodos directos</span><span class="sxs-lookup"><span data-stu-id="bbd1d-111">Direct methods</span></span> | <span data-ttu-id="bbd1d-112">Propiedades deseadas del dispositivo gemelo</span><span class="sxs-lookup"><span data-stu-id="bbd1d-112">Twin's desired properties</span></span> | <span data-ttu-id="bbd1d-113">Mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="bbd1d-113">Cloud-to-device messages</span></span> |
| ---- | ------- | ---------- | ---- |
| <span data-ttu-id="bbd1d-114">Escenario</span><span class="sxs-lookup"><span data-stu-id="bbd1d-114">Scenario</span></span> | <span data-ttu-id="bbd1d-115">Comandos que necesitan confirmación inmediata, por ejemplo, encender un ventilador.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-115">Commands that require immediate confirmation, such as turning on a fan.</span></span> | <span data-ttu-id="bbd1d-116">Comandos de ejecución prolongada destinados a poner el dispositivo en un determinado estado deseado.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-116">Long-running commands intended to put the device into a certain desired state.</span></span> <span data-ttu-id="bbd1d-117">Por ejemplo, establecer el intervalo de envío de telemetría en 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-117">For example, set the telemetry send interval to 30 minutes.</span></span> | <span data-ttu-id="bbd1d-118">Notificaciones unidireccionales a la aplicación de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-118">One-way notifications to the device app.</span></span> |
| <span data-ttu-id="bbd1d-119">flujo de datos</span><span class="sxs-lookup"><span data-stu-id="bbd1d-119">Data flow</span></span> | <span data-ttu-id="bbd1d-120">Bidireccional.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-120">Two-way.</span></span> <span data-ttu-id="bbd1d-121">La aplicación de dispositivo puede responder al método inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-121">The device app can respond to the method right away.</span></span> <span data-ttu-id="bbd1d-122">El back-end de solución recibe el resultado contextualmente a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-122">The solution back end receives the outcome contextually to the request.</span></span> | <span data-ttu-id="bbd1d-123">Unidireccional.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-123">One-way.</span></span> <span data-ttu-id="bbd1d-124">La aplicación de dispositivo recibe una notificación con el cambio de propiedad.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-124">The device app receives a notification with the property change.</span></span> | <span data-ttu-id="bbd1d-125">Unidireccional.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-125">One-way.</span></span> <span data-ttu-id="bbd1d-126">La aplicación de dispositivo recibe el mensaje.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-126">The device app receives the message</span></span>
| <span data-ttu-id="bbd1d-127">Durabilidad.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-127">Durability</span></span> | <span data-ttu-id="bbd1d-128">No se establece contacto con los dispositivos desconectados.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-128">Disconnected devices are not contacted.</span></span> <span data-ttu-id="bbd1d-129">Se notifica al back-end de la solución que el dispositivo no está conectado.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-129">The solution back end is notified that the device is not connected.</span></span> | <span data-ttu-id="bbd1d-130">Se conservan los valores de propiedad en el dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-130">Property values are preserved in the device twin.</span></span> <span data-ttu-id="bbd1d-131">El dispositivo los leerá en la siguiente reconexión.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-131">Device will read it at next reconnection.</span></span> <span data-ttu-id="bbd1d-132">Los valores de propiedad son recuperables con el [lenguaje de consulta de IoT Hub][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="bbd1d-132">Property values are retrievable with the [IoT Hub query language][lnk-query].</span></span> | <span data-ttu-id="bbd1d-133">IoT Hub puede conservar los mensajes durante 48 horas como máximo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-133">Messages can be retained by IoT Hub for up to 48 hours.</span></span> |
| <span data-ttu-id="bbd1d-134">Destinos</span><span class="sxs-lookup"><span data-stu-id="bbd1d-134">Targets</span></span> | <span data-ttu-id="bbd1d-135">Un único dispositivo que usa **deviceId**, o varios dispositivos que usan [trabajos][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="bbd1d-135">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="bbd1d-136">Un único dispositivo que usa **deviceId**, o varios dispositivos que usan [trabajos][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="bbd1d-136">Single device using **deviceId**, or multiple devices using [jobs][lnk-jobs].</span></span> | <span data-ttu-id="bbd1d-137">Dispositivo único por **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-137">Single device by **deviceId**.</span></span> |
| <span data-ttu-id="bbd1d-138">Tamaño</span><span class="sxs-lookup"><span data-stu-id="bbd1d-138">Size</span></span> | <span data-ttu-id="bbd1d-139">Hasta 8 KB de solicitudes y 8 KB de respuestas.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-139">Up to 8KB requests and 8KB responses.</span></span> | <span data-ttu-id="bbd1d-140">El tamaño máximo de propiedades deseadas es 8 KB.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-140">Maximum desired properties size is 8KB.</span></span> | <span data-ttu-id="bbd1d-141">Mensajes de hasta 64 kB.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-141">Up to 64KB messages.</span></span> |
| <span data-ttu-id="bbd1d-142">Frecuencia</span><span class="sxs-lookup"><span data-stu-id="bbd1d-142">Frequency</span></span> | <span data-ttu-id="bbd1d-143">Alta.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-143">High.</span></span> <span data-ttu-id="bbd1d-144">Para más información, consulte los [Límites de IoT Hub][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="bbd1d-144">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="bbd1d-145">Mediana.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-145">Medium.</span></span> <span data-ttu-id="bbd1d-146">Para más información, consulte los [Límites de IoT Hub][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="bbd1d-146">For more information, see [IoT Hub limits][lnk-quotas].</span></span> | <span data-ttu-id="bbd1d-147">Baja.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-147">Low.</span></span> <span data-ttu-id="bbd1d-148">Para más información, consulte los [Límites de IoT Hub][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="bbd1d-148">For more information, see [IoT Hub limits][lnk-quotas].</span></span> |
| <span data-ttu-id="bbd1d-149">Protocol</span><span class="sxs-lookup"><span data-stu-id="bbd1d-149">Protocol</span></span> | <span data-ttu-id="bbd1d-150">Actualmente solo está disponible cuando se usa MQTT.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-150">Currently available only when using MQTT.</span></span> | <span data-ttu-id="bbd1d-151">Actualmente solo está disponible cuando se usa MQTT.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-151">Currently available only when using MQTT.</span></span> | <span data-ttu-id="bbd1d-152">Disponible en todos los protocolos.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-152">Available on all protocols.</span></span> <span data-ttu-id="bbd1d-153">El dispositivo debe sondear al utilizar HTTP.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-153">Device must poll when using HTTP.</span></span> |

<span data-ttu-id="bbd1d-154">Aprenda a usar métodos directos, propiedades deseadas y mensajes de nube a dispositivo en los siguientes tutoriales:</span><span class="sxs-lookup"><span data-stu-id="bbd1d-154">Learn how to use direct methods, desired properties, and cloud-to-device messages in the following tutorials:</span></span>

* <span data-ttu-id="bbd1d-155">[Uso de métodos directos][lnk-methods-tutorial], para métodos directos.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-155">[Use direct methods][lnk-methods-tutorial], for direct methods;</span></span>
* <span data-ttu-id="bbd1d-156">[Uso de propiedades deseadas para configurar dispositivos][lnk-twin-properties], para propiedades deseadas del dispositivo gemelo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-156">[Use desired properties to configure devices][lnk-twin-properties], for device twin's desired properties;</span></span> 
* <span data-ttu-id="bbd1d-157">[Envío de mensajes de nube a dispositivo][lnk-c2d-tutorial], para mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bbd1d-157">[Send cloud-to-device messages][lnk-c2d-tutorial], for cloud-to-device messages.</span></span>

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md