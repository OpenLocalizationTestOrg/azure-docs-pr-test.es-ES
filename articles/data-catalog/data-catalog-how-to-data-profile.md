---
title: "Generación de perfiles de datos de los orígenes de datos"
description: "Este artículo de procedimientos destaca cómo incluir perfiles de datos de nivel de tabla y de columna al registrar orígenes de datos en el Catálogo de datos de Azure y cómo utilizar perfiles de datos para entender los orígenes de datos."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="60be7-103">Orígenes de datos de perfiles de datos</span><span class="sxs-lookup"><span data-stu-id="60be7-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="60be7-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="60be7-104">Introduction</span></span>
<span data-ttu-id="60be7-105">**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales.</span><span class="sxs-lookup"><span data-stu-id="60be7-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="60be7-106">En otras palabras, el **Catálogo de datos de Azure** consiste en ayudar a las personas a detectar, comprender y usar orígenes de datos, y en ayudar a las organizaciones a obtener más valor de sus datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="60be7-107">Cuando un origen de datos se registra en el **Catálogo de datos de Azure**, el servicio copia e indexa sus metadatos, pero eso no es todo.</span><span class="sxs-lookup"><span data-stu-id="60be7-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="60be7-108">La característica de **perfiles de datos** de **Azure Data Catalog** examina los datos de orígenes de datos admitidos en el catálogo y recopila estadísticas e información sobre esos datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="60be7-109">Es fácil incluir un perfil de sus recursos de datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="60be7-110">Al registrar un recurso de datos, elija **Incluir perfil de datos** en la herramienta de registro de orígenes de datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="60be7-111">¿Qué es la generación de perfiles de datos?</span><span class="sxs-lookup"><span data-stu-id="60be7-111">What is Data Profiling</span></span>
<span data-ttu-id="60be7-112">La generación de perfiles de datos examina los datos del origen de datos que se registra y recopila estadísticas e información sobre esos datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="60be7-113">Durante la detección del origen de datos, estas estadísticas pueden ayudar a los usuarios a determinar la idoneidad de los datos para resolver sus problemas empresariales.</span><span class="sxs-lookup"><span data-stu-id="60be7-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="60be7-114">Los siguientes orígenes de datos admiten la generación de perfiles de datos:</span><span class="sxs-lookup"><span data-stu-id="60be7-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="60be7-115">Vistas y tablas de SQL Server (incluidos Almacenamiento de datos SQL y Base de datos SQL de Azure)</span><span class="sxs-lookup"><span data-stu-id="60be7-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="60be7-116">Vistas y tablas de Oracle</span><span class="sxs-lookup"><span data-stu-id="60be7-116">Oracle tables and views</span></span>
* <span data-ttu-id="60be7-117">Vistas y tablas de Teradata</span><span class="sxs-lookup"><span data-stu-id="60be7-117">Teradata tables and views</span></span>
* <span data-ttu-id="60be7-118">Tablas de Hive</span><span class="sxs-lookup"><span data-stu-id="60be7-118">Hive tables</span></span>

<span data-ttu-id="60be7-119">Incluir los perfiles de datos al registrar lo recursos de datos ayuda a los usuarios a responder preguntas acerca de los orígenes de datos, incluidas:</span><span class="sxs-lookup"><span data-stu-id="60be7-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="60be7-120">¿Puede utilizarse para solucionar mi problema empresarial?</span><span class="sxs-lookup"><span data-stu-id="60be7-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="60be7-121">¿Los datos se ajustan a estándares o patrones específicos?</span><span class="sxs-lookup"><span data-stu-id="60be7-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="60be7-122">¿Cuáles son algunas de las anomalías del origen de datos?</span><span class="sxs-lookup"><span data-stu-id="60be7-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="60be7-123">¿Cuáles son los posibles retos de integración de estos datos en mi aplicación?</span><span class="sxs-lookup"><span data-stu-id="60be7-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="60be7-124">También puede agregar documentación a un recurso para describir cómo se pueden integrar los datos en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="60be7-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="60be7-125">Consulte [Documentación de los orígenes de datos](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="60be7-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="60be7-126">Cómo incluir un perfil de datos al registrar un origen de datos</span><span class="sxs-lookup"><span data-stu-id="60be7-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="60be7-127">Es fácil incluir un perfil de sus origen de datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="60be7-128">Al registrar un origen de datos, en el panel **Objetos que se registrarán** de la herramienta de registro de orígenes de datos, elija **Incluir perfil de datos**.</span><span class="sxs-lookup"><span data-stu-id="60be7-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="60be7-129">Para más información sobre cómo registrar orígenes de datos, vea [Registro de orígenes de datos](data-catalog-how-to-register.md) e [Introducción a Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="60be7-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="60be7-130">Filtrado de recursos de datos que incluyen perfiles de datos</span><span class="sxs-lookup"><span data-stu-id="60be7-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="60be7-131">Para detectar los recursos de datos que incluyen un perfil de datos, puede incluir `has:tableDataProfiles` o `has:columnsDataProfiles` como uno de los términos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="60be7-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="60be7-132">Al seleccionar **Incluir perfil de datos** en la herramienta de registro de orígenes de datos, se incluye la información de perfil de nivel de columna y tabla.</span><span class="sxs-lookup"><span data-stu-id="60be7-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="60be7-133">Sin embargo, la API de Data Catalog permite que los recursos de datos se registren con un único conjunto de información de perfil.</span><span class="sxs-lookup"><span data-stu-id="60be7-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="60be7-134">Visualización de la información del perfil de datos</span><span class="sxs-lookup"><span data-stu-id="60be7-134">Viewing data profile information</span></span>
<span data-ttu-id="60be7-135">Una vez que encuentre un origen de datos adecuado con un perfil, puede ver los detalles del perfil de datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="60be7-136">Para ver el perfil de datos, seleccione un recurso de datos y elija **Perfil de datos** en la ventana del portal de Catálogo de datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="60be7-137">Un perfil de datos del **Catálogo de datos de Azure** muestra la información del perfil de tabla y columna, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="60be7-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="60be7-138">Perfil de datos de objeto</span><span class="sxs-lookup"><span data-stu-id="60be7-138">Object data profile</span></span>
* <span data-ttu-id="60be7-139">Número de filas</span><span class="sxs-lookup"><span data-stu-id="60be7-139">Number of rows</span></span>
* <span data-ttu-id="60be7-140">Tamaño de la tabla</span><span class="sxs-lookup"><span data-stu-id="60be7-140">Table size</span></span>
* <span data-ttu-id="60be7-141">Cuándo se actualizó por última vez el objeto</span><span class="sxs-lookup"><span data-stu-id="60be7-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="60be7-142">Perfil de datos de columna</span><span class="sxs-lookup"><span data-stu-id="60be7-142">Column data profile</span></span>
* <span data-ttu-id="60be7-143">Tipo de datos de columna</span><span class="sxs-lookup"><span data-stu-id="60be7-143">Column data type</span></span>
* <span data-ttu-id="60be7-144">Número de valores distintivos</span><span class="sxs-lookup"><span data-stu-id="60be7-144">Number of distinct values</span></span>
* <span data-ttu-id="60be7-145">Número de filas con valores NULL</span><span class="sxs-lookup"><span data-stu-id="60be7-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="60be7-146">Mínimo, máximo, promedio y desviación estándar para los valores de las columnas</span><span class="sxs-lookup"><span data-stu-id="60be7-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="60be7-147">Resumen</span><span class="sxs-lookup"><span data-stu-id="60be7-147">Summary</span></span>
<span data-ttu-id="60be7-148">La generación de perfiles de datos proporciona estadísticas e información sobre los recursos de datos registrados para ayudar a los usuarios a determinar la idoneidad de los datos para resolver problemas empresariales.</span><span class="sxs-lookup"><span data-stu-id="60be7-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="60be7-149">Junto con la anotación y documentación de los orígenes de datos, los perfiles de datos pueden dar a los usuarios una comprensión más profunda de los datos.</span><span class="sxs-lookup"><span data-stu-id="60be7-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="60be7-150">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="60be7-150">See Also</span></span>
* [<span data-ttu-id="60be7-151">Registro de orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="60be7-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="60be7-152">Introducción al Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="60be7-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
