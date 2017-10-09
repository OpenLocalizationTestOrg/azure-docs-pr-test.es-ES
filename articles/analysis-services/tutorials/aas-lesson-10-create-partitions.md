---
<span data-ttu-id="48234-101">título: aaa "lección tutorial de Analysis Services de Azure 10: crear particiones | Descripción de Microsoft Docs": describe cómo toocreate particiones en el proyecto tutorial de hello Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="48234-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="48234-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="48234-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="48234-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="48234-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="48234-104">Lección 10: Creación de particiones</span><span class="sxs-lookup"><span data-stu-id="48234-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="48234-105">En esta lección, creará la tabla de particiones toodivide hello FactInternetSales en piezas lógicas más pequeñas que pueden ser procesado independiente (actualizar) de las demás particiones.</span><span class="sxs-lookup"><span data-stu-id="48234-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="48234-106">De forma predeterminada, cada tabla que se incluye en el modelo tiene una partición, lo que incluye la tabla Hola todas las columnas y filas.</span><span class="sxs-lookup"><span data-stu-id="48234-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="48234-107">Para la tabla FactInternetSales de hello, queremos que los datos de hello toodivide por año; una partición para cada uno de los cinco años de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="48234-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="48234-108">Así, cada partición se podrá procesar de manera independiente.</span><span class="sxs-lookup"><span data-stu-id="48234-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="48234-109">más información, consulte toolearn [particiones](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="48234-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="48234-110">Estimado toocomplete de tiempo en esta lección: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="48234-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="48234-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48234-111">Prerequisites</span></span>  
<span data-ttu-id="48234-112">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="48234-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="48234-113">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 9: crear jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="48234-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="48234-114">Creación de particiones</span><span class="sxs-lookup"><span data-stu-id="48234-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="48234-115">toocreate particiones de tabla de hello FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="48234-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="48234-116">En el Explorador de modelos tabulares, expanda **Tablas** y haga clic con el botón derecho en **FactInternetSales** > **Particiones**.</span><span class="sxs-lookup"><span data-stu-id="48234-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="48234-117">En el Administrador de particiones, haga clic en **copia**y, a continuación, cambiar nombre de hello demasiado**FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="48234-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="48234-118">Porque desea Hola partición tooinclude sólo aquellas filas en un período determinado, para el año 2010, de hello debe modificar la expresión de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="48234-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="48234-119">Haga clic en **diseño** tooopen Editor de consultas y, a continuación, haga clic en hello **FactInternetSales2010** consulta.</span><span class="sxs-lookup"><span data-stu-id="48234-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="48234-120">En la vista previa, haga clic en hello flecha abajo en hello **OrderDate** encabezado de columna y, a continuación, haga clic en **filtros de fecha y hora** > **entre**.</span><span class="sxs-lookup"><span data-stu-id="48234-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="48234-122">En el cuadro de diálogo Filtrar filas de hello, en **mostrar filas donde: OrderDate**, deje **es posterior o igual a**y, a continuación, en el campo de fecha de hello, escriba **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="48234-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="48234-123">Deje hello **y** operador seleccionado, a continuación, seleccione **antes**, a continuación, en el campo de fecha de hello, escriba **/1/1/2011**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="48234-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="48234-125">Observe que en PASOS APLICADOS del Editor de consultas encontrará otro paso denominado Filas filtradas.</span><span class="sxs-lookup"><span data-stu-id="48234-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="48234-126">Este filtro es tooselect solo las fechas de pedidos de 2010.</span><span class="sxs-lookup"><span data-stu-id="48234-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="48234-127">Haga clic en **Import**.</span><span class="sxs-lookup"><span data-stu-id="48234-127">Click **Import**.</span></span>

    <span data-ttu-id="48234-128">En el Administrador de particiones, tenga en cuenta consulta Hola expresión ahora tiene una cláusula de filtrado de filas adicional.</span><span class="sxs-lookup"><span data-stu-id="48234-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="48234-130">Esta instrucción especifica que esta partición debe incluir solo datos de hello en las filas donde hello OrderDate es Hola año 2010 tal como se especifica en la cláusula de filtrado de filas de Hola.</span><span class="sxs-lookup"><span data-stu-id="48234-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="48234-131">toocreate una partición para hello año 2011</span><span class="sxs-lookup"><span data-stu-id="48234-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="48234-132">En la lista de particiones de hello, haga clic en hello **FactInternetSales2010** de partición que creó y, a continuación, haga clic en **copia**.</span><span class="sxs-lookup"><span data-stu-id="48234-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="48234-133">Cambiar el nombre de la partición de hello demasiado**FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="48234-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="48234-134">No es necesario toouse Editor de consultas toocreate una nueva cláusula de filtrado de filas.</span><span class="sxs-lookup"><span data-stu-id="48234-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="48234-135">Porque se ha creado una copia de la consulta de Hola para 2010, todo lo que necesita toodo es realizar un pequeño cambio en consulta Hola de 2011.</span><span class="sxs-lookup"><span data-stu-id="48234-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="48234-136">En **expresión de consulta**, en orden para esta partición tooinclude sólo aquellas filas para hello año 2011, reemplace los años Hola de cláusula de filtrado de filas de hello tiene **2011** y **2012**, respectivamente, al igual que:</span><span class="sxs-lookup"><span data-stu-id="48234-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="48234-137">particiones de toocreate de 2012, 2013 y 2014.</span><span class="sxs-lookup"><span data-stu-id="48234-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="48234-138">Siga los pasos anteriores hello, creación de particiones de 2012, 2013 y 2014, cambiar años de hello en hello filtrar filas cláusula tooinclude solo las filas correspondientes a ese año.</span><span class="sxs-lookup"><span data-stu-id="48234-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="48234-139">Eliminar hello FactInternetSales partición</span><span class="sxs-lookup"><span data-stu-id="48234-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="48234-140">Ahora que tiene particiones para cada año, puede eliminar la partición de hello FactInternetSales; al elegir todos los procesos cuando el procesamiento de particiones, que impiden que se superponen.</span><span class="sxs-lookup"><span data-stu-id="48234-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="48234-141">Hola toodelete FactInternetSales partición</span><span class="sxs-lookup"><span data-stu-id="48234-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="48234-142">Haga clic en hello FactInternetSales partición y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="48234-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="48234-143">Procesar las particiones</span><span class="sxs-lookup"><span data-stu-id="48234-143">Process partitions</span></span>  
<span data-ttu-id="48234-144">En el Administrador de particiones, tenga en cuenta hello **procesa última** columna para cada una de las nuevas particiones Hola creaste muestra estas particiones nunca se han procesado.</span><span class="sxs-lookup"><span data-stu-id="48234-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="48234-145">Al crear particiones, se deben ejecutar un procesar particiones o datos de tabla de proceso operación toorefresh hello en esas particiones.</span><span class="sxs-lookup"><span data-stu-id="48234-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="48234-146">tooprocess Hola FactInternetSales particiones</span><span class="sxs-lookup"><span data-stu-id="48234-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="48234-147">Haga clic en **Aceptar** tooclose Administrador de particiones.</span><span class="sxs-lookup"><span data-stu-id="48234-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="48234-148">Haga clic en hello **FactInternetSales** de tabla, a continuación, haga clic en hello **modelo** menú > **proceso** > **procesar particiones**.</span><span class="sxs-lookup"><span data-stu-id="48234-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="48234-149">En el cuadro de diálogo procesar particiones de hello, compruebe **modo** se establece demasiado**proceso predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="48234-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="48234-150">Active la casilla de verificación de Hola Hola **proceso** columna para cada uno de hello cinco particiones que ha creado y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="48234-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="48234-152">Si se le pide las credenciales de suplantación, escriba el nombre de usuario de Windows hello y la contraseña que especificó en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="48234-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="48234-153">Hola **procesamiento de datos** cuadro de diálogo aparece y muestra los detalles del proceso para cada partición.</span><span class="sxs-lookup"><span data-stu-id="48234-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="48234-154">Tenga en cuenta que se transfiere un número de filas diferente para cada partición.</span><span class="sxs-lookup"><span data-stu-id="48234-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="48234-155">Cada partición incluye solamente las filas para el año de hello especificado en la cláusula WHERE de la instrucción SQL Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="48234-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="48234-156">Cuando finalice el procesamiento, continúe y cerrar el cuadro de diálogo de procesamiento de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48234-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="48234-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48234-158">What's next?</span></span>
<span data-ttu-id="48234-159">Vaya toohello siguiente lección: [lección 11: crear Roles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="48234-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
