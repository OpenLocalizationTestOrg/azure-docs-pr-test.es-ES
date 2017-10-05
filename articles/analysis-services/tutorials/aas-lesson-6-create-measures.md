---
title: "Lección 6 del tutorial de Analysis Services Azure: Creación de medidas | Microsoft Docs"
description: "Describe cómo crear medidas en el proyecto del tutorial de Azure Analysis Services."
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
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 90833fa9744eac298b0da82cd3d12f27cc237510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="673b9-103">Lección 6: Creación de medidas</span><span class="sxs-lookup"><span data-stu-id="673b9-103">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="673b9-104">En esta lección creará medidas para incluirlas en el modelo.</span><span class="sxs-lookup"><span data-stu-id="673b9-104">In this lesson, you create measures to be included in your model.</span></span> <span data-ttu-id="673b9-105">De forma similar a las columnas calculadas que ha creado, una medida es un cálculo creado con una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="673b9-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="673b9-106">Sin embargo, a diferencia de las columnas calculadas, las medidas se evalúan en función de un *filtro* seleccionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="673b9-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="673b9-107">Por ejemplo, una columna en particular o una segmentación de datos que se agrega al campo etiquetas de fila en una tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="673b9-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span></span> <span data-ttu-id="673b9-108">Luego, la medida aplicada calculará un valor para cada celda del filtro.</span><span class="sxs-lookup"><span data-stu-id="673b9-108">A value for each cell in the filter is then calculated by the applied measure.</span></span> <span data-ttu-id="673b9-109">Las medidas son cálculos eficaces y flexibles que puede incluir en casi cualquier modelo tabular para efectuar cálculos dinámicos sobre datos numéricos.</span><span class="sxs-lookup"><span data-stu-id="673b9-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span></span> <span data-ttu-id="673b9-110">Para obtener más información, consulte [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular) (Medidas).</span><span class="sxs-lookup"><span data-stu-id="673b9-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="673b9-111">Para crear medidas, use la *cuadrícula de medidas*.</span><span class="sxs-lookup"><span data-stu-id="673b9-111">To create measures, you use the *Measure Grid*.</span></span> <span data-ttu-id="673b9-112">De forma predeterminada, cada tabla tiene una cuadrícula de medidas vacía, aunque en principio no se crean medidas para todas las tablas.</span><span class="sxs-lookup"><span data-stu-id="673b9-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="673b9-113">La cuadrícula de medidas aparece debajo de una tabla del Diseñador de modelos cuando se encuentra en Vista de datos.</span><span class="sxs-lookup"><span data-stu-id="673b9-113">The measure grid appears below a table in the model designer when in Data View.</span></span> <span data-ttu-id="673b9-114">Para mostrar u ocultar la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y haga clic en **Mostrar cuadrícula de medidas**.</span><span class="sxs-lookup"><span data-stu-id="673b9-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="673b9-115">Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas y, luego, escribiendo una fórmula DAX en la barra de fórmulas.</span><span class="sxs-lookup"><span data-stu-id="673b9-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span></span> <span data-ttu-id="673b9-116">Al hacer clic en ENTRAR para completar la fórmula, la medida aparece en la celda.</span><span class="sxs-lookup"><span data-stu-id="673b9-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span></span> <span data-ttu-id="673b9-117">También puede crear medidas usando una función de agregación estándar; para ello, haga clic en una columna y, luego, haga clic en el botón Autosuma (**∑**) de la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="673b9-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span></span> <span data-ttu-id="673b9-118">Las medidas creadas con la característica Autosuma aparecen en la celda de la cuadrícula de medidas, justo debajo de la columna, aunque se pueden mover.</span><span class="sxs-lookup"><span data-stu-id="673b9-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span></span>  
  
<span data-ttu-id="673b9-119">En esta lección creará medidas especificando una fórmula DAX en la barra de fórmulas y usando la característica Autosuma.</span><span class="sxs-lookup"><span data-stu-id="673b9-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span></span>  
  
<span data-ttu-id="673b9-120">Tiempo estimado para completar esta lección: **30 minutos**</span><span class="sxs-lookup"><span data-stu-id="673b9-120">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="673b9-121">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="673b9-121">Prerequisites</span></span>  
<span data-ttu-id="673b9-122">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="673b9-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="673b9-123">Antes de llevar a cabo las tareas de esta lección, debe haber finalizado la lección anterior: [Lección 5: Creación de columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="673b9-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="673b9-124">Crear medidas</span><span class="sxs-lookup"><span data-stu-id="673b9-124">Create measures</span></span>  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a><span data-ttu-id="673b9-125">Para crear una medida DaysCurrentQuarterToDate en la tabla DimDate</span><span class="sxs-lookup"><span data-stu-id="673b9-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="673b9-126">En el Diseñador de modelos, haga clic en la tabla **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="673b9-126">In the model designer, click the **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="673b9-127">En la cuadrícula de medidas, haga clic en la celda vacía situada en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="673b9-127">In the measure grid, click the top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="673b9-128">En la barra de fórmulas, escriba la fórmula siguiente:</span><span class="sxs-lookup"><span data-stu-id="673b9-128">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="673b9-129">Observe que la celda superior izquierda ahora contiene un nombre de medida, **DaysCurrentQuarterToDate**, seguido del resultado, **92**.</span><span class="sxs-lookup"><span data-stu-id="673b9-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="673b9-131">A diferencia de las columnas calculadas, con las fórmulas de medidas puede escribir el nombre de la medida, seguido de dos puntos, seguido de la expresión de la fórmula.</span><span class="sxs-lookup"><span data-stu-id="673b9-131">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span></span>

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a><span data-ttu-id="673b9-132">Para crear una medida DaysInCurrentQuarter en la tabla DimDate</span><span class="sxs-lookup"><span data-stu-id="673b9-132">To create a DaysInCurrentQuarter measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="673b9-133">Con la tabla **DimDate** activa en el diseñador de modelos, en la cuadrícula de medidas, haga clic en la celda vacía situada debajo de la medida que ha creado.</span><span class="sxs-lookup"><span data-stu-id="673b9-133">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span></span>  
  
2.  <span data-ttu-id="673b9-134">En la barra de fórmulas, escriba la fórmula siguiente:</span><span class="sxs-lookup"><span data-stu-id="673b9-134">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="673b9-135">Al crear una relación de comparación entre un período incompleto y el período anterior.</span><span class="sxs-lookup"><span data-stu-id="673b9-135">When creating a comparison ratio between one incomplete period and the previous period.</span></span> <span data-ttu-id="673b9-136">La fórmula debe calcular la proporción del período que ha transcurrido y compararla con la misma proporción del período anterior.</span><span class="sxs-lookup"><span data-stu-id="673b9-136">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span></span> <span data-ttu-id="673b9-137">En este caso, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] proporciona la proporción transcurrida del período actual.</span><span class="sxs-lookup"><span data-stu-id="673b9-137">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span></span>  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a><span data-ttu-id="673b9-138">Para crear una medida InternetDistinctCountSalesOrder en la tabla FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="673b9-138">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="673b9-139">Haga clic en la tabla **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="673b9-139">Click the **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="673b9-140">Haga clic en el encabezado de la columna **SalesOrderNumber**.</span><span class="sxs-lookup"><span data-stu-id="673b9-140">Click the **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="673b9-141">En la barra de herramientas, haga clic en la flecha hacia abajo situada junto al botón Autosuma (**∑**) y, luego, seleccione **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="673b9-141">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="673b9-142">La característica Autosuma crea automáticamente una medida para la columna seleccionada con la fórmula de agregación estándar DistinctCount.</span><span class="sxs-lookup"><span data-stu-id="673b9-142">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="673b9-144">En la cuadrícula de medidas, haga clic en la nueva medida y, en la ventana **Propiedades**, en **Nombre de la medida**, cambie el nombre de la medida por **InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="673b9-144">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a><span data-ttu-id="673b9-145">Para crear medidas adicionales en la tabla FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="673b9-145">To create additional measures in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="673b9-146">Con la característica Autosuma, cree las siguientes medidas y asígneles un nombre:</span><span class="sxs-lookup"><span data-stu-id="673b9-146">By using the AutoSum feature, create and name the following measures:</span></span>  

    |<span data-ttu-id="673b9-147">Columna</span><span class="sxs-lookup"><span data-stu-id="673b9-147">Column</span></span>|<span data-ttu-id="673b9-148">Nombre de la medida</span><span class="sxs-lookup"><span data-stu-id="673b9-148">Measure name</span></span>|<span data-ttu-id="673b9-149">Autosuma (∑)</span><span class="sxs-lookup"><span data-stu-id="673b9-149">AutoSum (∑)</span></span>|<span data-ttu-id="673b9-150">Fórmula</span><span class="sxs-lookup"><span data-stu-id="673b9-150">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="673b9-151">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="673b9-151">SalesOrderLineNumber</span></span>|<span data-ttu-id="673b9-152">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="673b9-152">InternetOrderLinesCount</span></span>|<span data-ttu-id="673b9-153">Recuento</span><span class="sxs-lookup"><span data-stu-id="673b9-153">Count</span></span>|<span data-ttu-id="673b9-154">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="673b9-154">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="673b9-155">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="673b9-155">OrderQuantity</span></span>|<span data-ttu-id="673b9-156">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="673b9-156">InternetTotalUnits</span></span>|<span data-ttu-id="673b9-157">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-157">Sum</span></span>|<span data-ttu-id="673b9-158">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="673b9-158">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="673b9-159">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="673b9-159">DiscountAmount</span></span>|<span data-ttu-id="673b9-160">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="673b9-160">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="673b9-161">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-161">Sum</span></span>|<span data-ttu-id="673b9-162">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="673b9-162">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="673b9-163">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="673b9-163">TotalProductCost</span></span>|<span data-ttu-id="673b9-164">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="673b9-164">InternetTotalProductCost</span></span>|<span data-ttu-id="673b9-165">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-165">Sum</span></span>|<span data-ttu-id="673b9-166">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="673b9-166">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="673b9-167">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="673b9-167">SalesAmount</span></span>|<span data-ttu-id="673b9-168">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="673b9-168">InternetTotalSales</span></span>|<span data-ttu-id="673b9-169">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-169">Sum</span></span>|<span data-ttu-id="673b9-170">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="673b9-170">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="673b9-171">Margin</span><span class="sxs-lookup"><span data-stu-id="673b9-171">Margin</span></span>|<span data-ttu-id="673b9-172">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="673b9-172">InternetTotalMargin</span></span>|<span data-ttu-id="673b9-173">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-173">Sum</span></span>|<span data-ttu-id="673b9-174">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="673b9-174">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="673b9-175">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="673b9-175">TaxAmt</span></span>|<span data-ttu-id="673b9-176">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="673b9-176">InternetTotalTaxAmt</span></span>|<span data-ttu-id="673b9-177">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-177">Sum</span></span>|<span data-ttu-id="673b9-178">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="673b9-178">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="673b9-179">Freight</span><span class="sxs-lookup"><span data-stu-id="673b9-179">Freight</span></span>|<span data-ttu-id="673b9-180">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="673b9-180">InternetTotalFreight</span></span>|<span data-ttu-id="673b9-181">Suma</span><span class="sxs-lookup"><span data-stu-id="673b9-181">Sum</span></span>|<span data-ttu-id="673b9-182">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="673b9-182">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="673b9-183">Haga clic en una celda vacía de la cuadrícula de medidas y use la barra de fórmulas para crear las siguientes medidas en orden y asignarles un nombre:</span><span class="sxs-lookup"><span data-stu-id="673b9-183">By clicking an empty cell in the measure grid, and by using the formula bar, create, and name the following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="673b9-184">Las medidas creadas para la tabla FactInternetSales se pueden usar para analizar datos financieros esenciales, como las ventas, los costos y el margen de beneficio de los elementos definidos por el filtro seleccionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="673b9-184">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="673b9-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="673b9-185">What's next?</span></span>
<span data-ttu-id="673b9-186">[Lección 7: Creación de indicadores clave de rendimiento](../tutorials/aas-lesson-7-create-key-performance-indicators.md)</span><span class="sxs-lookup"><span data-stu-id="673b9-186">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
