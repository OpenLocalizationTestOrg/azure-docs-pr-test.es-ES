---
title: soluciones de aaaAzure para Internet de las cosas (IoT Suite) | Documentos de Microsoft
description: "Una visión general de IoT de Azure y una arquitectura de solución de ejemplo y cómo se relaciona con hello y tooAzure IoT Suite soluciones preconfiguradas."
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
ms.openlocfilehash: e527ca3f7541c84fbd6abc99ee38792468f88644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="azure-iot-suite"></a><span data-ttu-id="5572e-103">Conjunto de aplicaciones de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="5572e-103">Azure IoT Suite</span></span>
<span data-ttu-id="5572e-104">Hola Microsoft Azure IoT Suite es una solución de nivel empresarial que permite tooget a trabajar rápidamente a través de un conjunto de soluciones preconfiguradas extensibles.</span><span class="sxs-lookup"><span data-stu-id="5572e-104">hello Microsoft Azure IoT Suite is an enterprise-grade solution that enables you tooget started quickly through a set of extensible preconfigured solutions.</span></span> <span data-ttu-id="5572e-105">Estas soluciones abordan escenarios de IoT habituales, como la [supervisión remota][lnk-preconfigured-solutions], el [mantenimiento predictivo][lnk-predictive-maintenance], y la [fábrica conectada][lnk-connected-factory].</span><span class="sxs-lookup"><span data-stu-id="5572e-105">These solutions address common IoT scenarios, such as [remote monitoring][lnk-preconfigured-solutions], [predictive maintenance][lnk-predictive-maintenance], and [connected factory][lnk-connected-factory].</span></span> <span data-ttu-id="5572e-106">Estas soluciones son implementaciones de hello IoT arquitectura de la solución que se describen en este artículo.</span><span class="sxs-lookup"><span data-stu-id="5572e-106">These solutions are implementations of hello IoT solution architecture outlined in this article.</span></span>

<span data-ttu-id="5572e-107">Hello soluciones preconfiguradas están completos, trabajar, soluciones end-to-end que incluyen:</span><span class="sxs-lookup"><span data-stu-id="5572e-107">hello preconfigured solutions are complete, working, end-to-end solutions that include:</span></span>

- <span data-ttu-id="5572e-108">Simular tooget de dispositivos que se inició.</span><span class="sxs-lookup"><span data-stu-id="5572e-108">Simulated devices tooget you started.</span></span>
- <span data-ttu-id="5572e-109">Servicios de Azure configurados previamente como [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning] y [Azure Storage][Azure storage].</span><span class="sxs-lookup"><span data-stu-id="5572e-109">Preconfigured Azure services such as [Azure IoT Hub][Azure IoT Hub], [Azure Event Hubs][Azure Event Hubs], [Azure Stream Analytics][Azure Stream Analytics], [Azure Machine Learning][Azure Machine Learning], and [Azure storage][Azure storage].</span></span>
- <span data-ttu-id="5572e-110">Consolas de administración específicas de la solución.</span><span class="sxs-lookup"><span data-stu-id="5572e-110">Solution-specific management consoles.</span></span>

<span data-ttu-id="5572e-111">las soluciones de Hello preconfigurado contienen código probada y para entornos de producción que puede personalizar y extender tooimplement sus propios escenarios específicos de IoT.</span><span class="sxs-lookup"><span data-stu-id="5572e-111">hello preconfigured solutions contain proven, production-ready code that you can customize and extend tooimplement your own specific IoT scenarios.</span></span>

<span data-ttu-id="5572e-112">Es podrán que le interese hello [centro de IoT de Azure] [ Azure IoT Hub] servicio que utilizan muchas de las soluciones de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="5572e-112">You may also be interested in hello [Azure IoT Hub][Azure IoT Hub] service that many of hello preconfigured solutions use.</span></span> <span data-ttu-id="5572e-113">[Centro de IoT de Azure] [ Azure IoT Hub] proporciona comunicaciones de bidireccional de hello segura y confiable entre los dispositivos y la nube de hello utilizado en la arquitectura de la solución de hello preconfigurado.</span><span class="sxs-lookup"><span data-stu-id="5572e-113">[Azure IoT Hub][Azure IoT Hub] provides hello secure and reliable bi-directional communications between devices and hello cloud used in hello preconfigured solution architecture.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5572e-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5572e-114">Next steps</span></span>
<span data-ttu-id="5572e-115">Explorar estos toocontinue de recursos de aprendizaje sobre los conjuntos de IoT y Hola soluciones preconfiguradas:</span><span class="sxs-lookup"><span data-stu-id="5572e-115">Explore these resources toocontinue learning about IoT Suite and hello preconfigured solutions:</span></span>

* <span data-ttu-id="5572e-116">[¿Qué es el Conjunto de aplicaciones de IoT de Azure?][lnk-whatissuite]</span><span class="sxs-lookup"><span data-stu-id="5572e-116">[What is Azure IoT Suite?][lnk-whatissuite]</span></span>
* <span data-ttu-id="5572e-117">[¿Qué soluciones de Azure IoT conjunto preconfigurado de hello?][lnk-whatarepreconfigured]</span><span class="sxs-lookup"><span data-stu-id="5572e-117">[What are hello Azure IoT Suite preconfigured solutions?][lnk-whatarepreconfigured]</span></span>

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