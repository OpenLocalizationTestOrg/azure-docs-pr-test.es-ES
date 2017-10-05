---
title: "Conexión de un Raspberry Pi al Conjunto de aplicaciones de IoT de Azure | Microsoft Docs"
description: "Tutoriales con Node.js o C para ayudarle a aprender a usar el Starter Kit de IoT de Microsoft Azure para Raspberry Pi 3 y la solución de supervisión remota del Conjunto de aplicaciones de IoT. Puede elegir un tutorial que simula telemetría, que usa sensores reales o que habilita las actualizaciones de firmware remotas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="7bb4f-104">Conexión de su Starter Kit de Raspberry Pi 3 de IoT de Microsoft Azure a la solución de supervisión remota</span><span class="sxs-lookup"><span data-stu-id="7bb4f-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="7bb4f-105">Los tutoriales de esta sección le ayudan a obtener información sobre cómo conectar un dispositivo Raspberry Pi 3 a la solución de supervisión remota.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="7bb4f-106">Elija el tutorial adecuado para su lenguaje de programación preferido y si tiene el hardware de sensor disponible para su uso con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="7bb4f-107">Los tutoriales</span><span class="sxs-lookup"><span data-stu-id="7bb4f-107">The tutorials</span></span>

| <span data-ttu-id="7bb4f-108">Tutorial</span><span class="sxs-lookup"><span data-stu-id="7bb4f-108">Tutorial</span></span> | <span data-ttu-id="7bb4f-109">Notas</span><span class="sxs-lookup"><span data-stu-id="7bb4f-109">Notes</span></span> | <span data-ttu-id="7bb4f-110">Idiomas</span><span class="sxs-lookup"><span data-stu-id="7bb4f-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="7bb4f-111">Telemetría simulada (básico)</span><span class="sxs-lookup"><span data-stu-id="7bb4f-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="7bb4f-112">Simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-112">Simulates sensor data.</span></span> <span data-ttu-id="7bb4f-113">Usa un Raspberry Pi independiente.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="7bb4f-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="7bb4f-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="7bb4f-115">Sensor real (intermedio)</span><span class="sxs-lookup"><span data-stu-id="7bb4f-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="7bb4f-116">Usa datos de un sensor BME280 conectado a su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="7bb4f-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="7bb4f-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="7bb4f-118">Implementación de la actualización de firmware (avanzado)</span><span class="sxs-lookup"><span data-stu-id="7bb4f-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="7bb4f-119">Usa datos de un sensor BME280 conectado a su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="7bb4f-120">Habilita las actualizaciones de firmware remotas en su Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="7bb4f-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="7bb4f-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7bb4f-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7bb4f-122">Next steps</span></span>

<span data-ttu-id="7bb4f-123">Visite el [Centro para desarrolladores de IoT de Azure](https://azure.microsoft.com/develop/iot/) para obtener más ejemplos y la documentación de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb4f-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md