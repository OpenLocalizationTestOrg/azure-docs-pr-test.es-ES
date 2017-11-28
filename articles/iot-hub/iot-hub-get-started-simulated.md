---
title: "Introducción a la conexión de dispositivos simulados a Azure IoT Hub | Microsoft Docs"
description: "Aprenda a crear dispositivos IoT simulados y a conectarlos a Azure IoT Hub. Los dispositivos pueden enviar datos de telemetría a IoT Hub y este servicio supervisa y administra los dispositivos."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial de azure iot hub
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="82328-105">Tutoriales de introducción a los dispositivos simulados para Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="82328-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="82328-106">Estos tutoriales le presentan Azure IoT Hub y los SDK de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="82328-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="82328-107">Los tutoriales cubren escenarios comunes de IoT para demostrar las funcionalidades de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="82328-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="82328-108">Los tutoriales también muestran cómo combinar IoT Hub con otras herramientas y servicios de Azure para crear soluciones de IoT más eficaces.</span><span class="sxs-lookup"><span data-stu-id="82328-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="82328-109">Los tutoriales en la tabla siguiente muestran cómo crear dispositivos IoT simulados.</span><span class="sxs-lookup"><span data-stu-id="82328-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="82328-110">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="82328-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="82328-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="82328-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="82328-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="82328-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="82328-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="82328-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="82328-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="82328-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="82328-115">Además, puede usar una puerta de enlace de IoT Edge para permitir que los dispositivos simulados se conecten a su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="82328-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="82328-116">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="82328-116">Programming language</span></span> | <span data-ttu-id="82328-117">Plataforma</span><span class="sxs-lookup"><span data-stu-id="82328-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="82328-118">C</span><span class="sxs-lookup"><span data-stu-id="82328-118">C</span></span>                    | <span data-ttu-id="82328-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="82328-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="82328-120">C</span><span class="sxs-lookup"><span data-stu-id="82328-120">C</span></span>                    | <span data-ttu-id="82328-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="82328-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
