---
title: "Creación de soluciones integradas con SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: d407c29f99fd7537590ec787febd84a9e3f4f353
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="83315-103">Aprovechamiento de otros servicios con Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="83315-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="83315-104">Además de su funcionalidad básica, Almacenamiento de datos SQL permite a los usuarios aprovechar muchos de los otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="83315-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="83315-105">En concreto, hemos tomado medidas para que realizar una estrecha integración con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="83315-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="83315-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="83315-106">Power BI</span></span>
* <span data-ttu-id="83315-107">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="83315-107">Azure Data Factory</span></span>
* <span data-ttu-id="83315-108">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="83315-108">Azure Machine Learning</span></span>
* <span data-ttu-id="83315-109">Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="83315-109">Azure Stream Analytics</span></span>

<span data-ttu-id="83315-110">Estamos trabajando para conectar con más servicios en el ecosistema de Azure.</span><span class="sxs-lookup"><span data-stu-id="83315-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="83315-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="83315-111">Power BI</span></span>
<span data-ttu-id="83315-112">La integración de Power BI le permite aprovechar en gran medida la capacidad de procesamiento de Almacenamiento de datos SQL con los informes dinámicos y la visualización de Power BI.</span><span class="sxs-lookup"><span data-stu-id="83315-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="83315-113">La integración de Power BI actualmente incluye:</span><span class="sxs-lookup"><span data-stu-id="83315-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="83315-114">**Conexión directa**: una conexión más avanzada con aplicación de lógica en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="83315-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="83315-115">Esto proporciona un análisis más rápido a mayor escala.</span><span class="sxs-lookup"><span data-stu-id="83315-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="83315-116">**Open in Power BI**: el botón ‘Open in Power BI’ (Abrir en Power BI) pasa la información de la instancia a Power BI para lograr una conexión más fluida.</span><span class="sxs-lookup"><span data-stu-id="83315-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="83315-117">Consulte [Integración con Power BI](sql-data-warehouse-integrate-power-bi.md) o la [documentación de Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="83315-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="83315-118">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="83315-118">Azure Data Factory</span></span>
<span data-ttu-id="83315-119">Factoría de datos de Azure ofrece a los usuarios una plataforma administrada para crear canalizaciones complejas de extracción y carga.</span><span class="sxs-lookup"><span data-stu-id="83315-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="83315-120">La integración de Almacenamiento de datos SQL con Factoría de datos de Azure incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="83315-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="83315-121">**Procedimientos almacenados**: coordinar la ejecución de procedimientos almacenados en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="83315-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="83315-122">**Copia**: use ADF para mover datos a Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="83315-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="83315-123">Esta operación puede utilizar el mecanismo estándar de movimiento de datos de ADF o PolyBase en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="83315-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="83315-124">Consulte [Integración con Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) o la [documentación de Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) para más información.</span><span class="sxs-lookup"><span data-stu-id="83315-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="83315-125">Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="83315-125">Azure Machine Learning</span></span>
<span data-ttu-id="83315-126">Aprendizaje automático de Azure es un servicio de análisis totalmente administrado que permite a los usuarios crear modelos complejos aprovechando un amplio conjunto de herramientas de predicción.</span><span class="sxs-lookup"><span data-stu-id="83315-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="83315-127">Almacenamiento de datos SQL se admite como origen y destino para estos modelos con la siguiente funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="83315-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="83315-128">**Lectura de datos:** producir modelos a escala usando T-SQL en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="83315-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="83315-129">**Escritura de datos:** confirmar los cambios de cualquier modelo en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="83315-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="83315-130">Consulte [Integración con Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) o la[ documentación de Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) para más información.</span><span class="sxs-lookup"><span data-stu-id="83315-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="83315-131">Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="83315-131">Azure Stream Analytics</span></span>
<span data-ttu-id="83315-132">Análisis de transmisores de Azure es una infraestructura compleja y totalmente administrada para el procesamiento y consumo de datos de eventos generados por el Centro de eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="83315-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="83315-133">La integración con Almacenamiento de datos SQL permite que los datos de transmisión se procesen y almacenen junto con los datos relacionales para permitir un análisis más profundo y avanzado de los datos.</span><span class="sxs-lookup"><span data-stu-id="83315-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="83315-134">**Resultado del trabajo:** enviar los resultados de los trabajos de Análisis de transmisiones directamente al Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="83315-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="83315-135">Consulte [Integración con Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) o la [documentación de Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) para más información.</span><span class="sxs-lookup"><span data-stu-id="83315-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
