---
title: "Lección 2 del tutorial de Azure Analysis Services: Obtención de datos | Microsoft Docs"
description: "Describe cómo obtener e importar datos en el proyecto del tutorial de Azure Analysis Services."
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
ms.openlocfilehash: e77de4b9a74b528fa8a7ce86424fc14628b2cacc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-2-get-data"></a><span data-ttu-id="64bfb-103">Lección 2: Obtención de datos</span><span class="sxs-lookup"><span data-stu-id="64bfb-103">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="64bfb-104">En esta lección, usará Obtención de datos en SSDT para conectarse a la base de datos de ejemplo AdventureWorksDW2014, seleccionar datos, obtener una vista previa, filtrar e importar en el área de trabajo del modelo.</span><span class="sxs-lookup"><span data-stu-id="64bfb-104">In this lesson, you use Get Data in SSDT to connect to the AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="64bfb-105">Al usar Obtención de datos, puede importar datos de diversos de orígenes: Azure SQL Database, Oracle, Sybase, fuente OData, Teradata, archivos y mucho más.</span><span class="sxs-lookup"><span data-stu-id="64bfb-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="64bfb-106">También puede consultar datos mediante una expresión de fórmula de Power Query M.</span><span class="sxs-lookup"><span data-stu-id="64bfb-106">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="64bfb-107">Tiempo estimado para completar esta lección: **10 minutos**</span><span class="sxs-lookup"><span data-stu-id="64bfb-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="64bfb-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="64bfb-108">Prerequisites</span></span>  
<span data-ttu-id="64bfb-109">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="64bfb-109">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="64bfb-110">Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 1: Creación de un proyecto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span><span class="sxs-lookup"><span data-stu-id="64bfb-110">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="64bfb-111">Crear una conexión</span><span class="sxs-lookup"><span data-stu-id="64bfb-111">Create a connection</span></span>  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a><span data-ttu-id="64bfb-112">Para crear una conexión a la base de datos AdventureWorksDW2014</span><span class="sxs-lookup"><span data-stu-id="64bfb-112">To create a connection to the AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="64bfb-113">En el Explorador de modelos tabulares, haga clic con el botón derecho en **Orígenes de datos** > **Importar desde el origen de datos**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-113">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="64bfb-114">De este modo se inicia Obtención de datos, que le guiará por el proceso de conexión a un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="64bfb-114">This launches Get Data, which guides you through connecting to a data source.</span></span> <span data-ttu-id="64bfb-115">Si no ve el Explorador de modelos tabulares, en el **Explorador de soluciones**, haga doble clic en **Model.bim** para abrir el modelo en el diseñador.</span><span class="sxs-lookup"><span data-stu-id="64bfb-115">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span></span> 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="64bfb-117">En Obtención de datos, haga clic en **Base de datos** > **Base de datos de SQL Server** > **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-117">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="64bfb-118">En el cuadro de diálogo **Base de datos de SQL Server**, en **Servidor**, escriba el nombre del servidor en el que ha instalado la base de datos AdventureWorksDW2014 y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-118">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="64bfb-119">Cuando se le pida que escriba las credenciales, debe especificar las credenciales que Analysis Services usa para conectarse al origen de datos al importar y procesar datos.</span><span class="sxs-lookup"><span data-stu-id="64bfb-119">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span></span> <span data-ttu-id="64bfb-120">En **Modo de suplantación**, seleccione **Suplantar cuenta**, escriba las credenciales y haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-120">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="64bfb-121">Se recomienda que use una cuenta cuya contraseña no expire.</span><span class="sxs-lookup"><span data-stu-id="64bfb-121">It's recommended you use an account where the password doesn't expire.</span></span>

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="64bfb-123">El uso de una cuenta de usuario y contraseña de Windows proporciona el método más seguro de conectarse a un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="64bfb-123">Using a Windows user account and password provides the most secure method of connecting to a data source.</span></span>
  
5.  <span data-ttu-id="64bfb-124">En el navegador, seleccione la base de datos **AdventureWorksDW2014** y haga clic en **Aceptar**. De este modo, se crea la conexión con la base de datos.</span><span class="sxs-lookup"><span data-stu-id="64bfb-124">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span></span> 
  
6.  <span data-ttu-id="64bfb-125">En el navegador, active la casilla de las tablas siguientes: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** y **FactInternetSales**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-125">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="64bfb-127">Después de hacer clic en Aceptar, se abre el Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="64bfb-127">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="64bfb-128">En la sección siguiente, seleccione solo los datos que desea importar.</span><span class="sxs-lookup"><span data-stu-id="64bfb-128">In the next section, you select only the data you want to import.</span></span>

  
## <a name="filter-the-table-data"></a><span data-ttu-id="64bfb-129">Filtrar los datos de tabla</span><span class="sxs-lookup"><span data-stu-id="64bfb-129">Filter the table data</span></span>  
<span data-ttu-id="64bfb-130">Las tablas de la base de datos de ejemplo AdventureWorksDW2014 contienen datos que no es necesario incluir en el modelo.</span><span class="sxs-lookup"><span data-stu-id="64bfb-130">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span></span> <span data-ttu-id="64bfb-131">Siempre que sea posible, le interesa filtrar los datos que no son necesarios para ahorrar el espacio en memoria que usa el modelo.</span><span class="sxs-lookup"><span data-stu-id="64bfb-131">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span></span> <span data-ttu-id="64bfb-132">Filtre algunas de las columnas de las tablas, de modo que no se importen en la base de datos del área de trabajo o en la base de datos del modelo una vez que se haya implementado.</span><span class="sxs-lookup"><span data-stu-id="64bfb-132">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span></span> 
  
#### <a name="to-filter-the-table-data-before-importing"></a><span data-ttu-id="64bfb-133">Para filtrar los datos de la tabla antes de importar</span><span class="sxs-lookup"><span data-stu-id="64bfb-133">To filter the table data before importing</span></span>  
  
1.  <span data-ttu-id="64bfb-134">En el Editor de consultas, seleccione la tabla **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-134">In Query Editor, select the **DimCustomer** table.</span></span> <span data-ttu-id="64bfb-135">Aparece una vista de la tabla DimCustomer en el origen de datos (la base de datos de ejemplo AdventureWorksDWQ2014).</span><span class="sxs-lookup"><span data-stu-id="64bfb-135">A view of the DimCustomer table at the datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="64bfb-136">Seleccione al mismo tiempo (Ctrl+clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, haga clic con el botón derecho y, después, haga clic en **Quitar columnas**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-136">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="64bfb-138">Dado que los valores de estas columnas no son pertinentes para el análisis de ventas por Internet, no es necesario importar estas columnas.</span><span class="sxs-lookup"><span data-stu-id="64bfb-138">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span></span> <span data-ttu-id="64bfb-139">Si elimina las columnas innecesarias, el modelo será más pequeño y eficaz.</span><span class="sxs-lookup"><span data-stu-id="64bfb-139">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="64bfb-140">Elimine las siguientes columnas de cada tabla para filtrar las tablas restantes:</span><span class="sxs-lookup"><span data-stu-id="64bfb-140">Filter the remaining tables by removing the following columns in each table:</span></span>  
    
    <span data-ttu-id="64bfb-141">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="64bfb-141">**DimDate**</span></span>
    
      |<span data-ttu-id="64bfb-142">Columna</span><span class="sxs-lookup"><span data-stu-id="64bfb-142">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="64bfb-143">DateKey</span><span class="sxs-lookup"><span data-stu-id="64bfb-143">DateKey</span></span>|  
      |<span data-ttu-id="64bfb-144">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="64bfb-144">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="64bfb-145">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="64bfb-145">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="64bfb-146">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-146">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="64bfb-147">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-147">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="64bfb-148">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="64bfb-148">**DimGeography**</span></span>
  
      |<span data-ttu-id="64bfb-149">Columna</span><span class="sxs-lookup"><span data-stu-id="64bfb-149">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="64bfb-150">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-150">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="64bfb-151">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-151">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="64bfb-152">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="64bfb-152">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="64bfb-153">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="64bfb-153">**DimProduct**</span></span>
  
      |<span data-ttu-id="64bfb-154">Columna</span><span class="sxs-lookup"><span data-stu-id="64bfb-154">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="64bfb-155">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-155">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="64bfb-156">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-156">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="64bfb-157">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-157">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="64bfb-158">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-158">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="64bfb-159">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-159">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="64bfb-160">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-160">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="64bfb-161">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-161">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="64bfb-162">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-162">**GermanDescription**</span></span>|  
      |<span data-ttu-id="64bfb-163">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-163">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="64bfb-164">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="64bfb-164">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="64bfb-165">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="64bfb-165">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="64bfb-166">Columna</span><span class="sxs-lookup"><span data-stu-id="64bfb-166">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="64bfb-167">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-167">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="64bfb-168">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-168">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="64bfb-169">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="64bfb-169">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="64bfb-170">Columna</span><span class="sxs-lookup"><span data-stu-id="64bfb-170">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="64bfb-171">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-171">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="64bfb-172">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="64bfb-172">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="64bfb-173">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="64bfb-173">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="64bfb-174">Columna</span><span class="sxs-lookup"><span data-stu-id="64bfb-174">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="64bfb-175">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="64bfb-175">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="64bfb-176">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="64bfb-176">**DueDateKey**</span></span>|  
      |<span data-ttu-id="64bfb-177">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="64bfb-177">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="64bfb-178"><a name="Import"></a>Importar las tablas y los datos de columna seleccionados</span><span class="sxs-lookup"><span data-stu-id="64bfb-178"><a name="Import"></a>Import the selected tables and column data</span></span>  
<span data-ttu-id="64bfb-179">Ahora que ha obtenido una vista previa y ha filtrado los datos innecesarios, puede importar los datos que quiera.</span><span class="sxs-lookup"><span data-stu-id="64bfb-179">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span></span> <span data-ttu-id="64bfb-180">El asistente importa los datos de las tablas junto con las relaciones entre las tablas.</span><span class="sxs-lookup"><span data-stu-id="64bfb-180">The wizard imports the table data along with any relationships between tables.</span></span> <span data-ttu-id="64bfb-181">Se crean nuevas tablas y columnas en el modelo y no se importan los datos filtrados.</span><span class="sxs-lookup"><span data-stu-id="64bfb-181">New tables and columns are created in the model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a><span data-ttu-id="64bfb-182">Para importar las tablas y los datos de columna seleccionados</span><span class="sxs-lookup"><span data-stu-id="64bfb-182">To import the selected tables and column data</span></span>  
  
1.  <span data-ttu-id="64bfb-183">Revise lo que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="64bfb-183">Review your selections.</span></span> <span data-ttu-id="64bfb-184">Si todo es correcto, haga clic en **Importar**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-184">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="64bfb-185">En el cuadro de diálogo Procesamiento de datos se muestra el estado de los datos que se van a importar del origen de datos en la base de datos del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="64bfb-185">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="64bfb-187">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-187">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="64bfb-188">Guardar el proyecto de modelo</span><span class="sxs-lookup"><span data-stu-id="64bfb-188">Save your model project</span></span>  
<span data-ttu-id="64bfb-189">Es importante que guarde con frecuencia el proyecto de modelo.</span><span class="sxs-lookup"><span data-stu-id="64bfb-189">It's important to frequently save your model project.</span></span>  
  
#### <a name="to-save-the-model-project"></a><span data-ttu-id="64bfb-190">Para guardar el proyecto de modelo</span><span class="sxs-lookup"><span data-stu-id="64bfb-190">To save the model project</span></span>  
  
-   <span data-ttu-id="64bfb-191">Haga clic en **Archivo** > **Guardar todo**.</span><span class="sxs-lookup"><span data-stu-id="64bfb-191">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="64bfb-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64bfb-192">What's next?</span></span>
<span data-ttu-id="64bfb-193">[Lección 3: Marcado como tabla de fechas](../tutorials/aas-lesson-3-mark-as-date-table.md)</span><span class="sxs-lookup"><span data-stu-id="64bfb-193">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
