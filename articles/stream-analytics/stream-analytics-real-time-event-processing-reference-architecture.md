---
title: "procesamiento con el procesamiento de eventos de análisis de transmisiones de eventos de tiempo de aaaReal | Documentos de Microsoft"
description: "Aprenda cómo puede interoperar un conjunto de servicios de Azure para habilitar el procesado de eventos en tiempo real y el análisis."
keywords: procesamiento en tiempo real, procesamiento de eventos, arquitectura de referencia
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a><span data-ttu-id="078cb-104">Arquitectura de referencia: procesado de eventos en tiempo real con Análisis de transmisiones de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="078cb-104">Reference architecture: Real-time event processing with Microsoft Azure Stream Analytics</span></span>
<span data-ttu-id="078cb-105">arquitectura de referencia de Hola para procesamiento con análisis de transmisiones de Azure de eventos en tiempo real está previsto tooprovide un plano genérico para la implementación de una plataforma en tiempo real como una solución de procesamiento de transmisiones de servicio (PaaS) con Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="078cb-105">hello reference architecture for real-time event processing with Azure Stream Analytics is intended tooprovide a generic blueprint for deploying a real-time platform as a service (PaaS) stream-processing solution with Microsoft Azure.</span></span>

## <a name="summary"></a><span data-ttu-id="078cb-106">Resumen</span><span class="sxs-lookup"><span data-stu-id="078cb-106">Summary</span></span>
<span data-ttu-id="078cb-107">Tradicionalmente, las soluciones de análisis se han basado en funciones como ETL (extracción, transformación, carga) y el almacenamiento de datos, donde los datos están almacenados tooanalysis anterior.</span><span class="sxs-lookup"><span data-stu-id="078cb-107">Traditionally, analytics solutions have been based on capabilities such as ETL (extract, transform, load) and data warehousing, where data is stored prior tooanalysis.</span></span> <span data-ttu-id="078cb-108">Cambios en los requisitos, incluidos los datos más rápidamente que llegan tarde, están realizando la inserción de este límite de toohello modelo existente.</span><span class="sxs-lookup"><span data-stu-id="078cb-108">Changing requirements, including more rapidly arriving data, are pushing this existing model toohello limit.</span></span> <span data-ttu-id="078cb-109">datos Hola capacidad tooanalyze móvil toostorage anteriores de secuencias están una solución, y aunque no es una nueva capacidad, el enfoque de hello no se ha adoptado ampliamente en todos los mercados verticales de la industria.</span><span class="sxs-lookup"><span data-stu-id="078cb-109">hello ability tooanalyze data within moving streams prior toostorage is one solution, and while it is not a new capability, hello approach has not been widely adopted across all industry verticals.</span></span> 

<span data-ttu-id="078cb-110">Microsoft Azure proporciona un catálogo muy amplio de tecnologías de análisis que pueden admitir una matriz de diferentes requisitos y escenarios de solución.</span><span class="sxs-lookup"><span data-stu-id="078cb-110">Microsoft Azure provides an extensive catalog of analytics technologies that are capable of supporting an array of different solution scenarios and requirements.</span></span> <span data-ttu-id="078cb-111">Seleccionar qué toodeploy los servicios de Azure para una solución end-to-end puede ser un desafío dado la amplitud de Hola de ofertas.</span><span class="sxs-lookup"><span data-stu-id="078cb-111">Selecting which Azure services toodeploy for an end-to-end solution can be a challenge given hello breadth of offerings.</span></span> <span data-ttu-id="078cb-112">Este documento está diseñado toodescribe Hola capacidades e interoperación de Hola varios servicios de Azure que admiten una solución de transmisión de eventos.</span><span class="sxs-lookup"><span data-stu-id="078cb-112">This paper is designed toodescribe hello capabilities and interoperation of hello various Azure services that support an event-streaming solution.</span></span> <span data-ttu-id="078cb-113">También se explican algunos de los escenarios de hello en el que los clientes pueden beneficiarse de este tipo de enfoque.</span><span class="sxs-lookup"><span data-stu-id="078cb-113">It also explains some of hello scenarios in which customers can benefit from this type of approach.</span></span>

## <a name="contents"></a><span data-ttu-id="078cb-114">Contenido</span><span class="sxs-lookup"><span data-stu-id="078cb-114">Contents</span></span>
* <span data-ttu-id="078cb-115">Resumen ejecutivo</span><span class="sxs-lookup"><span data-stu-id="078cb-115">Executive Summary</span></span>
* <span data-ttu-id="078cb-116">Análisis en tiempo de tooReal Introducción</span><span class="sxs-lookup"><span data-stu-id="078cb-116">Introduction tooReal-Time Analytics</span></span>
* <span data-ttu-id="078cb-117">Propuesta de valor de datos en tiempo real en Azure</span><span class="sxs-lookup"><span data-stu-id="078cb-117">Value Proposition of Real-Time Data in Azure</span></span>
* <span data-ttu-id="078cb-118">Escenarios comunes para el análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="078cb-118">Common Scenarios for Real-Time Analytics</span></span>
* <span data-ttu-id="078cb-119">Arquitectura y componentes</span><span class="sxs-lookup"><span data-stu-id="078cb-119">Architecture and Components</span></span>
  * <span data-ttu-id="078cb-120">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="078cb-120">Data Sources</span></span>
  * <span data-ttu-id="078cb-121">Capa de integración de datos</span><span class="sxs-lookup"><span data-stu-id="078cb-121">Data-Integration Layer</span></span>
  * <span data-ttu-id="078cb-122">Capa de análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="078cb-122">Real-time Analytics Layer</span></span>
  * <span data-ttu-id="078cb-123">Capa de almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="078cb-123">Data Storage Layer</span></span>
  * <span data-ttu-id="078cb-124">Presentación / capa de consumo</span><span class="sxs-lookup"><span data-stu-id="078cb-124">Presentation / Consumption Layer</span></span>
* <span data-ttu-id="078cb-125">Conclusión</span><span class="sxs-lookup"><span data-stu-id="078cb-125">Conclusion</span></span>

<span data-ttu-id="078cb-126">**Autor:** Charles Feddersen, arquitecto de soluciones, Centro de excelencia de Data Insights, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="078cb-126">**Author:** Charles Feddersen, Solution Architect, Data Insights Center of Excellence, Microsoft Corporation</span></span>

<span data-ttu-id="078cb-127">**Publicado:** enero de 2015</span><span class="sxs-lookup"><span data-stu-id="078cb-127">**Published:** January 2015</span></span>

<span data-ttu-id="078cb-128">**Revisión:** 1.0</span><span class="sxs-lookup"><span data-stu-id="078cb-128">**Revision:** 1.0</span></span>

<span data-ttu-id="078cb-129">**Descarga:**[Procesado de eventos en tiempo real con Análisis de transmisiones de Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span><span class="sxs-lookup"><span data-stu-id="078cb-129">**Download:** [Real-Time Event Processing with Microsoft Azure Stream Analytics](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)</span></span>

## <a name="get-help"></a><span data-ttu-id="078cb-130">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="078cb-130">Get help</span></span>
<span data-ttu-id="078cb-131">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="078cb-131">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="078cb-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="078cb-132">Next steps</span></span>
* [<span data-ttu-id="078cb-133">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="078cb-133">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="078cb-134">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="078cb-134">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="078cb-135">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="078cb-135">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="078cb-136">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="078cb-136">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="078cb-137">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="078cb-137">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

