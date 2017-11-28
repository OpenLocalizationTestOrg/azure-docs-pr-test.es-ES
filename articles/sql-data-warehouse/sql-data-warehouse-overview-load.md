---
title: datos de aaaLoad en almacenamiento de datos de SQL de Azure | Documentos de Microsoft
description: "Obtenga información acerca de escenarios comunes de Hola de carga en el almacén de datos SQL de datos. Estos incluyen el uso de PolyBase, el almacenamiento de blobs de Azure, archivos planos y el envío de discos. También puede usar herramientas de otros fabricantes."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="da6b6-105">Carga de datos en Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="da6b6-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="da6b6-106">Resumen de opciones de escenario de Hola y recomendaciones para cargar datos en almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="da6b6-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="da6b6-107">la parte más difícil de Hello de la carga de datos normalmente es preparar los datos de Hola para carga Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="da6b6-108">Azure simplifica la carga mediante el uso de almacenamiento de blobs de Azure como almacén de datos común para muchos de los servicios de Hola y con Data Factory de Azure Hola tooorchestrate comunicación y movimiento de datos entre los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="da6b6-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="da6b6-109">Estos procesos se integran con la tecnología de PolyBase que utiliza el procesamiento en paralelo masivamente datos de tooload (MPP) en paralelo desde el almacenamiento de blobs de Azure en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="da6b6-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="da6b6-110">Para ver tutoriales que cargan bases de datos de ejemplo, vea [Carga de datos de ejemplo en SQL Data Warehouse][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="da6b6-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="da6b6-111">Carga desde el almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="da6b6-111">Load from Azure blob storage</span></span>
<span data-ttu-id="da6b6-112">datos de tooimport de manera más rápidos de saludo en almacenamiento de datos de SQL están toouse datos de tooload de PolyBase de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="da6b6-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="da6b6-113">PolyBase usa almacenamiento de datos SQL procesamiento en paralelo masivamente datos en tooload de diseño (MPP) en paralelo desde el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="da6b6-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="da6b6-114">toouse PolyBase, puede usar comandos de T-SQL o una canalización del generador de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="da6b6-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="da6b6-115">1. Usar PolyBase y T-SQL</span><span class="sxs-lookup"><span data-stu-id="da6b6-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="da6b6-116">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="da6b6-116">Summary of loading process:</span></span>

1. <span data-ttu-id="da6b6-117">Mover el almacenamiento de blobs de tooAzure de datos o el almacén de Azure Data Lake y almacenar en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="da6b6-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="da6b6-118">Configurar objetos externos en la ubicación de almacenamiento de datos SQL toodefine Hola y el formato de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="da6b6-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="da6b6-119">Ejecutar una instrucción T-SQL comando tooload Hola de datos en paralelo en una nueva tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="da6b6-120">Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="da6b6-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="da6b6-121">2. Usar Data Factory de Azure</span><span class="sxs-lookup"><span data-stu-id="da6b6-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="da6b6-122">Para una forma más sencilla toouse PolyBase, puede crear una canalización del generador de datos de Azure que utiliza datos de tooload de PolyBase de almacenamiento de blobs de Azure en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="da6b6-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="da6b6-123">Se trata de tooconfigure rápida puesto que no necesita objetos de T-SQL toodefine Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="da6b6-124">Si tiene datos externos de hello tooquery sin importarlo, usar T-SQL.</span><span class="sxs-lookup"><span data-stu-id="da6b6-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="da6b6-125">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="da6b6-125">Summary of loading process:</span></span>

1. <span data-ttu-id="da6b6-126">Mover el almacenamiento de blobs de datos tooAzure y almacenar en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="da6b6-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="da6b6-127">Azure Data Factory no admite actualmente la conectividad de ADLS con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="da6b6-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="da6b6-128">Crear una canalización de factoría de datos de Azure tooingest Hola datos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="da6b6-129">Use la opción de PolyBase de Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="da6b6-130">Programar y ejecutar la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="da6b6-131">Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (factoría de datos de Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="da6b6-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="da6b6-132">Carga desde SQL Server</span><span class="sxs-lookup"><span data-stu-id="da6b6-132">Load from SQL Server</span></span>
<span data-ttu-id="da6b6-133">datos tooload de SQL Server tooSQL almacenamiento de datos se pueden utilizar Integration Services (SSIS), transferencia de archivos planos o distribuir tooMicrosoft de discos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="da6b6-134">Siga leyendo toosee un resumen de hello diferente carga tootutorials procesos y vínculos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="da6b6-135">tooplan una migración completa de los datos de SQL Server tooSQL almacenamiento de datos, vea hello [Introducción a la migración][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="da6b6-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="da6b6-136">Uso de Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="da6b6-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="da6b6-137">Si ya usas tooload de paquetes de Integration Services (SSIS) en SQL Server, puede actualizar su toouse de paquetes SQL Server como origen de Hola y de almacenamiento de datos de SQL como destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="da6b6-138">Esto es muy rápido y fácil toodo, y es una buena elección si no está tratando de toomigrate su carga procesar datos toouse ya se encuentran en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="da6b6-139">contrapartida de Hello es carga Hola será más lento que usar PolyBase ya este SSIS no realiza la carga de hello en paralelo.</span><span class="sxs-lookup"><span data-stu-id="da6b6-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="da6b6-140">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="da6b6-140">Summary of loading process:</span></span>

1. <span data-ttu-id="da6b6-141">Revise la instancia de SQL Server Integration Services paquete toopoint toohello para el origen de Hola y base de datos de almacenamiento de datos SQL de Hola para destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="da6b6-142">Migrar el almacenamiento de datos, de esquema tooSQL si no está ya.</span><span class="sxs-lookup"><span data-stu-id="da6b6-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="da6b6-143">Cambiar la asignación de hello en los paquetes utilizan Hola de solo los tipos de datos que es compatibles con el almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="da6b6-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="da6b6-144">Programar y ejecutar paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="da6b6-144">Schedule and run hello package.</span></span>

<span data-ttu-id="da6b6-145">Para obtener un tutorial, vea [cargar datos de SQL Server tooAzure almacenamiento de datos de SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="da6b6-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="da6b6-146">Uso de AZCopy (recomendado para datos de menos de 10 TB)</span><span class="sxs-lookup"><span data-stu-id="da6b6-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="da6b6-147">Si el tamaño de datos es < 10 TB, puede exportar datos de Hola desde los archivos de tooflat de SQL Server, copie el almacenamiento de blobs de hello archivos tooAzure y, a continuación, utilizar datos de PolyBase tooload hello en almacenamiento de datos de SQL</span><span class="sxs-lookup"><span data-stu-id="da6b6-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="da6b6-148">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="da6b6-148">Summary of loading process:</span></span>

1. <span data-ttu-id="da6b6-149">Usar datos de tooexport de utilidad de línea de comandos de hello bcp de archivos de tooflat de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da6b6-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="da6b6-150">Usar hello AZCopy utilidad de línea de comandos toocopy datos desde almacenamiento de blobs de tooAzure de archivos sin formato.</span><span class="sxs-lookup"><span data-stu-id="da6b6-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="da6b6-151">Use PolyBase tooload en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="da6b6-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="da6b6-152">Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="da6b6-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="da6b6-153">Uso de bcp</span><span class="sxs-lookup"><span data-stu-id="da6b6-153">Use bcp</span></span>
<span data-ttu-id="da6b6-154">Si tiene una pequeña cantidad de datos puede usar bcp tooload directamente en el almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="da6b6-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="da6b6-155">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="da6b6-155">Summary of loading process:</span></span>

1. <span data-ttu-id="da6b6-156">Usar datos de tooexport de utilidad de línea de comandos de hello bcp de archivos de tooflat de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da6b6-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="da6b6-157">Usar bcp tooload datos de plano directamente archivos tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="da6b6-158">Para obtener un tutorial, vea [cargar datos de SQL Server tooAzure almacenamiento de datos de SQL (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="da6b6-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="da6b6-159">Uso de importación/exportación (recomendado para datos de menos de 10 TB)</span><span class="sxs-lookup"><span data-stu-id="da6b6-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="da6b6-160">Si el tamaño de los datos es > 10 TB y desea toomove se tooAzure, se recomienda que utilice nuestro servicio de envío de disco [importación/exportación][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="da6b6-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="da6b6-161">Resumen del proceso de carga</span><span class="sxs-lookup"><span data-stu-id="da6b6-161">Summary of loading process</span></span>

1. <span data-ttu-id="da6b6-162">Usar datos de tooexport de utilidad de línea de comandos de hello bcp de archivos de SQL Server tooflat en discos transferibles.</span><span class="sxs-lookup"><span data-stu-id="da6b6-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="da6b6-163">Hola Ship discos tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="da6b6-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="da6b6-164">Microsoft carga los datos de hello en almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="da6b6-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="da6b6-165">Carga desde HDInsight</span><span class="sxs-lookup"><span data-stu-id="da6b6-165">Load from HDInsight</span></span>
<span data-ttu-id="da6b6-166">El Almacenamiento de datos SQL admite la carga de datos desde HDInsight a través de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="da6b6-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="da6b6-167">proceso de Hello es Hola igual a la carga de datos desde almacenamiento de blobs de Azure: usar PolyBase tooconnect tooHDInsight tooload datos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="da6b6-168">1. Usar PolyBase y T-SQL</span><span class="sxs-lookup"><span data-stu-id="da6b6-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="da6b6-169">Resumen del proceso de carga:</span><span class="sxs-lookup"><span data-stu-id="da6b6-169">Summary of loading process:</span></span>

1. <span data-ttu-id="da6b6-170">Mover el tooHDInsight de datos y almacenarla en archivos de texto, formato ORC o Parquet.</span><span class="sxs-lookup"><span data-stu-id="da6b6-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="da6b6-171">Configure los objetos externos en la ubicación de almacenamiento de datos SQL toodefine Hola y el formato de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="da6b6-172">Ejecutar una instrucción T-SQL comando tooload Hola de datos en paralelo en una nueva tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="da6b6-173">Para obtener un tutorial, vea [cargar datos desde almacenamiento de blobs de Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="da6b6-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="da6b6-174">Recomendaciones</span><span class="sxs-lookup"><span data-stu-id="da6b6-174">Recommendations</span></span>
<span data-ttu-id="da6b6-175">Muchos de nuestros asociados tienen soluciones de carga.</span><span class="sxs-lookup"><span data-stu-id="da6b6-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="da6b6-176">toofind más información, consulte una lista de nuestros [socios de soluciones de][solution partners].</span><span class="sxs-lookup"><span data-stu-id="da6b6-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="da6b6-177">Si los datos provienen de un origen no relacionales y desea tooload en datos de SQL de almacenamiento se necesitará tootransform en filas y columnas antes de cargarlos.</span><span class="sxs-lookup"><span data-stu-id="da6b6-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="da6b6-178">no es necesario datos de Hello transforman toobe almacenado en una base de datos, pueden almacenarse en archivos de texto.</span><span class="sxs-lookup"><span data-stu-id="da6b6-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="da6b6-179">Cree estadísticas de los datos recién cargados.</span><span class="sxs-lookup"><span data-stu-id="da6b6-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="da6b6-180">Almacenamiento de datos SQL de Azure todavía no permite crear ni actualizar automáticamente las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="da6b6-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="da6b6-181">En orden tooget Hola un mejor rendimiento de las consultas, es importante toocreate estadísticas en todas las columnas de todas las tablas después de hello cargar por primera vez o se producen cambios sustanciales en datos Hola.</span><span class="sxs-lookup"><span data-stu-id="da6b6-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="da6b6-182">Para más información, vea las [estadísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="da6b6-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="da6b6-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="da6b6-183">Next steps</span></span>
<span data-ttu-id="da6b6-184">Para más sugerencias de desarrollo, vea hello [Introducción al desarrollo de][development overview].</span><span class="sxs-lookup"><span data-stu-id="da6b6-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
