---
title: aaaOverview del borde de IoT de Azure | Documentos de Microsoft
description: "Describe Hola conceptos arquitectónicos clave en Azure IoT Edge como puertas de enlace, los módulos y los corredores de bolsa."
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
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="04f7b-103">Conceptos de arquitectura de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="04f7b-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="04f7b-104">Antes de examinar cualquier código de ejemplo o crear su propia puerta de enlace de campo con el borde de IoT, debe comprender los conceptos de clave de Hola que respaldan la arquitectura de hello del borde de IoT.</span><span class="sxs-lookup"><span data-stu-id="04f7b-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="04f7b-105">Módulos de IoT Edge</span><span class="sxs-lookup"><span data-stu-id="04f7b-105">IoT Edge modules</span></span>

<span data-ttu-id="04f7b-106">Una puerta de enlace se crea con Azure IoT Edge mediante la creación y el ensamblado de *módulos de IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="04f7b-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="04f7b-107">Utilizar los módulos de *mensajes* tooexchange datos entre sí.</span><span class="sxs-lookup"><span data-stu-id="04f7b-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="04f7b-108">Un módulo recibe un mensaje, realiza alguna acción en él, opcionalmente transforma en un mensaje nuevo y, a continuación, publica para otros tooprocess de módulos.</span><span class="sxs-lookup"><span data-stu-id="04f7b-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="04f7b-109">Existe la posibilidad de que algunos módulos solo produzcan nuevos mensajes y nunca procesen los mensajes entrantes.</span><span class="sxs-lookup"><span data-stu-id="04f7b-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="04f7b-110">Una cadena de módulos, crea una canalización de procesamiento de datos con cada módulo realiza una transformación en los datos de hello en un punto de esa canalización.</span><span class="sxs-lookup"><span data-stu-id="04f7b-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Cadena de módulos de puerta de enlace creada con Azure IoT Edge][1]

<span data-ttu-id="04f7b-112">Borde de IoT contiene Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="04f7b-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="04f7b-113">Módulos escritos previamente que realizan funciones comunes de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="04f7b-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="04f7b-114">interfaces de Hello un desarrollador pueden utilizar módulos personalizados de toowrite.</span><span class="sxs-lookup"><span data-stu-id="04f7b-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="04f7b-115">Hola toodeploy necesarios de infraestructura y ejecutar un conjunto de módulos.</span><span class="sxs-lookup"><span data-stu-id="04f7b-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="04f7b-116">Hola SDK proporciona una capa de abstracción que permite toobuild toorun de puertas de enlace en varios sistemas operativos y plataformas.</span><span class="sxs-lookup"><span data-stu-id="04f7b-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Capa de abstracción de Azure IoT Edge][2]

## <a name="messages"></a><span data-ttu-id="04f7b-118">error de Hadoop</span><span class="sxs-lookup"><span data-stu-id="04f7b-118">Messages</span></span>

<span data-ttu-id="04f7b-119">Aunque pensar en módulos de pasar mensajes tooeach otros es una manera cómoda de tooconceptualize cómo funciona una puerta de enlace, no con precisión refleja lo que sucede.</span><span class="sxs-lookup"><span data-stu-id="04f7b-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="04f7b-120">Módulos de borde IoT usan un toocommunicate broker entre sí.</span><span class="sxs-lookup"><span data-stu-id="04f7b-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="04f7b-121">Módulos publicación a broker toohello de mensajes (mediante patrones de mensajería como bus o de publicación/suscripción) y, a continuación, permiten Hola broker ruta Hola mensaje toohello módulos conectados tooit.</span><span class="sxs-lookup"><span data-stu-id="04f7b-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="04f7b-122">Un módulo usa hello **Broker_Publish** función toopublish un agente de toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="04f7b-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="04f7b-123">broker de Hello entrega módulo tooa de mensajes mediante la invocación de una función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="04f7b-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="04f7b-124">Un mensaje consta de un conjunto de propiedades de clave/valor y del contenido que se pasa como un bloque de memoria.</span><span class="sxs-lookup"><span data-stu-id="04f7b-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![rol de Hola de hello Broker de borde de IoT de Azure][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="04f7b-126">Enrutamiento y filtro de mensajes</span><span class="sxs-lookup"><span data-stu-id="04f7b-126">Message routing and filtering</span></span>

<span data-ttu-id="04f7b-127">Hay dos maneras de módulos de borde IoT correctos de toodirect mensajes toohello:</span><span class="sxs-lookup"><span data-stu-id="04f7b-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="04f7b-128">Puede pasar un conjunto de vínculos se pueden pasar toohello broker para que sepa de broker de Hola Hola origen y el receptor para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="04f7b-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="04f7b-129">Un módulo puede filtrar según propiedades de Hola de mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="04f7b-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="04f7b-130">Un módulo sólo debe actuar un mensaje si el mensaje de saludo está destinado.</span><span class="sxs-lookup"><span data-stu-id="04f7b-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="04f7b-131">Los vínculos y el filtrado de mensajes crean de manera eficaz una canalización de mensajes.</span><span class="sxs-lookup"><span data-stu-id="04f7b-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04f7b-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04f7b-132">Next steps</span></span>

<span data-ttu-id="04f7b-133">toosee estos conceptos aplicados en un ejemplo que se puede ejecutar, consulte [arquitectura de explorar Azure IoT borde][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="04f7b-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md