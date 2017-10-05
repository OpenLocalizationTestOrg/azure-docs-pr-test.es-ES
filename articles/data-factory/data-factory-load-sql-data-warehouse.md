---
title: Carga de terabytes de datos en SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="2b5bc-103">Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Data Factory</span><span class="sxs-lookup"><span data-stu-id="2b5bc-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="2b5bc-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) es una base de datos de escalado horizontal y basada en la nube que es capaz de procesar volúmenes masivos de datos (tanto relacionales como no relacionales).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="2b5bc-105">Basado en nuestra arquitectura de procesamiento paralelo masivo (MPP), SQL Data Warehouse está mejorado para controlar las cargas de trabajo empresariales.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="2b5bc-106">Ofrece elasticidad en la nube con la flexibilidad para escalar almacenamiento y proceso de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="2b5bc-107">La introducción a Azure SQL Data Warehouse es ahora más fácil que nunca usando **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="2b5bc-108">Azure Data Factory es un servicio de integración de datos basado en la nube completamente administrado que se puede utilizar para rellenar una instancia de SQL Data Warehouse con los datos del sistema existente, lo que ahorra tiempo durante la evaluación de SQL Data Warehouse y la creación de soluciones de análisis.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="2b5bc-109">Estos son los beneficios claves de cargar datos en Azure SQL Data Warehouse usando Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="2b5bc-110">**Fácil de configurar**: con un asistente intuitivo en 5 pasos sin necesidad de scripting.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="2b5bc-111">**Amplia compatibilidad para el almacenamiento de datos**: compatibilidad integrada para un amplio conjunto de almacenes de datos tanto locales como basados en la nube.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="2b5bc-112">**Seguro y conforme con la normativa**: los datos se transfieren a través de HTTPS o ExpressRoute y la presencia del servicio global garantiza que los datos nunca abandonan el límite geográfico</span><span class="sxs-lookup"><span data-stu-id="2b5bc-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="2b5bc-113">**Rendimiento sin precedentes mediante PolyBase**: el uso de Polybase es la forma más eficiente de mover datos a Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2b5bc-114">Mediante la característica de blob de almacenamiento provisional, puede alcanzar velocidades de carga altas para todos los tipos de almacenes de datos además de Azure Blob Storage, que es compatible con Polybase de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="2b5bc-115">En este artículo se muestra cómo utilizar el Asistente para copia de Data Factory para cargar 1 TB de datos de Azure Blob Storage a Azure SQL Data Warehouse en menos de 15 minutos, con un rendimiento superior a 1,2 GB por segundo.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="2b5bc-116">Este artículo proporciona instrucciones paso a paso para mover datos a Azure SQL Data Warehouse mediante el Asistente para copia.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="2b5bc-117">Para obtener información general acerca de las funcionalidades de Data Factory para el movimiento de datos hacia y desde Azure SQL Data Warehouse, consulte el artículo [Movimiento de datos hacia y desde SQL Data Warehouse mediante Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="2b5bc-118">También puede crear canalizaciones utilizando Azure Portal, Visual Studio, PowerShell, etc. Consulte [Tutorial: Copia de datos de Azure Blob Storage en Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para ver un tutorial rápido con instrucciones detalladas para usar la actividad de copia en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="2b5bc-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2b5bc-119">Prerequisites</span></span>
* <span data-ttu-id="2b5bc-120">Azure Blob Storage: este experimento usa Azure Blob Storage (GRS) para almacenar un conjunto de datos de prueba TPC-H.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="2b5bc-121">Si no dispone de una cuenta de Azure Storage, infórmese sobre [cómo crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="2b5bc-122">Datos [TPC-H](http://www.tpc.org/tpch/): vamos a usar TPC-H como conjunto de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="2b5bc-123">Para ello, tiene que utilizar `dbgen` desde el Kit de herramientas de TPC-H, lo que le ayudará a generar el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="2b5bc-124">Puede descargar código fuente para `dbgen` en las [herramientas de TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) y compilarlo usted mismo, o descargar el binario compilado desde [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="2b5bc-125">Ejecute dbgen.exe con los siguientes comandos para generar un archivo sin formato de 1 TB para la tabla `lineitem` propagada a través de 10 archivos:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="2b5bc-126">…</span><span class="sxs-lookup"><span data-stu-id="2b5bc-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="2b5bc-127">Ahora, copie los archivos generados Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="2b5bc-128">Consulte [Movimiento de datos hacia el sistema de archivos local y desde él con Azure Data Factory](data-factory-onprem-file-system-connector.md) para saber cómo hacer esto usando copia de ADF.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="2b5bc-129">Azure SQL Data Warehouse: este experimento carga datos en una instancia de Azure SQL Data Warehouse creada con 6.000 DWU</span><span class="sxs-lookup"><span data-stu-id="2b5bc-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="2b5bc-130">Consulte [Creación de una instancia de Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para obtener instrucciones detalladas sobre cómo crear una base de datos de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="2b5bc-131">Para obtener el mejor rendimiento posible de la carga en SQL Data Warehouse mediante Polybase, elegimos el número máximo de unidades de almacenamiento de datos (DWU) permitidas en la configuración de rendimiento, que es 6.000 DWU.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2b5bc-132">Al cargar desde Azure Blob, el rendimiento de carga de los datos es directamente proporcionales al número de DWU que se configura en SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="2b5bc-133">Cargar 1 TB en SQL Data Warehouse de 1000 DWU tarda 87 minutos (con un rendimiento aproximado de 200 MB por segundo) Cargar 1 TB en SQL Data Warehouse de 2000 DWU tarda 46 minutos (con un rendimiento aproximado de 380 MB por segundo) Cargar 1 TB en SQL Data Warehouse de 6000 DWU tarda 14 minutos (con un rendimiento aproximado de 1,2 GB por segundo)</span><span class="sxs-lookup"><span data-stu-id="2b5bc-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="2b5bc-134">Para crear una instancia de SQL Data Warehouse con 6.000 DWU, mueva el control deslizante de rendimiento hasta el tope a la derecha:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Control deslizante de rendimiento](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="2b5bc-136">Para una base de datos existente que no esté configurada con 6.000 DWU, puede escalarla verticalmente utilizando Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="2b5bc-137">Vaya a la base de datos en Azure Portal donde encontrará un botón **Escala** en el panel de **información general** que se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Botón de escala](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="2b5bc-139">Haga clic en el botón **Escala** para abrir el siguiente panel, mueva el control deslizante al valor máximo y haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Cuadro de diálogo Escala](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="2b5bc-141">Este experimento carga datos en Azure SQL Data Warehouse usando la clase de recursos `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="2b5bc-142">Para obtener el mejor rendimiento posible, la copia tiene que realizarse utilizando el usuario de SQL Data Warehouse que pertenece a la clase de recursos `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="2b5bc-143">Infórmese acerca de cómo hacerlo siguiendo las instrucciones en [Cambio de ejemplo de clase de recursos de usuario](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="2b5bc-144">Cree el esquema de la tabla de destino en Azure SQL Data Warehouse, ejecutando la siguiente instrucción DDL:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="2b5bc-145">Con los pasos previos completados, ahora estamos preparados configurar la actividad de copia mediante el Asistente para copia.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="2b5bc-146">Inicio del Asistente para copia</span><span class="sxs-lookup"><span data-stu-id="2b5bc-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="2b5bc-147">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2b5bc-148">Haga clic en **+ NUEVO** en la esquina superior izquierda, después en **Inteligencia y análisis** y en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="2b5bc-149">En la hoja **Nueva factoría de datos** :</span><span class="sxs-lookup"><span data-stu-id="2b5bc-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="2b5bc-150">Escriba **LoadIntoSQLDWDataFactory** para el **nombre**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="2b5bc-151">El nombre del generador de datos de Azure debe ser único global.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="2b5bc-152">Si recibe el error: **El nombre de factoría de datos "LoadIntoSQLDWDataFactory" no está disponible**, cambie el nombre de la factoría de datos (por ejemplo, sunombreLoadIntoSQLDWDataFactory) e intente crearla de nuevo.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="2b5bc-153">Consulte el tema [Factoría de datos: reglas de nomenclatura](data-factory-naming-rules.md) para las reglas de nomenclatura para los artefactos de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="2b5bc-154">Selección la **suscripción**de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="2b5bc-155">Para el grupo de recursos, realice uno de los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="2b5bc-156">Seleccione en primer lugar **Usar existente** y después un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="2b5bc-157">Seleccione **Crear nuevo** y escriba un nombre para un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="2b5bc-158">Seleccione una **ubicación** para la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="2b5bc-159">Seleccione la casilla **Anclar al panel** en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="2b5bc-160">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-160">Click **Create**.</span></span>
4. <span data-ttu-id="2b5bc-161">Una vez completada la creación, puede ver la hoja **Data Factory** como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Página principal de Factoría de datos](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="2b5bc-163">En la página principal de Data Factory, haga clic en el icono **Copiar datos** para iniciar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b5bc-164">Si ve que el explorador web está atascado en "Autorizando...", deshabilite o desactive la opción **Bloquear cookies y datos de sitios de terceros** o déjela habilitada y cree una excepción para **login.microsoftonline.com** e intente iniciar de nuevo el asistente.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="2b5bc-165">Paso 1: Configuración de la programación de carga de datos</span><span class="sxs-lookup"><span data-stu-id="2b5bc-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="2b5bc-166">El primer paso es configurar la programación de carga de datos.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="2b5bc-167">En la página **Propiedades** :</span><span class="sxs-lookup"><span data-stu-id="2b5bc-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="2b5bc-168">Escriba **CopyFromBlobToAzureSqlDataWarehouse** en **Nombre de tarea**</span><span class="sxs-lookup"><span data-stu-id="2b5bc-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="2b5bc-169">Seleccione la opción **Ejecutar una vez ahora**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="2b5bc-170">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-170">Click **Next**.</span></span>  

    ![Asistente para copia: Página Propiedades](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="2b5bc-172">Paso 2: Configuración del origen</span><span class="sxs-lookup"><span data-stu-id="2b5bc-172">Step 2: Configure source</span></span>
<span data-ttu-id="2b5bc-173">Esta sección muestra los pasos necesarios para configurar el origen: Esta sección muestra los pasos necesarios para configurar el origen: instancia de Azure Blob que contiene los archivos del elemento de línea 1-TB TPC-H.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="2b5bc-174">Seleccione **Azure Blob Storage** como almacén de datos y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Asistente para copia: Selección de página de origen](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="2b5bc-176">Rellene la información de conexión para la cuenta de Azure Blob Storage y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Asistente para copia: Información de conexión de origen](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="2b5bc-178">Elija la **carpeta** que contiene los archivos de elemento de línea TPC-H y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Asistente para copia: Selección de carpeta de entrada](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="2b5bc-180">Al hacer clic en **Siguiente**, se detectan automáticamente los ajustes de formato de archivo.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="2b5bc-181">Asegúrese de que el delimitador de columnas es " | " en lugar del ajuste predeterminado de la coma ",".</span><span class="sxs-lookup"><span data-stu-id="2b5bc-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="2b5bc-182">Haga clic en **Siguiente** después de realizar una vista previa de los datos.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-182">Click **Next** after you have previewed the data.</span></span>

    ![Herramienta de copia: Ajustes de formato de archivo](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="2b5bc-184">Paso 3: Configuración del destino</span><span class="sxs-lookup"><span data-stu-id="2b5bc-184">Step 3: Configure destination</span></span>
<span data-ttu-id="2b5bc-185">En esta sección muestra cómo configurar el destino: tabla `lineitem` en la base de datos de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="2b5bc-186">Elija **Azure SQL Data Warehouse** como el destino de almacenamiento y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Asistente para copia: Selección del almacén de datos de destino](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="2b5bc-188">Rellene la información de conexión para Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="2b5bc-189">Asegúrese de especificar el usuario que sea miembro del rol `xlargerc` (consulte la sección **Requisitos previos** para obtener instrucciones detalladas) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Asistente para copia: Información de conexión de destino](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="2b5bc-191">Elija la tabla de destino y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-191">Choose the destination table and click **Next**.</span></span>

    ![Asistente para copia: Página de asignación de tabla](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="2b5bc-193">En la página de asignación de esquemas, deje desactivada la opción "Apply column mapping" (Aplicar asignación de columna) y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="2b5bc-194">Paso 4: Configuración de rendimiento</span><span class="sxs-lookup"><span data-stu-id="2b5bc-194">Step 4: Performance settings</span></span>

<span data-ttu-id="2b5bc-195">La opción **Allow polybase** (Permitir Polybase) está activada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="2b5bc-196">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-196">Click **Next**.</span></span>

![Asistente para copia: Página de asignación de esquema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="2b5bc-198">Paso 5: Implementación y supervisión de los resultados de carga</span><span class="sxs-lookup"><span data-stu-id="2b5bc-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="2b5bc-199">Haga clic en el botón **Finalizar** para implementar.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-199">Click **Finish** button to deploy.</span></span>

    ![Asistente para copiar: Página de resumen](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="2b5bc-201">Una vez completada la implementación, haga clic en `Click here to monitor copy pipeline` para supervisar el progreso de la ejecución de la copia.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="2b5bc-202">Seleccione la canalización de copia que creó en la lista **Activity Windows** (Ventanas de actividad).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Asistente para copiar: Página de resumen](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="2b5bc-204">Puede ver los detalles de la ejecución de la copia en **Activity Window Explorer** (Explorador de la ventana de actividad) en el panel derecho, esta información incluye el volumen de datos leídos en el origen y escritos en el destino, y el rendimiento medio de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="2b5bc-205">Como puede ver en la captura de pantalla siguiente, se tardaron 14 minutos en copiar 1 TB de Azure Blob Storage en SQL Data Warehouse, lo que quiere decir que se alcanzó el rendimiento de 1,22 GB por segundo.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Asistente para copia: Cuadro de diálogo de éxito en la operación](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="2b5bc-207">Prácticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="2b5bc-207">Best practices</span></span>
<span data-ttu-id="2b5bc-208">Estas son algunos de los procedimientos recomendados para la ejecución de la base de datos de Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="2b5bc-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="2b5bc-209">Use una clase de recurso más grande al cargar en un ÍNDICE AGRUPADO DE ALMACÉN DE COLUMNAS.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="2b5bc-210">Para las combinaciones más eficaces, considere el uso de distribución hash con una columna seleccionada, en lugar de la distribución round robin predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="2b5bc-211">Para conseguir una mayor velocidad de carga, considere la posibilidad de utilizar un montón para los datos transitorios.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="2b5bc-212">Cree estadísticas después de finalizar la carga de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="2b5bc-213">Para información más detallada consulte [Procedimientos recomendados para Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2b5bc-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b5bc-214">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2b5bc-214">Next steps</span></span>
* <span data-ttu-id="2b5bc-215">[Asistente para copia de Data Factory](data-factory-copy-wizard.md): este artículo proporciona detalles sobre el Asistente para copia.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="2b5bc-216">[Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md): este artículo contiene la guía de optimización y medidas de rendimiento de la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="2b5bc-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
