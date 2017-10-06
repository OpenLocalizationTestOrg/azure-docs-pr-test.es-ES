---
title: "aaaMove datos tooSQL Server en una máquina virtual de Azure | Documentos de Microsoft"
description: Mover datos de archivos planos o desde un tooSQL de SQL Server local Server en VM de Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>Mover datos tooSQL Server en una máquina virtual de Azure
Este tema describen las opciones de Hola para mover datos desde archivos sin formato (formatos CSV o TSV) o desde un tooSQL de SQL Server local Server en una máquina virtual de Azure. Estas tareas para mover datos en la nube toohello forman parte de hello proceso de ciencia de datos de equipo.

Para un tema que describe las opciones de Hola para mover datos tooan base de datos de SQL Azure para el aprendizaje automático, consulte [mover datos tooan base de datos de SQL Azure para el aprendizaje automático de Azure](machine-learning-data-science-move-sql-azure.md).

Hola **menú** debajo tootopics de vínculos que describen cómo tooingest datos en otros entornos de destino donde se pueden almacenar y procesar durante datos Hola Hola proceso de ciencia de datos de equipo (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello siguiente tabla resume las opciones de Hola para mover datos tooSQL Server en una máquina virtual de Azure.

| <b>ORIGEN</b> | <b>DESTINO: servidor SQL Server en una máquina virtual de Azure</b> |
| --- | --- |
| <b>Archivo plano</b> |1. <a href="#insert-tables-bcp">Utilidad de copia masiva (BCP) de la línea de comandos</a><br> 2. <a href="#insert-tables-bulkquery">Consulta SQL de inserción masiva</a><br> 3. <a href="#sql-builtin-utilities">Utilidades integradas gráficas de SQL Server</a> |
| <b>SQL Server local</b> |1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Implementar a un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa</a><br> 2. <a href="#export-flat-file">Exportar tooa planos, archivos</a><br> 3. <a href="#sql-migration">SQL Database Migration Wizard </a> <br> 4. <a href="#sql-backup">Copia de seguridad y restauración de una base de datos </a><br> |

Tenga en cuenta que en este documento se da por supuesto que los comandos SQL se ejecutan desde SQL Server Management Studio o el Explorador de bases de datos de Visual Studio.

> [!TIP]
> Como alternativa, puede usar [Data Factory de Azure](https://azure.microsoft.com/services/data-factory/) toocreate y programar una canalización que se moverá los datos tooa VM de SQL Server en Azure. Para obtener más información, consulte [Copia de datos con Factoría de datos de Azure (actividad de copia)](../data-factory/data-factory-data-movement-activities.md)
>
>

## <a name="prereqs"></a>Requisitos previos
En este tutorial se asume que dispone de:

* Una **suscripción de Azure**. Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Una **cuenta de almacenamiento de Azure**. Se usará una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial. Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo. Una vez haya creado la cuenta de almacenamiento de hello, necesita tooobtain Hola cuenta clave usa el almacenamiento de información de tooaccess Hola. Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* **Servidor SQL Server aprovisionado en una máquina virtual de Azure**. Para obtener instrucciones, vea [Configuración de una máquina virtual de Azure SQL Server como servidor del Notebook de IPython para realizar análisis avanzados](machine-learning-data-science-setup-sql-server-virtual-machine.md).
* **Azure PowerShell** instalado y configurado de forma local. Para obtener instrucciones, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).

## <a name="filesource_to_sqlonazurevm"></a>Migración de datos de un tooSQL de origen de archivo sin formato Server en una máquina virtual de Azure
Si los datos están en un archivo sin formato (organizado en un formato de fila o columna), puede ser movida tooSQL máquina virtual Server en Azure a través de los siguientes métodos de Hola:

1. [Utilidad de copia masiva (BCP) de la línea de comandos](#insert-tables-bcp)
2. [Consulta SQL de inserción masiva ](#insert-tables-bulkquery)
3. [Utilidades integradas gráficas de SQL Server (importación/exportación, SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>Utilidad de copia masiva (BCP) de la línea de comandos
BCP es una utilidad de línea de comandos que se instala con SQL Server y es uno de los datos de toomove de maneras más rápidos de saludo. Funciona en las tres variantes de SQL Server (SQL Server local, SQL Azure y máquina virtual SQL Server en Azure).

> [!NOTE]
> **¿Dónde deberían estar mis datos para BCP?**  
> Aunque no es necesario, con los archivos que contienen datos de origen que se encuentran en hello misma máquina que el destino de hello SQL Server permite más rápido transfiere (velocidad de E/S de disco local de red velocidad vs). Puede mover Hola plano máquina de toohello de datos que contiene los archivos donde está instalado SQL Server con copia de archivos de varias herramientas como [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) o copiar y pegar de windows a través de remoto Protocolo de escritorio (RDP).
>
>

1. Asegúrese de que se crean tablas de Hola y base de datos de hello en la base de datos de SQL Server de destino de Hola. Este es un ejemplo de cómo toodo que el uso de Hola `Create Database` y `Create Table` comandos:

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. Generar Hola archivo de formato que describe el esquema de hello para la tabla de hello emitiendo el siguiente comando desde la línea de comandos de la máquina de Hola Hola de Hola donde está instalado bcp.

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Insertar datos de hello en la base de datos de hello mediante un comando bcp hello como se indica a continuación. Esto debería funcionar desde la línea de comandos de hello suponiendo que hello instalado SQL Server está en el mismo equipo:

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **Optimizar BCP inserta** , consulte el artículo siguiente de hello ['Directrices para optimizar la importación masiva'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize tal inserta.
>
>

### <a name="insert-tables-bulkquery-parallel"></a>Poner en paralelo inserciones para el movimiento de datos más rápido
Si los datos de Hola que está moviendo están grandes, puede acelerar cosas ejecutando simultáneamente varios comandos BCP en paralelo en un PowerShell Script.

> [!NOTE]
> **Recopilación de datos grandes** para conjuntos de datos de gran tamaño y muy grande, la carga de datos de toooptimize particiones en las tablas de base de datos lógicos y físicos con varias tablas de grupos de archivos y la partición. Para obtener más información sobre cómo crear y cargar datos toopartition tablas, vea [paralelo tablas de partición de SQL de carga](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
>
>

Hello script de PowerShell de ejemplo siguiente muestran inserciones paralelas mediante bcp:

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>Consulta SQL de inserción masiva
[Consulta Insert de SQL de forma masiva](https://msdn.microsoft.com/library/ms188365) pueden ser datos tooimport usado en base de datos de Hola de archivos en función de fila o columna (Hola admitida tipos están cubiertas por el[preparar los datos para la exportación masiva o importación (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tema.

Estos son algunos ejemplos de comandos de inserción masiva:  

1. Analizar los datos y establecer las opciones personalizadas antes de importar toomake seguro de que esa base de datos de SQL Server de hello supone Hola mismo formato para los campos especiales como las fechas. Este es un ejemplo de cómo dar formato fecha de hello tooset como año-mes-día (si los datos contienen fecha hello en formato año-mes-día):

        SET DATEFORMAT ymd;    
2. Importar datos mediante instrucciones de importación en bloque:

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>Utilidades integradas de SQL Server
Puede usar datos de SQL Server Integration Services (SSIS) tooimport en VM de SQL Server en Azure desde un archivo sin formato.
SSIS está disponible en dos entornos de estudio. Para obtener más detalles, consulte [Entornos de Studio e Integration Services (SSIS)](https://technet.microsoft.com/library/ms140028.aspx):

* Para obtener más información acerca de las herramientas de datos de SQL Server, consulte [Herramientas de datos de Microsoft SQL Server](https://msdn.microsoft.com/data/tools.aspx)  
* Para obtener más información en el Asistente para importación y exportación de hello, consulte [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>Migración de datos de tooSQL de SQL Server local Server en una máquina virtual de Azure
También puede usar Hola después de estrategias de migración:

1. [Implementar a un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [Exportar archivo tooFlat](#export-flat-file)
3. [Asistente para migración de Base de datos SQL](#sql-migration)
4. [Copia de seguridad y restauración de una base de datos](#sql-backup)

Describimos cada una de estas opciones:

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>Implementar a un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa
Hola **implementar un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa** es una manera sencilla y recomendada toomove de datos de una instancia de SQL Server local tooSQL Server en una máquina virtual de Azure. Para obtener pasos detallados así como una explicación de las otras alternativas, vea [migrar un servidor en una máquina virtual de Azure de base de datos tooSQL](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).

### <a name="export-flat-file"></a>Exportar archivo tooFlat
Varios métodos pueden ser usado toobulk exportar datos desde un servidor local de SQL como se documenta en hello [importación y exportación de datos (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tema. Este documento tratará Hola programa de copia masiva (BCP) como un ejemplo. Una vez que se exportan datos en un archivo sin formato, puede ser importados tooanother SQL server mediante la importación masiva.

1. Exportar datos de Hola de tooa de SQL Server local archivo mediante la utilidad bcp de hello como se indica a continuación

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. Crear base de datos de Hola y tabla de hello en VM de SQL Server en Azure con hello `create database` y `create table` para el esquema de tabla de hello exportado en el paso 1.
3. Crear un archivo de formato para describir el esquema de la tabla de datos de Hola que se va a exportar e importar Hola. Detalles de archivo de formato de Hola se describen en [crear un archivo de formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).

    Generación del archivo de formato cuando ejecuta BCP de Hola máquina de SQL Server

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    Generación de archivos de formato cuando se ejecuta BCP de forma remota contra un SQL Server

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. Use cualquiera de los métodos de Hola se describe en la sección [mover datos de origen de archivo](#filesource_to_sqlonazurevm) toomove datos de hello en archivos planos tooa SQL Server.

### <a name="sql-migration"></a>Asistente para migración de Base de datos SQL
[Asistente para migración de base de datos de SQL Server](http://sqlazuremw.codeplex.com/) proporciona una manera fácil de usar toomove datos entre dos instancias de SQL server. Permite esquema Hola usuario toomap Hola datos entre orígenes y tablas de destino, elija los tipos de columna y otras funcionalidades. Utiliza la copia masiva (BCP) tras los bastidores de Hola. Una captura de pantalla de hello pantalla de Hola a continuación se muestra el Asistente para la migración en base de datos SQL de bienvenida.  

![Asistente para migración de SQL Server][2]

### <a name="sql-backup"></a>Copia de seguridad y restauración de una base de datos
SQL Server es compatible con:

1. [Base de datos copia de seguridad y restaurar la funcionalidad](https://msdn.microsoft.com/library/ms187048.aspx) (ambos tooa local bacpac o archivo de exportación tooblob) y [aplicaciones de capa de datos](https://msdn.microsoft.com/library/ee210546.aspx) (con bacpac).
2. Capacidad toodirectly crear VM de SQL Server en Azure con una base de datos copiada o la base de datos de SQL Azure existente de copia tooan. Para obtener más información, consulte [Hola Asistente para copia de base de datos de uso](https://msdn.microsoft.com/library/ms188664.aspx).

Una captura de pantalla de las copias de la base de datos de hello backup/restore opciones desde SQL Server Management Studio se muestra a continuación.

![Herramienta de importación SQL Server][1]

## <a name="resources"></a>Recursos
[Migrar un servidor en una máquina virtual de Azure de tooSQL de base de datos](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Información general de SQL Server en Azure Virtual Machines](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
