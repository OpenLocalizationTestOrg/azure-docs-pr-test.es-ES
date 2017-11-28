---
title: aaaSQL actividad de procedimiento almacenado de servidor
description: "Obtenga información acerca de cómo puede usar la actividad de procedimiento almacenado de SQL Server de hello tooinvoke un procedimiento almacenado en una base de datos de SQL Azure o el almacenamiento de datos de SQL Azure desde una canalización del generador de datos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="75739-103">Actividad de procedimiento almacenado de SQL Server</span><span class="sxs-lookup"><span data-stu-id="75739-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="75739-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="75739-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="75739-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="75739-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="75739-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="75739-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="75739-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="75739-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="75739-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="75739-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="75739-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="75739-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="75739-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="75739-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="75739-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="75739-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="75739-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="75739-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="75739-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="75739-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="75739-114">Información general</span><span class="sxs-lookup"><span data-stu-id="75739-114">Overview</span></span>
<span data-ttu-id="75739-115">Usar las actividades de transformación de datos en una factoría de datos [canalización](data-factory-create-pipelines.md) tootransform y procesar datos sin formato en las predicciones y visión.</span><span class="sxs-lookup"><span data-stu-id="75739-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="75739-116">Hello actividad de procedimiento almacenado es una de las actividades de transformación de Hola que admite factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="75739-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="75739-117">En este artículo se basa en hello [las actividades de transformación de datos](data-factory-data-transformation-activities.md) artículo, que presenta una descripción general de transformación de datos y las actividades de transformación de hello compatible de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="75739-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="75739-118">Puede utilizar tooinvoke de actividad de procedimiento almacenado Hola un procedimiento almacenado en uno de hello después de datos se almacena en su empresa o en una máquina virtual (VM) de Azure:</span><span class="sxs-lookup"><span data-stu-id="75739-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="75739-119">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="75739-119">Azure SQL Database</span></span>
- <span data-ttu-id="75739-120">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="75739-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="75739-121">Base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75739-121">SQL Server Database.</span></span>  <span data-ttu-id="75739-122">Si está utilizando SQL Server, instale Data Management Gateway en el mismo equipo que hospeda Hola base de datos o en un equipo independiente que tiene la base de datos de access toohello de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="75739-123">La puerta de enlace de administración de datos es un componente que conecta orígenes de datos locales o en la máquina virtual de Azure con servicios en la nube de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="75739-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="75739-124">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="75739-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75739-125">Cuando se copian datos en la base de datos de SQL Azure o SQL Server, puede configurar hello **SqlSink** en tooinvoke de actividad de copia un procedimiento almacenado mediante el uso de hello **sqlWriterStoredProcedureName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="75739-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="75739-126">Para más información, consulte [Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="75739-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="75739-127">Para obtener más información acerca de la propiedad de hello, consulte los siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="75739-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="75739-128">No se admite la invocación de un procedimiento almacenado al copiar datos en Azure SQL Data Warehouse mediante una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="75739-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="75739-129">Sin embargo, puede utilizar tooinvoke de actividad de procedimiento almacenado de hello un procedimiento almacenado en el almacén de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="75739-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="75739-130">Cuando se copian datos de base de datos de SQL Azure o SQL Server o almacenamiento de datos de SQL Azure, puede configurar **SqlSource** en tooinvoke de actividad de copia una tooread de datos de procedimiento almacenado de base de datos de origen de hello mediante hello  **sqlReaderStoredProcedureName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="75739-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="75739-131">Para obtener más información, vea Hola siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="75739-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="75739-132">Hola siguiendo el tutorial utiliza Hola actividad de procedimiento almacenado en un tooinvoke de canalización un procedimiento almacenado en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75739-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="75739-133">Tutorial</span><span class="sxs-lookup"><span data-stu-id="75739-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="75739-134">Procedimiento almacenado y tabla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="75739-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="75739-135">Cree Hola siguiente **tabla** en la base de datos de SQL Azure con SQL Server Management Studio o cualquier otra herramienta que está familiarizado con.</span><span class="sxs-lookup"><span data-stu-id="75739-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="75739-136">columna de datetimestamp Hello es Hola fecha y hora en que cuando se genera el identificador correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="75739-137">Id. es Hola único identificado y column de datetimestamp de Hola Hola fecha y hora en que cuando se genera el identificador correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Datos de ejemplo](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="75739-139">En este ejemplo, procedimiento almacenado de hello está en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75739-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="75739-140">Si hello procedimiento almacenado está en un almacén de datos de SQL Azure y base de datos de SQL Server, el enfoque de hello es similar.</span><span class="sxs-lookup"><span data-stu-id="75739-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="75739-141">Para una base de datos de SQL Server, debe instalar una [Puerta de enlace de administración de datos](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="75739-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="75739-142">Cree Hola siguiente **procedimiento almacenado** que inserta datos en toohello **tabla de muestra**.</span><span class="sxs-lookup"><span data-stu-id="75739-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="75739-143">**Nombre** y **mayúsculas y minúsculas** de hello parámetro (fecha y hora en este ejemplo) debe coincidir con el de los parámetros especificados en hello canalización/JSON de la actividad.</span><span class="sxs-lookup"><span data-stu-id="75739-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="75739-144">En la consulta Hola definición del procedimiento almacenado, asegúrese de que  **@**  se utiliza como un prefijo de parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="75739-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="75739-145">Crear una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="75739-145">Create a data factory</span></span>
1. <span data-ttu-id="75739-146">Inicie sesión demasiado[portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75739-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="75739-147">Haga clic en **NEW** en el menú de la izquierda hello, haga clic en **Intelligence + análisis**y haga clic en **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="75739-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nueva factoría de datos](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="75739-149">Hola **factoría de datos** hoja, escriba **SProcDF** para hello nombre.</span><span class="sxs-lookup"><span data-stu-id="75739-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="75739-150">Los nombres de Azure Data Factory son **únicos globalmente**.</span><span class="sxs-lookup"><span data-stu-id="75739-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="75739-151">Necesita tooprefix Hola nombre hello factoría de datos con el nombre, la creación correcta de hello tooenable de fábrica de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Nueva factoría de datos](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="75739-153">Seleccione la **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="75739-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="75739-154">Para **grupo de recursos**, realice una de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="75739-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="75739-155">Haga clic en **crear nuevo** y escriba un nombre para el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="75739-156">Haga clic en **Usar existente** y seleccione un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="75739-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="75739-157">Seleccione hello **ubicación** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="75739-158">Seleccione **toodashboard Pin** para que puedan ver factoría de datos de hello en el panel de hello próxima vez que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="75739-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="75739-159">Haga clic en **crear** en hello **factoría de datos** hoja.</span><span class="sxs-lookup"><span data-stu-id="75739-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="75739-160">Vea factoría de datos de Hola se creen en hello **panel** de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="75739-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="75739-161">Una vez creado correctamente la factoría de datos de hello, consulte página de factoría de datos de hello, que muestra Hola contenido Hola factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="75739-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Página principal de Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="75739-163">Crear un servicio vinculado SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="75739-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="75739-164">Después de crear la factoría de datos de hello, se crea un servicio de SQL Azure vinculado que se vincula la base de datos de SQL Azure, que contiene la tabla de la tabla de muestra de Hola y procedimiento almacenado de sp_sample, tooyour factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="75739-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="75739-165">Haga clic en **autor e implementar** en hello **factoría de datos** hoja para **SProcDF** toolaunch Hola Editor de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="75739-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="75739-166">Haga clic en **nuevo almacén de datos** en Hola barra de comandos y elija **base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="75739-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="75739-167">Debería ver Hola script JSON para crear una SQL Azure vinculado servicio en el editor de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Nuevo almacén de datos](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="75739-169">Hola script JSON, asegúrese de hello siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="75739-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="75739-170">Reemplace `<servername>` con el nombre de Hola de su servidor de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75739-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="75739-171">Reemplace `<databasename>` con base de datos de hello en el que creó hello y tabla de Hola de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="75739-172">Reemplace `<username@servername>` con cuenta de usuario de Hola que tiene la base de datos de access toohello.</span><span class="sxs-lookup"><span data-stu-id="75739-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="75739-173">Reemplace `<password>` con contraseña hello para la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Nuevo almacén de datos](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="75739-175">toodeploy Hola servicio vinculado, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="75739-176">Confirme que aparece hello AzureSqlLinkedService en el árbol de hello ver Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="75739-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="75739-178">Crear un conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="75739-178">Create an output dataset</span></span>
<span data-ttu-id="75739-179">Debe especificar que un conjunto de datos de salida para una actividad de procedimiento almacenado incluso si el procedimiento almacenado de hello no produce ningún dato.</span><span class="sxs-lookup"><span data-stu-id="75739-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="75739-180">Eso es porque su Hola del resultado de conjunto de datos que controla la programación de Hola de actividad de hello (¿con qué frecuencia hello actividad se ejecuta - cada hora, diariamente, etcetera.).</span><span class="sxs-lookup"><span data-stu-id="75739-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="75739-181">Hello conjunto de datos de salida debe usar un **servicio vinculado** que hace referencia tooan base de datos de SQL Azure o un almacén de datos de SQL Azure o una base de datos de SQL Server en el que desea Hola toorun de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="75739-182">Hello conjunto de datos de salida puede actuar como un resultado de hello de manera toopass del procedimiento de hello almacenan para su posterior procesamiento por otra actividad ([encadenamiento actividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="75739-183">Sin embargo, factoría de datos no escribe automáticamente Hola un resultado de un conjunto de datos de toothis de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="75739-184">Es el procedimiento almacenado Hola esa tabla SQL tooa de escrituras que Hola puntos de conjunto de datos de salida a.</span><span class="sxs-lookup"><span data-stu-id="75739-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="75739-185">En algunos casos, puede ser el conjunto de datos de salida de hello un **conjunto de datos ficticio** (procedimiento almacenado de un conjunto de datos que señala tooa tabla que no contienen realmente salida de hello).</span><span class="sxs-lookup"><span data-stu-id="75739-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="75739-186">Se usa este conjunto de datos ficticio solo toospecify programación de Hola para ejecutar Hola actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="75739-187">Haga clic en **... Más** en la barra de herramientas de hello, haga clic en **nuevo conjunto de datos**y haga clic en **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="75739-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="75739-188">**Nuevo conjunto de datos** en el comando de hello barra y seleccione **SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="75739-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="75739-190">Copie y pegue la siguiente secuencia de comandos JSON en el editor de JSON toohello de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="75739-191">toodeploy Hola conjunto de datos, haga clic en **implementar** en la barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="75739-192">Confirme que aparece Hola conjunto de datos en la vista de árbol de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="75739-194">Crear una canalización con una actividad SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="75739-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="75739-195">Ahora, vamos a crear una canalización con una actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="75739-196">Tenga en cuenta Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="75739-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="75739-197">Hola **tipo** propiedad se establece demasiado**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="75739-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="75739-198">Hola **storedProcedureName** en tipo de las propiedades se establecen demasiado**sp_sample** (nombre de hello procedimiento almacenado).</span><span class="sxs-lookup"><span data-stu-id="75739-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="75739-199">Hola **storedProcedureParameters** sección contiene un parámetro denominado **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="75739-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="75739-200">Nombre y mayúsculas y minúsculas del parámetro hello en JSON deben coincidir con nombre de Hola y mayúsculas y minúsculas del parámetro hello en la definición del procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="75739-201">Si necesita pasar null para un parámetro, use la sintaxis de hello: `"param1": null` (en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="75739-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="75739-202">Haga clic en **... Más** Hola barra de comandos y haga clic en **nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="75739-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="75739-203">Copiar y pegar Hola siguiente fragmento de JSON:</span><span class="sxs-lookup"><span data-stu-id="75739-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="75739-204">canalización de hello toodeploy, haga clic en **implementar** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="75739-205">Canalización de Hola de Monitor</span><span class="sxs-lookup"><span data-stu-id="75739-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="75739-206">Haga clic en **X** tooclose Editor de generador de datos hojas toonavigate hacer copia de hoja de la factoría de datos de toohello y haga clic en **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="75739-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="75739-208">Hola **vista de diagrama**, verá información general de las canalizaciones de Hola y conjuntos de datos utilizan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="75739-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="75739-210">Hola vista de diagrama, haga doble clic en el conjunto de datos de hello `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="75739-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="75739-211">Vea intervalos de hello en estado listo.</span><span class="sxs-lookup"><span data-stu-id="75739-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="75739-212">Debería haber cinco segmentos porque un segmento se genera para cada hora entre la hora de inicio de Hola y hora de finalización de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="75739-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="75739-214">Cuando se encuentra en un segmento **listo** estado, ejecute un `select * from sampletable` consultarlo tooverify de base de datos de SQL Azure Hola que Hola datos se insertó en la tabla de toohello por procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![Datos de salida](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="75739-216">Vea [canalización de hello Monitor](data-factory-monitor-manage-pipelines.md) para obtener información detallada sobre la supervisión de las canalizaciones de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="75739-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="75739-217">Especificación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="75739-217">Specify an input dataset</span></span>
<span data-ttu-id="75739-218">En el tutorial de hello, actividad de procedimiento almacenado no tiene los conjuntos de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="75739-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="75739-219">Si especifica un conjunto de datos de entrada, hello actividad de procedimiento almacenado no se ejecuta hasta Hola segmento del conjunto de datos de entrada está disponible (en estado listo).</span><span class="sxs-lookup"><span data-stu-id="75739-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="75739-220">conjunto de datos de Hello puede ser un conjunto de datos externo (que no se crea por otra actividad de hello misma canalización) o un conjunto de datos interno generado por una actividad de nivel superior (actividad de Hola que se ejecuta antes que esta actividad).</span><span class="sxs-lookup"><span data-stu-id="75739-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="75739-221">Puede especificar varios conjuntos de datos de entrada para la actividad de procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="75739-222">Si lo hace, hello actividad de procedimiento almacenado se ejecuta sólo cuando todos los sectores de conjunto de datos de entrada de hello están disponibles (en estado listo).</span><span class="sxs-lookup"><span data-stu-id="75739-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="75739-223">conjunto de datos de entrada de Hola no puede ser consumida en el procedimiento de hello almacenado como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="75739-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="75739-224">Es solo usa toocheck Hola dependencia antes de actividad de procedimiento almacenado de saludo inicial.</span><span class="sxs-lookup"><span data-stu-id="75739-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="75739-225">Encadenamiento con otras actividades</span><span class="sxs-lookup"><span data-stu-id="75739-225">Chaining with other activities</span></span>
<span data-ttu-id="75739-226">Si desea toochain una actividad de nivel superior con esta actividad, especifique la salida de hello de actividad de nivel superior de hello como una entrada de esta actividad.</span><span class="sxs-lookup"><span data-stu-id="75739-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="75739-227">Al hacerlo, hello actividad de procedimiento almacenado no se ejecuta hasta que finaliza la actividad de nivel superior de hello y conjunto de datos de salida de hello de actividad de nivel superior de hello está disponible (en estado listo).</span><span class="sxs-lookup"><span data-stu-id="75739-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="75739-228">Puede especificar los conjuntos de datos de salida de varias actividades de nivel superior como los conjuntos de datos de actividad de procedimiento almacenado de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="75739-229">Al hacerlo, Hola actividad de procedimiento almacenado se ejecuta solo cuando todos los sectores de conjunto de datos de entrada de hello están disponibles.</span><span class="sxs-lookup"><span data-stu-id="75739-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="75739-230">En el siguiente ejemplo de Hola, salida de hello de actividad de copia de hello es: OutputDataset, que es una entrada de hello actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="75739-231">Por lo tanto, hello actividad de procedimiento almacenado no se ejecuta hasta que finaliza la actividad de copia de Hola y Hola OutputDataset segmento está disponible (en estado listo).</span><span class="sxs-lookup"><span data-stu-id="75739-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="75739-232">Si especifica varios conjuntos de datos de entrada, hello actividad de procedimiento almacenado no se ejecuta hasta que estén disponibles todos los sectores de conjunto de datos de entrada de hello (en estado listo).</span><span class="sxs-lookup"><span data-stu-id="75739-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="75739-233">no se puede usar conjuntos de datos de entrada de Hello directamente como actividad de procedimiento almacenado de toohello de parámetros.</span><span class="sxs-lookup"><span data-stu-id="75739-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="75739-234">Para obtener más información sobre cómo encadenar actividades, vea [Varias actividades en una canalización](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="75739-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="75739-235">De forma similar, toolink Hola almacén actividad de procedimiento con **actividades de dirección descendente** (hello las actividades que se ejecutan una vez completadas hello actividades de procedimiento almacenado), especificar el conjunto de datos de salida de hello de la actividad de procedimiento almacenado de Hola como un entrada de actividad de nivel inferior hello en canalización Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75739-236">Cuando se copian datos en la base de datos de SQL Azure o SQL Server, puede configurar hello **SqlSink** en tooinvoke de actividad de copia un procedimiento almacenado mediante el uso de hello **sqlWriterStoredProcedureName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="75739-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="75739-237">Para más información, consulte [Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="75739-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="75739-238">Para obtener más información acerca de la propiedad de hello, vea Hola siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="75739-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="75739-239">Cuando se copian datos de base de datos de SQL Azure o SQL Server o almacenamiento de datos de SQL Azure, puede configurar **SqlSource** en tooinvoke de actividad de copia una tooread de datos de procedimiento almacenado de base de datos de origen de hello mediante hello  **sqlReaderStoredProcedureName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="75739-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="75739-240">Para obtener más información, vea Hola siguientes artículos de conector: [base de datos de SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="75739-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="75739-241">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="75739-241">JSON format</span></span>
<span data-ttu-id="75739-242">Este es el formato JSON de Hola para definir una actividad de procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="75739-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="75739-243">Hello en la tabla siguiente describe estas propiedades JSON:</span><span class="sxs-lookup"><span data-stu-id="75739-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="75739-244">Propiedad</span><span class="sxs-lookup"><span data-stu-id="75739-244">Property</span></span> | <span data-ttu-id="75739-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="75739-245">Description</span></span> | <span data-ttu-id="75739-246">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="75739-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="75739-247">name</span><span class="sxs-lookup"><span data-stu-id="75739-247">name</span></span> | <span data-ttu-id="75739-248">Nombre de actividad de Hola</span><span class="sxs-lookup"><span data-stu-id="75739-248">Name of hello activity</span></span> |<span data-ttu-id="75739-249">Sí</span><span class="sxs-lookup"><span data-stu-id="75739-249">Yes</span></span> |
| <span data-ttu-id="75739-250">description</span><span class="sxs-lookup"><span data-stu-id="75739-250">description</span></span> |<span data-ttu-id="75739-251">Texto que describe qué actividad Hola se usa para</span><span class="sxs-lookup"><span data-stu-id="75739-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="75739-252">No</span><span class="sxs-lookup"><span data-stu-id="75739-252">No</span></span> |
| <span data-ttu-id="75739-253">type</span><span class="sxs-lookup"><span data-stu-id="75739-253">type</span></span> | <span data-ttu-id="75739-254">Se debe establecer en: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="75739-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="75739-255">Sí</span><span class="sxs-lookup"><span data-stu-id="75739-255">Yes</span></span> |
| <span data-ttu-id="75739-256">inputs</span><span class="sxs-lookup"><span data-stu-id="75739-256">inputs</span></span> | <span data-ttu-id="75739-257">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75739-257">Optional.</span></span> <span data-ttu-id="75739-258">Si especifica un conjunto de datos de entrada, debe estar disponible (en estado "Listo") para hello almacenado toorun de actividad de procedimiento.</span><span class="sxs-lookup"><span data-stu-id="75739-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="75739-259">conjunto de datos de entrada de Hola no puede ser consumida en el procedimiento de hello almacenado como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="75739-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="75739-260">Es solo usa toocheck Hola dependencia antes de actividad de procedimiento almacenado de saludo inicial.</span><span class="sxs-lookup"><span data-stu-id="75739-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="75739-261">No</span><span class="sxs-lookup"><span data-stu-id="75739-261">No</span></span> |
| <span data-ttu-id="75739-262">outputs</span><span class="sxs-lookup"><span data-stu-id="75739-262">outputs</span></span> | <span data-ttu-id="75739-263">Debe especificar un conjunto de datos para una actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="75739-264">Conjunto de datos de salida especifica hello **programación** para hello almacenados actividad de procedimiento (cada hora, semanalmente, mensualmente, etcetera).</span><span class="sxs-lookup"><span data-stu-id="75739-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="75739-265">Hello conjunto de datos de salida debe usar un **servicio vinculado** que hace referencia tooan base de datos de SQL Azure o un almacén de datos de SQL Azure o una base de datos de SQL Server en el que desea Hola toorun de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="75739-266">Hello conjunto de datos de salida puede actuar como un resultado de hello de manera toopass del procedimiento de hello almacenan para su posterior procesamiento por otra actividad ([encadenamiento actividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="75739-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="75739-267">Sin embargo, factoría de datos no escribe automáticamente Hola un resultado de un conjunto de datos de toothis de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="75739-268">Es el procedimiento almacenado Hola esa tabla SQL tooa de escrituras que Hola puntos de conjunto de datos de salida a.</span><span class="sxs-lookup"><span data-stu-id="75739-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="75739-269">En algunos casos, puede ser el conjunto de datos de salida de hello un **conjunto de datos ficticio**, que se usa solo la programación de hello toospecify para ejecutar Hola actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="75739-270">Sí</span><span class="sxs-lookup"><span data-stu-id="75739-270">Yes</span></span> |
| <span data-ttu-id="75739-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="75739-271">storedProcedureName</span></span> |<span data-ttu-id="75739-272">Especifique el nombre de hello del procedimiento de hello almacenado en la base de datos de SQL Azure de Hola o base de datos de almacenamiento de datos de SQL Azure o SQL Server que se representa mediante el servicio vinculado de Hola que Hola usos de la tabla de salida.</span><span class="sxs-lookup"><span data-stu-id="75739-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="75739-273">Sí</span><span class="sxs-lookup"><span data-stu-id="75739-273">Yes</span></span> |
| <span data-ttu-id="75739-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="75739-274">storedProcedureParameters</span></span> |<span data-ttu-id="75739-275">Especifique valores para los parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="75739-276">Si necesitas toopass null para un parámetro, use la sintaxis de hello: "param1": null (todas las minúsculas).</span><span class="sxs-lookup"><span data-stu-id="75739-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="75739-277">Vea Hola después toolearn de ejemplo sobre el uso de esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="75739-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="75739-278">No</span><span class="sxs-lookup"><span data-stu-id="75739-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="75739-279">Pasar un valor estático</span><span class="sxs-lookup"><span data-stu-id="75739-279">Passing a static value</span></span>
<span data-ttu-id="75739-280">Ahora, veamos agregar otra columna con el nombre 'Escenario' en tabla de Hola que contiene un valor estático denominado 'Ejemplo de documento'.</span><span class="sxs-lookup"><span data-stu-id="75739-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Datos de ejemplo 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="75739-282">**Tabla:**</span><span class="sxs-lookup"><span data-stu-id="75739-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="75739-283">**Procedimiento almacenado:**</span><span class="sxs-lookup"><span data-stu-id="75739-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="75739-284">Ahora, pasar hello **escenario** hello y parámetro de valor de hello actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="75739-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="75739-285">Hola **typeProperties** sección Hola anterior ejemplo parece Hola siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="75739-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="75739-286">**Conjuntos de datos de Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="75739-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="75739-287">**Canalización de Data Factory**</span><span class="sxs-lookup"><span data-stu-id="75739-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```