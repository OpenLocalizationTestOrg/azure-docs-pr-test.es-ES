---
title: "datos de aaaCopy entre el almacén de Data Lake y base de datos de SQL Azure mediante Sqoop | Documentos de Microsoft"
description: "Usar Sqoop toocopy datos entre la base de datos de SQL Azure y almacén de Data Lake"
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
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="1d0d5-103">Copia de datos entre Almacén de Data Lake y Base de datos SQL de Azure mediante Sqoop</span><span class="sxs-lookup"><span data-stu-id="1d0d5-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="1d0d5-104">Obtenga información acerca de cómo toouse Apache Sqoop tooimport y exportar datos entre la base de datos de SQL Azure y almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="1d0d5-105">¿Qué es Sqoop?</span><span class="sxs-lookup"><span data-stu-id="1d0d5-105">What is Sqoop?</span></span>
<span data-ttu-id="1d0d5-106">Las aplicaciones de macrodatos son una opción natural para procesar datos no estructurados y semiestructurados, como registros y archivos.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="1d0d5-107">Sin embargo, también puede haber una necesidad de datos tooprocess estructurado que se almacenan en bases de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="1d0d5-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) es una herramienta diseñada tootransfer datos entre bases de datos relacionales y un repositorio de grandes cantidades de datos, como almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="1d0d5-109">Puede usarlo tooimport datos desde un sistema de administración de bases de datos relacionales (RDBMS) como base de datos de SQL Azure en el almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="1d0d5-110">Puede transformar, a continuación y analizar los datos de hello con cargas de trabajo de grandes cantidades de datos y, a continuación, exportar datos de hello en un RDBMS.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="1d0d5-111">En este tutorial, utilizará una base de datos de SQL Azure como tooimport y exportación de la base de datos relacional de.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d0d5-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1d0d5-112">Prerequisites</span></span>
<span data-ttu-id="1d0d5-113">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="1d0d5-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="1d0d5-114">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-114">**An Azure subscription**.</span></span> <span data-ttu-id="1d0d5-115">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1d0d5-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1d0d5-116">**Una cuenta de Almacén de Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="1d0d5-117">Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1d0d5-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="1d0d5-118">**Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="1d0d5-119">Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d0d5-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="1d0d5-120">En este artículo se supone que tiene un clúster de HDInsight Linux con acceso a Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="1d0d5-121">**Base de datos de SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-121">**Azure SQL Database**.</span></span> <span data-ttu-id="1d0d5-122">Para obtener instrucciones sobre cómo toocreate un, consulte [crear una base de datos de SQL Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1d0d5-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="1d0d5-123">¿Obtener información más rápidamente con vídeos?</span><span class="sxs-lookup"><span data-stu-id="1d0d5-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="1d0d5-124">[Vea este vídeo](https://mix.office.com/watch/1butcdjxmu114) acerca de cómo toocopy datos entre los Blobs de almacenamiento de Azure y almacén de Data Lake mediante DistCp.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="1d0d5-125">Crear tablas de ejemplo Hola base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1d0d5-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="1d0d5-126">toostart, cree dos tablas de ejemplo Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="1d0d5-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello base de datos de SQL Azure y, a continuación, ejecución Hola siguiendo las consultas.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="1d0d5-128">**Crear Tabla1**</span><span class="sxs-lookup"><span data-stu-id="1d0d5-128">**Create Table1**</span></span>

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

    <span data-ttu-id="1d0d5-129">**Crear Tabla2**</span><span class="sxs-lookup"><span data-stu-id="1d0d5-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="1d0d5-130">En **Tabla1**, agregue algunos datos de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="1d0d5-131">Deje **Tabla2** vacía.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-131">Leave **Table2** empty.</span></span> <span data-ttu-id="1d0d5-132">Los datos de **Tabla1** se importarán a Almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="1d0d5-133">Luego se importarán los datos de Almacén de Data Lake a **Tabla2**.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="1d0d5-134">Ejecute hello siguiente fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="1d0d5-135">Sqoop de uso de un clúster de HDInsight con acceso tooData Lake almacén</span><span class="sxs-lookup"><span data-stu-id="1d0d5-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="1d0d5-136">Un clúster de HDInsight ya tiene paquetes de Sqoop Hola disponibles.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="1d0d5-137">Si ha configurado el almacén de hello HDInsight clúster toouse Data Lake como un almacenamiento adicional, puede utilizar Sqoop (sin los cambios de configuración) tooimport o exportar datos entre una base de datos relacional (en este ejemplo, la base de datos de SQL Azure) y un almacén de Data Lake cuenta.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="1d0d5-138">Para este tutorial, se supone que ha creado un clúster de Linux, por lo que debe utilizar SSH tooconnect toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="1d0d5-139">Vea [clúster de HDInsight basados en Linux de conectar tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1d0d5-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="1d0d5-140">Compruebe si tiene acceso a cuenta de almacén de Data Lake Hola de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="1d0d5-141">Ejecute hello siguiente comando desde el símbolo del sistema de hello SSH:</span><span class="sxs-lookup"><span data-stu-id="1d0d5-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="1d0d5-142">Esto debería proporcionar una lista de archivos o carpetas en hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="1d0d5-143">Importación de datos de Base de datos SQL de Azure a Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1d0d5-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="1d0d5-144">Navegue directorio toohello donde Sqoop paquetes están disponibles.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="1d0d5-145">Normalmente, se encuentran en `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="1d0d5-146">Importar datos de Hola de **Table1** en hello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="1d0d5-147">Usar la sintaxis de hello:</span><span class="sxs-lookup"><span data-stu-id="1d0d5-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="1d0d5-148">Tenga en cuenta que **sql-base de datos-server-name** marcador de posición representa el nombre de Hola de servidor hello donde se ejecuta la base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="1d0d5-149">**nombre de base de datos de SQL** marcador de posición representa el nombre de la base de datos real de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="1d0d5-150">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="1d0d5-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="1d0d5-151">Comprobar que Hola datos ha sido transferido toohello cuenta de almacén de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="1d0d5-152">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1d0d5-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="1d0d5-153">Debería ver Hola después de salida.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="1d0d5-154">Cada **parte-m -*** archivo corresponde tooa fila en la tabla de origen de hello, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="1d0d5-155">Puede ver Hola contenido de parte de hello - m-* archivos tooverify.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="1d0d5-156">Exportación de datos de Almacén de Data Lake a Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="1d0d5-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="1d0d5-157">Exportar datos de Hola de tabla vacía de almacén de Data Lake cuenta toohello, **Table2**, Hola base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="1d0d5-158">Usar la sintaxis de hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="1d0d5-159">Por ejemplo,</span><span class="sxs-lookup"><span data-stu-id="1d0d5-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="1d0d5-160">Compruebe que Hola datos eran cargado toohello tabla de base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="1d0d5-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello base de datos de SQL Azure y, a continuación, Hola ejecución después de consulta.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="1d0d5-162">Esto debe tener Hola después de salida.</span><span class="sxs-lookup"><span data-stu-id="1d0d5-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="1d0d5-163">Consideraciones de rendimiento sobre el uso de Sqoop</span><span class="sxs-lookup"><span data-stu-id="1d0d5-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="1d0d5-164">Para su Sqoop de optimización del rendimiento de trabajos toocopy datos tooData Lake almacén, vea [documento de rendimiento de Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="1d0d5-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="1d0d5-165">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1d0d5-165">See also</span></span>
* [<span data-ttu-id="1d0d5-166">Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData</span><span class="sxs-lookup"><span data-stu-id="1d0d5-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="1d0d5-167">Protección de los datos en el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1d0d5-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1d0d5-168">Uso de Análisis de Azure Data Lake con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1d0d5-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1d0d5-169">Uso de HDInsight de Azure con el Almacén de Data Lake</span><span class="sxs-lookup"><span data-stu-id="1d0d5-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
