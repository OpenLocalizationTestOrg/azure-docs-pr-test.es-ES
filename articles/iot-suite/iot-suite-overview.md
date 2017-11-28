---
title: "Introducción a Azure IoT Suite aaaMicrosoft | Documentos de Microsoft"
description: "Información general sobre cómo Suite de IoT de Azure ofrece internet de las cosas soluciones preconfiguradas toocollect, analizar y almacenar los datos, proporcionar visualizaciones e integrar con otros sistemas."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="a49f3-103">Información general de Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="a49f3-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="a49f3-104">Hello Azure internet de servicios de las cosas (IoT) ofrecen una amplia gama de capacidades.</span><span class="sxs-lookup"><span data-stu-id="a49f3-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="a49f3-105">Estos servicios de nivel empresarial le permiten:</span><span class="sxs-lookup"><span data-stu-id="a49f3-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="a49f3-106">Recopilar datos de dispositivos</span><span class="sxs-lookup"><span data-stu-id="a49f3-106">Collect data from devices</span></span>
* <span data-ttu-id="a49f3-107">Analizar flujos de datos en movimiento</span><span class="sxs-lookup"><span data-stu-id="a49f3-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="a49f3-108">Almacenar y consultar grandes conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="a49f3-108">Store and query large data sets</span></span>
* <span data-ttu-id="a49f3-109">Visualizar datos tanto históricos como en tiempo real</span><span class="sxs-lookup"><span data-stu-id="a49f3-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="a49f3-110">Integración con sistemas del área de operaciones</span><span class="sxs-lookup"><span data-stu-id="a49f3-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="a49f3-111">Administración de los dispositivos</span><span class="sxs-lookup"><span data-stu-id="a49f3-111">Manage your devices</span></span>

<span data-ttu-id="a49f3-112">toodeliver estas capacidades, conjunto de IoT de Azure incorpora varios servicios de Azure con las extensiones personalizadas como *soluciones preconfiguradas*.</span><span class="sxs-lookup"><span data-stu-id="a49f3-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="a49f3-113">Estas soluciones preconfiguradas son implementaciones base de patrones comunes de solución de IoT que ayudan a la hora de hello tooreduce que tomar toodeliver sus soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="a49f3-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="a49f3-114">Con hello [kits de desarrollo de software de IoT][lnk-sdks], puede personalizar y extender estos toomeet soluciones sus propios requisitos.</span><span class="sxs-lookup"><span data-stu-id="a49f3-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="a49f3-115">También puede usar estas soluciones como ejemplos o plantillas al desarrollar nuevas soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="a49f3-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="a49f3-116">Hello vídeo siguiente proporciona un conjunto de IoT tooAzure de introducción:</span><span class="sxs-lookup"><span data-stu-id="a49f3-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="a49f3-117">Servicios IoT de Azure en Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="a49f3-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="a49f3-118">soluciones de Hello preconfigurado suelen usar Hola siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="a49f3-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="a49f3-119">Core tooAzure IoT Suite es hello [centro de IoT de Azure] [ lnk-iot-hub] servicio.</span><span class="sxs-lookup"><span data-stu-id="a49f3-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="a49f3-120">Este servicio proporciona Hola dispositivo a la nube y capacidades de mensajería de nube al dispositivo y actúa como Hola toohello de puerta de enlace en la nube y Hola otros servicios IoT Suite clave.</span><span class="sxs-lookup"><span data-stu-id="a49f3-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="a49f3-121">servicio de Hello permite tooreceive mensajes desde los dispositivos a escala y enviar comandos tooyour dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a49f3-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="a49f3-122">Hola servicio también permite demasiado[administrar sus dispositivos][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="a49f3-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="a49f3-123">Por ejemplo, puede configurar, reiniciar o realizar una restablecimiento de fábrica en Centro de toohello conectado uno o varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a49f3-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="a49f3-124">[Azure Stream Analytics][lnk-asa] ofrece análisis de datos en movimiento.</span><span class="sxs-lookup"><span data-stu-id="a49f3-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="a49f3-125">IoT Suite utiliza esta telemetría entrantes tooprocess de servicio, realizar la agregación y detectar eventos.</span><span class="sxs-lookup"><span data-stu-id="a49f3-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="a49f3-126">las soluciones de Hello preconfigurado también usan stream analytics tooprocess mensajes informativos que contienen datos como las respuestas de metadatos o el comando de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a49f3-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="a49f3-127">soluciones de Hello utilizan mensajes de Hola tooprocess de análisis de transmisiones de los dispositivos y ofrecen servicios de tooother de esos mensajes.</span><span class="sxs-lookup"><span data-stu-id="a49f3-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="a49f3-128">[Almacenamiento de Azure] [ lnk-azure-storage] y [base de datos de Azure Cosmos] [ lnk-document-db] proporcionan capacidades de almacenamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a49f3-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="a49f3-129">Hello soluciones preconfiguradas usan telemetría de toostore de almacenamiento de blobs y toomake estén disponibles para su análisis.</span><span class="sxs-lookup"><span data-stu-id="a49f3-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="a49f3-130">soluciones de Hello usan metadatos del dispositivo de base de datos de Cosmos toostore y habilitan las capacidades de administración del dispositivo de Hola de soluciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="a49f3-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="a49f3-131">[Las aplicaciones Web de Azure] [ lnk-web-apps] y [Microsoft Power BI] [ lnk-power-bi] proporcionan capacidades de visualización de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a49f3-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="a49f3-132">flexibilidad de Hola de Power BI permite tooquickly compilar sus propios paneles interactivos que utilizan datos de conjunto de IoT.</span><span class="sxs-lookup"><span data-stu-id="a49f3-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="a49f3-133">Para obtener información general de arquitectura de Hola de una solución de IoT típica, vea [hello Internet de las cosas (IoT) y Microsoft Azure][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="a49f3-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="a49f3-134">soluciones preconfiguradas</span><span class="sxs-lookup"><span data-stu-id="a49f3-134">Preconfigured solutions</span></span>

<span data-ttu-id="a49f3-135">IoT Suite incluye las soluciones preconfiguradas que habilitar tooquickly empezar a trabajar con y tooexplore Hola IoT los escenarios comunes, como:</span><span class="sxs-lookup"><span data-stu-id="a49f3-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="a49f3-136">Supervisión remota</span><span class="sxs-lookup"><span data-stu-id="a49f3-136">Remote monitoring</span></span>
* <span data-ttu-id="a49f3-137">Mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="a49f3-137">Predictive maintenance</span></span>
* <span data-ttu-id="a49f3-138">Fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="a49f3-138">Connected factory</span></span>

<span data-ttu-id="a49f3-139">Puede implementar estos tooyour soluciones suscripción de Azure y, a continuación, ejecutar un escenario IoT completando-to-end.</span><span class="sxs-lookup"><span data-stu-id="a49f3-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49f3-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a49f3-140">Next steps</span></span>

<span data-ttu-id="a49f3-141">Ahora que tiene información general sobre lo que puede hacer IoT Suite y cuáles son sus componentes principales, se puede obtener más información sobre las soluciones de Hola preconfigurado en el conjunto de IoT.</span><span class="sxs-lookup"><span data-stu-id="a49f3-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="a49f3-142">Para obtener más información, vea [¿qué hello Azure IoT soluciones preconfiguradas?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="a49f3-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
