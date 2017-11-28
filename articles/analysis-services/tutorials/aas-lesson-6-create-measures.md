---
<span data-ttu-id="28567-101">título: aaa "lección tutorial de Analysis Services de Azure 6: crear medidas | Descripción de Microsoft Docs": describe cómo toocreate se mide en el proyecto tutorial de hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="28567-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="28567-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="28567-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="28567-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="28567-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="28567-104">Lección 6: Creación de medidas</span><span class="sxs-lookup"><span data-stu-id="28567-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="28567-105">En esta lección, creará toobe medidas incluida en el modelo.</span><span class="sxs-lookup"><span data-stu-id="28567-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="28567-106">Toohello similar calcula columnas que creó, una medida es un cálculo creado usando una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="28567-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="28567-107">Sin embargo, a diferencia de las columnas calculadas, las medidas se evalúan en función de un *filtro* seleccionado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="28567-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="28567-108">Por ejemplo, una columna o una segmentación agrega toohello campo de etiquetas de fila en una tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="28567-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="28567-109">A continuación, se calcula un valor para cada celda de filtro de Hola por medida Hola aplicado.</span><span class="sxs-lookup"><span data-stu-id="28567-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="28567-110">Las medidas son cálculos eficaces y flexibles que desea tooinclude en casi todos los modelos tabulares tooperform dinámica los cálculos sobre datos numéricos.</span><span class="sxs-lookup"><span data-stu-id="28567-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="28567-111">más información, consulte toolearn [medidas](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="28567-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="28567-112">medidas de toocreate, usas Hola *cuadrícula de medidas*.</span><span class="sxs-lookup"><span data-stu-id="28567-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="28567-113">De forma predeterminada, cada tabla tiene una cuadrícula de medidas vacía, aunque en principio no se crean medidas para todas las tablas.</span><span class="sxs-lookup"><span data-stu-id="28567-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="28567-114">cuadrícula de medidas de Hello aparece debajo de una tabla en el Diseñador de modelos de hello en la vista de datos.</span><span class="sxs-lookup"><span data-stu-id="28567-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="28567-115">toohide o mostrar cuadrícula de medidas de Hola para una tabla, haga clic en hello **tabla** menú y, a continuación, haga clic en **Mostrar cuadrícula de medidas**.</span><span class="sxs-lookup"><span data-stu-id="28567-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="28567-116">Puede crear una medida haciendo clic en una celda vacía de la cuadrícula de medidas de Hola y, a continuación, escribiendo una fórmula DAX en la barra de fórmulas de Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="28567-117">Cuando haga clic en entrar toocomplete Hola fórmula, medida de Hola y aparece en la celda de Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="28567-118">También puede crear medidas mediante una función de agregación estándar haciendo clic en una columna y, a continuación, haga clic en Hola botón de Autosuma (**∑**) en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="28567-119">Las medidas creadas mediante la característica de Autosuma Hola aparecen en la celda de cuadrícula de medida de hello directamente debajo de la columna de hello, pero se pueden mover.</span><span class="sxs-lookup"><span data-stu-id="28567-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="28567-120">En esta lección, creará medidas escribiendo una fórmula DAX en la barra de fórmulas de Hola y mediante el uso de la característica de Autosuma Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="28567-121">Estimado toocomplete de tiempo en esta lección: **30 minutos**</span><span class="sxs-lookup"><span data-stu-id="28567-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="28567-122">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="28567-122">Prerequisites</span></span>  
<span data-ttu-id="28567-123">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="28567-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="28567-124">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 5: crear columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).</span><span class="sxs-lookup"><span data-stu-id="28567-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="28567-125">Crear medidas</span><span class="sxs-lookup"><span data-stu-id="28567-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="28567-126">una medida DaysCurrentQuarterToDate en la tabla DimDate de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="28567-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="28567-127">En el Diseñador de modelos de hello, haga clic en hello **DimDate** tabla.</span><span class="sxs-lookup"><span data-stu-id="28567-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="28567-128">En la cuadrícula de medidas de hello, haga clic en celda vacía superior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="28567-129">En la barra de fórmulas de hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="28567-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="28567-130">Celda superior izquierda de anuncio Hola ahora contiene un nombre de medida, **DaysCurrentQuarterToDate**, seguido del resultado de hello, **92**.</span><span class="sxs-lookup"><span data-stu-id="28567-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="28567-132">A diferencia de las columnas calculadas, con fórmulas de medida puede escribir nombre de medida de hello, seguido de dos puntos, seguido por la expresión de la fórmula Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="28567-133">una medida DaysInCurrentQuarter en la tabla DimDate de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="28567-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="28567-134">Con hello **DimDate** tabla sigue activa en el Diseñador de modelos de hello, en la cuadrícula de medidas de hello, haga clic en la celda vacía de hello debajo de la medida de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="28567-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="28567-135">En la barra de fórmulas de hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="28567-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="28567-136">Al crear una relación de comparación entre un período incompleto y Hola período anterior.</span><span class="sxs-lookup"><span data-stu-id="28567-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="28567-137">fórmula de Hello debe calcular la proporción de Hola de período de Hola que ha transcurrido y compararla toohello igual proporción Hola del período anterior.</span><span class="sxs-lookup"><span data-stu-id="28567-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="28567-138">En este caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] proporciona Hola proporción transcurrido en hello período actual.</span><span class="sxs-lookup"><span data-stu-id="28567-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="28567-139">una medida de InternetDistinctCountSalesOrder en la tabla FactInternetSales de hello toocreate</span><span class="sxs-lookup"><span data-stu-id="28567-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="28567-140">Haga clic en hello **FactInternetSales** tabla.</span><span class="sxs-lookup"><span data-stu-id="28567-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="28567-141">Haga clic en hello **SalesOrderNumber** encabezado de columna.</span><span class="sxs-lookup"><span data-stu-id="28567-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="28567-142">En la barra de herramientas de hello, haga clic en hello flecha abajo siguiente toohello Autosuma (**∑**) y, a continuación, seleccione **DistinctCount**.</span><span class="sxs-lookup"><span data-stu-id="28567-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="28567-143">característica de Autosuma Hola automáticamente crea una medida para la columna seleccionada de hello mediante la fórmula de agregación estándar de hello DistinctCount.</span><span class="sxs-lookup"><span data-stu-id="28567-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="28567-145">En la cuadrícula de medidas de hello, haga clic en nueva medida hello y, a continuación, en hello **propiedades** ventana, en **nombre de medida**, cambiar el nombre de medida de hello demasiado**InternetDistinctCountSalesOrder**.</span><span class="sxs-lookup"><span data-stu-id="28567-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="28567-146">toocreate saber qué medidas adicionales en la tabla FactInternetSales de Hola</span><span class="sxs-lookup"><span data-stu-id="28567-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="28567-147">Mediante la característica de Autosuma de hello, crear y asigne un nombre hello siguientes medidas:</span><span class="sxs-lookup"><span data-stu-id="28567-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="28567-148">Columna</span><span class="sxs-lookup"><span data-stu-id="28567-148">Column</span></span>|<span data-ttu-id="28567-149">Nombre de la medida</span><span class="sxs-lookup"><span data-stu-id="28567-149">Measure name</span></span>|<span data-ttu-id="28567-150">Autosuma (∑)</span><span class="sxs-lookup"><span data-stu-id="28567-150">AutoSum (∑)</span></span>|<span data-ttu-id="28567-151">Fórmula</span><span class="sxs-lookup"><span data-stu-id="28567-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="28567-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="28567-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="28567-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="28567-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="28567-154">Recuento</span><span class="sxs-lookup"><span data-stu-id="28567-154">Count</span></span>|<span data-ttu-id="28567-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="28567-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="28567-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="28567-156">OrderQuantity</span></span>|<span data-ttu-id="28567-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="28567-157">InternetTotalUnits</span></span>|<span data-ttu-id="28567-158">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-158">Sum</span></span>|<span data-ttu-id="28567-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="28567-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="28567-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="28567-160">DiscountAmount</span></span>|<span data-ttu-id="28567-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="28567-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="28567-162">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-162">Sum</span></span>|<span data-ttu-id="28567-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="28567-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="28567-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="28567-164">TotalProductCost</span></span>|<span data-ttu-id="28567-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="28567-165">InternetTotalProductCost</span></span>|<span data-ttu-id="28567-166">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-166">Sum</span></span>|<span data-ttu-id="28567-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="28567-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="28567-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="28567-168">SalesAmount</span></span>|<span data-ttu-id="28567-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="28567-169">InternetTotalSales</span></span>|<span data-ttu-id="28567-170">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-170">Sum</span></span>|<span data-ttu-id="28567-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="28567-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="28567-172">Margin</span><span class="sxs-lookup"><span data-stu-id="28567-172">Margin</span></span>|<span data-ttu-id="28567-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="28567-173">InternetTotalMargin</span></span>|<span data-ttu-id="28567-174">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-174">Sum</span></span>|<span data-ttu-id="28567-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="28567-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="28567-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="28567-176">TaxAmt</span></span>|<span data-ttu-id="28567-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="28567-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="28567-178">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-178">Sum</span></span>|<span data-ttu-id="28567-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="28567-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="28567-180">Freight</span><span class="sxs-lookup"><span data-stu-id="28567-180">Freight</span></span>|<span data-ttu-id="28567-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="28567-181">InternetTotalFreight</span></span>|<span data-ttu-id="28567-182">Suma</span><span class="sxs-lookup"><span data-stu-id="28567-182">Sum</span></span>|<span data-ttu-id="28567-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="28567-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="28567-184">Haciendo clic en crear una celda vacía en la cuadrícula de medidas de Hola y mediante el uso de la barra de fórmulas de hello, y mide el nombre detrás de hello en orden:</span><span class="sxs-lookup"><span data-stu-id="28567-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
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
  
<span data-ttu-id="28567-185">Las medidas creadas para la tabla FactInternetSales de hello pueden ser usado tooanalyze de datos financieros críticos como ventas, costos y margen de beneficio para los elementos definidos por el filtro seleccionado de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="28567-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="28567-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28567-186">What's next?</span></span>
<span data-ttu-id="28567-187">[Lección 7: Creación de indicadores clave de rendimiento](../tutorials/aas-lesson-7-create-key-performance-indicators.md)</span><span class="sxs-lookup"><span data-stu-id="28567-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
