---
title: "Información general de Conjunto de aplicaciones de IoT de Microsoft Azure | Microsoft Docs"
description: "Información general sobre cómo el Conjunto de aplicaciones de IoT de Azure ofrece soluciones preconfiguradas de Internet de las cosas para recopilar, analizar y almacenar datos, proporcionar visualizaciones e integrarlos con otros sistemas."
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
ms.openlocfilehash: bfa8dbbd0b1d943a9eb7a042df0bac25189d9ac9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="7cea2-103">Información general de Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="7cea2-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="7cea2-104">Los servicios de Internet de las cosas (IoT) de Azure ofrecen una amplia gama de funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="7cea2-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="7cea2-105">Estos servicios de nivel empresarial le permiten:</span><span class="sxs-lookup"><span data-stu-id="7cea2-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="7cea2-106">Recopilar datos de dispositivos</span><span class="sxs-lookup"><span data-stu-id="7cea2-106">Collect data from devices</span></span>
* <span data-ttu-id="7cea2-107">Analizar flujos de datos en movimiento</span><span class="sxs-lookup"><span data-stu-id="7cea2-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="7cea2-108">Almacenar y consultar grandes conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="7cea2-108">Store and query large data sets</span></span>
* <span data-ttu-id="7cea2-109">Visualizar datos tanto históricos como en tiempo real</span><span class="sxs-lookup"><span data-stu-id="7cea2-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="7cea2-110">Integración con sistemas del área de operaciones</span><span class="sxs-lookup"><span data-stu-id="7cea2-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="7cea2-111">Administración de los dispositivos</span><span class="sxs-lookup"><span data-stu-id="7cea2-111">Manage your devices</span></span>

<span data-ttu-id="7cea2-112">Con el fin de ofrecer estas funcionalidades, el Conjunto de aplicaciones de IoT de Azure ofrece paquetes de múltiples servicios de Azure con extensiones personalizadas como *soluciones preconfiguradas*.</span><span class="sxs-lookup"><span data-stu-id="7cea2-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="7cea2-113">Estas soluciones preconfiguradas son implementaciones base de patrones comunes de soluciones de IoT que le ayudan a reducir el tiempo que dedica a entregar sus soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="7cea2-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="7cea2-114">Con los [kits de desarrollo de software de IoT][lnk-sdks], puede personalizar y extender estas soluciones para satisfacer sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="7cea2-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="7cea2-115">También puede usar estas soluciones como ejemplos o plantillas al desarrollar nuevas soluciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="7cea2-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="7cea2-116">El vídeo siguiente proporciona una introducción al conjunto de aplicaciones de IoT de Azure:</span><span class="sxs-lookup"><span data-stu-id="7cea2-116">The following video provides an introduction to Azure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="7cea2-117">Servicios IoT de Azure en Azure IoT Suite</span><span class="sxs-lookup"><span data-stu-id="7cea2-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="7cea2-118">Normalmente, las soluciones preconfiguradas usan los siguientes servicios:</span><span class="sxs-lookup"><span data-stu-id="7cea2-118">The preconfigured solutions typically use the following services:</span></span>

* <span data-ttu-id="7cea2-119">El componente esencial del Conjunto de aplicaciones de IoT de Azure es el servicio [Azure IoT Hub][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="7cea2-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="7cea2-120">Este servicio ofrece las capacidades de mensajería de dispositivo a la nube y de la nube al dispositivo y actúa como la puerta de enlace para la nube y los demás servicios del Conjunto de aplicaciones de IoT clave.</span><span class="sxs-lookup"><span data-stu-id="7cea2-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span></span> <span data-ttu-id="7cea2-121">El servicio le permite recibir mensajes de los dispositivos, a escala, y enviar comandos a los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7cea2-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span></span> <span data-ttu-id="7cea2-122">El servicio también le permite [administrar los dispositivos][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="7cea2-122">The service also enables you to [manage your devices][lnk-device-management].</span></span> <span data-ttu-id="7cea2-123">Por ejemplo, puede configurar, reiniciar o realizar un restablecimiento de fábrica de uno o varios dispositivos conectados al centro.</span><span class="sxs-lookup"><span data-stu-id="7cea2-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span></span>
* <span data-ttu-id="7cea2-124">[Azure Stream Analytics][lnk-asa] ofrece análisis de datos en movimiento.</span><span class="sxs-lookup"><span data-stu-id="7cea2-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="7cea2-125">El Conjunto de aplicaciones de IoT usa este servicio para procesar la telemetría entrante, realizar la agregación y detectar eventos.</span><span class="sxs-lookup"><span data-stu-id="7cea2-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="7cea2-126">Las soluciones preconfiguradas también usan el análisis de transmisiones para procesar los mensajes informativos que contienen datos como los metadatos y las respuestas de comandos de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7cea2-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="7cea2-127">Las soluciones usan Análisis de transmisiones para procesar los mensajes de los dispositivos y entregarlos a otros servicios.</span><span class="sxs-lookup"><span data-stu-id="7cea2-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span></span>
* <span data-ttu-id="7cea2-128">[Azure Storage][lnk-azure-storage] y [Azure Cosmos DB][lnk-document-db] ofrecen las funcionalidades de almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="7cea2-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide the data storage capabilities.</span></span> <span data-ttu-id="7cea2-129">Las soluciones preconfiguradas usan el almacenamiento de blobs para almacenar la telemetría y que esté disponible para análisis.</span><span class="sxs-lookup"><span data-stu-id="7cea2-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span></span> <span data-ttu-id="7cea2-130">Las soluciones usan Cosmos DB para almacenar los metadatos de dispositivo y habilitar la funcionalidad de administración de dispositivos de las soluciones.</span><span class="sxs-lookup"><span data-stu-id="7cea2-130">The solutions use Cosmos DB to store device metadata and enable the device management capabilities of the solutions.</span></span>
* <span data-ttu-id="7cea2-131">[Azure Web Apps][lnk-web-apps] y [Microsoft Power BI][lnk-power-bi] ofrecen las funcionalidades de visualización de datos.</span><span class="sxs-lookup"><span data-stu-id="7cea2-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span></span> <span data-ttu-id="7cea2-132">La flexibilidad de Power BI le permite compilar rápidamente sus propios paneles interactivos que usan los datos del conjunto de aplicaciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="7cea2-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="7cea2-133">Para información general de la arquitectura de una solución de IoT típica, consulte [Microsoft Azure e Internet de las cosas (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="7cea2-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="7cea2-134">soluciones preconfiguradas</span><span class="sxs-lookup"><span data-stu-id="7cea2-134">Preconfigured solutions</span></span>

<span data-ttu-id="7cea2-135">El Conjunto de aplicaciones de IoT incluye soluciones preconfiguradas que le permiten empezar a trabajar rápidamente con los escenarios comunes de IoT, como:</span><span class="sxs-lookup"><span data-stu-id="7cea2-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as:</span></span>

* <span data-ttu-id="7cea2-136">Supervisión remota</span><span class="sxs-lookup"><span data-stu-id="7cea2-136">Remote monitoring</span></span>
* <span data-ttu-id="7cea2-137">Mantenimiento predictivo</span><span class="sxs-lookup"><span data-stu-id="7cea2-137">Predictive maintenance</span></span>
* <span data-ttu-id="7cea2-138">Fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="7cea2-138">Connected factory</span></span>

<span data-ttu-id="7cea2-139">Puede implementar estas soluciones en su suscripción de Azure y luego ejecutar un escenario de IoT completo e integral.</span><span class="sxs-lookup"><span data-stu-id="7cea2-139">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cea2-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7cea2-140">Next steps</span></span>

<span data-ttu-id="7cea2-141">Ahora que tiene una visión general de lo que puede hacer el Conjunto de aplicaciones de IoT y cuáles son sus componentes principales, puede obtener más información acerca de las soluciones preconfiguradas que incluye.</span><span class="sxs-lookup"><span data-stu-id="7cea2-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="7cea2-142">Para más información, consulte [¿Cuáles son las soluciones preconfiguradas de IoT de Azure?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="7cea2-142">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

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
