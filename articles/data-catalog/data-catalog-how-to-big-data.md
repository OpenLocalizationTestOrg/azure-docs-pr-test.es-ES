---
title: "aaaHow toowork con orígenes de datos de 'big data' | Documentos de Microsoft"
description: "Tooarticle cómo resaltados patrones para usar el catálogo de datos con orígenes de datos de 'big data', como almacenamiento de blobs de Azure y Azure Data Lake, Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="c45a7-103">Cómo orígenes toowork con grandes cantidades de datos en el catálogo de datos</span><span class="sxs-lookup"><span data-stu-id="c45a7-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="c45a7-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="c45a7-104">Introduction</span></span>
<span data-ttu-id="c45a7-105">**Catálogo de datos de Microsoft Azure** es un servicio en la nube totalmente administrado que actúa como sistema de registro y de detección de orígenes de datos empresariales.</span><span class="sxs-lookup"><span data-stu-id="c45a7-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="c45a7-106">Son algo fundamental que ayuda a personas detectar, comprender y usar orígenes de datos y ayudar a las organizaciones tooget más valor de sus orígenes de datos existentes, incluidas grandes cantidades de datos.</span><span class="sxs-lookup"><span data-stu-id="c45a7-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="c45a7-107">**Catálogo de datos de Azure** admite Hola registro de blobs de almacenamiento de blobs de Azure y directorios, así como archivos de Hadoop HDFS y directorios.</span><span class="sxs-lookup"><span data-stu-id="c45a7-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="c45a7-108">naturaleza semiestructurados de Hola de estos orígenes de datos proporciona gran flexibilidad.</span><span class="sxs-lookup"><span data-stu-id="c45a7-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="c45a7-109">Sin embargo, tooget Hola mayor valor de su registro con **el catálogo de datos**, los usuarios deben tener en cuenta cómo se organizan los orígenes de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a7-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="c45a7-110">Directorios como conjuntos de datos lógicos</span><span class="sxs-lookup"><span data-stu-id="c45a7-110">Directories as logical data sets</span></span>
<span data-ttu-id="c45a7-111">Un patrón común para organizar los orígenes de datos grandes es tootreat directorios como conjuntos de datos lógicos.</span><span class="sxs-lookup"><span data-stu-id="c45a7-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="c45a7-112">Directorios de nivel superior son toodefine usa un conjunto de datos, mientras las subcarpetas definición particiones y archivos de Hola que contienen almacenan datos de hello propio.</span><span class="sxs-lookup"><span data-stu-id="c45a7-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="c45a7-113">Un ejemplo de este patrón puede ser:</span><span class="sxs-lookup"><span data-stu-id="c45a7-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="c45a7-114">En este ejemplo, vehicle_maintenance_events y location_tracking_events representan conjuntos de datos lógicos.</span><span class="sxs-lookup"><span data-stu-id="c45a7-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="c45a7-115">Todas estas carpetas contienen archivos de datos que se organizan por año y mes en subcarpetas.</span><span class="sxs-lookup"><span data-stu-id="c45a7-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="c45a7-116">Potencialmente, cada una de estas carpetas puede contener cientos o miles de archivos.</span><span class="sxs-lookup"><span data-stu-id="c45a7-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="c45a7-117">En este patrón, el registro de archivos individuales en **Catálogo de datos de Azure** probablemente no tenga sentido.</span><span class="sxs-lookup"><span data-stu-id="c45a7-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="c45a7-118">En su lugar, registre los directorios de Hola que representan los conjuntos de datos de Hola que ser toohello significativa a los usuarios trabajar con datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a7-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="c45a7-119">Archivos de datos de referencia</span><span class="sxs-lookup"><span data-stu-id="c45a7-119">Reference data files</span></span>
<span data-ttu-id="c45a7-120">Un patrón complementario es toostore conjuntos de datos de referencia como archivos individuales.</span><span class="sxs-lookup"><span data-stu-id="c45a7-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="c45a7-121">Estos conjuntos de datos puede considerarse como el lado de "pequeño" hello de grandes cantidades de datos y suelen ser toodimensions similar en un modelo de datos analíticos.</span><span class="sxs-lookup"><span data-stu-id="c45a7-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="c45a7-122">Archivos de datos de referencia contienen registros de contexto tooprovide usado para cargas masivas de Hola Hola de archivos de datos almacenados en otras partes de almacén de datos grande de Hola.</span><span class="sxs-lookup"><span data-stu-id="c45a7-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="c45a7-123">Un ejemplo de este patrón puede ser:</span><span class="sxs-lookup"><span data-stu-id="c45a7-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="c45a7-124">Cuando científico de datos o analista se trabaja con datos de hello incluidos en estructuras de directorio de gran tamaño de hello, datos de hello en estos archivos de referencia pueden ser usado tooprovide información más detallada para las entidades que están mencionados tooonly por nombre o identificador de datos más grandes de Hola conjunto.</span><span class="sxs-lookup"><span data-stu-id="c45a7-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="c45a7-125">En este modelo, tiene sentido tooregister archivos de datos de referencia individual de hello con **el catálogo de datos**.</span><span class="sxs-lookup"><span data-stu-id="c45a7-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="c45a7-126">Cada archivo representa un conjunto de datos y cada uno de ellos se puede anotar y detectar individualmente.</span><span class="sxs-lookup"><span data-stu-id="c45a7-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="c45a7-127">Patrones alternativos</span><span class="sxs-lookup"><span data-stu-id="c45a7-127">Alternate patterns</span></span>
<span data-ttu-id="c45a7-128">patrones que se describen en la sección anterior de Hola Hola son sólo dos formas posibles de que un almacén de grandes cantidades de datos se puede organizar, pero cada implementación es diferente.</span><span class="sxs-lookup"><span data-stu-id="c45a7-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="c45a7-129">Independientemente de cómo se estructuran los orígenes de datos, al registrar orígenes de datos grandes con **el catálogo de datos**, se centran en registrar Hola archivos y directorios que representan los conjuntos de datos de hello del valor tooothers dentro de su organización.</span><span class="sxs-lookup"><span data-stu-id="c45a7-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="c45a7-130">Registrar todos los archivos y directorios puede abarrotar catálogo hello, lo que sea más difícil para los usuarios toofind lo necesitan.</span><span class="sxs-lookup"><span data-stu-id="c45a7-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="c45a7-131">Resumen</span><span class="sxs-lookup"><span data-stu-id="c45a7-131">Summary</span></span>
<span data-ttu-id="c45a7-132">Registrar orígenes de datos con **el catálogo de datos** hace que sea más fácil toodiscover y comprender.</span><span class="sxs-lookup"><span data-stu-id="c45a7-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="c45a7-133">Mediante el registro y anotar Hola grandes cantidades de datos archivos y directorios que representan los conjuntos de datos lógicos, puede ayudar a los usuarios buscar y usar orígenes de datos grandes de Hola que necesitan.</span><span class="sxs-lookup"><span data-stu-id="c45a7-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
