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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="293ee-103">Mover datos tooSQL Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="293ee-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="293ee-104">Este tema describen las opciones de Hola para mover datos desde archivos sin formato (formatos CSV o TSV) o desde un tooSQL de SQL Server local Server en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="293ee-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="293ee-105">Estas tareas para mover datos en la nube toohello forman parte de hello proceso de ciencia de datos de equipo.</span><span class="sxs-lookup"><span data-stu-id="293ee-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="293ee-106">Para un tema que describe las opciones de Hola para mover datos tooan base de datos de SQL Azure para el aprendizaje automático, consulte [mover datos tooan base de datos de SQL Azure para el aprendizaje automático de Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="293ee-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="293ee-107">Hola **menú** debajo tootopics de vínculos que describen cómo tooingest datos en otros entornos de destino donde se pueden almacenar y procesar durante datos Hola Hola proceso de ciencia de datos de equipo (TDSP).</span><span class="sxs-lookup"><span data-stu-id="293ee-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="293ee-108">Hello siguiente tabla resume las opciones de Hola para mover datos tooSQL Server en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="293ee-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="293ee-109"><b>ORIGEN</b></span><span class="sxs-lookup"><span data-stu-id="293ee-109"><b>SOURCE</b></span></span> | <span data-ttu-id="293ee-110"><b>DESTINO: servidor SQL Server en una máquina virtual de Azure</b></span><span class="sxs-lookup"><span data-stu-id="293ee-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="293ee-111"><b>Archivo plano</b></span><span class="sxs-lookup"><span data-stu-id="293ee-111"><b>Flat File</b></span></span> |<span data-ttu-id="293ee-112">1. <a href="#insert-tables-bcp">Utilidad de copia masiva (BCP) de la línea de comandos</a></span><span class="sxs-lookup"><span data-stu-id="293ee-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="293ee-113">2. <a href="#insert-tables-bulkquery">Consulta SQL de inserción masiva</a></span><span class="sxs-lookup"><span data-stu-id="293ee-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="293ee-114">3. <a href="#sql-builtin-utilities">Utilidades integradas gráficas de SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="293ee-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="293ee-115"><b>SQL Server local</b></span><span class="sxs-lookup"><span data-stu-id="293ee-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="293ee-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Implementar a un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa</a></span><span class="sxs-lookup"><span data-stu-id="293ee-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="293ee-117">2. <a href="#export-flat-file">Exportar tooa planos, archivos</a></span><span class="sxs-lookup"><span data-stu-id="293ee-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="293ee-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span><span class="sxs-lookup"><span data-stu-id="293ee-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="293ee-119">4. <a href="#sql-backup">Copia de seguridad y restauración de una base de datos </a></span><span class="sxs-lookup"><span data-stu-id="293ee-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="293ee-120">Tenga en cuenta que en este documento se da por supuesto que los comandos SQL se ejecutan desde SQL Server Management Studio o el Explorador de bases de datos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="293ee-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="293ee-121">Como alternativa, puede usar [Data Factory de Azure](https://azure.microsoft.com/services/data-factory/) toocreate y programar una canalización que se moverá los datos tooa VM de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="293ee-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="293ee-122">Para obtener más información, consulte [Copia de datos con Factoría de datos de Azure (actividad de copia)](../data-factory/data-factory-data-movement-activities.md)</span><span class="sxs-lookup"><span data-stu-id="293ee-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="293ee-123"><a name="prereqs"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="293ee-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="293ee-124">En este tutorial se asume que dispone de:</span><span class="sxs-lookup"><span data-stu-id="293ee-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="293ee-125">Una **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="293ee-125">An **Azure subscription**.</span></span> <span data-ttu-id="293ee-126">Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="293ee-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="293ee-127">Una **cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="293ee-127">An **Azure storage account**.</span></span> <span data-ttu-id="293ee-128">Se usará una cuenta de almacenamiento de Azure para almacenar datos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="293ee-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="293ee-129">Si no tiene una cuenta de almacenamiento de Azure, vea hello [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artículo.</span><span class="sxs-lookup"><span data-stu-id="293ee-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="293ee-130">Una vez haya creado la cuenta de almacenamiento de hello, necesita tooobtain Hola cuenta clave usa el almacenamiento de información de tooaccess Hola.</span><span class="sxs-lookup"><span data-stu-id="293ee-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="293ee-131">Consulte [Administración de la cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="293ee-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="293ee-132">**Servidor SQL Server aprovisionado en una máquina virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="293ee-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="293ee-133">Para obtener instrucciones, vea [Configuración de una máquina virtual de Azure SQL Server como servidor del Notebook de IPython para realizar análisis avanzados](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="293ee-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="293ee-134">**Azure PowerShell** instalado y configurado de forma local.</span><span class="sxs-lookup"><span data-stu-id="293ee-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="293ee-135">Para obtener instrucciones, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="293ee-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="293ee-136"><a name="filesource_to_sqlonazurevm"></a>Migración de datos de un tooSQL de origen de archivo sin formato Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="293ee-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="293ee-137">Si los datos están en un archivo sin formato (organizado en un formato de fila o columna), puede ser movida tooSQL máquina virtual Server en Azure a través de los siguientes métodos de Hola:</span><span class="sxs-lookup"><span data-stu-id="293ee-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="293ee-138">Utilidad de copia masiva (BCP) de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="293ee-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="293ee-139">Consulta SQL de inserción masiva </span><span class="sxs-lookup"><span data-stu-id="293ee-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="293ee-140">Utilidades integradas gráficas de SQL Server (importación/exportación, SSIS)</span><span class="sxs-lookup"><span data-stu-id="293ee-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="293ee-141"><a name="insert-tables-bcp"></a>Utilidad de copia masiva (BCP) de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="293ee-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="293ee-142">BCP es una utilidad de línea de comandos que se instala con SQL Server y es uno de los datos de toomove de maneras más rápidos de saludo.</span><span class="sxs-lookup"><span data-stu-id="293ee-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="293ee-143">Funciona en las tres variantes de SQL Server (SQL Server local, SQL Azure y máquina virtual SQL Server en Azure).</span><span class="sxs-lookup"><span data-stu-id="293ee-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="293ee-144">**¿Dónde deberían estar mis datos para BCP?**</span><span class="sxs-lookup"><span data-stu-id="293ee-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="293ee-145">Aunque no es necesario, con los archivos que contienen datos de origen que se encuentran en hello misma máquina que el destino de hello SQL Server permite más rápido transfiere (velocidad de E/S de disco local de red velocidad vs).</span><span class="sxs-lookup"><span data-stu-id="293ee-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="293ee-146">Puede mover Hola plano máquina de toohello de datos que contiene los archivos donde está instalado SQL Server con copia de archivos de varias herramientas como [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) o copiar y pegar de windows a través de remoto Protocolo de escritorio (RDP).</span><span class="sxs-lookup"><span data-stu-id="293ee-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="293ee-147">Asegúrese de que se crean tablas de Hola y base de datos de hello en la base de datos de SQL Server de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="293ee-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="293ee-148">Este es un ejemplo de cómo toodo que el uso de Hola `Create Database` y `Create Table` comandos:</span><span class="sxs-lookup"><span data-stu-id="293ee-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="293ee-149">Generar Hola archivo de formato que describe el esquema de hello para la tabla de hello emitiendo el siguiente comando desde la línea de comandos de la máquina de Hola Hola de Hola donde está instalado bcp.</span><span class="sxs-lookup"><span data-stu-id="293ee-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="293ee-150">Insertar datos de hello en la base de datos de hello mediante un comando bcp hello como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="293ee-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="293ee-151">Esto debería funcionar desde la línea de comandos de hello suponiendo que hello instalado SQL Server está en el mismo equipo:</span><span class="sxs-lookup"><span data-stu-id="293ee-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="293ee-152">**Optimizar BCP inserta** , consulte el artículo siguiente de hello ['Directrices para optimizar la importación masiva'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize tal inserta.</span><span class="sxs-lookup"><span data-stu-id="293ee-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="293ee-153"><a name="insert-tables-bulkquery-parallel"></a>Poner en paralelo inserciones para el movimiento de datos más rápido</span><span class="sxs-lookup"><span data-stu-id="293ee-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="293ee-154">Si los datos de Hola que está moviendo están grandes, puede acelerar cosas ejecutando simultáneamente varios comandos BCP en paralelo en un PowerShell Script.</span><span class="sxs-lookup"><span data-stu-id="293ee-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="293ee-155">**Recopilación de datos grandes** para conjuntos de datos de gran tamaño y muy grande, la carga de datos de toooptimize particiones en las tablas de base de datos lógicos y físicos con varias tablas de grupos de archivos y la partición.</span><span class="sxs-lookup"><span data-stu-id="293ee-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="293ee-156">Para obtener más información sobre cómo crear y cargar datos toopartition tablas, vea [paralelo tablas de partición de SQL de carga](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="293ee-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="293ee-157">Hello script de PowerShell de ejemplo siguiente muestran inserciones paralelas mediante bcp:</span><span class="sxs-lookup"><span data-stu-id="293ee-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

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


### <span data-ttu-id="293ee-158"><a name="insert-tables-bulkquery"></a>Consulta SQL de inserción masiva</span><span class="sxs-lookup"><span data-stu-id="293ee-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="293ee-159">[Consulta Insert de SQL de forma masiva](https://msdn.microsoft.com/library/ms188365) pueden ser datos tooimport usado en base de datos de Hola de archivos en función de fila o columna (Hola admitida tipos están cubiertas por el[preparar los datos para la exportación masiva o importación (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tema.</span><span class="sxs-lookup"><span data-stu-id="293ee-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="293ee-160">Estos son algunos ejemplos de comandos de inserción masiva:</span><span class="sxs-lookup"><span data-stu-id="293ee-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="293ee-161">Analizar los datos y establecer las opciones personalizadas antes de importar toomake seguro de que esa base de datos de SQL Server de hello supone Hola mismo formato para los campos especiales como las fechas.</span><span class="sxs-lookup"><span data-stu-id="293ee-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="293ee-162">Este es un ejemplo de cómo dar formato fecha de hello tooset como año-mes-día (si los datos contienen fecha hello en formato año-mes-día):</span><span class="sxs-lookup"><span data-stu-id="293ee-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="293ee-163">Importar datos mediante instrucciones de importación en bloque:</span><span class="sxs-lookup"><span data-stu-id="293ee-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="293ee-164"><a name="sql-builtin-utilities"></a>Utilidades integradas de SQL Server</span><span class="sxs-lookup"><span data-stu-id="293ee-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="293ee-165">Puede usar datos de SQL Server Integration Services (SSIS) tooimport en VM de SQL Server en Azure desde un archivo sin formato.</span><span class="sxs-lookup"><span data-stu-id="293ee-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="293ee-166">SSIS está disponible en dos entornos de estudio.</span><span class="sxs-lookup"><span data-stu-id="293ee-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="293ee-167">Para obtener más detalles, consulte [Entornos de Studio e Integration Services (SSIS)](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="293ee-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="293ee-168">Para obtener más información acerca de las herramientas de datos de SQL Server, consulte [Herramientas de datos de Microsoft SQL Server](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="293ee-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="293ee-169">Para obtener más información en el Asistente para importación y exportación de hello, consulte [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="293ee-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="293ee-170"><a name="sqlonprem_to_sqlonazurevm"></a>Migración de datos de tooSQL de SQL Server local Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="293ee-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="293ee-171">También puede usar Hola después de estrategias de migración:</span><span class="sxs-lookup"><span data-stu-id="293ee-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="293ee-172">Implementar a un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa</span><span class="sxs-lookup"><span data-stu-id="293ee-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="293ee-173">Exportar archivo tooFlat</span><span class="sxs-lookup"><span data-stu-id="293ee-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="293ee-174">Asistente para migración de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="293ee-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="293ee-175">Copia de seguridad y restauración de una base de datos</span><span class="sxs-lookup"><span data-stu-id="293ee-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="293ee-176">Describimos cada una de estas opciones:</span><span class="sxs-lookup"><span data-stu-id="293ee-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="293ee-177">Implementar a un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa</span><span class="sxs-lookup"><span data-stu-id="293ee-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="293ee-178">Hola **implementar un Asistente para la máquina virtual de Microsoft Azure de base de datos de SQL Server tooa** es una manera sencilla y recomendada toomove de datos de una instancia de SQL Server local tooSQL Server en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="293ee-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="293ee-179">Para obtener pasos detallados así como una explicación de las otras alternativas, vea [migrar un servidor en una máquina virtual de Azure de base de datos tooSQL](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="293ee-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="293ee-180"><a name="export-flat-file"></a>Exportar archivo tooFlat</span><span class="sxs-lookup"><span data-stu-id="293ee-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="293ee-181">Varios métodos pueden ser usado toobulk exportar datos desde un servidor local de SQL como se documenta en hello [importación y exportación de datos (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="293ee-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="293ee-182">Este documento tratará Hola programa de copia masiva (BCP) como un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="293ee-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="293ee-183">Una vez que se exportan datos en un archivo sin formato, puede ser importados tooanother SQL server mediante la importación masiva.</span><span class="sxs-lookup"><span data-stu-id="293ee-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="293ee-184">Exportar datos de Hola de tooa de SQL Server local archivo mediante la utilidad bcp de hello como se indica a continuación</span><span class="sxs-lookup"><span data-stu-id="293ee-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="293ee-185">Crear base de datos de Hola y tabla de hello en VM de SQL Server en Azure con hello `create database` y `create table` para el esquema de tabla de hello exportado en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="293ee-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="293ee-186">Crear un archivo de formato para describir el esquema de la tabla de datos de Hola que se va a exportar e importar Hola.</span><span class="sxs-lookup"><span data-stu-id="293ee-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="293ee-187">Detalles de archivo de formato de Hola se describen en [crear un archivo de formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="293ee-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="293ee-188">Generación del archivo de formato cuando ejecuta BCP de Hola máquina de SQL Server</span><span class="sxs-lookup"><span data-stu-id="293ee-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="293ee-189">Generación de archivos de formato cuando se ejecuta BCP de forma remota contra un SQL Server</span><span class="sxs-lookup"><span data-stu-id="293ee-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="293ee-190">Use cualquiera de los métodos de Hola se describe en la sección [mover datos de origen de archivo](#filesource_to_sqlonazurevm) toomove datos de hello en archivos planos tooa SQL Server.</span><span class="sxs-lookup"><span data-stu-id="293ee-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="293ee-191"><a name="sql-migration"></a>Asistente para migración de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="293ee-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="293ee-192">[Asistente para migración de base de datos de SQL Server](http://sqlazuremw.codeplex.com/) proporciona una manera fácil de usar toomove datos entre dos instancias de SQL server.</span><span class="sxs-lookup"><span data-stu-id="293ee-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="293ee-193">Permite esquema Hola usuario toomap Hola datos entre orígenes y tablas de destino, elija los tipos de columna y otras funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="293ee-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="293ee-194">Utiliza la copia masiva (BCP) tras los bastidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="293ee-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="293ee-195">Una captura de pantalla de hello pantalla de Hola a continuación se muestra el Asistente para la migración en base de datos SQL de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="293ee-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Asistente para migración de SQL Server][2]

### <span data-ttu-id="293ee-197"><a name="sql-backup"></a>Copia de seguridad y restauración de una base de datos</span><span class="sxs-lookup"><span data-stu-id="293ee-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="293ee-198">SQL Server es compatible con:</span><span class="sxs-lookup"><span data-stu-id="293ee-198">SQL Server supports:</span></span>

1. <span data-ttu-id="293ee-199">[Base de datos copia de seguridad y restaurar la funcionalidad](https://msdn.microsoft.com/library/ms187048.aspx) (ambos tooa local bacpac o archivo de exportación tooblob) y [aplicaciones de capa de datos](https://msdn.microsoft.com/library/ee210546.aspx) (con bacpac).</span><span class="sxs-lookup"><span data-stu-id="293ee-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="293ee-200">Capacidad toodirectly crear VM de SQL Server en Azure con una base de datos copiada o la base de datos de SQL Azure existente de copia tooan.</span><span class="sxs-lookup"><span data-stu-id="293ee-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="293ee-201">Para obtener más información, consulte [Hola Asistente para copia de base de datos de uso](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="293ee-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="293ee-202">Una captura de pantalla de las copias de la base de datos de hello backup/restore opciones desde SQL Server Management Studio se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="293ee-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Herramienta de importación SQL Server][1]

## <a name="resources"></a><span data-ttu-id="293ee-204">Recursos</span><span class="sxs-lookup"><span data-stu-id="293ee-204">Resources</span></span>
[<span data-ttu-id="293ee-205">Migrar un servidor en una máquina virtual de Azure de tooSQL de base de datos</span><span class="sxs-lookup"><span data-stu-id="293ee-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="293ee-206">Información general de SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="293ee-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
