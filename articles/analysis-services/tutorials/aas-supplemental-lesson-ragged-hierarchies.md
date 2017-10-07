---
<span data-ttu-id="9f409-101">título: aaa "lección complementaria tutorial de Analysis Services de Azure: jerarquías desiguales | Descripción de Microsoft Docs": describe cómo toofix jerarquías desiguales hello Azure tutorial de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9f409-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Ragged hierarchies | Microsoft Docs" description: Describes how toofix ragged hierarchies in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="9f409-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="9f409-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="9f409-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 26/05/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="9f409-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---ragged-hierarchies"></a><span data-ttu-id="9f409-104">Lección complementaria: Jerarquías desiguales</span><span class="sxs-lookup"><span data-stu-id="9f409-104">Supplemental lesson - Ragged hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="9f409-105">En esta lección complementaria, resolverá un problema común que se produce al dinamizar en jerarquías que contienen valores en blanco (miembros) en distintos niveles.</span><span class="sxs-lookup"><span data-stu-id="9f409-105">In this supplemental lesson, you resolve a common problem when pivoting on hierarchies that contain blank values (members) at different levels.</span></span> <span data-ttu-id="9f409-106">Un ejemplo de esto sería una organización donde un director de alto nivel tiene como subordinados directos a directores de departamento y a trabajadores que no son directores.</span><span class="sxs-lookup"><span data-stu-id="9f409-106">For example, an organization where a high-level manager has both departmental managers and non-managers as direct reports.</span></span> <span data-ttu-id="9f409-107">O bien, las jerarquías geográficas formadas por país-región-ciudad, donde algunas ciudades no tienen un elemento primario de estado o provincia, como Washington D. C. o Ciudad del Vaticano.</span><span class="sxs-lookup"><span data-stu-id="9f409-107">Or, geographic hierarchies composed of Country-Region-City, where some cities lack a parent State or Province, such as Washington D.C., Vatican City.</span></span> <span data-ttu-id="9f409-108">Cuando una jerarquía tiene miembros en blanco, a menudo desciende toodifferent o desigual, niveles.</span><span class="sxs-lookup"><span data-stu-id="9f409-108">When a hierarchy has blank members, it often descends toodifferent, or ragged, levels.</span></span>

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

<span data-ttu-id="9f409-110">Los modelos tabulares en el nivel de compatibilidad de hello 1400 tienen más **ocultar miembros** propiedad para las jerarquías.</span><span class="sxs-lookup"><span data-stu-id="9f409-110">Tabular models at hello 1400 compatibility level have an additional **Hide Members** property for hierarchies.</span></span> <span data-ttu-id="9f409-111">Hola **predeterminado** configuración supone que no hay ningún miembro en blanco en cualquier nivel.</span><span class="sxs-lookup"><span data-stu-id="9f409-111">hello **Default** setting assumes there are no blank members at any level.</span></span> <span data-ttu-id="9f409-112">Hola **ocultar miembros en blanco** configuración excluye los miembros en blanco de jerarquía de hello cuando agrega tooa tabla dinámica o informe.</span><span class="sxs-lookup"><span data-stu-id="9f409-112">hello **Hide blank members** setting excludes blank members from hello hierarchy when added tooa PivotTable or report.</span></span>  
  
<span data-ttu-id="9f409-113">Estimado toocomplete de tiempo en esta lección: **20 minutos**</span><span class="sxs-lookup"><span data-stu-id="9f409-113">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="9f409-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9f409-114">Prerequisites</span></span>  
<span data-ttu-id="9f409-115">Esta lección complementaria forma parte de un tutorial de modelado tabular.</span><span class="sxs-lookup"><span data-stu-id="9f409-115">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="9f409-116">Antes de realizar tareas de hello en esta lección complementaria, deberá haber finalizado todas las lecciones anteriores o tiene un proyecto de modelo de ejemplo Adventure Works Internet Sales completado.</span><span class="sxs-lookup"><span data-stu-id="9f409-116">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span> 

<span data-ttu-id="9f409-117">Si ha creado el proyecto de hello AW Internet Sales como parte del tutorial de hello, el modelo no contiene aún los datos o jerarquías desiguales.</span><span class="sxs-lookup"><span data-stu-id="9f409-117">If you've created hello AW Internet Sales project as part of hello tutorial, your model does not yet contain any data or hierarchies that are ragged.</span></span> <span data-ttu-id="9f409-118">toocomplete esta lección complementaria, primero tienes toocreate Hola problema agregando algunas tablas adicionales, crear una nueva jerarquía de organización, una medida, las columnas calculadas y relaciones.</span><span class="sxs-lookup"><span data-stu-id="9f409-118">toocomplete this supplemental lesson, you first have toocreate hello problem by adding some additional tables, create relationships, calculated columns, a measure, and a new Organization hierarchy.</span></span> <span data-ttu-id="9f409-119">Solo tardará unos 15 minutos en hacerlo.</span><span class="sxs-lookup"><span data-stu-id="9f409-119">That part takes about 15 minutes.</span></span> <span data-ttu-id="9f409-120">A continuación, obtener toosolve en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="9f409-120">Then, you get toosolve it in just a few minutes.</span></span>  

## <a name="add-tables-and-objects"></a><span data-ttu-id="9f409-121">Agregar tablas y objetos</span><span class="sxs-lookup"><span data-stu-id="9f409-121">Add tables and objects</span></span>
  
### <a name="tooadd-new-tables-tooyour-model"></a><span data-ttu-id="9f409-122">nuevo modelo de tooyour tablas tooadd</span><span class="sxs-lookup"><span data-stu-id="9f409-122">tooadd new tables tooyour model</span></span>
  
1.  <span data-ttu-id="9f409-123">En el Explorador de modelos tabulares, expanda **Orígenes de datos** y haga clic con el botón derecho en la conexión > **Importar nuevas tablas**.</span><span class="sxs-lookup"><span data-stu-id="9f409-123">In Tabular Model Explorer, expand **Data Sources**, then right-click your connection > **Import New Tables**.</span></span>
  
2.  <span data-ttu-id="9f409-124">En el navegador, seleccione **DimEmployee** y **FactResellerSales** y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9f409-124">In Navigator, select **DimEmployee** and **FactResellerSales**, and then click **OK**.</span></span>

3.  <span data-ttu-id="9f409-125">En el Editor de consultas, haga clic en **Importar**.</span><span class="sxs-lookup"><span data-stu-id="9f409-125">In Query Editor, click **Import**</span></span>

4.  <span data-ttu-id="9f409-126">Cree Hola siguiente [relaciones](../tutorials/aas-lesson-4-create-relationships.md):</span><span class="sxs-lookup"><span data-stu-id="9f409-126">Create hello following [relationships](../tutorials/aas-lesson-4-create-relationships.md):</span></span>

    | <span data-ttu-id="9f409-127">Tabla 1</span><span class="sxs-lookup"><span data-stu-id="9f409-127">Table 1</span></span>           | <span data-ttu-id="9f409-128">Columna</span><span class="sxs-lookup"><span data-stu-id="9f409-128">Column</span></span>       | <span data-ttu-id="9f409-129">Dirección del filtro</span><span class="sxs-lookup"><span data-stu-id="9f409-129">Filter Direction</span></span>   | <span data-ttu-id="9f409-130">Tabla 2</span><span class="sxs-lookup"><span data-stu-id="9f409-130">Table 2</span></span>     | <span data-ttu-id="9f409-131">Columna</span><span class="sxs-lookup"><span data-stu-id="9f409-131">Column</span></span>      | <span data-ttu-id="9f409-132">Active</span><span class="sxs-lookup"><span data-stu-id="9f409-132">Active</span></span> |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | <span data-ttu-id="9f409-133">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="9f409-133">FactResellerSales</span></span> | <span data-ttu-id="9f409-134">OrderDateKey</span><span class="sxs-lookup"><span data-stu-id="9f409-134">OrderDateKey</span></span> | <span data-ttu-id="9f409-135">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="9f409-135">Default</span></span>            | <span data-ttu-id="9f409-136">DimDate</span><span class="sxs-lookup"><span data-stu-id="9f409-136">DimDate</span></span>     | <span data-ttu-id="9f409-137">Date</span><span class="sxs-lookup"><span data-stu-id="9f409-137">Date</span></span>        | <span data-ttu-id="9f409-138">Sí</span><span class="sxs-lookup"><span data-stu-id="9f409-138">Yes</span></span>    |
    | <span data-ttu-id="9f409-139">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="9f409-139">FactResellerSales</span></span> | <span data-ttu-id="9f409-140">DueDate</span><span class="sxs-lookup"><span data-stu-id="9f409-140">DueDate</span></span>      | <span data-ttu-id="9f409-141">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="9f409-141">Default</span></span>            | <span data-ttu-id="9f409-142">DimDate</span><span class="sxs-lookup"><span data-stu-id="9f409-142">DimDate</span></span>     | <span data-ttu-id="9f409-143">Date</span><span class="sxs-lookup"><span data-stu-id="9f409-143">Date</span></span>        | <span data-ttu-id="9f409-144">No</span><span class="sxs-lookup"><span data-stu-id="9f409-144">No</span></span>     |
    | <span data-ttu-id="9f409-145">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="9f409-145">FactResellerSales</span></span> | <span data-ttu-id="9f409-146">ShipDateKey</span><span class="sxs-lookup"><span data-stu-id="9f409-146">ShipDateKey</span></span>  | <span data-ttu-id="9f409-147">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="9f409-147">Default</span></span>            | <span data-ttu-id="9f409-148">DimDate</span><span class="sxs-lookup"><span data-stu-id="9f409-148">DimDate</span></span>     | <span data-ttu-id="9f409-149">Date</span><span class="sxs-lookup"><span data-stu-id="9f409-149">Date</span></span>        | <span data-ttu-id="9f409-150">No</span><span class="sxs-lookup"><span data-stu-id="9f409-150">No</span></span>     |
    | <span data-ttu-id="9f409-151">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="9f409-151">FactResellerSales</span></span> | <span data-ttu-id="9f409-152">ProductKey</span><span class="sxs-lookup"><span data-stu-id="9f409-152">ProductKey</span></span>   | <span data-ttu-id="9f409-153">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="9f409-153">Default</span></span>            | <span data-ttu-id="9f409-154">DimProduct</span><span class="sxs-lookup"><span data-stu-id="9f409-154">DimProduct</span></span>  | <span data-ttu-id="9f409-155">ProductKey</span><span class="sxs-lookup"><span data-stu-id="9f409-155">ProductKey</span></span>  | <span data-ttu-id="9f409-156">Sí</span><span class="sxs-lookup"><span data-stu-id="9f409-156">Yes</span></span>    |
    | <span data-ttu-id="9f409-157">FactResellerSales</span><span class="sxs-lookup"><span data-stu-id="9f409-157">FactResellerSales</span></span> | <span data-ttu-id="9f409-158">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="9f409-158">EmployeeKey</span></span>  | <span data-ttu-id="9f409-159">Tablas de tooBoth</span><span class="sxs-lookup"><span data-stu-id="9f409-159">tooBoth Tables</span></span> | <span data-ttu-id="9f409-160">DimEmployee</span><span class="sxs-lookup"><span data-stu-id="9f409-160">DimEmployee</span></span> | <span data-ttu-id="9f409-161">EmployeeKey</span><span class="sxs-lookup"><span data-stu-id="9f409-161">EmployeeKey</span></span> | <span data-ttu-id="9f409-162">Sí</span><span class="sxs-lookup"><span data-stu-id="9f409-162">Yes</span></span>    |

5. <span data-ttu-id="9f409-163">Hola **DimEmployee** de tabla, cree Hola siguiente [columnas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md):</span><span class="sxs-lookup"><span data-stu-id="9f409-163">In hello **DimEmployee** table, create hello following [calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md):</span></span> 

    <span data-ttu-id="9f409-164">**Ruta de acceso**</span><span class="sxs-lookup"><span data-stu-id="9f409-164">**Path**</span></span> 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    <span data-ttu-id="9f409-165">**FullName**</span><span class="sxs-lookup"><span data-stu-id="9f409-165">**FullName**</span></span> 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    <span data-ttu-id="9f409-166">**Level1**</span><span class="sxs-lookup"><span data-stu-id="9f409-166">**Level1**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    <span data-ttu-id="9f409-167">**Level2**</span><span class="sxs-lookup"><span data-stu-id="9f409-167">**Level2**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    <span data-ttu-id="9f409-168">**Level3**</span><span class="sxs-lookup"><span data-stu-id="9f409-168">**Level3**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    <span data-ttu-id="9f409-169">**Level4**</span><span class="sxs-lookup"><span data-stu-id="9f409-169">**Level4**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    <span data-ttu-id="9f409-170">**Level5**</span><span class="sxs-lookup"><span data-stu-id="9f409-170">**Level5**</span></span> 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  <span data-ttu-id="9f409-171">Hola **DimEmployee** de tabla, cree un [jerarquía](../tutorials/aas-lesson-9-create-hierarchies.md) denominado **organización**.</span><span class="sxs-lookup"><span data-stu-id="9f409-171">In hello **DimEmployee** table, create a [hierarchy](../tutorials/aas-lesson-9-create-hierarchies.md) named **Organization**.</span></span> <span data-ttu-id="9f409-172">Agregar Hola siguiendo en orden de columnas: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span><span class="sxs-lookup"><span data-stu-id="9f409-172">Add hello following columns in-order: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.</span></span>

7.  <span data-ttu-id="9f409-173">Hola **FactResellerSales** de tabla, cree Hola siguiente [medida](../tutorials/aas-lesson-6-create-measures.md):</span><span class="sxs-lookup"><span data-stu-id="9f409-173">In hello **FactResellerSales** table, create hello following [measure](../tutorials/aas-lesson-6-create-measures.md):</span></span>

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  <span data-ttu-id="9f409-174">Use [analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel y crear automáticamente una tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="9f409-174">Use [Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel and automatically create a PivotTable.</span></span>

9.  <span data-ttu-id="9f409-175">En **PivotTable Fields**, agregar hello **organización** jerarquía de hello **DimEmployee** tabla demasiado**filas**, hello y**ResellerTotalSales** medida de hello **FactResellerSales** tabla demasiado**valores**.</span><span class="sxs-lookup"><span data-stu-id="9f409-175">In **PivotTable Fields**, add hello **Organization** hierarchy from hello **DimEmployee** table too**Rows**, and hello **ResellerTotalSales** measure from hello **FactResellerSales**  table too**Values**.</span></span>

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    <span data-ttu-id="9f409-177">Como puede ver en la tabla dinámica de hello, jerarquía de hello muestra las filas que son desiguales.</span><span class="sxs-lookup"><span data-stu-id="9f409-177">As you can see in hello PivotTable, hello hierarchy displays rows that are ragged.</span></span> <span data-ttu-id="9f409-178">Hay muchas filas en las que se muestran miembros en blanco.</span><span class="sxs-lookup"><span data-stu-id="9f409-178">There are many rows where blank members are shown.</span></span>

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a><span data-ttu-id="9f409-179">Hola toofix jerarquía desigual estableciendo los miembros de ocultación de hello, propiedad</span><span class="sxs-lookup"><span data-stu-id="9f409-179">toofix hello ragged hierarchy by setting hello Hide members property</span></span>

1.  <span data-ttu-id="9f409-180">En el **Explorador de modelos tabulares**, expanda **Tablas** > **DimEmployee** > **Jerarquías** > **Organización**.</span><span class="sxs-lookup"><span data-stu-id="9f409-180">In **Tabular Model Explorer**, expand **Tables** > **DimEmployee** > **Hierarchies** > **Organization**.</span></span>

2.  <span data-ttu-id="9f409-181">En **Propiedades** > **Ocultar miembros**, seleccione **Ocultar miembros en blanco**.</span><span class="sxs-lookup"><span data-stu-id="9f409-181">In **Properties** > **Hide Members**, select **Hide blank members**.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  <span data-ttu-id="9f409-183">En Excel, actualizar Hola tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="9f409-183">Back in Excel, refresh hello PivotTable.</span></span> 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    <span data-ttu-id="9f409-185">Ahora el aspecto es mucho mejor.</span><span class="sxs-lookup"><span data-stu-id="9f409-185">Now that looks a whole lot better!</span></span>

## <a name="see-also"></a><span data-ttu-id="9f409-186">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9f409-186">See Also</span></span>   
[<span data-ttu-id="9f409-187">Lección 9: Creación de jerarquías</span><span class="sxs-lookup"><span data-stu-id="9f409-187">Lesson 9: Create hierarchies</span></span>](../tutorials/aas-lesson-9-create-hierarchies.md)  
[<span data-ttu-id="9f409-188">Lección complementaria: Seguridad dinámica</span><span class="sxs-lookup"><span data-stu-id="9f409-188">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="9f409-189">Lección complementaria: Filas de detalles</span><span class="sxs-lookup"><span data-stu-id="9f409-189">Supplemental Lesson - Detail rows</span></span>](../tutorials/aas-supplemental-lesson-detail-rows.md)  