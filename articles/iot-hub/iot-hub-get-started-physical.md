---
title: "Introducción a la conexión de dispositivos físicos a Azure IoT Hub | Microsoft Docs"
description: "Aprenda a conectar dispositivos físicos y paneles a Azure IoT Hub. Los dispositivos pueden enviar datos de telemetría a IoT Hub y este servicio supervisa y administra los dispositivos."
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
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: f4128b6b049aa876e170c56dcf2e40720644dc3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="9af66-105">Tutoriales de introducción a Azure IoT Hub con dispositivos físicos</span><span class="sxs-lookup"><span data-stu-id="9af66-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="9af66-106">Estos tutoriales le presentan Azure IoT Hub y los SDK de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9af66-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="9af66-107">Los tutoriales cubren escenarios comunes de IoT para demostrar las funcionalidades de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9af66-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="9af66-108">Los tutoriales también muestran cómo combinar IoT Hub con otras herramientas y servicios de Azure para crear soluciones de IoT más eficaces.</span><span class="sxs-lookup"><span data-stu-id="9af66-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="9af66-109">Los tutoriales de la tabla siguiente muestran cómo crear dispositivos de IoT físicos.</span><span class="sxs-lookup"><span data-stu-id="9af66-109">The tutorials listed in the following table show you how to create physical IoT devices.</span></span>

| <span data-ttu-id="9af66-110">Dispositivo IoT</span><span class="sxs-lookup"><span data-stu-id="9af66-110">IoT device</span></span>                       | <span data-ttu-id="9af66-111">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="9af66-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="9af66-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9af66-112">Raspberry Pi</span></span>                    | <span data-ttu-id="9af66-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="9af66-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="9af66-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="9af66-114">IoT DevKit</span></span>                      | <span data-ttu-id="9af66-115">[Arduino en VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="9af66-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="9af66-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="9af66-116">Intel Edison</span></span>                    | <span data-ttu-id="9af66-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="9af66-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="9af66-118">Adafruit Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="9af66-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="9af66-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="9af66-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="9af66-120">Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="9af66-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="9af66-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="9af66-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="9af66-122">Adafruit Feather M0</span><span class="sxs-lookup"><span data-stu-id="9af66-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="9af66-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="9af66-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="9af66-124">Además, puede usar una puerta de enlace de IoT Edge para habilitar dispositivos para conectarse a su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9af66-124">In addition, you can use an IoT Edge gateway to enable devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="9af66-125">Dispositivo de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="9af66-125">Gateway device</span></span>               | <span data-ttu-id="9af66-126">Lenguaje de programación</span><span class="sxs-lookup"><span data-stu-id="9af66-126">Programming language</span></span> | <span data-ttu-id="9af66-127">Plataforma</span><span class="sxs-lookup"><span data-stu-id="9af66-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="9af66-128">Intel NUC (modelo DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="9af66-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="9af66-129">C</span><span class="sxs-lookup"><span data-stu-id="9af66-129">C</span></span>                    | <span data-ttu-id="9af66-130">[Wind River Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="9af66-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
