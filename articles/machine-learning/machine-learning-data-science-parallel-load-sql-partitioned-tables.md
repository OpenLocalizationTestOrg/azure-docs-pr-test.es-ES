---
title: "aaaBuild y optimizar tablas de importación en paralelo rápida de datos en un servidor SQL Server en una máquina virtual de Azure | Documentos de Microsoft"
description: "Importación paralela de conjuntos masivos de datos mediante tablas de partición de SQL"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="104d9-103">Importación paralela de conjuntos masivos de datos mediante tablas de partición de SQL</span><span class="sxs-lookup"><span data-stu-id="104d9-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="104d9-104">Este documento describe cómo toobuild crear esas particiones de tablas para la importación masiva paralelo rápido de base de datos de SQL Server de tooa de datos.</span><span class="sxs-lookup"><span data-stu-id="104d9-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="104d9-105">Para grandes cantidades de datos carga/transferencia tooa base de datos SQL, importar datos toohello base de datos SQL y las consultas posteriores se puede mejorar mediante el uso de *Partitioned Tables and vistas*.</span><span class="sxs-lookup"><span data-stu-id="104d9-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="104d9-106">Crear una nueva base de datos y un conjunto de grupos de archivos</span><span class="sxs-lookup"><span data-stu-id="104d9-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="104d9-107">[Cree una nueva base de datos](https://technet.microsoft.com/library/ms176061.aspx), si todavía no existe.</span><span class="sxs-lookup"><span data-stu-id="104d9-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="104d9-108">Agregar base de datos de la toohello de grupos de archivos de base de datos que contendrá los archivos físicos de hello con particiones. Esto puede hacerse con [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) si la nueva o [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) si la base de datos de hello ya existe.</span><span class="sxs-lookup"><span data-stu-id="104d9-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="104d9-109">Agregue uno o varios grupos de archivos de base de datos de tooeach de archivos (según sea necesario).</span><span class="sxs-lookup"><span data-stu-id="104d9-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="104d9-110">Especifique el grupo de archivos de destino de Hola que contiene datos para este nombres de los archivos de base de datos física hello y partición donde se almacenarán los datos del grupo de archivos de saludo.</span><span class="sxs-lookup"><span data-stu-id="104d9-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="104d9-111">Hello en el ejemplo siguiente se crea una nueva base de datos con tres grupos de archivos que no sean Hola principal y los grupos de registros, que contiene un archivo físico en cada uno.</span><span class="sxs-lookup"><span data-stu-id="104d9-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="104d9-112">archivos de base de datos de Hola se crean en la carpeta de datos de SQL Server predeterminada de hello, como está configurado en la instancia de SQL Server de Hola.</span><span class="sxs-lookup"><span data-stu-id="104d9-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="104d9-113">Para obtener más información acerca de las ubicaciones de archivo predeterminado de hello, consulte [ubicaciones de archivos para las predeterminadas y con nombre de instancias de SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="104d9-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="104d9-114">Crear una tabla con particiones</span><span class="sxs-lookup"><span data-stu-id="104d9-114">Create a partitioned table</span></span>
<span data-ttu-id="104d9-115">Crear tablas con particiones según el esquema de datos toohello toohello asignado grupos de archivos de base de datos creada en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="104d9-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="104d9-116">Cuando los datos se importan de forma masiva toohello particiones de tabla (s), los registros se distribuirán entre los grupos de archivos de hello según el esquema de partición de tooa, tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="104d9-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="104d9-117">**toocreate una tabla de partición, debe:**</span><span class="sxs-lookup"><span data-stu-id="104d9-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="104d9-118">[Crear una función de partición](https://msdn.microsoft.com/library/ms187802.aspx) que define el intervalo de Hola de valores/límites toobe incluidos en cada tabla de particiones individuales, por ejemplo, toolimit particiones por mes (algunos\_datetime\_campo) en el año de hello 2013:</span><span class="sxs-lookup"><span data-stu-id="104d9-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="104d9-119">[Crear un esquema de partición](https://msdn.microsoft.com/library/ms179854.aspx) que asigna cada intervalo de partición de hello partición función tooa físico archivos, p. ej.:</span><span class="sxs-lookup"><span data-stu-id="104d9-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="104d9-120">intervalos de hello tooverify en vigor en cada uno de ellos correspondiente toohello función o esquema de partición, ejecute hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="104d9-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="104d9-121">[Crear una tabla con particiones](https://msdn.microsoft.com/library/ms174979.aspx)(s) según el esquema de datos de tooyour y especificar el campo de esquema y la restricción de la partición de hello usa tabla Hola de toopartition, p. ej.:</span><span class="sxs-lookup"><span data-stu-id="104d9-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="104d9-122">Para obtener más información, consulte [Crear tablas e índices con particiones](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="104d9-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="104d9-123">Importación masiva Hola de datos para cada tabla de partición individuales</span><span class="sxs-lookup"><span data-stu-id="104d9-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="104d9-124">Puede usar BCP, BULK INSERT u otros métodos como el [Asistente para migración de SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="104d9-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="104d9-125">ejemplo de Hola incluido usa el método BCP de Hola.</span><span class="sxs-lookup"><span data-stu-id="104d9-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="104d9-126">[Modificar base de datos de hello](https://msdn.microsoft.com/library/bb522682.aspx) esquema tooBULK_LOGGED toominimize sobrecarga del inicio de sesión, por ejemplo, de registro de transacciones de toochange:</span><span class="sxs-lookup"><span data-stu-id="104d9-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="104d9-127">datos tooexpedite cargar, iniciar operaciones de importación masiva de hello en paralelo.</span><span class="sxs-lookup"><span data-stu-id="104d9-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="104d9-128">Para obtener sugerencias sobre la aceleración de la importación masiva de big data en las bases de datos de SQL Server, consulte [Cargar 1 TB en menos de 1 hora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="104d9-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="104d9-129">Hello siguiente script de PowerShell es un ejemplo de uso de BCP de cargar datos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="104d9-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="104d9-130">Crear índices toooptimize combinaciones y rendimiento de las consultas</span><span class="sxs-lookup"><span data-stu-id="104d9-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="104d9-131">Si extraerá datos para el modelado de varias tablas, crear índices en las claves de combinación de hello rendimiento de combinación de tooimprove Hola.</span><span class="sxs-lookup"><span data-stu-id="104d9-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="104d9-132">[Crear índices](https://technet.microsoft.com/library/ms188783.aspx) (agrupado o no agrupado) como destino hello mismo grupo de archivos para cada partición para p. ej.:</span><span class="sxs-lookup"><span data-stu-id="104d9-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="104d9-133">o bien,</span><span class="sxs-lookup"><span data-stu-id="104d9-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="104d9-134">Puede elegir toocreate índices de hello antes de la importación masiva de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="104d9-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="104d9-135">Creación de índices antes de la importación masiva ralentizará la carga de datos Hola.</span><span class="sxs-lookup"><span data-stu-id="104d9-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="104d9-136">Ejemplo de Tecnología y procesos de análisis avanzado en acción</span><span class="sxs-lookup"><span data-stu-id="104d9-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="104d9-137">Para obtener un ejemplo de tutorial de extremo a extremo mediante Hola proceso de análisis de Cortana con un conjunto de datos pública, consulte [proceso de análisis de Cortana en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="104d9-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

