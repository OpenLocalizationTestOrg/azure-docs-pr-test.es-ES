---
title: Actividad de procedimiento almacenado de SQL Server
description: "Sepa cómo usar la actividad de procedimiento almacenado de SQL Server para invocar un procedimiento almacenado en una Base de datos SQL de Azure o en un Almacenamiento de datos SQL de Azure desde una canalización de Factoría de datos."
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="70949-103">Actividad de procedimiento almacenado de SQL Server</span><span class="sxs-lookup"><span data-stu-id="70949-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="70949-104">Actividad de Hive</span><span class="sxs-lookup"><span data-stu-id="70949-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="70949-105">Actividad de Pig</span><span class="sxs-lookup"><span data-stu-id="70949-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="70949-106">Actividad MapReduce</span><span class="sxs-lookup"><span data-stu-id="70949-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="70949-107">Actividad de streaming de Hadoop</span><span class="sxs-lookup"><span data-stu-id="70949-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="70949-108">Actividad de Spark</span><span class="sxs-lookup"><span data-stu-id="70949-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="70949-109">Actividad de ejecución de Batch de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="70949-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="70949-110">Actividad Actualizar recurso de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="70949-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="70949-111">Actividad de procedimiento almacenado</span><span class="sxs-lookup"><span data-stu-id="70949-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="70949-112">Actividad U-SQL de Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="70949-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="70949-113">Actividad personalizada de .NET</span><span class="sxs-lookup"><span data-stu-id="70949-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="70949-114">Información general</span><span class="sxs-lookup"><span data-stu-id="70949-114">Overview</span></span>
<span data-ttu-id="70949-115">Las actividades de transformación en una [canalización](data-factory-create-pipelines.md) de Data Factory transforman y procesan sus datos sin procesar para convertirlos en predicciones y perspectivas.</span><span class="sxs-lookup"><span data-stu-id="70949-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="70949-116">La actividad de procedimiento almacenado es una de las actividades de transformación que admite Data Factory.</span><span class="sxs-lookup"><span data-stu-id="70949-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="70949-117">Este artículo se basa en el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md), que presenta información general de la transformación de datos y las actividades de transformación admitidas en Data Factory.</span><span class="sxs-lookup"><span data-stu-id="70949-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="70949-118">Puede usar la actividad de procedimiento almacenado para invocar un procedimiento almacenado en uno de los siguientes almacenes de datos de la empresa o en una máquina virtual (VM) de Azure:</span><span class="sxs-lookup"><span data-stu-id="70949-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="70949-119">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="70949-119">Azure SQL Database</span></span>
- <span data-ttu-id="70949-120">Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="70949-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="70949-121">Base de datos de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="70949-121">SQL Server Database.</span></span>  <span data-ttu-id="70949-122">Si se usa SQL Server, se debe instalar la puerta de enlace de administración de datos en el mismo equipo que hospeda la base de datos o en un equipo independiente que tenga acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="70949-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="70949-123">La puerta de enlace de administración de datos es un componente que conecta orígenes de datos locales o en la máquina virtual de Azure con servicios en la nube de forma segura y administrada.</span><span class="sxs-lookup"><span data-stu-id="70949-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="70949-124">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="70949-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70949-125">Al copiar datos en Azure SQL Database o SQL Server, se puede configurar **SqlSink** en la actividad de copia para invocar un procedimiento almacenado mediante la propiedad **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="70949-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="70949-126">Para más información, consulte [Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="70949-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="70949-127">Para obtener más información sobre la propiedad, vea los artículos sobre los conectores siguientes: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties) y [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="70949-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="70949-128">No se admite la invocación de un procedimiento almacenado al copiar datos en Azure SQL Data Warehouse mediante una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="70949-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="70949-129">Sin embargo, puede usar la actividad de procedimiento almacenado para invocar un procedimiento almacenado en un SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="70949-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="70949-130">Al copiar datos de Azure SQL Database, SQL Server o Azure SQL Data Warehouse, se puede configurar **SqlSource** en la actividad de copia para invocar un procedimiento almacenado de lectura de datos mediante la propiedad **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="70949-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="70949-131">Para más información, consulte los artículos sobre los conectores siguientes: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) y [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="70949-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="70949-132">El siguiente procedimiento usa la actividad del procedimiento almacenado en una canalización para invocar un procedimiento almacenado en una base de datos de Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="70949-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="70949-133">Tutorial</span><span class="sxs-lookup"><span data-stu-id="70949-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="70949-134">Procedimiento almacenado y tabla de ejemplo</span><span class="sxs-lookup"><span data-stu-id="70949-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="70949-135">Cree la siguiente **tabla** en la Base de datos SQL de Azure con SQL Server Management Studio o cualquier otra herramienta que le resulte cómoda.</span><span class="sxs-lookup"><span data-stu-id="70949-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="70949-136">La columna datetimestamp indica la fecha y la hora en que se generó el identificador correspondiente.</span><span class="sxs-lookup"><span data-stu-id="70949-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="70949-137">Id es el identificador único y la columna datetimestamp indica la fecha y la hora en que se generó el identificador correspondiente.</span><span class="sxs-lookup"><span data-stu-id="70949-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Datos de ejemplo](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="70949-139">En este ejemplo, el procedimiento almacenado está en una base de datos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="70949-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="70949-140">Si el procedimiento almacenado está en un Azure SQL Data Warehouse y una base de datos de SQL Server, el enfoque es similar.</span><span class="sxs-lookup"><span data-stu-id="70949-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="70949-141">Para una base de datos de SQL Server, debe instalar una [Puerta de enlace de administración de datos](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="70949-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="70949-142">Cree el siguiente **procedimiento almacenado**, que inserta datos en **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="70949-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="70949-143">El **nombre** y el **uso de mayúsculas y minúsculas** en el parámetro (DateTime en este ejemplo) tienen que coincidir con los del parámetro especificado en el código JSON de la canalización o actividad.</span><span class="sxs-lookup"><span data-stu-id="70949-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="70949-144">En la definición del procedimiento almacenado, asegúrese de que se usa **@** como prefijo del parámetro.</span><span class="sxs-lookup"><span data-stu-id="70949-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="70949-145">Crear una factoría de datos</span><span class="sxs-lookup"><span data-stu-id="70949-145">Create a data factory</span></span>
1. <span data-ttu-id="70949-146">Inicie sesión en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="70949-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="70949-147">En el menú de la izquierda, haga clic en **NUEVO**, en **Inteligencia y análisis** y en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="70949-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nueva factoría de datos](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="70949-149">En la hoja **Nueva factoría de datos**, escriba **SProcDF** para el nombre.</span><span class="sxs-lookup"><span data-stu-id="70949-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="70949-150">Los nombres de Azure Data Factory son **únicos globalmente**.</span><span class="sxs-lookup"><span data-stu-id="70949-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="70949-151">Es necesario agregar su nombre como prefijo al nombre de la factoría de datos para permitir la creación correcta de la factoría.</span><span class="sxs-lookup"><span data-stu-id="70949-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Nueva factoría de datos](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="70949-153">Seleccione la **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="70949-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="70949-154">Para el **grupo de recursos**, realice uno de los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="70949-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="70949-155">Haga clic en **Crear nuevo** y escriba un nombre para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="70949-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="70949-156">Haga clic en **Usar existente** y seleccione un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="70949-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="70949-157">Seleccione la **ubicación** de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="70949-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="70949-158">Seleccione **Anclar al panel** de manera que pueda ver la factoría de datos en el panel la próxima vez que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="70949-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="70949-159">Haga clic en **Crear** en la hoja **Nueva fábrica de datos**.</span><span class="sxs-lookup"><span data-stu-id="70949-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="70949-160">Verá la factoría de datos que se crea en el **panel** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="70949-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="70949-161">Tras crear correctamente la factoría de datos, se ve la página de la factoría de datos, que muestra el contenido de la misma.</span><span class="sxs-lookup"><span data-stu-id="70949-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Página principal de Data Factory](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="70949-163">Crear un servicio vinculado SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="70949-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="70949-164">Después de crear la factoría de datos, cree un servicio vinculado de Azure SQL que conecte Azure SQL Database, que contiene la tabla sampletable y el procedimiento almacenado sp_sample, con la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="70949-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="70949-165">En la hoja **Crear e implementar**, haga clic en la hoja **Data Factory** para que **SProcDF** inicie Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="70949-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="70949-166">Haga clic en **Nuevo almacén de datos** en la barra de comandos y elija **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="70949-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="70949-167">Debería ver el script JSON para crear un servicio vinculado SQL de Azure en el editor.</span><span class="sxs-lookup"><span data-stu-id="70949-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Nuevo almacén de datos](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="70949-169">Realice los siguientes cambios en el script JSON:</span><span class="sxs-lookup"><span data-stu-id="70949-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="70949-170">Reemplace `<servername>` por el nombre del servidor de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="70949-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="70949-171">Reemplace `<databasename>` por la base de datos en la que creó la tabla y el procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="70949-172">Reemplace `<username@servername>` por la cuenta de usuario que tiene acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="70949-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="70949-173">Reemplace `<password>` por la contraseña de la cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="70949-173">Replace `<password>` with the password for the user account.</span></span>

      ![Nuevo almacén de datos](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="70949-175">Para implementar el servicio vinculado, haga clic en **Implementar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="70949-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="70949-176">Confirme que AzureSqlLinkedService aparece en la vista de árbol a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="70949-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="70949-178">Crear un conjunto de datos de salida</span><span class="sxs-lookup"><span data-stu-id="70949-178">Create an output dataset</span></span>
<span data-ttu-id="70949-179">Debe especificar un conjunto de datos de salida para una actividad de procedimiento almacenado aunque el procedimiento almacenado no genere ningún dato.</span><span class="sxs-lookup"><span data-stu-id="70949-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="70949-180">Esto se debe a que se trata del conjunto de datos de salida que determina la programación de la actividad (frecuencia con que se ejecuta la actividad: cada hora, diariamente, etc.).</span><span class="sxs-lookup"><span data-stu-id="70949-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="70949-181">El conjunto de datos de salida debe utilizar un **servicio vinculado** que haga referencia a una Base de datos SQL de Azure, un Almacenamiento de datos SQL o una base de datos de SQL Server donde desee que el procedimiento almacenado se ejecute.</span><span class="sxs-lookup"><span data-stu-id="70949-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="70949-182">El conjunto de datos de salida puede usarse como una forma de pasar el resultado del procedimiento almacenado para su posterior procesamiento por otra actividad ([encadenamiento de actividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) en la canalización.</span><span class="sxs-lookup"><span data-stu-id="70949-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="70949-183">Sin embargo, Data Factory no escribe automáticamente la salida de un procedimiento almacenado en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="70949-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="70949-184">Es el procedimiento almacenado el que escribe en una tabla SQL a la que apunta el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="70949-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="70949-185">En algunos casos, el conjunto de datos de salida puede ser un **conjunto de datos ficticio** (un conjunto de datos que apunta a una tabla que no contiene realmente la salida del procedimiento almacenado).</span><span class="sxs-lookup"><span data-stu-id="70949-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="70949-186">Este conjunto de datos ficticio solo se usa para especificar la programación de la ejecución de la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="70949-187">Haga clic en **... Más** en la barra de herramientas, haga clic en **Nuevo conjunto de datos** y en **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="70949-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="70949-188">Haga clic en **Nuevo conjunto de datos** en la barra de comandos y seleccione **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="70949-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="70949-190">Copie y pegue el siguiente script JSON en el editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="70949-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="70949-191">Para implementar el conjunto de datos, haga clic en **Implementar** en la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="70949-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="70949-192">Confirme que el conjunto de datos aparece en la vista de árbol.</span><span class="sxs-lookup"><span data-stu-id="70949-192">Confirm that you see the dataset in the tree view.</span></span>

    ![vista de árbol con servicios vinculados](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="70949-194">Crear una canalización con una actividad SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="70949-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="70949-195">Ahora, vamos a crear una canalización con una actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="70949-196">Tenga en cuenta las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="70949-196">Notice the following properties:</span></span> 

- <span data-ttu-id="70949-197">La propiedad **type** se establece en **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="70949-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="70949-198">El valor de **storedProcedureName** de las propiedades de tipo se establece en **sp_sample** (nombre del procedimiento almacenado).</span><span class="sxs-lookup"><span data-stu-id="70949-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="70949-199">La sección **storedProcedureParameters** contiene un parámetro denominado **DataTime**.</span><span class="sxs-lookup"><span data-stu-id="70949-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="70949-200">El nombre y el uso de mayúsculas y minúsculas en el parámetro JSON deben coincidir con los del parámetro de la definición del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="70949-201">Si necesita pasar null para un parámetro, use la sintaxis: `"param1": null` null (todo en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="70949-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="70949-202">Haga clic en **... Más** en la barra de comandos y en **Nueva canalización**.</span><span class="sxs-lookup"><span data-stu-id="70949-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="70949-203">Copie y pegue el siguiente fragmento de código JSON:</span><span class="sxs-lookup"><span data-stu-id="70949-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="70949-204">Para implementar la canalización, haga clic en **Implementar** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="70949-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="70949-205">Supervisar la canalización</span><span class="sxs-lookup"><span data-stu-id="70949-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="70949-206">Haga clic en el botón **X** para cerrar las hojas del Editor de Data Factory y volver a la hoja de Data Factory. A continuación, haga clic en **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="70949-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="70949-208">En la **Vista de diagrama**, se ve información general de las canalizaciones y los conjuntos de datos empleados en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="70949-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="70949-210">En la Vista de diagrama, haga doble clic en el conjunto de datos `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="70949-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="70949-211">Verá los segmentos con estado Listo.</span><span class="sxs-lookup"><span data-stu-id="70949-211">You see the slices in Ready state.</span></span> <span data-ttu-id="70949-212">Debería haber cinco segmentos, porque se genera un segmento para cada hora entre la hora de inicio y de finalización del código JSON.</span><span class="sxs-lookup"><span data-stu-id="70949-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![icono Diagrama](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="70949-214">Cuando un segmento tiene el estado **Listo**, ejecute una consulta `select * from sampletable` en la base de datos de Azure SQL para comprobar que el procedimiento almacenado insertó los datos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="70949-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Datos de salida](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="70949-216">Vea [Supervisar la canalización](data-factory-monitor-manage-pipelines.md) para obtener información detallada sobre cómo supervisar las canalizaciones de Factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="70949-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="70949-217">Especificación de un conjunto de datos de entrada</span><span class="sxs-lookup"><span data-stu-id="70949-217">Specify an input dataset</span></span>
<span data-ttu-id="70949-218">En el tutorial, la actividad de procedimiento almacenado no tiene ningún conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="70949-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="70949-219">Si especifica un conjunto de datos de entrada, la actividad de procedimiento almacenado no se ejecuta hasta que el segmento del conjunto de datos de entrada esté disponible (en estado Listo).</span><span class="sxs-lookup"><span data-stu-id="70949-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="70949-220">El conjunto de datos puede ser externo (no producido por otra actividad de la misma canalización) o interno que produce una actividad del canal de subida (la actividad que se ejecuta antes de esta).</span><span class="sxs-lookup"><span data-stu-id="70949-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="70949-221">Puede especificar varios conjuntos de datos de entrada para la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="70949-222">Si lo hace, la actividad de procedimiento almacenado solo se ejecuta cuando están disponibles todos los sectores de conjunto de datos de entrada (en estado Listo).</span><span class="sxs-lookup"><span data-stu-id="70949-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="70949-223">El conjunto de datos de entrada no se puede usar en el procedimiento almacenado como parámetro.</span><span class="sxs-lookup"><span data-stu-id="70949-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="70949-224">Solo se utiliza para comprobar la dependencia antes de iniciar la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="70949-225">Encadenamiento con otras actividades</span><span class="sxs-lookup"><span data-stu-id="70949-225">Chaining with other activities</span></span>
<span data-ttu-id="70949-226">Si quiere encadenar una actividad del canal de subida a esta actividad, especifique la salida de la actividad del canal de subida como entrada de esta actividad.</span><span class="sxs-lookup"><span data-stu-id="70949-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="70949-227">Al hacerlo, la actividad de procedimiento almacenado no se ejecuta hasta que la actividad del canal de subida finalice y el conjunto de datos de salida de la actividad del canal de subida esté disponible (en estado Listo).</span><span class="sxs-lookup"><span data-stu-id="70949-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="70949-228">Puede especificar conjuntos de datos de salida de varias actividades del canal de subida como conjuntos de datos de entrada de la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="70949-229">Si lo hace, la actividad de procedimiento almacenado solo se ejecuta cuando están disponibles todos los sectores de conjunto de datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="70949-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="70949-230">En el ejemplo siguiente, la salida de la actividad de copia es: OutputDataset, que es una entrada de la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="70949-231">Por consiguiente, la actividad de procedimiento almacenado no se ejecuta hasta que la actividad de copia finalice y el segmento OutputDataset esté disponible (en estado Listo).</span><span class="sxs-lookup"><span data-stu-id="70949-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="70949-232">Si especifica varios conjuntos de datos de entrada, la actividad de procedimiento almacenado no se ejecuta hasta que todos los segmentos del conjunto de datos de entrada estén disponibles (en estado Listo).</span><span class="sxs-lookup"><span data-stu-id="70949-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="70949-233">Los conjuntos de datos de entrada no se pueden usar directamente como parámetros en la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="70949-234">Para obtener más información sobre cómo encadenar actividades, vea [Varias actividades en una canalización](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="70949-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="70949-235">De manera similar, para vincular la actividad de procedimiento almacenado con **actividades de bajada** (las actividades que se ejecutan después de que finalice la actividad de procedimiento almacenado), especifique el conjunto de datos de salida de la actividad de procedimiento almacenado como entrada de la actividad de bajada en la canalización.</span><span class="sxs-lookup"><span data-stu-id="70949-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70949-236">Al copiar datos en Azure SQL Database o SQL Server, se puede configurar **SqlSink** en la actividad de copia para invocar un procedimiento almacenado mediante la propiedad **sqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="70949-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="70949-237">Para más información, consulte [Invocación del procedimiento almacenado desde la actividad de copia en Azure Data Factory](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="70949-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="70949-238">Para obtener más información sobre la propiedad, vea los artículos sobre los conectores siguientes: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties) y [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="70949-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="70949-239">Al copiar datos de Azure SQL Database, SQL Server o Azure SQL Data Warehouse, se puede configurar **SqlSource** en la actividad de copia para invocar un procedimiento almacenado de lectura de datos mediante la propiedad **sqlReaderStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="70949-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="70949-240">Para más información, consulte los artículos sobre los conectores siguientes: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties) y [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="70949-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="70949-241">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="70949-241">JSON format</span></span>
<span data-ttu-id="70949-242">Este es el formato JSON para definir una actividad de procedimiento almacenado:</span><span class="sxs-lookup"><span data-stu-id="70949-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="70949-243">En la tabla siguiente se describen estas propiedades JSON:</span><span class="sxs-lookup"><span data-stu-id="70949-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="70949-244">Propiedad</span><span class="sxs-lookup"><span data-stu-id="70949-244">Property</span></span> | <span data-ttu-id="70949-245">Descripción</span><span class="sxs-lookup"><span data-stu-id="70949-245">Description</span></span> | <span data-ttu-id="70949-246">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="70949-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70949-247">name</span><span class="sxs-lookup"><span data-stu-id="70949-247">name</span></span> | <span data-ttu-id="70949-248">Nombre de la actividad</span><span class="sxs-lookup"><span data-stu-id="70949-248">Name of the activity</span></span> |<span data-ttu-id="70949-249">Sí</span><span class="sxs-lookup"><span data-stu-id="70949-249">Yes</span></span> |
| <span data-ttu-id="70949-250">Descripción</span><span class="sxs-lookup"><span data-stu-id="70949-250">description</span></span> |<span data-ttu-id="70949-251">Texto que describe para qué se usa la actividad.</span><span class="sxs-lookup"><span data-stu-id="70949-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="70949-252">No</span><span class="sxs-lookup"><span data-stu-id="70949-252">No</span></span> |
| <span data-ttu-id="70949-253">type</span><span class="sxs-lookup"><span data-stu-id="70949-253">type</span></span> | <span data-ttu-id="70949-254">Se debe establecer en: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="70949-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="70949-255">Sí</span><span class="sxs-lookup"><span data-stu-id="70949-255">Yes</span></span> |
| <span data-ttu-id="70949-256">inputs</span><span class="sxs-lookup"><span data-stu-id="70949-256">inputs</span></span> | <span data-ttu-id="70949-257">Opcional.</span><span class="sxs-lookup"><span data-stu-id="70949-257">Optional.</span></span> <span data-ttu-id="70949-258">Si especifica un conjunto de datos de entrada, debe estar disponible (en estado "Listo") para que se ejecute la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="70949-259">El conjunto de datos de entrada no se puede usar en el procedimiento almacenado como parámetro.</span><span class="sxs-lookup"><span data-stu-id="70949-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="70949-260">Solo se utiliza para comprobar la dependencia antes de iniciar la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="70949-261">No</span><span class="sxs-lookup"><span data-stu-id="70949-261">No</span></span> |
| <span data-ttu-id="70949-262">outputs</span><span class="sxs-lookup"><span data-stu-id="70949-262">outputs</span></span> | <span data-ttu-id="70949-263">Debe especificar un conjunto de datos para una actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="70949-264">El conjunto de datos de salida especifica la **programación** para la actividad de procedimiento almacenada (por hora, semanal, mensual, etc.).</span><span class="sxs-lookup"><span data-stu-id="70949-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="70949-265">El conjunto de datos de salida debe utilizar un **servicio vinculado** que haga referencia a una Base de datos SQL de Azure, un Almacenamiento de datos SQL o una base de datos de SQL Server donde desee que el procedimiento almacenado se ejecute.</span><span class="sxs-lookup"><span data-stu-id="70949-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="70949-266">El conjunto de datos de salida puede usarse como una forma de pasar el resultado del procedimiento almacenado para su posterior procesamiento por otra actividad ([encadenamiento de actividades](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)) en la canalización.</span><span class="sxs-lookup"><span data-stu-id="70949-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="70949-267">Sin embargo, Data Factory no escribe automáticamente la salida de un procedimiento almacenado en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="70949-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="70949-268">Es el procedimiento almacenado el que escribe en una tabla SQL a la que apunta el conjunto de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="70949-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="70949-269">En algunos casos, el conjunto de datos de salida puede ser un **conjunto de datos ficticio**, que solo se utilice para especificar la programación para ejecutar la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="70949-270">Sí</span><span class="sxs-lookup"><span data-stu-id="70949-270">Yes</span></span> |
| <span data-ttu-id="70949-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="70949-271">storedProcedureName</span></span> |<span data-ttu-id="70949-272">Especifique el nombre del procedimiento almacenado de Azure SQL Database, Azure SQL Data Warehouse o la base de datos de SQL Server que se representa mediante el servicio vinculado que usa la tabla de salida.</span><span class="sxs-lookup"><span data-stu-id="70949-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="70949-273">Sí</span><span class="sxs-lookup"><span data-stu-id="70949-273">Yes</span></span> |
| <span data-ttu-id="70949-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="70949-274">storedProcedureParameters</span></span> |<span data-ttu-id="70949-275">Especifique valores para los parámetros del procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="70949-276">Si necesita pasar null para un parámetro, use la sintaxis: "param1": null (todo en minúsculas).</span><span class="sxs-lookup"><span data-stu-id="70949-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="70949-277">Vea el ejemplo siguiente para aprender el uso de esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="70949-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="70949-278">No</span><span class="sxs-lookup"><span data-stu-id="70949-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="70949-279">Pasar un valor estático</span><span class="sxs-lookup"><span data-stu-id="70949-279">Passing a static value</span></span>
<span data-ttu-id="70949-280">Ahora, pensemos en agregar otra columna denominada 'Escenario' en la tabla que contiene un valor estático denominado 'Ejemplo de documento'.</span><span class="sxs-lookup"><span data-stu-id="70949-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Datos de ejemplo 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="70949-282">**Tabla:**</span><span class="sxs-lookup"><span data-stu-id="70949-282">**Table:**</span></span>

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

<span data-ttu-id="70949-283">**Procedimiento almacenado:**</span><span class="sxs-lookup"><span data-stu-id="70949-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="70949-284">Ahora, pase el parámetro **Escenario** y el valor desde la actividad de procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="70949-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="70949-285">La sección **typeProperties** del ejemplo anterior es similar al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="70949-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="70949-286">**Conjuntos de datos de Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="70949-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="70949-287">**Canalización de Data Factory**</span><span class="sxs-lookup"><span data-stu-id="70949-287">**Data Factory pipeline**</span></span>

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