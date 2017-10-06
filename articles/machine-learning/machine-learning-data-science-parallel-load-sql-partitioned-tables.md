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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Importación paralela de conjuntos masivos de datos mediante tablas de partición de SQL
Este documento describe cómo toobuild crear esas particiones de tablas para la importación masiva paralelo rápido de base de datos de SQL Server de tooa de datos. Para grandes cantidades de datos carga/transferencia tooa base de datos SQL, importar datos toohello base de datos SQL y las consultas posteriores se puede mejorar mediante el uso de *Partitioned Tables and vistas*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Crear una nueva base de datos y un conjunto de grupos de archivos
* [Cree una nueva base de datos](https://technet.microsoft.com/library/ms176061.aspx), si todavía no existe.
* Agregar base de datos de la toohello de grupos de archivos de base de datos que contendrá los archivos físicos de hello con particiones. Esto puede hacerse con [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) si la nueva o [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) si la base de datos de hello ya existe.
* Agregue uno o varios grupos de archivos de base de datos de tooeach de archivos (según sea necesario).
  
  > [!NOTE]
  > Especifique el grupo de archivos de destino de Hola que contiene datos para este nombres de los archivos de base de datos física hello y partición donde se almacenarán los datos del grupo de archivos de saludo.
  > 
  > 

Hello en el ejemplo siguiente se crea una nueva base de datos con tres grupos de archivos que no sean Hola principal y los grupos de registros, que contiene un archivo físico en cada uno. archivos de base de datos de Hola se crean en la carpeta de datos de SQL Server predeterminada de hello, como está configurado en la instancia de SQL Server de Hola. Para obtener más información acerca de las ubicaciones de archivo predeterminado de hello, consulte [ubicaciones de archivos para las predeterminadas y con nombre de instancias de SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

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

## <a name="create-a-partitioned-table"></a>Crear una tabla con particiones
Crear tablas con particiones según el esquema de datos toohello toohello asignado grupos de archivos de base de datos creada en el paso anterior de Hola. Cuando los datos se importan de forma masiva toohello particiones de tabla (s), los registros se distribuirán entre los grupos de archivos de hello según el esquema de partición de tooa, tal y como se describe a continuación.

**toocreate una tabla de partición, debe:**

* [Crear una función de partición](https://msdn.microsoft.com/library/ms187802.aspx) que define el intervalo de Hola de valores/límites toobe incluidos en cada tabla de particiones individuales, por ejemplo, toolimit particiones por mes (algunos\_datetime\_campo) en el año de hello 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Crear un esquema de partición](https://msdn.microsoft.com/library/ms179854.aspx) que asigna cada intervalo de partición de hello partición función tooa físico archivos, p. ej.:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  intervalos de hello tooverify en vigor en cada uno de ellos correspondiente toohello función o esquema de partición, ejecute hello después de consulta:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Crear una tabla con particiones](https://msdn.microsoft.com/library/ms174979.aspx)(s) según el esquema de datos de tooyour y especificar el campo de esquema y la restricción de la partición de hello usa tabla Hola de toopartition, p. ej.:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Para obtener más información, consulte [Crear tablas e índices con particiones](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Importación masiva Hola de datos para cada tabla de partición individuales
* Puede usar BCP, BULK INSERT u otros métodos como el [Asistente para migración de SQL Server](http://sqlazuremw.codeplex.com/). ejemplo de Hola incluido usa el método BCP de Hola.
* [Modificar base de datos de hello](https://msdn.microsoft.com/library/bb522682.aspx) esquema tooBULK_LOGGED toominimize sobrecarga del inicio de sesión, por ejemplo, de registro de transacciones de toochange:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* datos tooexpedite cargar, iniciar operaciones de importación masiva de hello en paralelo. Para obtener sugerencias sobre la aceleración de la importación masiva de big data en las bases de datos de SQL Server, consulte [Cargar 1 TB en menos de 1 hora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Hello siguiente script de PowerShell es un ejemplo de uso de BCP de cargar datos en paralelo.

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Crear índices toooptimize combinaciones y rendimiento de las consultas
* Si extraerá datos para el modelado de varias tablas, crear índices en las claves de combinación de hello rendimiento de combinación de tooimprove Hola.
* [Crear índices](https://technet.microsoft.com/library/ms188783.aspx) (agrupado o no agrupado) como destino hello mismo grupo de archivos para cada partición para p. ej.:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  o bien,
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Puede elegir toocreate índices de hello antes de la importación masiva de datos de Hola. Creación de índices antes de la importación masiva ralentizará la carga de datos Hola.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Ejemplo de Tecnología y procesos de análisis avanzado en acción
Para obtener un ejemplo de tutorial de extremo a extremo mediante Hola proceso de análisis de Cortana con un conjunto de datos pública, consulte [proceso de análisis de Cortana en acción: uso de SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

