---
<span data-ttu-id="9f3b8-101">título: aaa "lección complementaria tutorial de Analysis Services de Azure: filas de detalles | Descripción de Microsoft Docs": describe cómo toocreate una expresión de filas de detalle de Hola tutorial de Azure de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="9f3b8-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="9f3b8-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="9f3b8-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="9f3b8-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="9f3b8-104">Lección complementaria: Filas de detalles</span><span class="sxs-lookup"><span data-stu-id="9f3b8-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9f3b8-105">En esta lección complementaria, utilice Hola Editor DAX toodefine una expresión personalizada de filas de detalle.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="9f3b8-106">Una expresión de filas de detalles es una propiedad en una medida, proporciona más información acerca de los resultados de hello agregado de una medida de los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="9f3b8-107">Estimado toocomplete de tiempo en esta lección: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="9f3b8-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9f3b8-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f3b8-108">Prerequisites</span></span>  
<span data-ttu-id="9f3b8-109">Esta lección complementaria forma parte de un tutorial de modelado tabular.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="9f3b8-110">Antes de realizar tareas de hello en esta lección complementaria, deberá haber finalizado todas las lecciones anteriores o tiene un proyecto de modelo de ejemplo Adventure Works Internet Sales completado.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="9f3b8-111">¿Qué debemos toosolve?</span><span class="sxs-lookup"><span data-stu-id="9f3b8-111">What do we need toosolve?</span></span>
<span data-ttu-id="9f3b8-112">Echemos un vistazo a los detalles de hello de la medida InternetTotalSales, antes de agregar una expresión de filas de detalle.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="9f3b8-113">En SSDT, haga clic en hello **modelo** menú > **analizar en Excel** tooopen Excel y cree una tabla dinámica en blanco.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="9f3b8-114">En **PivotTable Fields**, agregar hello **InternetTotalSales** demasiado de medida de la tabla de hello FactInternetSales**valores**, **CalendarYear**de hello DimDate tabla demasiado**columnas**, y **Spanishcountryregionname** demasiado**filas**.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="9f3b8-115">La tabla dinámica ahora obtenemos resultados agregados de medida de hello InternetTotalSales por regiones y año.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="9f3b8-117">Hola tabla dinámica, haga doble clic en un valor agregado para un año y un nombre de región.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="9f3b8-118">A continuación se hace doble clic en valor de Hola para hello y Australia año 2014.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="9f3b8-119">Se abre una nueva hoja que contiene datos, pero los datos no resultan de utilidad.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="9f3b8-121">¿Qué le gustaría toosee aquí es una tabla que contiene columnas y filas de datos que contribuyen toohello agrega el resultado de la medida InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="9f3b8-122">toodo que, podemos agregar una expresión de filas de detalles como una propiedad de medida de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="9f3b8-123">Adición de una expresión de filas de detalles</span><span class="sxs-lookup"><span data-stu-id="9f3b8-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="9f3b8-124">toocreate una expresión de filas de detalle</span><span class="sxs-lookup"><span data-stu-id="9f3b8-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="9f3b8-125">En SSDT, en la cuadrícula de medidas de la tabla de hello FactInternetSales, haga clic en hello **InternetTotalSales** medida.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="9f3b8-126">En **propiedades** > **expresión de filas de detalle**, haga clic en Hola de tooopen de botón Hola editor Editor de DAX.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="9f3b8-128">En el Editor de DAX, escriba Hola siguiente expresión:</span><span class="sxs-lookup"><span data-stu-id="9f3b8-128">In DAX Editor, enter hello following expression:</span></span>

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

    <span data-ttu-id="9f3b8-129">Esta expresión especifica nombres de columnas, y se devuelven resultados de medida de la tabla FactInternetSales de Hola y las tablas relacionadas cuando un usuario hace doble clic en un resultado agregado en una tabla dinámica o informe.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="9f3b8-130">En Excel, eliminar hoja Hola creado en el paso 3, a continuación, haga doble clic en un valor agregado.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="9f3b8-131">Esta vez, con una propiedad de expresión de filas de detalle definida para la medida de hello, una nueva hoja abre que contienen datos mucho más útiles.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="9f3b8-133">Vuelva a implementar el modelo.</span><span class="sxs-lookup"><span data-stu-id="9f3b8-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="9f3b8-134">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9f3b8-134">See Also</span></span>  
<span data-ttu-id="9f3b8-135">[Función SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="9f3b8-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="9f3b8-136">Lección complementaria: Seguridad dinámica</span><span class="sxs-lookup"><span data-stu-id="9f3b8-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="9f3b8-137">Lección complementaria: Jerarquías desiguales</span><span class="sxs-lookup"><span data-stu-id="9f3b8-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
