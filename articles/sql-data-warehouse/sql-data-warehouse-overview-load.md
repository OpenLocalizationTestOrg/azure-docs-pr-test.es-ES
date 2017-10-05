---
title: Carga de datos en Azure SQL Data Warehouse | Microsoft Docs
description: "Conozca los escenarios comunes para la carga de datos en Almacenamiento de datos SQL. Estos incluyen el uso de PolyBase, el almacenamiento de blobs de Azure, archivos planos y el envío de discos. También puede usar herramientas de otros fabricantes."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="f5591-105">Carga de datos en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="f5591-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f5591-106">Resumen de las opciones de escenario y recomendaciones para cargar datos en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="f5591-107">La parte más difícil de carga de datos suele ser la preparación de los datos para la carga.</span><span class="sxs-lookup"><span data-stu-id="f5591-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="f5591-108">Azure simplifica la carga mediante el almacenamiento de blobs de Azure como almacén de datos común para muchos de los servicios y usando Data Factory de Azure para organizar la comunicación y el movimiento de datos entre los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5591-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="f5591-109">Estos procesos se integran con la tecnología PolyBase, que usa el procesamiento paralelo masivo (MPP) para cargar datos en paralelo desde el almacenamiento de blobs de Azure en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="f5591-110">Para ver tutoriales que cargan bases de datos de ejemplo, vea [Carga de datos de ejemplo en SQL Data Warehouse][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="f5591-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="f5591-111">Carga desde el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="f5591-111">Load from Azure blob storage</span></span>
<span data-ttu-id="f5591-112">La manera más rápida de importar datos en Almacenamiento de datos SQL es usar PolyBase para cargar datos desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5591-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="f5591-113">PolyBase usa el procesamiento paralelo masivo (MPP) de Almacenamiento de datos SQL para cargar datos en paralelo desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5591-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="f5591-114">Para usar PolyBase, puede usar comandos T-SQL o una canalización de Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5591-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="f5591-115">1. Usar PolyBase y T-SQL</span><span class="sxs-lookup"><span data-stu-id="f5591-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="f5591-116">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="f5591-116">Summary of loading process:</span></span>

1. <span data-ttu-id="f5591-117">Mueva los datos a Azure Blob Storage o Azure Data Lake Store y almacénelos en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="f5591-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="f5591-118">Configure objetos externos en Almacenamiento de datos SQL para definir la ubicación y el formato de los datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="f5591-119">Ejecute un comando T-SQL para cargar los datos en paralelo en una nueva tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="f5591-120">Para ver un tutorial, consulte [Carga de datos de Azure Blob Storage en SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="f5591-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="f5591-121">2. Usar Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="f5591-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="f5591-122">Para usar PolyBase de manera más sencilla, puede crear una canalización de Data Factory de Azure que use PolyBase para cargar datos del almacenamiento de blobs de Azure en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="f5591-123">Esto se configura rápido porque no es necesario definir los objetos T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="f5591-124">Si necesita consultar los datos externos sin importarlos, use T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="f5591-125">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="f5591-125">Summary of loading process:</span></span>

1. <span data-ttu-id="f5591-126">Mueva los datos al almacenamiento de blobs de Azure y almacénelos en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="f5591-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="f5591-127">Azure Data Factory no admite actualmente la conectividad de ADLS con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f5591-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="f5591-128">Cree una canalización de Data Factory de Azure para introducir los datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="f5591-129">Use la opción PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f5591-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="f5591-130">Programe y ejecute la canalización.</span><span class="sxs-lookup"><span data-stu-id="f5591-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="f5591-131">Para ver un tutorial, consulte [Carga de datos de Azure Blob Storage en SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="f5591-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="f5591-132">Carga desde SQL Server</span><span class="sxs-lookup"><span data-stu-id="f5591-132">Load from SQL Server</span></span>
<span data-ttu-id="f5591-133">Para cargar datos desde SQL Server en Almacenamiento de datos SQL, puede usar Integration Services (SSIS), transferir archivos planos o enviar discos a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5591-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="f5591-134">Siga leyendo para ver un resumen de los distintos procesos de carga y los vínculos a tutoriales.</span><span class="sxs-lookup"><span data-stu-id="f5591-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="f5591-135">Para planear una migración de datos completa de SQL Server a SQL Data Warehouse, consulte la [información general sobre migración][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="f5591-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="f5591-136">Uso de Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="f5591-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="f5591-137">Si ya usa paquetes de Integration Services (SSIS) para cargarlos en SQL Server, puede actualizarlos para usar SQL Server como origen y Almacenamiento de datos SQL como destino.</span><span class="sxs-lookup"><span data-stu-id="f5591-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="f5591-138">Esto es rápido y fácil de hacer, y es una buena opción si no desea migrar el proceso de carga para usar datos que ya están en la nube.</span><span class="sxs-lookup"><span data-stu-id="f5591-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="f5591-139">La desventaja es que la carga será más lenta que con PolyBase porque este SSIS no realiza la carga en paralelo.</span><span class="sxs-lookup"><span data-stu-id="f5591-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="f5591-140">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="f5591-140">Summary of loading process:</span></span>

1. <span data-ttu-id="f5591-141">Revisar el paquete de Integration Services para que apunte a la instancia de SQL Server para el origen y a la base de datos de Almacenamiento de datos SQL para el destino.</span><span class="sxs-lookup"><span data-stu-id="f5591-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="f5591-142">Migre el esquema a Almacenamiento de datos SQL si aún no está allí.</span><span class="sxs-lookup"><span data-stu-id="f5591-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="f5591-143">Cambie la asignación en los paquetes para usar solamente los tipos de datos que admite Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="f5591-144">Programe y ejecute el paquete.</span><span class="sxs-lookup"><span data-stu-id="f5591-144">Schedule and run the package.</span></span>

<span data-ttu-id="f5591-145">Para ver un tutorial, consulte [Carga de datos de SQL Server en Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="f5591-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="f5591-146">Uso de AZCopy (recomendado para datos de menos de 10 TB)</span><span class="sxs-lookup"><span data-stu-id="f5591-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="f5591-147">Si el tamaño de los datos es menor que 10 TB, puede exportar los datos de SQL Server a archivos planos, copiar los archivos al almacenamiento de blobs de Azure y luego usar PolyBase para cargar los datos en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="f5591-148">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="f5591-148">Summary of loading process:</span></span>

1. <span data-ttu-id="f5591-149">Use la utilidad de línea de comandos bcp para exportar datos de SQL Server a archivos planos.</span><span class="sxs-lookup"><span data-stu-id="f5591-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="f5591-150">Usar la utilidad de línea de comandos AZCopy para copiar datos de archivos planos en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5591-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="f5591-151">Use PolyBase para cargar datos en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f5591-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="f5591-152">Para ver un tutorial, consulte [Carga de datos de Azure Blob Storage en SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="f5591-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="f5591-153">Uso de bcp</span><span class="sxs-lookup"><span data-stu-id="f5591-153">Use bcp</span></span>
<span data-ttu-id="f5591-154">Si tiene una pequeña cantidad de datos, puede usar bcp para cargar directamente en Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f5591-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="f5591-155">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="f5591-155">Summary of loading process:</span></span>

1. <span data-ttu-id="f5591-156">Use la utilidad de línea de comandos bcp para exportar datos de SQL Server a archivos planos.</span><span class="sxs-lookup"><span data-stu-id="f5591-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="f5591-157">Use bcp para cargar datos de archivos planos directamente en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f5591-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="f5591-158">Para ver un tutorial, consulte [Carga de datos de SQL Server en Azure SQL Data Warehouse (archivos planos)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="f5591-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="f5591-159">Uso de importación/exportación (recomendado para datos de menos de 10 TB)</span><span class="sxs-lookup"><span data-stu-id="f5591-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="f5591-160">Si el tamaño de los datos es menor que 10 TB y quiere moverlos a Azure, se recomienda que use el servicio de envío de discos [Import/Export][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="f5591-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="f5591-161">Resumen del proceso de carga</span><span class="sxs-lookup"><span data-stu-id="f5591-161">Summary of loading process</span></span>

1. <span data-ttu-id="f5591-162">Use la utilidad de línea de comandos bcp para exportar datos de SQL Server a archivos planos o discos transferibles.</span><span class="sxs-lookup"><span data-stu-id="f5591-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="f5591-163">Envíe los discos a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f5591-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="f5591-164">Microsoft carga los datos en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="f5591-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="f5591-165">Carga desde HDInsight</span><span class="sxs-lookup"><span data-stu-id="f5591-165">Load from HDInsight</span></span>
<span data-ttu-id="f5591-166">El Almacenamiento de datos SQL admite la carga de datos desde HDInsight a través de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f5591-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="f5591-167">El proceso es el mismo que para cargar datos desde el Almacenamiento de blobs de Azure: mediante PolyBase para conectarse a HDInsight para cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="f5591-168">1. Usar PolyBase y T-SQL</span><span class="sxs-lookup"><span data-stu-id="f5591-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="f5591-169">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="f5591-169">Summary of loading process:</span></span>

1. <span data-ttu-id="f5591-170">Mueva los datos a HDInsight y almacénelos en formato de archivos de texto, ORC o Parquet.</span><span class="sxs-lookup"><span data-stu-id="f5591-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="f5591-171">Configure objetos externos en Almacenamiento de datos SQL para definir la ubicación y el formato de los datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="f5591-172">Ejecute un comando T-SQL para cargar los datos en paralelo en una nueva tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="f5591-173">Para ver un tutorial, consulte [Carga de datos de Azure Blob Storage en SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="f5591-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="f5591-174">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="f5591-174">Recommendations</span></span>
<span data-ttu-id="f5591-175">Muchos de nuestros asociados tienen soluciones de carga.</span><span class="sxs-lookup"><span data-stu-id="f5591-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="f5591-176">Para más información, consulte una lista de los [asociados de soluciones][solution partners].</span><span class="sxs-lookup"><span data-stu-id="f5591-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="f5591-177">Si los datos provienen de un origen no relacional y quiere cargarlos en Almacenamiento de datos SQL,debe transformarlos en filas y columnas antes de cargarlos.</span><span class="sxs-lookup"><span data-stu-id="f5591-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="f5591-178">Los datos transformados no necesitan almacenarse en una base de datos; se puede almacenar en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="f5591-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="f5591-179">Cree estadísticas de los datos recién cargados.</span><span class="sxs-lookup"><span data-stu-id="f5591-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="f5591-180">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="f5591-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="f5591-181">Para obtener el mejor rendimiento a partir de las consultas, es importante crear estadísticas en todas las columnas de todas las tablas después de la primera carga o después de que se realiza cualquier cambio importante en los datos.</span><span class="sxs-lookup"><span data-stu-id="f5591-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="f5591-182">Para más información, vea las [estadísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="f5591-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5591-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5591-183">Next steps</span></span>
<span data-ttu-id="f5591-184">Para obtener más sugerencias sobre desarrollo, vea la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="f5591-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
