---
title: soluciones de aaaAzure para Internet de las cosas (IoT Suite) | Documentos de Microsoft
description: "Información general sobre la arquitectura de una solución de IoT de ejemplo y cómo se relaciona con toodevices, Hola servicio del centro de IoT de Azure, SDK de dispositivos de IoT de Azure, SDK de servicio de IoT de Azure y otros servicios de Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="97bd4-103">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97bd4-103">Next steps</span></span>

<span data-ttu-id="97bd4-104">Azure IoT Hub es un servicio de Azure que permite la comunicación bidireccional fiable y segura entre el back-end de la solución y millones de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="97bd4-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="97bd4-105">Permite back-end de soluciones de Hola para:</span><span class="sxs-lookup"><span data-stu-id="97bd4-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="97bd4-106">Recibir telemetría a escala de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="97bd4-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="97bd4-107">Enrutar datos desde el procesador de eventos de flujo de tooa de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="97bd4-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="97bd4-108">Recibir cargas de archivos de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="97bd4-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="97bd4-109">Enviar mensajes de la nube al dispositivo toospecific dispositivos.</span><span class="sxs-lookup"><span data-stu-id="97bd4-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="97bd4-110">Puede usar tooimplement centro de IoT finalizar su propia solución de nuevo.</span><span class="sxs-lookup"><span data-stu-id="97bd4-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="97bd4-111">Además, centro de IoT incluye un dispositivos de tooprovision del registro usadas de identidad, sus credenciales de seguridad y su centro de IoT de derechos tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="97bd4-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="97bd4-112">toolearn más información acerca del centro de IoT, consulte [¿qué es el centro de IoT?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="97bd4-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="97bd4-113">toolearn cómo centro de IoT de Azure permite la administración de dispositivos basada en estándares tooremotely administrar, configurar y actualizar los dispositivos, consulte [información general de administración de dispositivos con el centro de IoT][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="97bd4-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="97bd4-114">tooimplement las aplicaciones de cliente en una amplia variedad de plataformas de hardware de dispositivos y sistemas operativos, puede usar dispositivos de IoT de Azure de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="97bd4-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="97bd4-115">dispositivo de Hello SDK incluye bibliotecas que facilitan el envío telemetría tooan IoT hub y la recepción en la nube al dispositivo de mensajes.</span><span class="sxs-lookup"><span data-stu-id="97bd4-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="97bd4-116">Cuando se utilizan dispositivos de hello SDK, puede elegir entre varios toocommunicate de protocolos de red con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="97bd4-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="97bd4-117">toolearn más información, vea hello [obtener información acerca del dispositivo SDK][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="97bd4-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="97bd4-118">tooget iniciado escribiendo código y ejecutar algunos ejemplos, vea hello [empezar a trabajar con el centro de IoT] [ lnk-getstarted] tutorial.</span><span class="sxs-lookup"><span data-stu-id="97bd4-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="97bd4-119">También puede interesarle [Conjunto de aplicaciones de IoT de Azure][lnk-iot-suite], que es una colección de soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="97bd4-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="97bd4-120">Conjunto de IoT permite tooget a trabajar rápidamente y escalar IoT proyectos tooaddress IoT escenarios comunes, como la supervisión remota, la administración de activos y el mantenimiento predictivo.</span><span class="sxs-lookup"><span data-stu-id="97bd4-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
