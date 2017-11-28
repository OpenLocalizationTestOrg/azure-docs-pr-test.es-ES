---
title: "Mantenimiento de vehículo aaaPredict y dirigir hábitos - Azure | Documentos de Microsoft"
description: "Usar funciones de Hola de toogain en tiempo real y predicción visión de inteligencia de Cortana en el estado del vehículo y dirigir hábitos."
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
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a><span data-ttu-id="22d76-103">Cuaderno de estrategias de soluciones de análisis de telemetría de vehículo</span><span class="sxs-lookup"><span data-stu-id="22d76-103">Vehicle telemetry analytics solution playbook</span></span>
<span data-ttu-id="22d76-104">Esto **menú** vincula toohello capítulos en esta guía.</span><span class="sxs-lookup"><span data-stu-id="22d76-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a><span data-ttu-id="22d76-105">Información general</span><span class="sxs-lookup"><span data-stu-id="22d76-105">Overview</span></span>
<span data-ttu-id="22d76-106">Equipos superusuarios han movido fuera del laboratorio de Hola y ahora están aparcados en nuestros artículos!</span><span class="sxs-lookup"><span data-stu-id="22d76-106">Super computers have moved out of hello lab and are now parked in our garage!</span></span> <span data-ttu-id="22d76-107">Estos automóviles vanguardistas contienen una gran cantidad de sensores, darles tootrack de capacidad de Hola y supervisar millones de eventos por segundo.</span><span class="sxs-lookup"><span data-stu-id="22d76-107">These cutting-edge automobiles contain a myriad of sensors, giving them hello ability tootrack and monitor millions of events every second.</span></span> <span data-ttu-id="22d76-108">Esperamos que por 2020, la mayoría de estos coches habrá sido toohello conectado Internet.</span><span class="sxs-lookup"><span data-stu-id="22d76-108">We expect that by 2020, most of these cars will have been connected toohello Internet.</span></span> <span data-ttu-id="22d76-109">¡Imagine pulsar en esta gran cantidad de datos tooprovide mayor seguridad, confiabilidad y una experiencia mejor determinante!</span><span class="sxs-lookup"><span data-stu-id="22d76-109">Imagine tapping into this wealth of data tooprovide greater safety, reliability and a better driving experience!</span></span> <span data-ttu-id="22d76-110">Microsoft ha convertido ese sueño en una realidad gracias a Cortana Intelligence.</span><span class="sxs-lookup"><span data-stu-id="22d76-110">Microsoft has made this dream a reality with Cortana Intelligence.</span></span>

<span data-ttu-id="22d76-111">Inteligencia de Cortana de Microsoft es una grande de datos totalmente administrado y avanzado conjunto de análisis que permite tootransform los datos en acción inteligente.</span><span class="sxs-lookup"><span data-stu-id="22d76-111">Microsoft’s Cortana Intelligence is a fully managed big data and advanced analytics suite that enables you tootransform your data into intelligent action.</span></span> <span data-ttu-id="22d76-112">Queremos toointroduce toohello plantilla de solución de análisis de telemetría de Cortana Intelligence vehículo.</span><span class="sxs-lookup"><span data-stu-id="22d76-112">We want toointroduce you toohello Cortana Intelligence Vehicle Telemetry Analytics Solution Template.</span></span> <span data-ttu-id="22d76-113">Esta solución muestra cómo concesiones de coches, los fabricantes de automóviles y compañías de seguros pueden usar las capacidades de Hola de inteligencia de Cortana toogain en tiempo real y transformación de la visión de predicción en mantenimiento de vehículo y dirigir.</span><span class="sxs-lookup"><span data-stu-id="22d76-113">This solution demonstrates how car dealerships, automobile manufacturers, and insurance companies can use hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits.</span></span> 

<span data-ttu-id="22d76-114">solución de Hola se implementa como un [lambda (modelo) arquitectura](https://en.wikipedia.org/wiki/Lambda_architecture) que muestra todas las posibilidades de plataforma de inteligencia de Cortana de Hola para hello en tiempo real y procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="22d76-114">hello solution is implemented as a [lambda architecture pattern](https://en.wikipedia.org/wiki/Lambda_architecture) showing hello full potential of hello Cortana Intelligence platform for real-time and batch processing.</span></span> <span data-ttu-id="22d76-115">solución de Hello:</span><span class="sxs-lookup"><span data-stu-id="22d76-115">hello solution:</span></span> 

* <span data-ttu-id="22d76-116">Proporcionar un simulador telemático de vehículo</span><span class="sxs-lookup"><span data-stu-id="22d76-116">provides a Vehicle Telematics simulator</span></span>
* <span data-ttu-id="22d76-117">Utilizar Event Hubs para la introducción de millones de eventos de telemetría de vehículo en Azure</span><span class="sxs-lookup"><span data-stu-id="22d76-117">leverages Event Hubs for ingesting millions of simulated vehicle telemetry events into Azure</span></span> 
* <span data-ttu-id="22d76-118">usa la información de análisis de transmisiones toogain en tiempo real en el estado del vehículo</span><span class="sxs-lookup"><span data-stu-id="22d76-118">uses Stream Analytics toogain real-time insights on vehicle health</span></span>
* <span data-ttu-id="22d76-119">conserva los datos de hello en el almacenamiento a largo plazo para el análisis de lote más rica.</span><span class="sxs-lookup"><span data-stu-id="22d76-119">persists hello data into long-term storage for richer batch analytics.</span></span> 
* <span data-ttu-id="22d76-120">aprovecha las ventajas de aprendizaje automático para la detección de anomalías de en tiempo real y procesamiento toogain predictivo visión de lote.</span><span class="sxs-lookup"><span data-stu-id="22d76-120">takes advantage of Machine Learning for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="22d76-121">aprovecha los datos de tootransform de HDInsight en la escala y orquestación toohandle de factoría de datos, programación, administración de recursos y supervisión de canalización de procesamiento por lotes de Hola</span><span class="sxs-lookup"><span data-stu-id="22d76-121">leverages HDInsight tootransform data at scale and Data Factory toohandle orchestration, scheduling, resource management, and monitoring of hello batch processing pipeline</span></span> 
* <span data-ttu-id="22d76-122">Ofrecer a esta solución un panel completo de datos en tiempo real y visualizaciones de análisis predictivo mediante Power BI</span><span class="sxs-lookup"><span data-stu-id="22d76-122">gives this solution a rich dashboard for real-time data and predictive analytics visualizations using Power BI</span></span>

## <a name="architecture"></a><span data-ttu-id="22d76-123">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="22d76-123">Architecture</span></span>
<span data-ttu-id="22d76-124">![Diagrama de la arquitectura de la solución](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figura 1: Arquitectura de la solución de análisis de telemetría de vehículos*</span><span class="sxs-lookup"><span data-stu-id="22d76-124">![Solution architecture diagram](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Vehicle Telemetry Analytics Solution Architecture*</span></span>

<span data-ttu-id="22d76-125">Esta solución incluye siguiente hello **componentes Cortana Intelligence** y muestra su integración de tooend final:</span><span class="sxs-lookup"><span data-stu-id="22d76-125">This solution includes hello following **Cortana Intelligence components** and showcases their end tooend integration:</span></span>

* <span data-ttu-id="22d76-126">**Centros de eventos** para la introducción de millones de eventos de telemetría del vehículo en Azure.</span><span class="sxs-lookup"><span data-stu-id="22d76-126">**Event Hubs** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="22d76-127">**Análisis de transmisiones** para obtener información en tiempo real sobre el estado del vehículo y conserva los datos en el almacenamiento a largo plazo para análisis de lotes más completo.</span><span class="sxs-lookup"><span data-stu-id="22d76-127">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="22d76-128">**Aprendizaje automático** para la detección de anomalías en tiempo real y toogain predictiva visión de procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="22d76-128">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="22d76-129">**HDInsight** tootransform aprovechado datos a escala</span><span class="sxs-lookup"><span data-stu-id="22d76-129">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="22d76-130">**Factoría de datos** controla la orquestación, programación, administración de recursos y la supervisión de la canalización de procesamiento por lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="22d76-130">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>
* <span data-ttu-id="22d76-131">**Power BI** ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="22d76-131">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span>

<span data-ttu-id="22d76-132">Esta solución tiene acceso a dos **orígenes de datos**diferentes:</span><span class="sxs-lookup"><span data-stu-id="22d76-132">This solution accesses two different **data sources**:</span></span> 

* <span data-ttu-id="22d76-133">**Simular las señales de vehículo y diagnóstico**: un simulador de telemáticas vehículo emite información de diagnóstico y las señales que corresponden toohello estado del vehículo de Hola y Hola automóvil patrón en un momento dado en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="22d76-133">**Simulated vehicle signals and diagnostics**: A vehicle telematics simulator emits diagnostic information and signals that correspond toohello state of hello vehicle and hello driving pattern at a given point in time.</span></span> 
* <span data-ttu-id="22d76-134">**Catálogo de vehículo**: un conjunto de datos de referencia que contiene una asignación de toomodel Niv.</span><span class="sxs-lookup"><span data-stu-id="22d76-134">**Vehicle catalog**: A reference dataset containing a VIN toomodel mapping.</span></span>

