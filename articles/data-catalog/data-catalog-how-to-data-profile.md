---
title: "orígenes de datos de perfil de aaaHow tooData"
description: "Tooarticle cómo resaltar cómo los perfiles de datos de nivel de tabla y columna tooinclude para registrar orígenes de datos en el catálogo de datos de Azure y cómo datos toouse perfiles toounderstand orígenes de datos."
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
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="3186d-103">Orígenes de datos de perfiles de datos</span><span class="sxs-lookup"><span data-stu-id="3186d-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="3186d-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="3186d-104">Introduction</span></span>
<span data-ttu-id="3186d-105">**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales.</span><span class="sxs-lookup"><span data-stu-id="3186d-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="3186d-106">En otras palabras, **el catálogo de datos** es todo acerca de las personas le ayuda a detectar, comprender y usar orígenes de datos, y ayudar a las organizaciones tooget más valor de sus datos existentes.</span><span class="sxs-lookup"><span data-stu-id="3186d-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="3186d-107">Cuando se registra un origen de datos con **el catálogo de datos**, sus metadatos se copian y se indizan por servicio de hello, pero el caso de hello no termina aquí.</span><span class="sxs-lookup"><span data-stu-id="3186d-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="3186d-108">Hola **perfiles de datos** característica de **el catálogo de datos** examina Hola datos desde orígenes de datos admitidos en el catálogo y recopila las estadísticas e información sobre esos datos.</span><span class="sxs-lookup"><span data-stu-id="3186d-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="3186d-109">Es fácil tooinclude un perfil de sus activos de datos.</span><span class="sxs-lookup"><span data-stu-id="3186d-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="3186d-110">Al registrar un recurso de datos, elija **incluyen el perfil de datos** en la herramienta de registro de origen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3186d-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="3186d-111">¿Qué es la generación de perfiles de datos?</span><span class="sxs-lookup"><span data-stu-id="3186d-111">What is Data Profiling</span></span>
<span data-ttu-id="3186d-112">Generación de perfiles de datos examina los datos de Hola Hola origen de datos que se va a registrar y recopila las estadísticas e información sobre esos datos.</span><span class="sxs-lookup"><span data-stu-id="3186d-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="3186d-113">Durante la detección del origen de datos, estas estadísticas pueden ayudarle a determinar la idoneidad de Hola de hello datos toosolve sus problemas empresariales.</span><span class="sxs-lookup"><span data-stu-id="3186d-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="3186d-114">Hello orígenes de datos siguientes admiten la generación de perfiles de datos:</span><span class="sxs-lookup"><span data-stu-id="3186d-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="3186d-115">Vistas y tablas de SQL Server (incluidos Almacenamiento de datos SQL y Base de datos SQL de Azure)</span><span class="sxs-lookup"><span data-stu-id="3186d-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="3186d-116">Vistas y tablas de Oracle</span><span class="sxs-lookup"><span data-stu-id="3186d-116">Oracle tables and views</span></span>
* <span data-ttu-id="3186d-117">Vistas y tablas de Teradata</span><span class="sxs-lookup"><span data-stu-id="3186d-117">Teradata tables and views</span></span>
* <span data-ttu-id="3186d-118">Tablas de Hive</span><span class="sxs-lookup"><span data-stu-id="3186d-118">Hive tables</span></span>

<span data-ttu-id="3186d-119">Incluir los perfiles de datos al registrar lo recursos de datos ayuda a los usuarios a responder preguntas acerca de los orígenes de datos, incluidas:</span><span class="sxs-lookup"><span data-stu-id="3186d-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="3186d-120">¿Puede ser usado toosolve mi problema empresarial?</span><span class="sxs-lookup"><span data-stu-id="3186d-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="3186d-121">¿Ajustan datos hello tooparticular estándares o patrones?</span><span class="sxs-lookup"><span data-stu-id="3186d-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="3186d-122">¿Cuáles son algunas de las anomalías de Hola Hola del origen de datos?</span><span class="sxs-lookup"><span data-stu-id="3186d-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="3186d-123">¿Cuáles son los posibles retos de integración de estos datos en mi aplicación?</span><span class="sxs-lookup"><span data-stu-id="3186d-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="3186d-124">También puede agregar documentación tooan asset toodescribe cómo se pueden integrar datos en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3186d-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="3186d-125">Vea [cómo orígenes de datos de toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="3186d-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="3186d-126">Cómo generar perfiles de datos tooinclude al registrar un origen de datos</span><span class="sxs-lookup"><span data-stu-id="3186d-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="3186d-127">Es fácil tooinclude un perfil del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="3186d-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="3186d-128">Al registrar un origen de datos, en hello **toobe de objetos registrado** el panel del registro del origen de datos de Hola de herramientas, elija **incluyen el perfil de datos**.</span><span class="sxs-lookup"><span data-stu-id="3186d-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="3186d-129">toolearn Obtenga más información sobre cómo ver los orígenes de datos de tooregister, [cómo orígenes de datos de tooregister](data-catalog-how-to-register.md) y [empezar a trabajar con el catálogo de datos](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3186d-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="3186d-130">Filtrado de recursos de datos que incluyen perfiles de datos</span><span class="sxs-lookup"><span data-stu-id="3186d-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="3186d-131">toodiscover los activos de datos que incluyen un perfil de datos, puede incluir `has:tableDataProfiles` o `has:columnsDataProfiles` como uno de los términos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="3186d-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="3186d-132">Seleccionar **incluyen el perfil de datos** en datos Hola herramienta de registro de origen incluye la tabla y la información de perfil de nivel de columna.</span><span class="sxs-lookup"><span data-stu-id="3186d-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="3186d-133">Sin embargo, hello API de catálogo de datos permite toobe de activos de datos registrado con un solo conjunto de información de perfil incluida.</span><span class="sxs-lookup"><span data-stu-id="3186d-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="3186d-134">Visualización de la información del perfil de datos</span><span class="sxs-lookup"><span data-stu-id="3186d-134">Viewing data profile information</span></span>
<span data-ttu-id="3186d-135">Una vez que encuentre un origen de datos adecuado con un perfil, puede ver detalles del perfil de datos Hola.</span><span class="sxs-lookup"><span data-stu-id="3186d-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="3186d-136">datos de hello tooview perfil, seleccione un recurso de datos y elija **perfil de datos** en la ventana del portal Hola catálogo de datos.</span><span class="sxs-lookup"><span data-stu-id="3186d-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="3186d-137">Un perfil de datos del **Catálogo de datos de Azure** muestra la información del perfil de tabla y columna, incluido lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3186d-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="3186d-138">Perfil de datos de objeto</span><span class="sxs-lookup"><span data-stu-id="3186d-138">Object data profile</span></span>
* <span data-ttu-id="3186d-139">Número de filas</span><span class="sxs-lookup"><span data-stu-id="3186d-139">Number of rows</span></span>
* <span data-ttu-id="3186d-140">Tamaño de la tabla</span><span class="sxs-lookup"><span data-stu-id="3186d-140">Table size</span></span>
* <span data-ttu-id="3186d-141">Se actualizó por última vez el objeto de Hola</span><span class="sxs-lookup"><span data-stu-id="3186d-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="3186d-142">Perfil de datos de columna</span><span class="sxs-lookup"><span data-stu-id="3186d-142">Column data profile</span></span>
* <span data-ttu-id="3186d-143">Tipo de datos de columna</span><span class="sxs-lookup"><span data-stu-id="3186d-143">Column data type</span></span>
* <span data-ttu-id="3186d-144">Número de valores distintivos</span><span class="sxs-lookup"><span data-stu-id="3186d-144">Number of distinct values</span></span>
* <span data-ttu-id="3186d-145">Número de filas con valores NULL</span><span class="sxs-lookup"><span data-stu-id="3186d-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="3186d-146">Mínimo, máximo, promedio y desviación estándar para los valores de las columnas</span><span class="sxs-lookup"><span data-stu-id="3186d-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="3186d-147">Resumen</span><span class="sxs-lookup"><span data-stu-id="3186d-147">Summary</span></span>
<span data-ttu-id="3186d-148">Datos de generación de perfiles proporciona estadísticas y obtener información sobre registrado toohelp de activos de datos determina la idoneidad de Hola Hola datos toosolve problemas del negocio.</span><span class="sxs-lookup"><span data-stu-id="3186d-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="3186d-149">Junto con la anotación y documentación de los orígenes de datos, los perfiles de datos pueden dar a los usuarios una comprensión más profunda de los datos.</span><span class="sxs-lookup"><span data-stu-id="3186d-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="3186d-150">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3186d-150">See Also</span></span>
* [<span data-ttu-id="3186d-151">¿Cómo tooregister los orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="3186d-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="3186d-152">Introducción al Catálogo de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="3186d-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
