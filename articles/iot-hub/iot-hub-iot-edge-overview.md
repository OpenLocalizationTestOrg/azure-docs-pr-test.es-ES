---
title: "Información general de Azure IoT Edge | Microsoft Docs"
description: "Describe los conceptos clave de la arquitectura de Azure IoT Edge, como puertas de enlace, módulos y agentes."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="11596-103">Conceptos de arquitectura de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="11596-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="11596-104">Antes de examinar el código de ejemplo o de crear su propia puerta de enlace de campo mediante IoT Edge, debe comprender los conceptos clave que subyacen a la arquitectura de IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="11596-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="11596-105">Módulos de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="11596-105">IoT Edge modules</span></span>

<span data-ttu-id="11596-106">Una puerta de enlace se crea con Azure IoT Edge mediante la creación y el ensamblado de *módulos de IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="11596-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="11596-107">Los módulos utilizan *mensajes* para intercambiarse datos.</span><span class="sxs-lookup"><span data-stu-id="11596-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="11596-108">Un módulo recibe un mensaje, realiza alguna acción en él, opcionalmente lo transforma en un nuevo mensaje y luego lo publica para que otros módulos lo procesen.</span><span class="sxs-lookup"><span data-stu-id="11596-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="11596-109">Existe la posibilidad de que algunos módulos solo produzcan nuevos mensajes y nunca procesen los mensajes entrantes.</span><span class="sxs-lookup"><span data-stu-id="11596-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="11596-110">Una cadena de módulos crea una canalización de procesamiento de datos donde cada módulo realiza una transformación en los datos en un punto de esa canalización.</span><span class="sxs-lookup"><span data-stu-id="11596-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Cadena de módulos de puerta de enlace creada con Azure IoT Edge][1]

<span data-ttu-id="11596-112">IoT Edge contiene los siguientes componentes:</span><span class="sxs-lookup"><span data-stu-id="11596-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="11596-113">Módulos escritos previamente que realizan funciones comunes de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="11596-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="11596-114">Las interfaces que un desarrollador puede utilizar para escribir módulos personalizados.</span><span class="sxs-lookup"><span data-stu-id="11596-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="11596-115">La infraestructura necesaria para implementar y ejecutar un conjunto de módulos.</span><span class="sxs-lookup"><span data-stu-id="11596-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="11596-116">El SDK proporciona una capa de abstracción que permite crear puertas de enlace para trabajar en varios sistemas operativos y plataformas.</span><span class="sxs-lookup"><span data-stu-id="11596-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Capa de abstracción de Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="11596-118">error de Hadoop</span><span class="sxs-lookup"><span data-stu-id="11596-118">Messages</span></span>

<span data-ttu-id="11596-119">Aunque una manera práctica de conceptualizar cómo funciona una puerta de enlace es pensar que los módulos se pasan mensajes entre ellos, no refleja realmente lo que sucede.</span><span class="sxs-lookup"><span data-stu-id="11596-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="11596-120">Los módulos de IoT Edge usan un agente para comunicarte entre sí.</span><span class="sxs-lookup"><span data-stu-id="11596-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="11596-121">Los módulos publican mensajes al agente (mediante patrones de mensajería como bus o de publicación y suscripción) y, a continuación, permiten al agente enrutar el mensaje a los módulos conectados a él.</span><span class="sxs-lookup"><span data-stu-id="11596-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="11596-122">Un módulo usa la función **Broker_Publish** para publicar un mensaje en el agente.</span><span class="sxs-lookup"><span data-stu-id="11596-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="11596-123">El agente entrega los mensajes a un módulo mediante la invocación de una función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="11596-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="11596-124">Un mensaje consta de un conjunto de propiedades de clave/valor y del contenido que se pasa como un bloque de memoria.</span><span class="sxs-lookup"><span data-stu-id="11596-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Rol del agente en Azure IoT Edge][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="11596-126">Enrutamiento y filtro de mensajes</span><span class="sxs-lookup"><span data-stu-id="11596-126">Message routing and filtering</span></span>

<span data-ttu-id="11596-127">Hay dos maneras de dirigir los mensajes a los módulos de IoT Edge correctos:</span><span class="sxs-lookup"><span data-stu-id="11596-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="11596-128">Se puede pasar un conjunto de vínculos al agente para que este conozca tanto el origen como el receptor de cada módulo.</span><span class="sxs-lookup"><span data-stu-id="11596-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="11596-129">Un módulo puede filtrar por las propiedades del mensaje.</span><span class="sxs-lookup"><span data-stu-id="11596-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="11596-130">Un módulo solo debe actuar en los mensajes destinados a ello.</span><span class="sxs-lookup"><span data-stu-id="11596-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="11596-131">Los vínculos y el filtrado de mensajes crean de manera eficaz una canalización de mensajes.</span><span class="sxs-lookup"><span data-stu-id="11596-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11596-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11596-132">Next steps</span></span>

<span data-ttu-id="11596-133">Para ver estos conceptos aplicados en un ejemplo que se puede ejecutar, consulte [Explorar la arquitectura de Azure IoT Edge][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="11596-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md