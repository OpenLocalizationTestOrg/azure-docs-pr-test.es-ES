---
title: Empezar a conectar dispositivos simulados tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate simular dispositivos de IoT y conectarlos tooAzure centro de IoT. Los dispositivos pueden enviar telemetría tooIoT concentrador y centro de Iot pueden supervisar y administrar los dispositivos."
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
ms.openlocfilehash: 2c9b76477d12c853abd93aa96043417a013daaef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="ba66c-105">Tutoriales de introducción a los dispositivos simulados para Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ba66c-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="ba66c-106">Estos tutoriales presentan tooAzure centro de IoT y el dispositivo de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="ba66c-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="ba66c-107">tutoriales de Hola cubren IoT escenarios toodemonstrate hello las funciones comunes de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ba66c-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="ba66c-108">Hello tutoriales también muestran cómo toocombine centro de IoT con otro Azure servicios y toobuild de las herramientas más eficaces soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="ba66c-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="ba66c-109">tutoriales de Hello enumerados en hello en la tabla siguiente muestra cómo toocreate simular dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="ba66c-109">hello tutorials listed in hello following table show you how toocreate simulated IoT devices.</span></span>

| <span data-ttu-id="ba66c-110">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="ba66c-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="ba66c-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="ba66c-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="ba66c-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="ba66c-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="ba66c-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="ba66c-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="ba66c-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="ba66c-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="ba66c-115">Además, puede usar un centro de IoT IoT borde puerta de enlace tooenable simulada dispositivos tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="ba66c-115">In addition, you can use an IoT Edge gateway tooenable simulated devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="ba66c-116">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="ba66c-116">Programming language</span></span> | <span data-ttu-id="ba66c-117">Plataforma</span><span class="sxs-lookup"><span data-stu-id="ba66c-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="ba66c-118">C</span><span class="sxs-lookup"><span data-stu-id="ba66c-118">C</span></span>                    | <span data-ttu-id="ba66c-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="ba66c-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="ba66c-120">C</span><span class="sxs-lookup"><span data-stu-id="ba66c-120">C</span></span>                    | <span data-ttu-id="ba66c-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="ba66c-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
