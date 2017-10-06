---
title: "aaaMicrosoft Power BI Embedded - origen de datos de conexión tooa"
description: "Power BI Embedded, conectar orígenes toodata"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="5acc2-103">Conectar el origen de datos de tooa</span><span class="sxs-lookup"><span data-stu-id="5acc2-103">Connect tooa data source</span></span>
<span data-ttu-id="5acc2-104">Con **Power BI Embedded**, puede insertar informes en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="5acc2-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="5acc2-105">Al incrustar un informe de Power BI en su aplicación, conecta toohello subyacente datos por informe de hello **importar** una copia de datos de Hola o por **conectar directamente** toohello origen de datos mediante  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="5acc2-106">Estas son Hola diferencias entre el uso de **importación** y **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="5acc2-107">Importación</span><span class="sxs-lookup"><span data-stu-id="5acc2-107">Import</span></span> | <span data-ttu-id="5acc2-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5acc2-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="5acc2-109">Tablas, columnas, *y datos* se importan o copian en el conjunto de datos del informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="5acc2-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="5acc2-110">toosee cambia datos subyacente toohello se produjo, debe actualizar o importar un completo actual conjunto de datos nuevo.</span><span class="sxs-lookup"><span data-stu-id="5acc2-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="5acc2-111">Solo *tablas y columnas* se importan o copian en el conjunto de datos del informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="5acc2-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="5acc2-112">Siempre verá los datos más actualizados de Hola.</span><span class="sxs-lookup"><span data-stu-id="5acc2-112">You always view hello most current data.</span></span> |

<span data-ttu-id="5acc2-113">Con Power BI incrustado, en este momento se puede usar DirectQuery con orígenes de datos de nube, pero no en orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="5acc2-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="5acc2-114">Hello puerta de enlace de datos local no es compatible con Power BI Embedded en este momento.</span><span class="sxs-lookup"><span data-stu-id="5acc2-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="5acc2-115">Esto significa que no se puede usar DirectQuery con orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="5acc2-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="5acc2-116">Orígenes de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="5acc2-116">Supported data sources</span></span>

<span data-ttu-id="5acc2-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="5acc2-117">**DirectQuery**</span></span>
* <span data-ttu-id="5acc2-118">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="5acc2-118">Azure SQL database</span></span>
* <span data-ttu-id="5acc2-119">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="5acc2-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="5acc2-120">**Importaciónación**</span><span class="sxs-lookup"><span data-stu-id="5acc2-120">**Import**</span></span>

<span data-ttu-id="5acc2-121">Puede importar usando el máximo de orígenes de datos disponibles de hello en Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="5acc2-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="5acc2-122">Que se van a **no** ser capaz de toorefresh esos datos en Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="5acc2-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="5acc2-123">Tendrá cambios tooupload tooyour PBIX archivo tooPower BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="5acc2-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="5acc2-124">Esto es debido a toono puerta de enlace disponible.</span><span class="sxs-lookup"><span data-stu-id="5acc2-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="5acc2-125">Ventajas del uso de DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5acc2-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="5acc2-126">Existen dos ventajas principales al usar **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="5acc2-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="5acc2-127">**DirectQuery** permite crear visualizaciones con conjuntos de datos muy grandes, donde lo contrario sería imposible toofirst importación todos Hola datos.</span><span class="sxs-lookup"><span data-stu-id="5acc2-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="5acc2-128">Datos subyacentes cambian pueden requerir una actualización de datos, y en algunos informes, hello necesitan datos actuales de toodisplay puede requerir grandes transferencias de datos, realizar imposible volver a importar datos.</span><span class="sxs-lookup"><span data-stu-id="5acc2-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="5acc2-129">Por el contrario, los informes de **DirectQuery** siempre usan datos actuales.</span><span class="sxs-lookup"><span data-stu-id="5acc2-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="5acc2-130">Limitaciones de DirectQuery</span><span class="sxs-lookup"><span data-stu-id="5acc2-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="5acc2-131">Hay algunas de las limitaciones toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="5acc2-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="5acc2-132">Todas las tablas deben proceder de una base de datos única.</span><span class="sxs-lookup"><span data-stu-id="5acc2-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="5acc2-133">Si consulta hello es demasiado compleja, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="5acc2-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="5acc2-134">error de hello tooremedy debe refactorizar consulta Hola por lo que es menos complejo.</span><span class="sxs-lookup"><span data-stu-id="5acc2-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="5acc2-135">Si consulta Hola debe ser compleja, será necesario tooimport datos de hello en lugar de usar **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="5acc2-136">El filtrado de relaciones es una dirección única tooa limitada, en lugar de ambas direcciones.</span><span class="sxs-lookup"><span data-stu-id="5acc2-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="5acc2-137">No se puede cambiar el tipo de datos de Hola de una columna.</span><span class="sxs-lookup"><span data-stu-id="5acc2-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="5acc2-138">De forma predeterminada, las limitaciones se colocan en expresiones DAX permitidas en las medidas.</span><span class="sxs-lookup"><span data-stu-id="5acc2-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="5acc2-139">Consulte [DirectQuery y medidas](#measures).</span><span class="sxs-lookup"><span data-stu-id="5acc2-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="5acc2-140">DirectQuery y medidas</span><span class="sxs-lookup"><span data-stu-id="5acc2-140">DirectQuery and measures</span></span>
<span data-ttu-id="5acc2-141">las consultas de tooensure enviadas toohello origen de datos subyacente tengan un rendimiento aceptable, se aplican limitaciones en medidas.</span><span class="sxs-lookup"><span data-stu-id="5acc2-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="5acc2-142">Cuando se usa **Power BI Desktop**avanzadas los usuarios pueden elegir toobypass esta limitación eligiendo **archivo > Opciones y configuración > opciones**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="5acc2-143">Hola **opciones** cuadro de diálogo, elija **DirectQuery**y seleccione la opción de hello **permitir medidas sin restricciones en el modo DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="5acc2-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="5acc2-144">Cuando se selecciona esta opción, se puede usar cualquier expresión DAX que sea válida para una medida.</span><span class="sxs-lookup"><span data-stu-id="5acc2-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="5acc2-145">Los usuarios deben tener en cuenta; Sin embargo, que algunas expresiones que funcionan muy bien cuando se importan datos de hello penada back-end de consultas muy lentas toohello de origen en **DirectQuery** modo.</span><span class="sxs-lookup"><span data-stu-id="5acc2-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="5acc2-146">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="5acc2-146">See Also</span></span>
* [<span data-ttu-id="5acc2-147">Introducción a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="5acc2-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="5acc2-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="5acc2-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="5acc2-149">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="5acc2-149">More questions?</span></span> [<span data-ttu-id="5acc2-150">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="5acc2-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

