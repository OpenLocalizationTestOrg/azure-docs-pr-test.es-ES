---
<span data-ttu-id="aaa69-101">título: aaa "lección de Azure Analysis Services tutorial 2: obtener datos | Descripción de Microsoft Docs": describe cómo tooget e importar datos en Hola proyecto tutorial de Analysis Services de Azure.</span><span class="sxs-lookup"><span data-stu-id="aaa69-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="aaa69-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="aaa69-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="aaa69-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 01/06/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="aaa69-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="aaa69-104">Lección 2: Obtención de datos</span><span class="sxs-lookup"><span data-stu-id="aaa69-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="aaa69-105">En esta lección, usa obtener datos de la base de datos de ejemplo de tooconnect toohello AdventureWorksDW2014 SSDT, seleccione datos, vista previa y filtrar y, a continuación, importar el área de trabajo del modelo.</span><span class="sxs-lookup"><span data-stu-id="aaa69-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="aaa69-106">Al usar Obtención de datos, puede importar datos de diversos de orígenes: Azure SQL Database, Oracle, Sybase, fuente OData, Teradata, archivos y mucho más.</span><span class="sxs-lookup"><span data-stu-id="aaa69-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="aaa69-107">También puede consultar datos mediante una expresión de fórmula de Power Query M.</span><span class="sxs-lookup"><span data-stu-id="aaa69-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="aaa69-108">Estimado toocomplete de tiempo en esta lección: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="aaa69-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="aaa69-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aaa69-109">Prerequisites</span></span>  
<span data-ttu-id="aaa69-110">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="aaa69-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="aaa69-111">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 1: crear un nuevo proyecto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="aaa69-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="aaa69-112">Crear una conexión</span><span class="sxs-lookup"><span data-stu-id="aaa69-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="aaa69-113">una base de datos de conexión toohello AdventureWorksDW2014 toocreate</span><span class="sxs-lookup"><span data-stu-id="aaa69-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="aaa69-114">En el Explorador de modelos tabulares, haga clic con el botón derecho en **Orígenes de datos** > **Importar desde el origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="aaa69-115">Esto inicia obtener datos, que le guiará por el origen de datos de conexión tooa.</span><span class="sxs-lookup"><span data-stu-id="aaa69-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="aaa69-116">Si no ve el Explorador de modelos tabulares, en **el Explorador de soluciones**, haga doble clic en **Model.bim** tooopen modelo de hello en el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="aaa69-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="aaa69-118">En Obtención de datos, haga clic en **Base de datos** > **Base de datos de SQL Server** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="aaa69-119">Hola **base de datos de SQL Server** cuadro de diálogo, en **Server**, escriba nombre de saludo del servidor de Hola donde instaló la base de datos de hello AdventureWorksDW2014 y, a continuación, haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="aaa69-120">Cuando se le solicite credenciales tooenter, necesita credenciales de hello toospecify Analysis Services utiliza el origen de datos de toohello tooconnect al importar y procesar datos.</span><span class="sxs-lookup"><span data-stu-id="aaa69-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="aaa69-121">En **Modo de suplantación**, seleccione **Suplantar cuenta**, escriba las credenciales y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="aaa69-122">Se recomienda que usar una cuenta que no expire contraseña Hola.</span><span class="sxs-lookup"><span data-stu-id="aaa69-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="aaa69-124">Mediante una cuenta de usuario de Windows y una contraseña proporciona el método más seguro de hello conexión tooa del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="aaa69-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="aaa69-125">En el navegador, seleccione hello **AdventureWorksDW2014** la base de datos y, a continuación, haga clic en **Aceptar**. Esto crea la base de datos de hello conexión toohello.</span><span class="sxs-lookup"><span data-stu-id="aaa69-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="aaa69-126">En el navegador, seleccione Hola casilla de verificación de hello las tablas siguientes: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, y **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="aaa69-128">Después de hacer clic en Aceptar, se abre el Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="aaa69-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="aaa69-129">En la siguiente sección hello, seleccione solo los datos de Hola que desea tooimport.</span><span class="sxs-lookup"><span data-stu-id="aaa69-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="aaa69-130">Filtrar datos de la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="aaa69-130">Filter hello table data</span></span>  
<span data-ttu-id="aaa69-131">Tablas de base de datos de ejemplo de Hola AdventureWorksDW2014 tienen datos que no es necesario tooinclude en el modelo.</span><span class="sxs-lookup"><span data-stu-id="aaa69-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="aaa69-132">Cuando sea posible, desea toofilter espacio de datos innecesarios toosave en la memoria utilizada por el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="aaa69-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="aaa69-133">Filtra algunas de las columnas de Hola de tablas por lo que no está importados en la base de datos de área de trabajo de Hola o base de datos de modelo de hello después de que se haya implementado.</span><span class="sxs-lookup"><span data-stu-id="aaa69-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="aaa69-134">datos de la tabla toofilter Hola antes de importar</span><span class="sxs-lookup"><span data-stu-id="aaa69-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="aaa69-135">En el Editor de consultas, seleccione hello **DimCustomer** tabla.</span><span class="sxs-lookup"><span data-stu-id="aaa69-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="aaa69-136">Aparece una vista de tabla de DimCustomer hello en el origen de datos de hello (la base de datos de ejemplo AdventureWorksDWQ2014).</span><span class="sxs-lookup"><span data-stu-id="aaa69-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="aaa69-137">Seleccione al mismo tiempo (Ctrl+clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, haga clic con el botón derecho y, después, haga clic en **Quitar columnas**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="aaa69-139">Puesto que los valores de hello para estas columnas no son relevantes tooInternet análisis de ventas, no hay necesidad de tooimport estas columnas.</span><span class="sxs-lookup"><span data-stu-id="aaa69-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="aaa69-140">Si elimina las columnas innecesarias, el modelo será más pequeño y eficaz.</span><span class="sxs-lookup"><span data-stu-id="aaa69-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="aaa69-141">Filtrar Hola restantes tablas mediante la eliminación de hello después de las columnas de cada tabla:</span><span class="sxs-lookup"><span data-stu-id="aaa69-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="aaa69-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="aaa69-142">**DimDate**</span></span>
    
      |<span data-ttu-id="aaa69-143">Columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="aaa69-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="aaa69-144">DateKey</span></span>|  
      |<span data-ttu-id="aaa69-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="aaa69-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="aaa69-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="aaa69-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="aaa69-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="aaa69-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="aaa69-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="aaa69-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="aaa69-150">Columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="aaa69-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="aaa69-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="aaa69-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="aaa69-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="aaa69-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="aaa69-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="aaa69-155">Columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="aaa69-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="aaa69-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="aaa69-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="aaa69-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="aaa69-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="aaa69-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="aaa69-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="aaa69-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="aaa69-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="aaa69-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="aaa69-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="aaa69-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="aaa69-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="aaa69-167">Columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="aaa69-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="aaa69-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="aaa69-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="aaa69-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="aaa69-171">Columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="aaa69-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="aaa69-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="aaa69-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="aaa69-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="aaa69-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="aaa69-175">Columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="aaa69-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="aaa69-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="aaa69-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="aaa69-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="aaa69-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="aaa69-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="aaa69-179"><a name="Import"></a>Importar datos de las columnas y las tablas de hello seleccionado</span><span class="sxs-lookup"><span data-stu-id="aaa69-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="aaa69-180">Ahora que ha obtenido una vista previa y filtran los datos innecesarios, puede importar el resto de Hola de datos de Hola que desea.</span><span class="sxs-lookup"><span data-stu-id="aaa69-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="aaa69-181">Asistente de Hello importa datos de la tabla de hello junto con las relaciones entre tablas.</span><span class="sxs-lookup"><span data-stu-id="aaa69-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="aaa69-182">Las nuevas tablas y columnas se crean en el modelo de Hola y datos que filtró no se importará.</span><span class="sxs-lookup"><span data-stu-id="aaa69-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="aaa69-183">Hola tooimport seleccionado tablas y los datos de columna</span><span class="sxs-lookup"><span data-stu-id="aaa69-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="aaa69-184">Revise lo que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="aaa69-184">Review your selections.</span></span> <span data-ttu-id="aaa69-185">Si todo es correcto, haga clic en **Importar**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="aaa69-186">cuadro de diálogo de procesamiento de datos de Hello muestra estado Hola de datos que se va a importar desde el origen de datos en la base de datos del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="aaa69-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="aaa69-188">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="aaa69-189">Guardar el proyecto de modelo</span><span class="sxs-lookup"><span data-stu-id="aaa69-189">Save your model project</span></span>  
<span data-ttu-id="aaa69-190">Es importante toofrequently guardar el proyecto de modelo.</span><span class="sxs-lookup"><span data-stu-id="aaa69-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="aaa69-191">proyecto de modelos de hello toosave</span><span class="sxs-lookup"><span data-stu-id="aaa69-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="aaa69-192">Haga clic en **Archivo** > **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="aaa69-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="aaa69-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aaa69-193">What's next?</span></span>
<span data-ttu-id="aaa69-194">[Lección 3: Marcado como tabla de fechas](../tutorials/aas-lesson-3-mark-as-date-table.md)</span><span class="sxs-lookup"><span data-stu-id="aaa69-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
