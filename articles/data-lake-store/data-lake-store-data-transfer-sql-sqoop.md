---
title: Copia de datos entre Data Lake Store y Azure SQL Database mediante Sqoop | Microsoft Docs
description: "Uso de Sqoop para copiar datos entre Almacén de Data Lake y Base de datos SQL de Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="797ba-103">Copia de datos entre Almacén de Data Lake y Base de datos SQL de Azure mediante Sqoop</span><span class="sxs-lookup"><span data-stu-id="797ba-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="797ba-104">Aprenda a usar Apache Sqoop para importar y exportar datos entre Base de datos SQL de Azure y Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="797ba-105">¿Qué es Sqoop?</span><span class="sxs-lookup"><span data-stu-id="797ba-105">What is Sqoop?</span></span>
<span data-ttu-id="797ba-106">Las aplicaciones de macrodatos son una opción natural para procesar datos no estructurados y semiestructurados, como registros y archivos.</span><span class="sxs-lookup"><span data-stu-id="797ba-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="797ba-107">Pero también puede que sea necesario procesar datos estructurados que se almacenan en bases de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="797ba-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="797ba-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) es una herramienta diseñada para transferir datos entre bases de datos relacionales y un repositorio de macrodatos, como Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="797ba-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="797ba-109">Puede usarla para importar datos desde un sistema de administración de bases de datos relacionales (RDBMS) como Base de datos SQL de Azure a Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="797ba-110">Después, puede transformar y analizar los datos mediante cargas de trabajo de macrodatos y exportar los datos a un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="797ba-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="797ba-111">En este tutorial, use una Base de datos SQL de Azure como la base de datos relacional para importar y exportar.</span><span class="sxs-lookup"><span data-stu-id="797ba-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="797ba-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="797ba-112">Prerequisites</span></span>
<span data-ttu-id="797ba-113">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="797ba-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="797ba-114">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="797ba-114">**An Azure subscription**.</span></span> <span data-ttu-id="797ba-115">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="797ba-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="797ba-116">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="797ba-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="797ba-117">Para obtener instrucciones sobre cómo crear una, consulte la [introducción al Almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="797ba-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="797ba-118">**Clúster de HDInsight de Azure** con acceso a una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="797ba-119">Consulte [Creación de un clúster de HDInsight con Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="797ba-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="797ba-120">En este artículo se supone que tiene un clúster de HDInsight Linux con acceso a Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="797ba-121">**Base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="797ba-121">**Azure SQL Database**.</span></span> <span data-ttu-id="797ba-122">Para obtener instrucciones sobre cómo crear una, vea [Creación de una Base de datos SQL de Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="797ba-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="797ba-123">¿Obtener información más rápidamente con vídeos?</span><span class="sxs-lookup"><span data-stu-id="797ba-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="797ba-124">[Vea este vídeo](https://mix.office.com/watch/1butcdjxmu114) para saber cómo copiar datos entre los blobs de Almacenamiento de Azure y Almacén de Data Lake mediante DistCp.</span><span class="sxs-lookup"><span data-stu-id="797ba-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="797ba-125">Creación de tablas de ejemplo en la Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="797ba-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="797ba-126">Para empezar, cree dos tablas de ejemplo en la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="797ba-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="797ba-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio para conectarse a la Base de datos SQL de Azure y ejecute las consultas siguientes:</span><span class="sxs-lookup"><span data-stu-id="797ba-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="797ba-128">**Crear Tabla1**</span><span class="sxs-lookup"><span data-stu-id="797ba-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="797ba-129">**Crear Tabla2**</span><span class="sxs-lookup"><span data-stu-id="797ba-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="797ba-130">En **Tabla1**, agregue algunos datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="797ba-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="797ba-131">Deje **Tabla2** vacía.</span><span class="sxs-lookup"><span data-stu-id="797ba-131">Leave **Table2** empty.</span></span> <span data-ttu-id="797ba-132">Los datos de **Tabla1** se importarán a Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="797ba-133">Luego se importarán los datos de Almacén de Data Lake a **Tabla2**.</span><span class="sxs-lookup"><span data-stu-id="797ba-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="797ba-134">Ejecute el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="797ba-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="797ba-135">Uso de Sqoop en un clúster de HDInsight con acceso a Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="797ba-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="797ba-136">Un clúster de HDInsight ya tiene los paquetes de Sqoop disponibles.</span><span class="sxs-lookup"><span data-stu-id="797ba-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="797ba-137">Si ha configurado el clúster de HDInsight para utilizar Almacén de Data Lake como almacenamiento adicional, puede usar Sqoop (sin cambios de configuración) para importar o exportar datos entre una base de datos relacional (en este ejemplo, Base de datos SQL de Azure) y una cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="797ba-138">Para este tutorial, se supone que ha creado un clúster de Linux, por lo que debe usar SSH para conectarse al clúster.</span><span class="sxs-lookup"><span data-stu-id="797ba-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="797ba-139">Consulte [Conexión a un clúster de HDInsight basado en Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="797ba-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="797ba-140">Compruebe que puede acceder a la cuenta de Almacén de Data Lake desde el clúster.</span><span class="sxs-lookup"><span data-stu-id="797ba-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="797ba-141">Ejecute el siguiente comando desde el símbolo del sistema de SSH:</span><span class="sxs-lookup"><span data-stu-id="797ba-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="797ba-142">Esto debería proporcionar una lista de archivos o carpetas en la cuenta del Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="797ba-143">Importación de datos de Base de datos SQL de Azure a Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="797ba-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="797ba-144">Navegue al directorio donde están disponibles los paquetes de Sqoop.</span><span class="sxs-lookup"><span data-stu-id="797ba-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="797ba-145">Normalmente, se encuentran en `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="797ba-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="797ba-146">Importe datos de **Tabla1** a la cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="797ba-147">Use la sintaxis siguiente:</span><span class="sxs-lookup"><span data-stu-id="797ba-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="797ba-148">Tenga en cuenta que el marcador de posición **sql-database-server-name** representa el nombre del servidor donde se ejecuta la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="797ba-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="797ba-149">**sql-database-name** representa el nombre de la base de datos real.</span><span class="sxs-lookup"><span data-stu-id="797ba-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="797ba-150">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="797ba-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="797ba-151">Compruebe que los datos se han transferido a la cuenta de Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="797ba-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="797ba-152">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="797ba-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="797ba-153">Debería ver la siguiente salida.</span><span class="sxs-lookup"><span data-stu-id="797ba-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="797ba-154">Cada archivo **part-m-*** corresponde a una fila de la tabla de origen, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="797ba-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="797ba-155">Puede ver el contenido de los archivos part-m-* para comprobarlo.</span><span class="sxs-lookup"><span data-stu-id="797ba-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="797ba-156">Exportación de datos de Almacén de Data Lake a Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="797ba-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="797ba-157">Exporte los datos de la cuenta de Data Lake Store a la tabla vacía, **Table2**, en la Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="797ba-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="797ba-158">Use la sintaxis siguiente.</span><span class="sxs-lookup"><span data-stu-id="797ba-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="797ba-159">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="797ba-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="797ba-160">Compruebe que los datos se han cargado en la tabla de Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="797ba-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="797ba-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio para conectarse a la Base de datos SQL de Azure y ejecute la siguiente consulta.</span><span class="sxs-lookup"><span data-stu-id="797ba-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="797ba-162">El resultado debe ser el siguiente.</span><span class="sxs-lookup"><span data-stu-id="797ba-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="797ba-163">Consideraciones de rendimiento sobre el uso de Sqoop</span><span class="sxs-lookup"><span data-stu-id="797ba-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="797ba-164">Para optimizar el rendimiento del trabajo de Scoop con el fin de copiar datos en el Data Lake Store, consulte el [documento de rendimiento de Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="797ba-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="797ba-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="797ba-165">See also</span></span>
* [<span data-ttu-id="797ba-166">Copiar datos de los blobs de almacenamiento de Azure en el Almacén Data Lake</span><span class="sxs-lookup"><span data-stu-id="797ba-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="797ba-167">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="797ba-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="797ba-168">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="797ba-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="797ba-169">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="797ba-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
