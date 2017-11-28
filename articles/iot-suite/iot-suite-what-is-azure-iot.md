---
title: Soluciones de Azure para Internet de las cosas (IoT Suite) | Microsoft Docs
description: "Descripción general de IoT en Azure, lo que incluye la arquitectura de una solución de ejemplo y cómo se relaciona con el Conjunto de aplicaciones de IoT de Azure y las soluciones preconfiguradas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 437d2655-896f-4a9e-a4a8-b864790d3ef8
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 320190488bb4c7b8192421f9dd50a5264f558584
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a><span data-ttu-id="9d3c1-103">Conjunto de aplicaciones de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="9d3c1-103">Azure IoT Suite</span></span>
<span data-ttu-id="9d3c1-104">El Conjunto de aplicaciones de IoT de Microsoft Azure es una solución de clase empresarial que le permite comenzar a trabajar rápidamente mediante un conjunto de soluciones preconfiguradas extensibles.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-104">The Microsoft Azure IoT Suite is an enterprise-grade solution that enables you to get started quickly through a set of extensible preconfigured solutions.</span></span> <span data-ttu-id="9d3c1-105">Estas soluciones abordan escenarios de IoT habituales, como la [supervisión remota][lnk-preconfigured-solutions], el [mantenimiento predictivo][lnk-predictive-maintenance], y la [fábrica conectada][lnk-connected-factory].</span><span class="sxs-lookup"><span data-stu-id="9d3c1-105">These solutions address common IoT scenarios, such as [remote monitoring][lnk-preconfigured-solutions], [predictive maintenance][lnk-predictive-maintenance], and [connected factory][lnk-connected-factory].</span></span> <span data-ttu-id="9d3c1-106">Estas soluciones son implementaciones de la arquitectura de la solución de IoT descrita en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-106">These solutions are implementations of the IoT solution architecture outlined in this article.</span></span>

<span data-ttu-id="9d3c1-107">Las soluciones preconfiguradas son soluciones completas, integrales y funcionales que incluyen:</span><span class="sxs-lookup"><span data-stu-id="9d3c1-107">The preconfigured solutions are complete, working, end-to-end solutions that include:</span></span>

- <span data-ttu-id="9d3c1-108">Dispositivos simulados para que pueda empezar a usarla.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-108">Simulated devices to get you started.</span></span>
- <span data-ttu-id="9d3c1-109">Servicios de Azure configurados previamente como [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning] y [Azure Storage][Azure storage].</span><span class="sxs-lookup"><span data-stu-id="9d3c1-109">Preconfigured Azure services such as [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], and [Azure storage][Azure storage].</span></span>
- <span data-ttu-id="9d3c1-110">Consolas de administración específicas de la solución.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-110">Solution-specific management consoles.</span></span>

<span data-ttu-id="9d3c1-111">Contienen código comprobado y listo para producción que puede personalizar y ampliar para implementar sus propios escenarios IoT específicos.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-111">The preconfigured solutions contain proven, production-ready code that you can customize and extend to implement your own specific IoT scenarios.</span></span>

<span data-ttu-id="9d3c1-112">También es posible que le interese el servicio [Azure IoT Hub][Azure IoT Hub] que usan muchas de las soluciones preconfiguradas.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-112">You may also be interested in the [Azure IoT Hub][Azure IoT Hub] service that many of the preconfigured solutions use.</span></span> <span data-ttu-id="9d3c1-113">[Azure IoT Hub][Azure IoT Hub] ofrece las comunicaciones bidireccionales entre dispositivos y la nube seguras y fiables que se utilizan en la arquitectura de la solución preconfigurada.</span><span class="sxs-lookup"><span data-stu-id="9d3c1-113">[Azure IoT Hub][Azure IoT Hub] provides the secure and reliable bi-directional communications between devices and the cloud used in the preconfigured solution architecture.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d3c1-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d3c1-114">Next steps</span></span>
<span data-ttu-id="9d3c1-115">Explore estos recursos para más información acerca del Conjunto de aplicaciones de IoT y las soluciones preconfiguradas:</span><span class="sxs-lookup"><span data-stu-id="9d3c1-115">Explore these resources to continue learning about IoT Suite and the preconfigured solutions:</span></span>

* <span data-ttu-id="9d3c1-116">[¿Qué es el Conjunto de aplicaciones de IoT de Azure?][lnk-whatissuite]</span><span class="sxs-lookup"><span data-stu-id="9d3c1-116">[What is Azure IoT Suite?][lnk-whatissuite]</span></span>
* <span data-ttu-id="9d3c1-117">[¿Qué son las soluciones preconfiguradas del Conjunto de aplicaciones de IoT de Azure?][lnk-whatarepreconfigured]</span><span class="sxs-lookup"><span data-stu-id="9d3c1-117">[What are the Azure IoT Suite preconfigured solutions?][lnk-whatarepreconfigured]</span></span>

[lnk-whatissuite]: iot-suite-overview.md
[lnk-whatarepreconfigured]: iot-suite-what-are-preconfigured-solutions.md

[lnk-preconfigured-solutions]: iot-suite-getstarted-preconfigured-solutions.md
[Azure IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[Azure Event Hubs]: https://azure.microsoft.com/documentation/services/event-hubs/
[Azure Stream Analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[Azure Machine Learning]: https://azure.microsoft.com/documentation/services/machine-learning/
[Azure storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-connected-factory]: iot-suite-connected-factory-overview.md