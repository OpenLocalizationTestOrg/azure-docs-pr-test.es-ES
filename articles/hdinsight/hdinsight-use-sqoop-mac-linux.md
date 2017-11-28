---
title: Apache Sqoop con Hadoop - Azure HDInsight | Microsoft Docs
description: Aprenda a usar Apache Sqoop para realizar importaciones y exportaciones entre Hadoop en HDInsight y Azure SQL Database.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: 35dcbb91e6af1480685c9fd5b829c54277c1c605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="a67c5-104">Uso de Apache Sqoop para importar y exportar datos entre Hadoop en HDInsight y SQL Database</span><span class="sxs-lookup"><span data-stu-id="a67c5-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="a67c5-105">Aprenda a usar Apache Sqoop para realizar importaciones y exportaciones entre un clúster de Hadoop en Azure HDInsight y Azure SQL Database o la base de datos de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a67c5-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="a67c5-106">En los pasos descritos en este documento se usa el comando `sqoop` directamente desde el nodo principal del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a67c5-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="a67c5-107">Usaremos SSH para conectarnos al nodo principal y ejecutar los comandos de este documento.</span><span class="sxs-lookup"><span data-stu-id="a67c5-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a67c5-108">Los pasos de este documento solo funcionan con clústeres de HDInsight que usan Linux.</span><span class="sxs-lookup"><span data-stu-id="a67c5-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="a67c5-109">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="a67c5-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a67c5-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a67c5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="a67c5-111">Instalación de FreeTDS</span><span class="sxs-lookup"><span data-stu-id="a67c5-111">Install FreeTDS</span></span>

1. <span data-ttu-id="a67c5-112">Use SSH para conectarse al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a67c5-112">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="a67c5-113">Por ejemplo, el siguiente comando se conecta al nodo primario principal de un clúster denominado `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="a67c5-113">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a67c5-114">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a67c5-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a67c5-115">Use el siguiente comando para instalar FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="a67c5-115">Use the following command to install FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="a67c5-116">FreeTDS se usa en varios pasos para la conexión con la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a67c5-116">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="a67c5-117">Creación de la tabla en la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a67c5-117">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a67c5-118">Si usa el clúster de HDInsight y una instancia de SQL Database creados en [Creación del clúster y la base de datos SQL](hdinsight-use-sqoop.md), omita los pasos de esta sección.</span><span class="sxs-lookup"><span data-stu-id="a67c5-118">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="a67c5-119">La base de datos y la tabla se crearon como parte de los pasos del documento [Creación del clúster y la base de datos SQL](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="a67c5-119">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="a67c5-120">Desde la sesión de SSH, use el comando siguiente para conectarse al servidor de la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a67c5-120">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="a67c5-121">Recibirá una salida similar al texto siguiente:</span><span class="sxs-lookup"><span data-stu-id="a67c5-121">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="a67c5-122">En el símbolo del sistema `1>`, escriba la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="a67c5-122">At the `1>` prompt, enter the following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="a67c5-123">Cuando se haya especificado la instrucción `GO`, se evaluarán las instrucciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="a67c5-123">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="a67c5-124">En primer lugar, se crea la tabla **mobiledata** y, a continuación, se agrega un índice agrupado a ella (es necesario para la base de datos SQL).</span><span class="sxs-lookup"><span data-stu-id="a67c5-124">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="a67c5-125">Use la siguiente consulta para comprobar que se ha creado la tabla:</span><span class="sxs-lookup"><span data-stu-id="a67c5-125">Use the following query to verify that the table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="a67c5-126">Verá un resultado similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="a67c5-126">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="a67c5-127">Entrar `exit` at the `1>` .</span><span class="sxs-lookup"><span data-stu-id="a67c5-127">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="a67c5-128">Exportación de Sqoop</span><span class="sxs-lookup"><span data-stu-id="a67c5-128">Sqoop export</span></span>

1. <span data-ttu-id="a67c5-129">Desde la conexión SSH con el clúster, use el siguiente comando para comprobar que Sqoop puede ver la instancia de SQL Database:</span><span class="sxs-lookup"><span data-stu-id="a67c5-129">From the SSH connection to the cluster, use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="a67c5-130">Cuando se le solicite, escriba la contraseña para el inicio de sesión de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a67c5-130">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="a67c5-131">Este comando devuelve una lista de bases de datos, incluida la base de datos **sqooptest** que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a67c5-131">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="a67c5-132">Use el siguiente comando para exportar los datos desde **hivesampletable** a la tabla **mobiledata**:</span><span class="sxs-lookup"><span data-stu-id="a67c5-132">To export data from **hivesampletable** to the **mobiledata** table, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="a67c5-133">Este comando indica a Sqoop que se conecte a la base de datos **sqooptest**.</span><span class="sxs-lookup"><span data-stu-id="a67c5-133">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="a67c5-134">Luego Sqoop exporta datos de **wasb:///hive/warehouse/hivesampletable** a la tabla **mobiledata**.</span><span class="sxs-lookup"><span data-stu-id="a67c5-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a67c5-135">Use `wasb:///` si el almacenamiento predeterminado del clúster es una cuenta de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a67c5-135">Use `wasb:///` if the default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="a67c5-136">Use `adl:///` si es una instancia de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a67c5-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="a67c5-137">Una vez completado el comando, use el siguiente comando para conectarse a la base de datos mediante TSQL:</span><span class="sxs-lookup"><span data-stu-id="a67c5-137">After the command completes, use the following command to connect to the database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="a67c5-138">Una vez conectado, utilice las instrucciones siguientes para comprobar que los datos se exportaron a la tabla **mobiledata** :</span><span class="sxs-lookup"><span data-stu-id="a67c5-138">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="a67c5-139">Debería ver una lista de los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="a67c5-139">You should see a listing of data in the table.</span></span> <span data-ttu-id="a67c5-140">Escriba `exit` para salir de la utilidad de tsql.</span><span class="sxs-lookup"><span data-stu-id="a67c5-140">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="a67c5-141">Importación de Sqoop</span><span class="sxs-lookup"><span data-stu-id="a67c5-141">Sqoop import</span></span>

1. <span data-ttu-id="a67c5-142">Use el siguiente comando para importar datos de la tabla **mobiledata** de SQL Database al directorio **wasb:///tutorials/usesqoop/importeddata** de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a67c5-142">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="a67c5-143">Los campos de los datos se separan mediante un carácter de tabulación y las líneas terminan con un carácter de nueva línea.</span><span class="sxs-lookup"><span data-stu-id="a67c5-143">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="a67c5-144">Una vez completada la importación, use el siguiente comando para enumerar los datos en el nuevo directorio:</span><span class="sxs-lookup"><span data-stu-id="a67c5-144">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="a67c5-145">Uso de SQL Server</span><span class="sxs-lookup"><span data-stu-id="a67c5-145">Using SQL Server</span></span>

<span data-ttu-id="a67c5-146">También puede utilizar Sqoop para importar y exportar datos de SQL Server, tanto en el centro de datos como en una máquina Virtual hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="a67c5-146">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="a67c5-147">Las diferencias entre el uso de la base de datos SQL y SQL Server son:</span><span class="sxs-lookup"><span data-stu-id="a67c5-147">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="a67c5-148">Tanto HDInsight como SQL Server deben estar en la misma red Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="a67c5-148">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="a67c5-149">Para obtener un ejemplo, vea el documento [Conexión de HDInsight a la red local](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="a67c5-149">For an example, see the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="a67c5-150">Para más información sobre cómo usar HDInsight con redes Azure Virtual Network, vea el documento [Extensión de las funcionalidades de HDInsight con Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="a67c5-150">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="a67c5-151">Para más información sobre Azure Virtual Network, vea el documento [Información general sobre Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a67c5-151">For more information on Azure Virtual Network, see the [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="a67c5-152">SQL Server estar configurado para permitir la autenticación SQL.</span><span class="sxs-lookup"><span data-stu-id="a67c5-152">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="a67c5-153">Para más información, vea el documento [Choose an Authentication Mode (Elegir un modo de autenticación)](https://msdn.microsoft.com/ms144284.aspx).</span><span class="sxs-lookup"><span data-stu-id="a67c5-153">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="a67c5-154">Es posible que tenga que configurar SQL Server para aceptar conexiones remotas.</span><span class="sxs-lookup"><span data-stu-id="a67c5-154">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="a67c5-155">Para más información, vea el documento [How to troubleshoot connecting to the SQL Server database engine (Solución de problemas de conexión al motor de base de datos de SQL Server)](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx).</span><span class="sxs-lookup"><span data-stu-id="a67c5-155">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="a67c5-156">Cree la base de datos **sqooptest** en SQL Server mediante una utilidad como **SQL Server Management Studio** o **tsql**.</span><span class="sxs-lookup"><span data-stu-id="a67c5-156">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="a67c5-157">Los pasos para usar la CLI de Azure solo funcionan para Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a67c5-157">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="a67c5-158">Use las siguientes instrucciones Transact-SQL para crear la tabla **mobiledata**:</span><span class="sxs-lookup"><span data-stu-id="a67c5-158">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="a67c5-159">Al conectarse a SQL Server desde HDInsight, es posible que tenga que usar la dirección IP de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a67c5-159">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="a67c5-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a67c5-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="a67c5-161">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="a67c5-161">Limitations</span></span>

* <span data-ttu-id="a67c5-162">Exportación masiva: con HDInsight basado en Linux, el conector Sqoop que se utiliza para exportar datos a Microsoft SQL Server o Base de datos SQL Azure no es compatible actualmente con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="a67c5-162">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="a67c5-163">Procesamiento por lotes: con HDInsight basado en Linux, cuando se usa `-batch` al realizar inserciones, Sqoop realiza varias inserciones en lugar de procesar por lotes las operaciones de inserción.</span><span class="sxs-lookup"><span data-stu-id="a67c5-163">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a67c5-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a67c5-164">Next steps</span></span>

<span data-ttu-id="a67c5-165">Ahora ya ha aprendido a usar Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a67c5-165">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="a67c5-166">Para obtener más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="a67c5-166">To learn more, see:</span></span>

* <span data-ttu-id="a67c5-167">[Uso de Oozie con HDInsight][hdinsight-use-oozie]: use la acción Sqoop en un flujo de trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="a67c5-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="a67c5-168">[Análisis de la información de retraso de vuelos con HDInsight][hdinsight-analyze-flight-data]: use Hive para analizar la información de retraso de los vuelos y luego use Sqoop para exportar los datos a una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="a67c5-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="a67c5-169">[Carga de datos en HDInsight][hdinsight-upload-data]: busque otros métodos para cargar datos en HDInsight o Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a67c5-169">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
