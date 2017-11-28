---
<span data-ttu-id="a05f6-101">título: aaa "lección de Azure Analysis Services tutorial 5: crear columnas calculadas | Descripción de Microsoft Docs": describe cómo toocreate calcula las columnas en el proyecto tutorial de hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="a05f6-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="a05f6-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="a05f6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="a05f6-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="a05f6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="a05f6-104">Lección 5: Creación de columnas calculadas</span><span class="sxs-lookup"><span data-stu-id="a05f6-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="a05f6-105">En esta lección, se crean datos en el modelo mediante la adición de columnas calculadas.</span><span class="sxs-lookup"><span data-stu-id="a05f6-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="a05f6-106">Puede crear columnas calculadas (como columnas personalizadas) cuando se usa obtener datos, utilizando el Editor de consultas Hola o, más adelante en el tipo de diseñador de modelo de hello hacer aquí.</span><span class="sxs-lookup"><span data-stu-id="a05f6-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="a05f6-107">más información, consulte toolearn [columnas calculadas](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span><span class="sxs-lookup"><span data-stu-id="a05f6-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="a05f6-108">Creará cinco columnas calculadas en tres tablas diferentes.</span><span class="sxs-lookup"><span data-stu-id="a05f6-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="a05f6-109">Hola pasos son ligeramente diferentes para cada tarea que muestra que hay varias maneras de toocreate columnas, cambiarles el nombre y colocarlos en varias ubicaciones en una tabla.</span><span class="sxs-lookup"><span data-stu-id="a05f6-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="a05f6-110">En esta lección también usará por primera vez Expresiones de análisis de datos (DAX).</span><span class="sxs-lookup"><span data-stu-id="a05f6-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="a05f6-111">DAX es un lenguaje especial para crear expresiones de fórmula altamente personalizables para modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="a05f6-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="a05f6-112">En este tutorial, utilice DAX toocreate calculado columnas, medidas y filtros de rol.</span><span class="sxs-lookup"><span data-stu-id="a05f6-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="a05f6-113">más información, consulte toolearn [DAX en modelos tabulares](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="a05f6-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="a05f6-114">Estimado toocomplete de tiempo en esta lección: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="a05f6-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a05f6-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a05f6-115">Prerequisites</span></span>  
<span data-ttu-id="a05f6-116">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="a05f6-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="a05f6-117">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 4: crear relaciones](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="a05f6-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="a05f6-118">Crear columnas calculadas</span><span class="sxs-lookup"><span data-stu-id="a05f6-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="a05f6-119">Crear una columna calculada MonthCalendar en la tabla DimDate de Hola</span><span class="sxs-lookup"><span data-stu-id="a05f6-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="a05f6-120">Haga clic en hello **modelo** menú > **vista de modelo** > **vista de datos**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="a05f6-121">Las columnas calculadas solo pueden crearse mediante el Diseñador de modelo de hello en la vista de datos.</span><span class="sxs-lookup"><span data-stu-id="a05f6-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="a05f6-122">En el Diseñador de modelos de hello, haga clic en hello **DimDate** tabla (pestaña).</span><span class="sxs-lookup"><span data-stu-id="a05f6-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="a05f6-123">Menú contextual hello **CalendarQuarter** encabezado de columna y, a continuación, haga clic en **Insertar columna**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="a05f6-124">Una nueva columna denominada **calcula columna 1** quede toohello insertado de hello **Calendar Quarter** columna.</span><span class="sxs-lookup"><span data-stu-id="a05f6-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="a05f6-125">En la barra de fórmulas de Hola por encima de la tabla de hello, escriba Hola después de la fórmula DAX: Hola de Autocompletar le ayuda a escribir los nombres completos de columnas y tablas y listas de Hola funciones que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="a05f6-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="a05f6-126">A continuación, se rellenan valores para todas las filas de hello en la columna calculada Hola.</span><span class="sxs-lookup"><span data-stu-id="a05f6-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="a05f6-127">Si se desplaza hacia abajo por la tabla hello, verá las filas pueden tener valores diferentes para esta columna se basa en datos de hello en cada fila.</span><span class="sxs-lookup"><span data-stu-id="a05f6-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="a05f6-128">Cambiar el nombre de esta columna demasiado**MonthCalendar**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="a05f6-130">columna calculada de Hello MonthCalendar proporciona un nombre que se puede ordenar por mes.</span><span class="sxs-lookup"><span data-stu-id="a05f6-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="a05f6-131">Crear una columna calculada DayOfWeek de tabla de DimDate Hola</span><span class="sxs-lookup"><span data-stu-id="a05f6-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="a05f6-132">Con hello **DimDate** tabla sigue activa, haga clic en hello **columna** menú y, a continuación, haga clic en **Agregar columna**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="a05f6-133">En la barra de fórmulas de hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="a05f6-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="a05f6-134">Cuando haya terminado de crear Hola fórmula, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="a05f6-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="a05f6-135">Hola nueva columna se agrega más a la derecha de la tabla de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="a05f6-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="a05f6-136">Cambiar el nombre de columna de hello demasiado**DayOfWeek**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="a05f6-137">Haga clic en el encabezado de columna de Hola y a continuación, arrastre la columna Hola entre hello **EnglishDayNameOfWeek** hello y columna **DayNumberOfMonth** columna.</span><span class="sxs-lookup"><span data-stu-id="a05f6-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="a05f6-138">Movimiento de columnas en la tabla hace más fácil toonavigate.</span><span class="sxs-lookup"><span data-stu-id="a05f6-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="a05f6-139">columna calculada de Hello DayOfWeek proporciona un nombre ordenable del día de saludo de la semana.</span><span class="sxs-lookup"><span data-stu-id="a05f6-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="a05f6-140">Crear una columna calculada ProductSubcategoryName en la tabla DimProduct de Hola</span><span class="sxs-lookup"><span data-stu-id="a05f6-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="a05f6-141">Hola **DimProduct** tabla, desplácese toohello más a la derecha de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="a05f6-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="a05f6-142">Columna del extremo derecho de Hola de aviso se denomina **Agregar columna** (en cursiva), haga clic en el encabezado de columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="a05f6-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="a05f6-143">En la barra de fórmulas de hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="a05f6-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="a05f6-144">Cambiar el nombre de columna de hello demasiado**ProductSubcategoryName**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="a05f6-145">columna calculada de Hello ProductSubcategoryName es toocreate usa una jerarquía en la tabla DimProduct de hello, que incluye datos de columna de hello EnglishProductSubcategoryName en la tabla DimProductSubcategory de Hola.</span><span class="sxs-lookup"><span data-stu-id="a05f6-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="a05f6-146">Las jerarquías no pueden abarcar más de una tabla.</span><span class="sxs-lookup"><span data-stu-id="a05f6-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="a05f6-147">Creará jerarquías más adelante en la lección 9.</span><span class="sxs-lookup"><span data-stu-id="a05f6-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="a05f6-148">Crear una columna calculada ProductCategoryName en la tabla DimProduct de Hola</span><span class="sxs-lookup"><span data-stu-id="a05f6-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="a05f6-149">Con hello **DimProduct** tabla sigue activa, haga clic en hello **columna** menú y, a continuación, haga clic en **Agregar columna**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="a05f6-150">En la barra de fórmulas de hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="a05f6-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="a05f6-151">Cambiar el nombre de columna de hello demasiado**ProductCategoryName**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="a05f6-152">columna calculada de Hello ProductCategoryName es toocreate usa una jerarquía en la tabla DimProduct de hello, que incluye datos de columna de hello EnglishProductCategoryName en la tabla de DimProductCategory Hola.</span><span class="sxs-lookup"><span data-stu-id="a05f6-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="a05f6-153">Las jerarquías no pueden abarcar más de una tabla.</span><span class="sxs-lookup"><span data-stu-id="a05f6-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="a05f6-154">Crear una columna calculada margen en la tabla FactInternetSales de Hola</span><span class="sxs-lookup"><span data-stu-id="a05f6-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="a05f6-155">En el Diseñador de modelos de hello, seleccione hello **FactInternetSales** tabla.</span><span class="sxs-lookup"><span data-stu-id="a05f6-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="a05f6-156">Crear una nueva columna calculada entre hello **SalesAmount** hello y columna **TaxAmt** columna.</span><span class="sxs-lookup"><span data-stu-id="a05f6-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="a05f6-157">En la barra de fórmulas de hello, escriba Hola siguiente fórmula:</span><span class="sxs-lookup"><span data-stu-id="a05f6-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="a05f6-158">Cambiar el nombre de columna de hello demasiado**margen**.</span><span class="sxs-lookup"><span data-stu-id="a05f6-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="a05f6-160">columna calculada de margen de Hello es tooanalyze usado los márgenes de beneficios de cada venta.</span><span class="sxs-lookup"><span data-stu-id="a05f6-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="a05f6-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a05f6-161">What's next?</span></span>
<span data-ttu-id="a05f6-162">[Lección 6: Creación de medidas](../tutorials/aas-lesson-6-create-measures.md)</span><span class="sxs-lookup"><span data-stu-id="a05f6-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
