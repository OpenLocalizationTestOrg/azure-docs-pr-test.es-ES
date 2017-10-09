---
title: aaaBuild soluciones integradas con almacenamiento de datos SQL | Documentos de Microsoft
description: 'Herramientas y asociados con soluciones que se integran con Almacenamiento de datos SQL. '
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="e17d5-103">Aprovechamiento de otros servicios con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e17d5-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="e17d5-104">Además tooits las funcionalidades básicas, almacenamiento de datos de SQL permite a los usuarios tooleverage muchas de Hola otros servicios en Azure junto con él.</span><span class="sxs-lookup"><span data-stu-id="e17d5-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="e17d5-105">En concreto, le hemos llevado actualmente toodeeply integrar con los siguientes Hola de pasos:</span><span class="sxs-lookup"><span data-stu-id="e17d5-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="e17d5-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="e17d5-106">Power BI</span></span>
* <span data-ttu-id="e17d5-107">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="e17d5-107">Azure Data Factory</span></span>
* <span data-ttu-id="e17d5-108">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e17d5-108">Azure Machine Learning</span></span>
* <span data-ttu-id="e17d5-109">Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="e17d5-109">Azure Stream Analytics</span></span>

<span data-ttu-id="e17d5-110">Estamos trabajando tooconnect con más servicios a través de hello ecosistema de Azure.</span><span class="sxs-lookup"><span data-stu-id="e17d5-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="e17d5-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="e17d5-111">Power BI</span></span>
<span data-ttu-id="e17d5-112">Integración de Power BI permite la capacidad de proceso de hello tooleverage de almacenamiento de datos de SQL con los informes dinámicos de Hola y la visualización de Power BI.</span><span class="sxs-lookup"><span data-stu-id="e17d5-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="e17d5-113">La integración de Power BI actualmente incluye:</span><span class="sxs-lookup"><span data-stu-id="e17d5-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="e17d5-114">**Conexión directa**: una conexión más avanzada con aplicación de lógica en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e17d5-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="e17d5-115">Esto proporciona un análisis más rápido a mayor escala.</span><span class="sxs-lookup"><span data-stu-id="e17d5-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="e17d5-116">**Abrir en Power BI**: botón 'Abrir en Power BI' hello pasa información de instancia tooPower BI, lo que permite una conexión más sencilla.</span><span class="sxs-lookup"><span data-stu-id="e17d5-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="e17d5-117">Vea [integrar con Power BI](sql-data-warehouse-integrate-power-bi.md) o hello [documentación de Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e17d5-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="e17d5-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e17d5-118">Azure Data Factory</span></span>
<span data-ttu-id="e17d5-119">Factoría de datos de Azure ofrece a los usuarios un toocreate de plataforma administrada que canalizaciones complejas de extracción y carga.</span><span class="sxs-lookup"><span data-stu-id="e17d5-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="e17d5-120">La integración del almacenamiento de datos de SQL con Data Factory de Azure incluye siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e17d5-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="e17d5-121">**Procedimientos almacenados**: coordinar la ejecución de Hola de procedimientos almacenados en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="e17d5-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="e17d5-122">**Copia**: datos de uso ADF toomove en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="e17d5-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="e17d5-123">Esta operación puede utilizar el mecanismo de movimiento de datos estándar de ADF o PolyBase en hello cubre.</span><span class="sxs-lookup"><span data-stu-id="e17d5-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="e17d5-124">Vea [integración con Data Factory de Azure](sql-data-warehouse-integrate-azure-data-factory.md) o hello [documentación de Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e17d5-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="e17d5-125">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="e17d5-125">Azure Machine Learning</span></span>
<span data-ttu-id="e17d5-126">Aprendizaje automático de Azure es un servicio de análisis totalmente administrado que permite a los usuarios aprovechar un gran conjunto de herramientas de predicción de modelos intrincados toocreate.</span><span class="sxs-lookup"><span data-stu-id="e17d5-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="e17d5-127">Almacenamiento de datos de SQL se admite como un origen y un destino para estos modelos con hello después funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="e17d5-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="e17d5-128">**Lectura de datos:** producir modelos a escala usando T-SQL en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e17d5-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="e17d5-129">**Datos de escritura:** confirmar los cambios de cualquier modelo de realizar copias de tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e17d5-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="e17d5-130">Vea [integrar con aprendizaje automático de Azure](sql-data-warehouse-integrate-azure-machine-learning.md) o hello [documentación de aprendizaje automático de Azure](https://azure.microsoft.com/services/machine-learning/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e17d5-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="e17d5-131">Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="e17d5-131">Azure Stream Analytics</span></span>
<span data-ttu-id="e17d5-132">Análisis de transmisores de Azure es una infraestructura compleja y totalmente administrada para el procesamiento y consumo de datos de eventos generados por el Centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e17d5-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="e17d5-133">Integración con el almacenamiento de datos de SQL permite streaming toobe datos eficazmente procesa y almacenan junto con datos relacionales, lo que permite un poco más, más análisis avanzado.</span><span class="sxs-lookup"><span data-stu-id="e17d5-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="e17d5-134">**Salida del trabajo:** salida de envío de análisis de transmisiones directamente trabajos tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="e17d5-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="e17d5-135">Vea [integrar con análisis de transmisiones de Azure](sql-data-warehouse-integrate-azure-stream-analytics.md) o hello [documentación de análisis de transmisiones de Azure](https://azure.microsoft.com/documentation/services/stream-analytics/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e17d5-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
