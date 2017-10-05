---
title: "Mover datos a un servidor SQL Server en una máquina virtual de Azure| Microsoft Docs"
description: "Mover datos desde archivos planos o desde un servidor SQL Server local a un servidor SQL Server en una máquina virtual de Azure"
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="02ed1-103">Mover datos a un servidor SQL Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="02ed1-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="02ed1-104">En este tema se describen las opciones para mover datos desde archivos planos (formatos CSV o TSV) o desde un servidor SQL Server local hasta un servidor SQL Server en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="02ed1-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="02ed1-105">Estas tareas para mover datos a la nube forman parte del proceso de ciencia de datos en equipos.</span><span class="sxs-lookup"><span data-stu-id="02ed1-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="02ed1-106">Para ver un tema que describa las opciones para mover datos a una base de datos SQL de Azure para Aprendizaje automático, vea [Mover datos a una base de datos SQL de Azure para Aprendizaje automático de Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="02ed1-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="02ed1-107">El **menú** siguiente redirige a temas en los que se describe cómo introducir datos en otros entornos de destino en que se pueden almacenar y procesar datos durante el proceso de ciencia de datos en equipos (TDSP).</span><span class="sxs-lookup"><span data-stu-id="02ed1-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="02ed1-108">En la tabla siguiente se resumen las opciones para mover datos a un servidor SQL Server en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="02ed1-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="02ed1-109"><b>ORIGEN</b></span><span class="sxs-lookup"><span data-stu-id="02ed1-109"><b>SOURCE</b></span></span> | <span data-ttu-id="02ed1-110"><b>DESTINO: servidor SQL Server en una máquina virtual de Azure</b></span><span class="sxs-lookup"><span data-stu-id="02ed1-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="02ed1-111"><b>Archivo plano</b></span><span class="sxs-lookup"><span data-stu-id="02ed1-111"><b>Flat File</b></span></span> |<span data-ttu-id="02ed1-112">1. <a href="#insert-tables-bcp">Utilidad de copia masiva (BCP) de la línea de comandos</a></span><span class="sxs-lookup"><span data-stu-id="02ed1-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="02ed1-113">2. <a href="#insert-tables-bulkquery">Consulta SQL de inserción masiva</a></span><span class="sxs-lookup"><span data-stu-id="02ed1-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="02ed1-114">3. <a href="#sql-builtin-utilities">Utilidades integradas gráficas de SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="02ed1-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="02ed1-115"><b>SQL Server local</b></span><span class="sxs-lookup"><span data-stu-id="02ed1-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="02ed1-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Asistente para implementación de una base de datos de SQL Server en una máquina virtual de Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="02ed1-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="02ed1-117">2. <a href="#export-flat-file">Exportación a un archivo plano </a></span><span class="sxs-lookup"><span data-stu-id="02ed1-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="02ed1-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span><span class="sxs-lookup"><span data-stu-id="02ed1-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="02ed1-119">4. <a href="#sql-backup">Copia de seguridad y restauración de una base de datos </a></span><span class="sxs-lookup"><span data-stu-id="02ed1-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="02ed1-120">Tenga en cuenta que en este documento se da por supuesto que los comandos SQL se ejecutan desde SQL Server Management Studio o el Explorador de bases de datos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="02ed1-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="02ed1-121">Como alternativa, puede usar [factoría de datos de Azure](https://azure.microsoft.com/services/data-factory/) para crear y programar una canalización de datos se moverá a una máquina virtual de SQL Server en Azure.</span><span class="sxs-lookup"><span data-stu-id="02ed1-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="02ed1-122">Para obtener más información, consulte [Copia de datos con Factoría de datos de Azure (actividad de copia)](../data-factory/data-factory-data-movement-activities.md)</span><span class="sxs-lookup"><span data-stu-id="02ed1-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="02ed1-123"><a name="prereqs"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="02ed1-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="02ed1-124">En este tutorial se asume que dispone de:</span><span class="sxs-lookup"><span data-stu-id="02ed1-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="02ed1-125">Una **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="02ed1-125">An **Azure subscription**.</span></span> <span data-ttu-id="02ed1-126">Si no tiene una suscripción, puede registrarse para obtener una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02ed1-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="02ed1-127">Una **cuenta de almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="02ed1-127">An **Azure storage account**.</span></span> <span data-ttu-id="02ed1-128">En este tutorial, usará una cuenta de almacenamiento de Azure para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="02ed1-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="02ed1-129">Si no dispone de una cuenta de almacenamiento de Azure, vea el artículo [Creación de una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="02ed1-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="02ed1-130">Tras crear la cuenta de almacenamiento, tendrá que obtener la clave de cuenta que se usa para tener acceso al almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="02ed1-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="02ed1-131">Consulte [Administración de las claves de acceso de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="02ed1-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="02ed1-132">**Servidor SQL Server aprovisionado en una máquina virtual de Azure**.</span><span class="sxs-lookup"><span data-stu-id="02ed1-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="02ed1-133">Para obtener instrucciones, vea [Configuración de una máquina virtual de Azure SQL Server como servidor del Notebook de IPython para realizar análisis avanzados](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="02ed1-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="02ed1-134">**Azure PowerShell** instalado y configurado de forma local.</span><span class="sxs-lookup"><span data-stu-id="02ed1-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="02ed1-135">Para obtener instrucciones, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="02ed1-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="02ed1-136"><a name="filesource_to_sqlonazurevm"></a> Mover datos desde un origen de archivo plano a un servidor SQL Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="02ed1-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="02ed1-137">Si los datos se encuentran en un archivo plano (organizado en un formato de fila y columna), se pueden mover a la VM de SQL Server en Azure mediante los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="02ed1-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="02ed1-138">Utilidad de copia masiva (BCP) de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="02ed1-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="02ed1-139">Consulta SQL de inserción masiva </span><span class="sxs-lookup"><span data-stu-id="02ed1-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="02ed1-140">Utilidades integradas gráficas de SQL Server (importación/exportación, SSIS)</span><span class="sxs-lookup"><span data-stu-id="02ed1-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="02ed1-141"><a name="insert-tables-bcp"></a>Utilidad de copia masiva (BCP) de la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="02ed1-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="02ed1-142">BCP es una utilidad de línea de comandos instalada con SQL Server y es una de las maneras más rápidas de mover datos.</span><span class="sxs-lookup"><span data-stu-id="02ed1-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="02ed1-143">Funciona en las tres variantes de SQL Server (SQL Server local, SQL Azure y máquina virtual SQL Server en Azure).</span><span class="sxs-lookup"><span data-stu-id="02ed1-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="02ed1-144">**¿Dónde deberían estar mis datos para BCP?**</span><span class="sxs-lookup"><span data-stu-id="02ed1-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="02ed1-145">Aunque no es necesario, tener archivos que contienen datos de origen que se encuentran en la misma máquina que el SQL Server de destino permite transferencias más rápidas (velocidad de red frente a velocidad de E/S de disco local).</span><span class="sxs-lookup"><span data-stu-id="02ed1-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="02ed1-146">Puede mover los archivos planos que contienen los datos en la máquina en la que está instalado SQL Server mediante las diversas herramientas de copia de archivos como [AZCopy](../storage/common/storage-use-azcopy.md), el [Explorador de Azure Storage](http://storageexplorer.com/) o copiar y pegar de Windows mediante el Protocolo de escritorio remoto (RDP).</span><span class="sxs-lookup"><span data-stu-id="02ed1-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="02ed1-147">Asegúrese de que la base de datos y las tablas se crean en la base de datos de SQL Server de destino.</span><span class="sxs-lookup"><span data-stu-id="02ed1-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="02ed1-148">Este es un ejemplo de cómo realizar esa tarea con los comandos `Create Database` y `Create Table`:</span><span class="sxs-lookup"><span data-stu-id="02ed1-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="02ed1-149">Genere el archivo de formato que describe el esquema de la tabla emitiendo el siguiente comando desde la línea de comandos de la máquina donde está instalado bcp.</span><span class="sxs-lookup"><span data-stu-id="02ed1-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="02ed1-150">Inserte los datos en la base de datos usando el comando bcp de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="02ed1-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="02ed1-151">Esto debería funcionar desde la línea de comandos suponiendo que SQL Server esté instalado en la misma máquina:</span><span class="sxs-lookup"><span data-stu-id="02ed1-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="02ed1-152">**Optimización de inserciones de BCP** Consulte el siguiente artículo ['Directrices para optimizar la importación masiva'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) para optimizar este tipo de inserciones.</span><span class="sxs-lookup"><span data-stu-id="02ed1-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="02ed1-153"><a name="insert-tables-bulkquery-parallel"></a>Poner en paralelo inserciones para el movimiento de datos más rápido</span><span class="sxs-lookup"><span data-stu-id="02ed1-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="02ed1-154">Si los datos que está moviendo son grandes, puede acelerar las cosas ejecutando simultáneamente varios comandos BCP en paralelo en un script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02ed1-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="02ed1-155">**Ingesta de Big Data** Para optimizar la carga de datos para conjuntos de datos grandes y muy grandes, cree particiones de sus tablas de bases de datos lógicas y físicas con varios grupos de archivos y tablas de particiones.</span><span class="sxs-lookup"><span data-stu-id="02ed1-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="02ed1-156">Para obtener más información acerca de cómo crear y cargar datos en las tablas de partición, consulte [Tablas de particiones de SQL de carga paralela](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="02ed1-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="02ed1-157">El script de PowerShell de ejemplo siguiente muestra inserciones paralelas con bcp:</span><span class="sxs-lookup"><span data-stu-id="02ed1-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="02ed1-158"><a name="insert-tables-bulkquery"></a>Consulta SQL de inserción masiva</span><span class="sxs-lookup"><span data-stu-id="02ed1-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="02ed1-159">La [Consulta SQL de inserción masiva](https://msdn.microsoft.com/library/ms188365) se puede usar para importar datos en la base de datos desde archivos basados en fila o columnas [los tipos admitidos se tratan en el tema [Preparar los datos para exportar o importar de forma masiva (SQL Server)](https://msdn.microsoft.com/library/ms188609)].</span><span class="sxs-lookup"><span data-stu-id="02ed1-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="02ed1-160">Estos son algunos ejemplos de comandos de inserción masiva:</span><span class="sxs-lookup"><span data-stu-id="02ed1-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="02ed1-161">Analice sus datos y establezca las opciones personalizadas antes de importar para asegurarse de que la base de datos de SQL Server asume el mismo formato para todos los campos especiales, como las fechas.</span><span class="sxs-lookup"><span data-stu-id="02ed1-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="02ed1-162">Este es un ejemplo de cómo establecer el formato de fecha como año-mes-día (si los datos contienen la fecha en formato año-mes-día):</span><span class="sxs-lookup"><span data-stu-id="02ed1-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="02ed1-163">Importar datos mediante instrucciones de importación en bloque:</span><span class="sxs-lookup"><span data-stu-id="02ed1-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="02ed1-164"><a name="sql-builtin-utilities"></a>Utilidades integradas de SQL Server</span><span class="sxs-lookup"><span data-stu-id="02ed1-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="02ed1-165">Puede utilizar los servicios de integraciones de SQL Server (SSIS) para importar datos en la VM de SQL Server de Azure desde un archivo plano.</span><span class="sxs-lookup"><span data-stu-id="02ed1-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="02ed1-166">SSIS está disponible en dos entornos de estudio.</span><span class="sxs-lookup"><span data-stu-id="02ed1-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="02ed1-167">Para obtener más detalles, consulte [Entornos de Studio e Integration Services (SSIS)](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="02ed1-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="02ed1-168">Para obtener más información acerca de las herramientas de datos de SQL Server, consulte [Herramientas de datos de Microsoft SQL Server](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="02ed1-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="02ed1-169">Para obtener más información acerca del Asistente para importación y exportación, consulte [Asistente para importación y exportación de SQL Server](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="02ed1-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="02ed1-170"><a name="sqlonprem_to_sqlonazurevm"></a>Mover datos desde un servidor SQL Server local a un servidor SQL Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="02ed1-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="02ed1-171">También puede usar las siguientes estrategias de migración:</span><span class="sxs-lookup"><span data-stu-id="02ed1-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="02ed1-172">Asistente para implementación de una base de datos de SQL Server en una máquina virtual de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="02ed1-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="02ed1-173">Exportación a un archivo plano</span><span class="sxs-lookup"><span data-stu-id="02ed1-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="02ed1-174">Asistente para migración de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="02ed1-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="02ed1-175">Copia de seguridad y restauración de una base de datos</span><span class="sxs-lookup"><span data-stu-id="02ed1-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="02ed1-176">Describimos cada una de estas opciones:</span><span class="sxs-lookup"><span data-stu-id="02ed1-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="02ed1-177">Asistente para implementación de una base de datos de SQL Server en una máquina virtual de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="02ed1-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="02ed1-178">El **Asistente para implementación de una base de datos de SQL Server en una máquina virtual de Microsoft Azure** es una manera sencilla y recomendada de mover datos de una instancia local de SQL Server a SQL Server en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="02ed1-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="02ed1-179">Para obtener pasos detallados así como un debate sobre otras alternativas, vea [Migración de una Base de datos SQL Server a SQL Server en una máquina virtual de Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="02ed1-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="02ed1-180"><a name="export-flat-file"></a>Exportación a un archivo plano</span><span class="sxs-lookup"><span data-stu-id="02ed1-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="02ed1-181">Se pueden usar diversos métodos para la exportación masiva de datos desde un servidor SQL Server local, como se documenta en el tema [Importación y exportación masiva de datos (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) .</span><span class="sxs-lookup"><span data-stu-id="02ed1-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="02ed1-182">Este documento tratará el programa de copia masiva (BCP) como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="02ed1-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="02ed1-183">Una vez que los datos se exportan a un archivo plano, se puede importar a otro servidor SQL Server mediante la importación masiva.</span><span class="sxs-lookup"><span data-stu-id="02ed1-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="02ed1-184">Exporte los datos del SQL Server local a un archivo mediante la utilidad bcp como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="02ed1-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="02ed1-185">Cree la base de datos y la tabla en la máquina virtual de SQL Server en Azure mediante `create database` y `create table` para el esquema de tablas que se exportó en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="02ed1-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="02ed1-186">Cree un archivo de formato para describir el esquema de tabla de los datos que se están exportando e importando.</span><span class="sxs-lookup"><span data-stu-id="02ed1-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="02ed1-187">En [Crear un archivo de formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx)se describen detalles del archivo de formato.</span><span class="sxs-lookup"><span data-stu-id="02ed1-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="02ed1-188">Generación de archivos de formato cuando se ejecuta BCP desde la máquina de SQL Server</span><span class="sxs-lookup"><span data-stu-id="02ed1-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="02ed1-189">Generación de archivos de formato cuando se ejecuta BCP de forma remota contra un SQL Server</span><span class="sxs-lookup"><span data-stu-id="02ed1-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="02ed1-190">Utilice cualquiera de los métodos descritos en la sección [Mover datos desde el origen de archivo](#filesource_to_sqlonazurevm) para mover los datos de los archivos planos a un servidor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="02ed1-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="02ed1-191"><a name="sql-migration"></a>Asistente para migración de Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="02ed1-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="02ed1-192">[Asistente para migración de Base de datos SQL](http://sqlazuremw.codeplex.com/) proporciona una manera fácil de mover datos entre dos instancias de SQL server.</span><span class="sxs-lookup"><span data-stu-id="02ed1-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="02ed1-193">Permite al usuario asignar el esquema de datos entre orígenes y tablas de destino, elegir los tipos de columna y otras funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="02ed1-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="02ed1-194">Utiliza la copia masiva (BCP) en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="02ed1-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="02ed1-195">A continuación se muestra una captura de la pantalla de bienvenida del Asistente para migración de base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="02ed1-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![Asistente para migración de SQL Server][2]

### <span data-ttu-id="02ed1-197"><a name="sql-backup"></a>Copia de seguridad y restauración de una base de datos</span><span class="sxs-lookup"><span data-stu-id="02ed1-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="02ed1-198">SQL Server es compatible con:</span><span class="sxs-lookup"><span data-stu-id="02ed1-198">SQL Server supports:</span></span>

1. <span data-ttu-id="02ed1-199">La [funcionalidad de copia de seguridad y restauración de la base de datos](https://msdn.microsoft.com/library/ms187048.aspx) (tanto a un archivo local como la exportación de bacpac a blob) y [Aplicaciones de capa de datos](https://msdn.microsoft.com/library/ee210546.aspx) (con bacpac).</span><span class="sxs-lookup"><span data-stu-id="02ed1-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="02ed1-200">Capacidad para crear directamente las máquinas virtuales de SQL Server en Azure con una copia o una base de datos copiada en una base de datos existente de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02ed1-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="02ed1-201">Para obtener más detalles, consulte [Usar el Asistente para copiar bases de datos](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="02ed1-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="02ed1-202">A continuación se muestra una captura de pantalla de las opciones de copia de seguridad y restauración de base de datos desde SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="02ed1-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Herramienta de importación SQL Server][1]

## <a name="resources"></a><span data-ttu-id="02ed1-204">Recursos</span><span class="sxs-lookup"><span data-stu-id="02ed1-204">Resources</span></span>
[<span data-ttu-id="02ed1-205">Migración de una Base de datos SQL Server a SQL Server en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="02ed1-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="02ed1-206">Información general de SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="02ed1-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
