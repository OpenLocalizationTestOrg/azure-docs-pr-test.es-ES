---
title: "Lección complementaria del tutorial de Azure Analysis Services:Filas de detalles | Microsoft Docs"
description: "Se describe cómo crear una expresión de filas de detalle en el tutorial de Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="cb538-103">Lección complementaria: Filas de detalles</span><span class="sxs-lookup"><span data-stu-id="cb538-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="cb538-104">En esta lección complementaria, usará el Editor DAX para definir una expresión personalizada de filas de detalles.</span><span class="sxs-lookup"><span data-stu-id="cb538-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="cb538-105">Una expresión de filas de detalles es una propiedad de una medida, que proporciona a los usuarios finales más información sobre los resultados agregados de una medida.</span><span class="sxs-lookup"><span data-stu-id="cb538-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="cb538-106">Tiempo estimado para completar esta lección: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="cb538-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="cb538-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cb538-107">Prerequisites</span></span>  
<span data-ttu-id="cb538-108">Esta lección complementaria forma parte de un tutorial de modelado tabular.</span><span class="sxs-lookup"><span data-stu-id="cb538-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="cb538-109">Antes de realizar las tareas de esta lección complementaria, debería haber finalizado todas las lecciones anteriores o haber completado un proyecto de modelo de ejemplo de ventas por Internet de Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="cb538-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="cb538-110">¿Qué es necesario solucionar?</span><span class="sxs-lookup"><span data-stu-id="cb538-110">What do we need to solve?</span></span>
<span data-ttu-id="cb538-111">Vamos a echar un vistazo a los detalles de nuestra medida InternetTotalSales, antes de agregar una expresión de filas de detalles.</span><span class="sxs-lookup"><span data-stu-id="cb538-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="cb538-112">En SSDT, haga clic en el menú **Modelo** > **Analizar en Excel** para abrir Excel y crear una tabla dinámica en blanco.</span><span class="sxs-lookup"><span data-stu-id="cb538-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="cb538-113">En **Campos de tabla dinámica**, agregue la medida **InternetTotalSales** de la tabla FactInternetSales a **Valores**, **CalendarYear** de la tabla DimDate a **Columnas** y **EnglishCountryRegionName** a **Filas**.</span><span class="sxs-lookup"><span data-stu-id="cb538-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="cb538-114">Nuestra tabla dinámica nos proporciona ahora resultados agregados de la medida InternetTotalSales por regiones y año.</span><span class="sxs-lookup"><span data-stu-id="cb538-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="cb538-116">En la tabla dinámica, haga doble clic en un valor agregado de un año y una región.</span><span class="sxs-lookup"><span data-stu-id="cb538-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="cb538-117">Aquí, hacemos doble clic en el valor de Australia y el año 2014.</span><span class="sxs-lookup"><span data-stu-id="cb538-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="cb538-118">Se abre una nueva hoja que contiene datos, pero los datos no resultan de utilidad.</span><span class="sxs-lookup"><span data-stu-id="cb538-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="cb538-120">Lo que nos gustaría ver aquí es una tabla que contenga columnas y filas de datos que contribuyan al resultado agregado de nuestra medida InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="cb538-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="cb538-121">Para ello, podemos agregar una expresión de filas de detalles como una propiedad de la medida.</span><span class="sxs-lookup"><span data-stu-id="cb538-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="cb538-122">Adición de una expresión de filas de detalles</span><span class="sxs-lookup"><span data-stu-id="cb538-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="cb538-123">Para crear una expresión de filas de detalles, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="cb538-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="cb538-124">En SSDT, en la cuadrícula de medidas de la tabla FactInternetSales, haga clic en la medida **InternetTotalSales**.</span><span class="sxs-lookup"><span data-stu-id="cb538-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="cb538-125">En **Propiedades** > **Expresión de filas de detalles**, haga clic en el botón del editor para abrir el Editor DAX.</span><span class="sxs-lookup"><span data-stu-id="cb538-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="cb538-127">En el Editor DAX, escriba la siguiente expresión:</span><span class="sxs-lookup"><span data-stu-id="cb538-127">In DAX Editor, enter the following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="cb538-128">Esta expresión especifica nombres, columnas y resultados de medida de la tabla FactInternetSales y las tablas relacionadas devueltas cuando un usuario hace doble clic en un resultado agregado en una tabla dinámica o un informe.</span><span class="sxs-lookup"><span data-stu-id="cb538-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="cb538-129">De nuevo en Excel, elimine la hoja creada en el paso 3 y luego haga doble clic en un valor agregado.</span><span class="sxs-lookup"><span data-stu-id="cb538-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="cb538-130">Esta vez, con la propiedad Expresión de filas de detalles definida para la medida, se abre una nueva hoja que contiene muchos datos útiles.</span><span class="sxs-lookup"><span data-stu-id="cb538-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="cb538-132">Vuelva a implementar el modelo.</span><span class="sxs-lookup"><span data-stu-id="cb538-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="cb538-133">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="cb538-133">See Also</span></span>  
<span data-ttu-id="cb538-134">[Función SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="cb538-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="cb538-135">Lección complementaria: Seguridad dinámica</span><span class="sxs-lookup"><span data-stu-id="cb538-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="cb538-136">Lección complementaria: Jerarquías desiguales</span><span class="sxs-lookup"><span data-stu-id="cb538-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
