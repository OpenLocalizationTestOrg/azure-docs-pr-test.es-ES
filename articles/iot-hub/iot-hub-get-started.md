---
title: 'Centro de IoT de Azure: empezar a conectar en la nube IoT dispositivos toohello | Documentos de Microsoft'
description: "Obtenga información acerca de cómo tooconnect los paneles de IoT y starter kits tooAzure centro de IoT. Los dispositivos pueden enviar telemetría tooIoT concentrador y centro de IoT pueden supervisar y administrar los dispositivos."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: tutorial de azure iot hub
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="0fbd4-105">Tutoriales de introducción de Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0fbd4-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="0fbd4-106">Puede usar el centro de IoT de Azure y soluciones de hello Azure IoT dispositivos SDK toobuild Internet de las cosas (IoT):</span><span class="sxs-lookup"><span data-stu-id="0fbd4-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="0fbd4-107">Centro de IoT de Azure es un servicio completamente administrado en la nube de Hola que se conecta, supervisa y administra los dispositivos de IoT de forma segura.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="0fbd4-108">Utilice Hola SDK de dispositivos de IoT de Azure tooimplement los dispositivos de IoT.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="0fbd4-109">Use una puerta de enlace de IoT en escenarios IoT más complejos.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="0fbd4-110">Por ejemplo, donde debe tooconsider factores como los dispositivos heredados, los costos de ancho de banda, las directivas de seguridad y privacidad o procesamiento de datos de borde.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="0fbd4-111">En estos casos, utilice Azure IoT borde tooimplement una puerta de enlace que se conecta el centro de IoT tooyour de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="0fbd4-112">Aspectos tratan en tutoriales de Hola</span><span class="sxs-lookup"><span data-stu-id="0fbd4-112">What hello tutorials cover</span></span>

<span data-ttu-id="0fbd4-113">Estos tutoriales presentan tooAzure centro de IoT y el dispositivo de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="0fbd4-114">tutoriales de Hola cubren IoT escenarios toodemonstrate hello las funciones comunes de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="0fbd4-115">Hello tutoriales también muestran cómo toocombine centro de IoT con otro Azure servicios y toobuild de las herramientas más eficaces soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="0fbd4-116">En los tutoriales de hello, puede elegir toouse dispositivos de IoT simulados o reales.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="0fbd4-117">Además, puede obtener información sobre cómo toouse un centro de IoT de puerta de enlace tooenable dispositivos tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="0fbd4-118">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="0fbd4-118">Set up your device</span></span>

<span data-ttu-id="0fbd4-119">Conectar un IoT dispositivo o puerta de enlace tooAzure centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0fbd4-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="0fbd4-120">Puede elegir un tooget de dispositivo físico o simulada iniciado:</span><span class="sxs-lookup"><span data-stu-id="0fbd4-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="0fbd4-121">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="0fbd4-121">IoT device</span></span>                       | <span data-ttu-id="0fbd4-122">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="0fbd4-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="0fbd4-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="0fbd4-123">Raspberry Pi</span></span>                     | <span data-ttu-id="0fbd4-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="0fbd4-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="0fbd4-125">IoT DevKit</span></span>                       | <span data-ttu-id="0fbd4-126">[Arduino en VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="0fbd4-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="0fbd4-127">Intel Edison</span></span>                     | <span data-ttu-id="0fbd4-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="0fbd4-129">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="0fbd4-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="0fbd4-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="0fbd4-131">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="0fbd4-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="0fbd4-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="0fbd4-133">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="0fbd4-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="0fbd4-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="0fbd4-135">Dispositivo simulado en PC</span><span class="sxs-lookup"><span data-stu-id="0fbd4-135">Simulated device on PC</span></span>           | <span data-ttu-id="0fbd4-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd] y [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="0fbd4-137">Simulador de dispositivos en línea</span><span class="sxs-lookup"><span data-stu-id="0fbd4-137">Online device simulator</span></span>         | <span data-ttu-id="0fbd4-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="0fbd4-139">Además, puede usar un centro de IoT IoT borde puerta de enlace tooenable dispositivos tooconnect tooyour:</span><span class="sxs-lookup"><span data-stu-id="0fbd4-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="0fbd4-140">Dispositivo de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="0fbd4-140">Gateway device</span></span>               | <span data-ttu-id="0fbd4-141">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="0fbd4-141">Programming language</span></span> | <span data-ttu-id="0fbd4-142">Plataforma</span><span class="sxs-lookup"><span data-stu-id="0fbd4-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="0fbd4-143">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="0fbd4-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="0fbd4-144">C</span><span class="sxs-lookup"><span data-stu-id="0fbd4-144">C</span></span>                    | <span data-ttu-id="0fbd4-145">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="0fbd4-146">Puerta de enlace simulada</span><span class="sxs-lookup"><span data-stu-id="0fbd4-146">Simulated gateway</span></span>            | <span data-ttu-id="0fbd4-147">C</span><span class="sxs-lookup"><span data-stu-id="0fbd4-147">C</span></span>                    | <span data-ttu-id="0fbd4-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="0fbd4-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
