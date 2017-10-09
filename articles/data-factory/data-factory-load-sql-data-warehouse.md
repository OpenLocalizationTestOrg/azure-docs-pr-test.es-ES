---
title: aaaLoad terabytes de datos en almacenamiento de datos SQL | Documentos de Microsoft
description: "Muestra cómo se puede cargar 1 TB de datos en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="ea3ae-103">Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Data Factory</span><span class="sxs-lookup"><span data-stu-id="ea3ae-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="ea3ae-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) es una base de datos de escalado horizontal y basada en la nube que es capaz de procesar volúmenes masivos de datos (tanto relacionales como no relacionales).</span><span class="sxs-lookup"><span data-stu-id="ea3ae-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="ea3ae-105">Basado en nuestra arquitectura de procesamiento paralelo masivo (MPP), SQL Data Warehouse está mejorado para controlar las cargas de trabajo empresariales.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="ea3ae-106">Ofrece elasticidad con almacenamiento de tooscale de hello flexibilidad en la nube y calcular de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="ea3ae-107">La introducción a Azure SQL Data Warehouse es ahora más fácil que nunca usando **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="ea3ae-108">Factoría de datos de Azure es un servicio de integración de datos en la nube totalmente administrado, que puede ser usado toopopulate un almacenamiento de datos de SQL con datos de saludo del sistema actual y ahorra tiempo valioso durante la evaluación de almacenamiento de datos SQL y creación de sus análisis soluciones.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="ea3ae-109">Estos son las principales ventajas de Hola de cargar datos en almacenamiento de datos de SQL Azure mediante Data Factory de Azure:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="ea3ae-110">**Fácil tooset seguridad**: paso 5 asistente intuitivo sin scripting necesarios.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="ea3ae-111">**Amplia compatibilidad para el almacenamiento de datos**: compatibilidad integrada para un amplio conjunto de almacenes de datos tanto locales como basados en la nube.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="ea3ae-112">**Seguros y conformes**: los datos se transfieren a través de HTTPS o ExpressRoute y presencia de servicio global garantiza que los datos nunca abandona los límites geográficos de Hola</span><span class="sxs-lookup"><span data-stu-id="ea3ae-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="ea3ae-113">**Rendimiento sin parangón mediante PolyBase** : uso de Polybase es datos de toomove de manera más eficaces de hello en almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ea3ae-114">Hola característica blobs de almacenamiento provisional se pueden conseguir velocidades de alta carga de todos los tipos de almacenes de datos además de almacenamiento de blobs de Azure, que Hola Polybase admite de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="ea3ae-115">Este artículo muestra cómo toouse Asistente para copiar de factoría de datos tooload 1 TB de datos desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL Azure en menos de 15 minutos, a más de 1,2 rendimiento GBps.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="ea3ae-116">Este artículo proporciona instrucciones paso a paso para mover datos a almacenamiento de datos de SQL Azure mediante el uso de hello Asistente para copiar.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="ea3ae-117">Para obtener información general acerca de las capacidades de la factoría de datos para mover datos hacia y desde el almacenamiento de datos de SQL Azure, consulte [mover tooand de datos de almacenamiento de datos de SQL Azure mediante Data Factory de Azure](data-factory-azure-sql-data-warehouse-connector.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="ea3ae-118">También puede crear canalizaciones utilizando Azure Portal, Visual Studio, PowerShell, etc. Vea [Tutorial: copiar los datos de Blob de Azure tooAzure base de datos SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para ver un tutorial rápido con instrucciones paso a paso para usar Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="ea3ae-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ea3ae-119">Prerequisites</span></span>
* <span data-ttu-id="ea3ae-120">Azure Blob Storage: este experimento usa Azure Blob Storage (GRS) para almacenar un conjunto de datos de prueba TPC-H.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="ea3ae-121">Si no tiene una cuenta de almacenamiento de Azure, descubra [cómo toocreate una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ea3ae-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="ea3ae-122">[TPC-H](http://www.tpc.org/tpch/) datos: vamos toouse TPC-H como Hola prueba del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="ea3ae-123">toodo esto, necesita toouse `dbgen` del Kit de herramientas de TPC-H, que le ayudará a generar el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="ea3ae-124">Puede optar por descargar código fuente de `dbgen` de [TPC herramientas](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) y compílelo usted mismo o descarga Hola compila binarios de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="ea3ae-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="ea3ae-125">Ejecución dbgen.exe con siguiente Hola comandos de archivo sin formato de 1 TB de toogenerate para `lineitem` tabla propagación en 10 archivos:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="ea3ae-126">…</span><span class="sxs-lookup"><span data-stu-id="ea3ae-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="ea3ae-127">Ahora Hola copia genera archivos tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="ea3ae-128">Consulte demasiado[mover tooand de datos de un sistema de archivos local mediante el uso de Data Factory de Azure](data-factory-onprem-file-system-connector.md) para saber cómo toodo que mediante la copia de ADF.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="ea3ae-129">Azure SQL Data Warehouse: este experimento carga datos en una instancia de Azure SQL Data Warehouse creada con 6.000 DWU</span><span class="sxs-lookup"><span data-stu-id="ea3ae-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="ea3ae-130">Consulte demasiado[para crear un almacén de datos de SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para obtener instrucciones detalladas sobre cómo toocreate un almacenamiento de datos SQL de base de datos.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="ea3ae-131">tooget Hola carga posible un rendimiento óptimo en almacenamiento de datos de SQL con Polybase, elegimos número máximo de unidades de almacenamiento de datos (a Dwu) permitido en la configuración de rendimiento de hello, que es 6.000 a Dwu.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ea3ae-132">Al cargar desde el Blob de Azure, rendimiento de carga de datos de hello están el número de toohello directamente proporcional de a Dwu se configura en hello almacenamiento de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="ea3ae-133">Cargar 1 TB en SQL Data Warehouse de 1000 DWU tarda 87 minutos (con un rendimiento aproximado de 200 MB por segundo) Cargar 1 TB en SQL Data Warehouse de 2000 DWU tarda 46 minutos (con un rendimiento aproximado de 380 MB por segundo) Cargar 1 TB en SQL Data Warehouse de 6000 DWU tarda 14 minutos (con un rendimiento aproximado de 1,2 GB por segundo)</span><span class="sxs-lookup"><span data-stu-id="ea3ae-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="ea3ae-134">toocreate un almacenamiento de datos de SQL con a 6.000 Dwu, mover la control deslizante de rendimiento de hello todos los toohello de manera Hola derecha:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Control deslizante de rendimiento](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="ea3ae-136">Para una base de datos existente que no esté configurada con 6.000 DWU, puede escalarla verticalmente utilizando Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="ea3ae-137">Navegar por la base de datos de toohello en el portal de Azure y no hay un **escala** botón en hello **información general sobre** panel se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Botón de escala](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="ea3ae-139">Haga clic en hello **escala** siguiente de hello tooopen botón panel, mover el valor máximo de toohello de control deslizante de Hola y haga clic en **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Cuadro de diálogo Escala](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="ea3ae-141">Este experimento carga datos en Azure SQL Data Warehouse usando la clase de recursos `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="ea3ae-142">necesidades de copia de tooachieve mejor rendimiento posible, toobe realiza con un usuario de almacenamiento de datos de SQL que pertenezca demasiado`xlargerc` clase de recursos.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="ea3ae-143">Obtenga información acerca de cómo toodo que siguiendo [cambiar un ejemplo de clase del recurso de usuario](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="ea3ae-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="ea3ae-144">Crear esquema de la tabla de destino en la base de datos de almacenamiento de datos de SQL Azure, mediante la ejecución de hello después de la instrucción DDL:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="ea3ae-145">Con los pasos de requisitos previos de hello completados, ahora estamos actividad de copia de hello tooconfigure listo con hello Asistente para copiar.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="ea3ae-146">Inicio del Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="ea3ae-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="ea3ae-147">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea3ae-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ea3ae-148">Haga clic en **+ nuevo** desde la esquina superior izquierda de hello, haga clic en **Intelligence + análisis**y haga clic en **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="ea3ae-149">Hola **factoría de datos** hoja:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="ea3ae-150">Escriba **LoadIntoSQLDWDataFactory** para hello **nombre**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="ea3ae-151">nombre de Hola Hola Azure factoría de datos debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="ea3ae-152">Si recibe el error hello: **nombre de generador de datos "LoadIntoSQLDWDataFactory" no está disponible**, cambiar nombre de Hola Hola factoría de datos (por ejemplo, yournameLoadIntoSQLDWDataFactory) y pruebe a crear de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="ea3ae-153">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="ea3ae-154">Selección la **suscripción**de Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="ea3ae-155">Para el grupo de recursos, realice una de hello pasos:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="ea3ae-156">Seleccione **utilizar existente** tooselect un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="ea3ae-157">Seleccione **crear nuevo** tooenter un nombre para un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="ea3ae-158">Seleccione un **ubicación** de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="ea3ae-159">Seleccione **toodashboard Pin** casilla situada en la parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="ea3ae-160">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-160">Click **Create**.</span></span>
4. <span data-ttu-id="ea3ae-161">Una vez completada la creación de hello, vea hello **factoría de datos** hoja como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Página principal de Factoría de datos](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="ea3ae-163">En la página de inicio de la factoría de datos de hello, haga clic en hello **copiar datos** icono toolaunch **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ea3ae-164">Si ve ese explorador web de hello está atascado en "Autorizar …", deshabilite o desactive **bloquear las cookies de terceros y datos de sitio** configuración (o) manténgala habilitada y cree una excepción para **login.microsoftonline.com**y, a continuación, intente iniciar Asistente de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="ea3ae-165">Paso 1: Configuración de la programación de carga de datos</span><span class="sxs-lookup"><span data-stu-id="ea3ae-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="ea3ae-166">Hola primer paso es programación al cargar los datos tooconfigure Hola.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="ea3ae-167">Hola **propiedades** página:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="ea3ae-168">Escriba **CopyFromBlobToAzureSqlDataWarehouse** en **Nombre de tarea**</span><span class="sxs-lookup"><span data-stu-id="ea3ae-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="ea3ae-169">Seleccione la opción **Ejecutar una vez ahora**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="ea3ae-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-170">Click **Next**.</span></span>  

    ![Asistente para copia: Página Propiedades](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="ea3ae-172">Paso 2: Configuración del origen</span><span class="sxs-lookup"><span data-stu-id="ea3ae-172">Step 2: Configure source</span></span>
<span data-ttu-id="ea3ae-173">En esta sección se muestra Hola pasos tooconfigure origen de hello: Blob de Azure que contiene Hola 1 TB TPC-archivos de elementos de línea de H.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="ea3ae-174">Seleccione hello **almacenamiento de blobs de Azure** como datos de hello almacenar y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Asistente para copia: Selección de página de origen](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="ea3ae-176">Rellene la información de conexión de Hola para hello cuenta de almacenamiento Blob de Azure y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Asistente para copia: Información de conexión de origen](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="ea3ae-178">Elija hello **carpeta** que contiene la línea hello TPC-H elemento archivos y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Asistente para copia: Selección de carpeta de entrada](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="ea3ae-180">Al hacer clic en **siguiente**, configuración de formato de archivo de Hola se detecta automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="ea3ae-181">Comprobar toomake seguro de que el delimitador de columnas es ' | 'en lugar de hello predeterminado por comas','.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="ea3ae-182">Haga clic en **siguiente** después de que ha obtenido una vista previa de los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-182">Click **Next** after you have previewed hello data.</span></span>

    ![Herramienta de copia: Ajustes de formato de archivo](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="ea3ae-184">Paso 3: Configuración del destino</span><span class="sxs-lookup"><span data-stu-id="ea3ae-184">Step 3: Configure destination</span></span>
<span data-ttu-id="ea3ae-185">Esta sección muestra cómo tooconfigure Hola destino: `lineitem` tabla de base de datos de almacenamiento de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="ea3ae-186">Elija **almacenamiento de datos de SQL Azure** como destino de hello almacenar y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Asistente para copia: Selección del almacén de datos de destino](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="ea3ae-188">Rellene la información de conexión de hello para el almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="ea3ae-189">Asegúrese de especificar usuario Hola que es un miembro del rol de hello `xlargerc` (vea hello **requisitos previos** sección para obtener instrucciones detalladas) y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Asistente para copia: Información de conexión de destino](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="ea3ae-191">Elegir tabla de destino de Hola y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-191">Choose hello destination table and click **Next**.</span></span>

    ![Asistente para copia: Página de asignación de tabla](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="ea3ae-193">En la página de asignación de esquemas, deje desactivada la opción "Apply column mapping" (Aplicar asignación de columna) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="ea3ae-194">Paso 4: Configuración de rendimiento</span><span class="sxs-lookup"><span data-stu-id="ea3ae-194">Step 4: Performance settings</span></span>

<span data-ttu-id="ea3ae-195">La opción **Allow polybase** (Permitir Polybase) está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="ea3ae-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-196">Click **Next**.</span></span>

![Asistente para copia: Página de asignación de esquema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="ea3ae-198">Paso 5: Implementación y supervisión de los resultados de carga</span><span class="sxs-lookup"><span data-stu-id="ea3ae-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="ea3ae-199">Haga clic en **finalizar** toodeploy de botón.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-199">Click **Finish** button toodeploy.</span></span>

    ![Asistente para copiar: Página de resumen](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="ea3ae-201">Una vez completada la implementación de hello, haga clic en `Click here toomonitor copy pipeline` copia de hello toomonitor progreso de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="ea3ae-202">Canalización de copia de hello SELECT que creó en hello **Windows actividad** lista.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Asistente para copiar: Página de resumen](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="ea3ae-204">Puede ver detalles de la serie de Hola de copia de hello **Explorer de la ventana de actividad** en el panel derecho hello, incluidos el volumen de datos de hello leídos del origen y escribir en el destino, la duración y el rendimiento medio de Hola para hello ejecutar.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="ea3ae-205">Como puede ver en hello siguiente captura de pantalla, copiar 1 TB de almacenamiento de blobs de Azure en almacenamiento de datos de SQL tardó 14 minutos, eficazmente un rendimiento de GBps 1,22!</span><span class="sxs-lookup"><span data-stu-id="ea3ae-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Asistente para copia: Cuadro de diálogo de éxito en la operación](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="ea3ae-207">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="ea3ae-207">Best practices</span></span>
<span data-ttu-id="ea3ae-208">Estas son algunos de los procedimientos recomendados para la ejecución de la base de datos de Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="ea3ae-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="ea3ae-209">Use una clase de recurso más grande al cargar en un ÍNDICE AGRUPADO DE ALMACÉN DE COLUMNAS.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="ea3ae-210">Para las combinaciones más eficaces, considere el uso de distribución hash con una columna seleccionada, en lugar de la distribución round robin predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="ea3ae-211">Para conseguir una mayor velocidad de carga, considere la posibilidad de utilizar un montón para los datos transitorios.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="ea3ae-212">Cree estadísticas después de finalizar la carga de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="ea3ae-213">Para información más detallada consulte [Procedimientos recomendados para Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="ea3ae-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea3ae-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea3ae-214">Next steps</span></span>
* <span data-ttu-id="ea3ae-215">[Asistente para copiar de factoría de datos](data-factory-copy-wizard.md) -este artículo proporciona detalles acerca de hello Asistente para copiar.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="ea3ae-216">[Copiar actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md) -este artículo contiene las medidas de rendimiento de referencia de Hola y Guía de optimización.</span><span class="sxs-lookup"><span data-stu-id="ea3ae-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
