---
title: Microsoft Power BI Embedded - Conectarse a un origen de datos
description: "Power BI Embedded, conectarse a orígenes de datos"
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
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="c51dd-103">Conectarse a un origen de datos</span><span class="sxs-lookup"><span data-stu-id="c51dd-103">Connect to a data source</span></span>
<span data-ttu-id="c51dd-104">Con **Power BI Embedded**, puede insertar informes en su propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="c51dd-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="c51dd-105">Cuando inserta un informe de Power BI en su aplicación, el informe se conecta a los datos subyacentes **importando** una copia de los datos o **conectándose directamente** al origen de datos mediante **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c51dd-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="c51dd-106">Estas son las diferencias entre usar **Importación** y **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c51dd-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="c51dd-107">Importar</span><span class="sxs-lookup"><span data-stu-id="c51dd-107">Import</span></span> | <span data-ttu-id="c51dd-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="c51dd-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="c51dd-109">Las tablas, columnas *y datos* se importan o se copian en el conjunto de datos del informe.</span><span class="sxs-lookup"><span data-stu-id="c51dd-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="c51dd-110">Para ver los cambios que se han producido en los datos subyacentes, debe actualizar o importar de nuevo un conjunto de datos actual completo.</span><span class="sxs-lookup"><span data-stu-id="c51dd-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="c51dd-111">Solo las *tablas y columnas* se importan o se copian en el conjunto de datos del informe.</span><span class="sxs-lookup"><span data-stu-id="c51dd-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="c51dd-112">Siempre verá los datos más actuales.</span><span class="sxs-lookup"><span data-stu-id="c51dd-112">You always view the most current data.</span></span> |

<span data-ttu-id="c51dd-113">Con Power BI incrustado, en este momento se puede usar DirectQuery con orígenes de datos de nube, pero no en orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="c51dd-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="c51dd-114">No se admite la puerta de enlace de datos local con Power BI Embedded en este momento.</span><span class="sxs-lookup"><span data-stu-id="c51dd-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="c51dd-115">Esto significa que no se puede usar DirectQuery con orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="c51dd-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="c51dd-116">Orígenes de datos admitidos</span><span class="sxs-lookup"><span data-stu-id="c51dd-116">Supported data sources</span></span>

<span data-ttu-id="c51dd-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="c51dd-117">**DirectQuery**</span></span>
* <span data-ttu-id="c51dd-118">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="c51dd-118">Azure SQL database</span></span>
* <span data-ttu-id="c51dd-119">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="c51dd-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="c51dd-120">**Importaciónación**</span><span class="sxs-lookup"><span data-stu-id="c51dd-120">**Import**</span></span>

<span data-ttu-id="c51dd-121">Puede realizar la importación mediante todos los orígenes de datos disponibles en Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c51dd-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="c51dd-122">**No** podrá actualizar dichos datos en Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c51dd-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="c51dd-123">Tendrá que cargar los cambios en el archivo PBIX en Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="c51dd-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="c51dd-124">Esto se debe a que no hay ninguna puerta de enlace disponible.</span><span class="sxs-lookup"><span data-stu-id="c51dd-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="c51dd-125">Ventajas del uso de DirectQuery</span><span class="sxs-lookup"><span data-stu-id="c51dd-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="c51dd-126">Existen dos ventajas principales al usar **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="c51dd-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="c51dd-127">**DirectQuery** le permite crear visualizaciones sobre conjuntos de datos muy grandes, cuando, de otro modo, sería inviable importar por primera vez todos los datos.</span><span class="sxs-lookup"><span data-stu-id="c51dd-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="c51dd-128">Los cambios en los datos subyacentes pueden requerir una actualización de datos, y para algunos informes, la necesidad de mostrar los datos actuales puede requerir grandes transferencias de datos, haciendo inviable la reimportación de datos.</span><span class="sxs-lookup"><span data-stu-id="c51dd-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="c51dd-129">Por el contrario, los informes de **DirectQuery** siempre usan datos actuales.</span><span class="sxs-lookup"><span data-stu-id="c51dd-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="c51dd-130">Limitaciones de DirectQuery</span><span class="sxs-lookup"><span data-stu-id="c51dd-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="c51dd-131">Existen algunas limitaciones al usar **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="c51dd-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="c51dd-132">Todas las tablas deben proceder de una base de datos única.</span><span class="sxs-lookup"><span data-stu-id="c51dd-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="c51dd-133">Si la consulta es demasiado compleja, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="c51dd-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="c51dd-134">Para solucionar el error debe refactorizar la consulta, de forma que sea menos compleja.</span><span class="sxs-lookup"><span data-stu-id="c51dd-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="c51dd-135">Si la consulta debe ser compleja, deberá importar los datos en lugar de usar **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c51dd-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="c51dd-136">El filtrado de relación se limita a una dirección única, en lugar de a ambas direcciones.</span><span class="sxs-lookup"><span data-stu-id="c51dd-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="c51dd-137">No puede cambiar el tipo de datos de una columna.</span><span class="sxs-lookup"><span data-stu-id="c51dd-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="c51dd-138">De forma predeterminada, las limitaciones se colocan en expresiones DAX permitidas en las medidas.</span><span class="sxs-lookup"><span data-stu-id="c51dd-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="c51dd-139">Consulte [DirectQuery y medidas](#measures).</span><span class="sxs-lookup"><span data-stu-id="c51dd-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="c51dd-140">DirectQuery y medidas</span><span class="sxs-lookup"><span data-stu-id="c51dd-140">DirectQuery and measures</span></span>
<span data-ttu-id="c51dd-141">Para asegurarse de que las consultas que se envían al origen de datos subyacente tienen un rendimiento adecuado, se imponen limitaciones en las medidas.</span><span class="sxs-lookup"><span data-stu-id="c51dd-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="c51dd-142">Al usar **Power BI Desktop**, los usuarios avanzados pueden elegir derivar esta limitación eligiendo **Archivo > Opciones y configuración > Opciones**.</span><span class="sxs-lookup"><span data-stu-id="c51dd-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="c51dd-143">En el cuadro de diálogo **Opciones**, elija **DirectQuery** y seleccione la opción **Permitir medidas sin restricciones en el modo DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="c51dd-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="c51dd-144">Cuando se selecciona esta opción, se puede usar cualquier expresión DAX que sea válida para una medida.</span><span class="sxs-lookup"><span data-stu-id="c51dd-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="c51dd-145">Sin embargo, los usuarios deben tener en cuenta que algunas expresiones que se ejecutan correctamente cuando se importan los datos, pueden provocar consultas muy lentas en el origen de back-end del modo **DirectQuery** .</span><span class="sxs-lookup"><span data-stu-id="c51dd-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="c51dd-146">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c51dd-146">See Also</span></span>
* [<span data-ttu-id="c51dd-147">Introducción a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c51dd-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="c51dd-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c51dd-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="c51dd-149">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="c51dd-149">More questions?</span></span> [<span data-ttu-id="c51dd-150">Pruebe la comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="c51dd-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

