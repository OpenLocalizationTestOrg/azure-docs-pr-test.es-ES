---
title: "Predicción del estado de vehículo y los hábitos de conducción - Azure | Microsoft Docs"
description: "Aproveche las posibilidades de Cortana Intelligence para obtener información en tiempo real y predictiva del estado de los vehículos y los hábitos de conducción."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: d202d314c61416cf306f760f93e0a4a88a1ab42b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="1ec2e-103">Cuaderno de estrategias de soluciones de análisis de telemetría de vehículo</span><span class="sxs-lookup"><span data-stu-id="1ec2e-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="1ec2e-104">Este **menú** vincula a los capítulos de este cuaderno de estrategias.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="1ec2e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="1ec2e-105">Overview</span></span>
<span data-ttu-id="1ec2e-106">Se han incorporado superequipos a coches vanguardistas,</span><span class="sxs-lookup"><span data-stu-id="1ec2e-106">Super computers have moved out of the lab and are now parked in our garage!</span></span> <span data-ttu-id="1ec2e-107">con una infinidad de sensores, lo que ofrece la posibilidad de realizar un seguimiento y de supervisar millones de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-107">These cutting-edge automobiles contain a myriad of sensors, giving them the ability to track and monitor millions of events every second.</span></span> <span data-ttu-id="1ec2e-108">Esperamos que para el 2020, la mayoría de estos vehículos se conectará a Internet.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-108">We expect that by 2020, most of these cars will have been connected to the Internet.</span></span> <span data-ttu-id="1ec2e-109">Imagínese explotar esta riqueza de datos para ofrecer la mejor seguridad, confiabilidad y experiencia de conducción de su clase.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-109">Imagine tapping into this wealth of data to provide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="1ec2e-110">Microsoft ha convertido ese sueño en una realidad gracias a Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="1ec2e-111">La solución Cortana Intelligence de Microsoft es un conjunto de aplicaciones de análisis avanzados y macrodatos totalmente administrado que le permite transformar los datos en acciones inteligentes.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you to transform your data into intelligent action.</span></span> <span data-ttu-id="1ec2e-112">Queremos presentarle la plantilla de la solución de análisis de telemetría de vehículos de Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-112">We want to introduce you to the Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="1ec2e-113">Esta solución ilustra cómo los fabricantes y los concesionarios de automóviles, así como las compañías de seguros, pueden usar las funciones de Cortana Intelligence para obtener información predictiva y en tiempo real sobre el estado de los vehículos y los hábitos de conducción.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="1ec2e-114">La solución se implementa como un [patrón de arquitectura lambda](https://en.wikipedia.org/wiki/Lambda_architecture) en el que se muestran todas las posibilidades de la plataforma Cortana Intelligence para procesar datos por lotes y en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-114">The solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing the full potential of the Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="1ec2e-115">La solución consigue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1ec2e-115">The solution:</span></span> 

* <span data-ttu-id="1ec2e-116">Proporcionar un simulador telemático de vehículo</span><span class="sxs-lookup"><span data-stu-id="1ec2e-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="1ec2e-117">Utilizar Event Hubs para la introducción de millones de eventos de telemetría de vehículo en Azure</span><span class="sxs-lookup"><span data-stu-id="1ec2e-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="1ec2e-118">Usar Stream Analytics para obtener información en tiempo real sobre el estado del vehículo</span><span class="sxs-lookup"><span data-stu-id="1ec2e-118">uses Stream Analytics to gain real-time insights on vehicle health</span></span>
* <span data-ttu-id="1ec2e-119">Conservar los datos en un almacenamiento a largo plazo para realizar análisis por lotes más detallados</span><span class="sxs-lookup"><span data-stu-id="1ec2e-119">persists the data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="1ec2e-120">Aprovechar las ventajas de Machine Learning para la detección de anomalías en tiempo real y el procesamiento por lotes para obtener información predictiva</span><span class="sxs-lookup"><span data-stu-id="1ec2e-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="1ec2e-121">Usar HDInsight para transformar los datos a escala y Data Factory controla la orquestación, la programación, la administración de recursos y la supervisión de la canalización del procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="1ec2e-121">leverages HDInsight to transform data at scale and Data Factory to handle orchestration, scheduling, resource management, and monitoring of the batch processing pipeline</span></span> 
* <span data-ttu-id="1ec2e-122">Ofrecer a esta solución un panel completo de datos en tiempo real y visualizaciones de análisis predictivo mediante Power BI</span><span class="sxs-lookup"><span data-stu-id="1ec2e-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="1ec2e-123">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="1ec2e-123">Architecture</span></span>
<span data-ttu-id="1ec2e-124">![Diagrama de la arquitectura de la solución](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1: Arquitectura de la solución de análisis de telemetría de vehículos*</span><span class="sxs-lookup"><span data-stu-id="1ec2e-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="1ec2e-125">Esta solución incorpora los siguientes **componentes de Cortana Intelligence** y presenta su integración completa:</span><span class="sxs-lookup"><span data-stu-id="1ec2e-125">This solution includes the following **Cortana Intelligence components** and showcases their end to end integration:</span></span>

* <span data-ttu-id="1ec2e-126">**Centros de eventos** para la introducción de millones de eventos de telemetría del vehículo en Azure.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="1ec2e-127">**Análisis de transmisiones** para obtener información en tiempo real sobre el estado del vehículo y conserva los datos en el almacenamiento a largo plazo para análisis de lotes más completo.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="1ec2e-128">**Aprendizaje automático** para la detección de anomalías en tiempo real y el procesamiento por lotes para obtener información predictiva.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-128">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="1ec2e-129">**HDInsight** se aprovecha para transformar datos a escala.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-129">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="1ec2e-130">**Factoría de datos** controla la orquestación, la programación, la administración de recursos y la supervisión de la canalización del procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>
* <span data-ttu-id="1ec2e-131">**Power BI** ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="1ec2e-132">Esta solución tiene acceso a dos **orígenes de datos**diferentes:</span><span class="sxs-lookup"><span data-stu-id="1ec2e-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="1ec2e-133">**Diagnósticos y señales de vehículos simuladas**: un simulador telemático de vehículo emite información de diagnóstico y señales que se corresponden con el estado del vehículo y el patrón de conducción en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond to the state of the vehicle and the driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="1ec2e-134">**Catálogo de vehículo**: un conjunto de datos de referencia que contiene una asignación de número de identificación del vehículo a modelo.</span><span class="sxs-lookup"><span data-stu-id="1ec2e-134">**Vehicle catalog**: A reference dataset containing a VIN to model mapping.</span></span>

