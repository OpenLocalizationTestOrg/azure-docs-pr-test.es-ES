---
title: aaaApache Sqoop con Hadoop - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse tooimport Sqoop de Apache y exportación entre Hadoop en HDInsight y una base de datos de SQL Azure."
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
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="ace65-104">Usar Apache Sqoop tooimport y exportar datos entre la base de datos de SQL y Hadoop en HDInsight</span><span class="sxs-lookup"><span data-stu-id="ace65-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="ace65-105">Obtenga información acerca de cómo agrupar toouse Apache Sqoop tooimport y exportación entre un Hadoop en HDInsight de Azure y base de datos de Microsoft SQL Server o base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="ace65-106">Hola los pasos de este Hola de uso de documento `sqoop` comando directamente desde el nodo principal de hello del clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="ace65-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="ace65-107">Utilice el nodo principal de SSH tooconnect toohello y ejecutar comandos de hello en este documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ace65-108">Hello pasos descritos en este documento solo funcionan con clústeres de HDInsight que utilizan Linux.</span><span class="sxs-lookup"><span data-stu-id="ace65-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="ace65-109">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="ace65-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ace65-110">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ace65-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="ace65-111">Instalación de FreeTDS</span><span class="sxs-lookup"><span data-stu-id="ace65-111">Install FreeTDS</span></span>

1. <span data-ttu-id="ace65-112">Use el clúster de HDInsight de toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="ace65-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="ace65-113">Por ejemplo, hello siguiente comando conecta toohello de nodo principal principal de un clúster denominado `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="ace65-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="ace65-114">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ace65-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="ace65-115">Usar hello siguiendo el uso del comando tooinstall:</span><span class="sxs-lookup"><span data-stu-id="ace65-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="ace65-116">Uso se utiliza en varios pasos tooconnect tooSQL base de datos.</span><span class="sxs-lookup"><span data-stu-id="ace65-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="ace65-117">Crear tabla de hello en la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="ace65-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ace65-118">Si usas clúster de HDInsight de Hola y base de datos de SQL se crea en [crear clúster y la base de datos SQL](hdinsight-use-sqoop.md), omita los pasos de hello en esta sección.</span><span class="sxs-lookup"><span data-stu-id="ace65-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="ace65-119">Hello base de datos y tabla se han creado como parte del programa Hola a los pasos de hello [crear clúster y la base de datos SQL](hdinsight-use-sqoop.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="ace65-120">Desde la sesión de SSH de hello, usar hello después el servidor de base de datos SQL de comandos tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ace65-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="ace65-121">Recibir toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="ace65-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="ace65-122">En hello `1>` símbolo del sistema, escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="ace65-122">At hello `1>` prompt, enter hello following query:</span></span>

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

    <span data-ttu-id="ace65-123">Cuando Hola `GO` instrucción se haya especificado, se evalúan en las instrucciones anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="ace65-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="ace65-124">En primer lugar, Hola **mobiledata** se crea la tabla, a continuación, se agrega un índice agrupado tooit (requerido por la base de datos SQL).</span><span class="sxs-lookup"><span data-stu-id="ace65-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="ace65-125">Hola de uso después de tooverify de consulta que Hola tabla se ha creado:</span><span class="sxs-lookup"><span data-stu-id="ace65-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="ace65-126">Vea toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="ace65-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="ace65-127">Escriba `exit` en hello `1>` solicitar utilidad de tooexit Hola tsql.</span><span class="sxs-lookup"><span data-stu-id="ace65-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="ace65-128">Exportación de Sqoop</span><span class="sxs-lookup"><span data-stu-id="ace65-128">Sqoop export</span></span>

1. <span data-ttu-id="ace65-129">Del clúster de toohello de conexión de SSH hello, utilice Hola después tooverify de comando que Sqoop puede ver la base de datos de SQL:</span><span class="sxs-lookup"><span data-stu-id="ace65-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="ace65-130">Cuando se le solicite, escriba la contraseña de Hola para inicio de sesión de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="ace65-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="ace65-131">Este comando devuelve una lista de bases de datos, incluidos hello **sqooptest** base de datos que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ace65-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="ace65-132">datos de tooexport de **hivesampletable** toohello **mobiledata** tablas, utilice el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="ace65-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="ace65-133">Este comando indica a Sqoop tooconnect toohello **sqooptest** base de datos.</span><span class="sxs-lookup"><span data-stu-id="ace65-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="ace65-134">Sqoop, a continuación, exporta los datos de **wasb: / / / hive/almacenamiento/hivesampletable** toohello **mobiledata** tabla.</span><span class="sxs-lookup"><span data-stu-id="ace65-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ace65-135">Use `wasb:///` si almacenamiento predeterminado de hello para el clúster es una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="ace65-136">Use `adl:///` si es una instancia de Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ace65-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="ace65-137">Una vez completado el comando de hello, utilice Hola después comandos tooconnect toohello base de datos mediante TSQL:</span><span class="sxs-lookup"><span data-stu-id="ace65-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="ace65-138">Una vez conectado, Hola de uso después de tooverify instrucciones que Hola datos fue exportado toohello **mobiledata** tabla:</span><span class="sxs-lookup"><span data-stu-id="ace65-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="ace65-139">Debería ver una lista de datos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ace65-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="ace65-140">Tipo `exit` utilidad de tooexit Hola tsql.</span><span class="sxs-lookup"><span data-stu-id="ace65-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="ace65-141">Importación de Sqoop</span><span class="sxs-lookup"><span data-stu-id="ace65-141">Sqoop import</span></span>

1. <span data-ttu-id="ace65-142">Siguiente Hola de uso del comando tooimport datos de hello **mobiledata** tabla de base de datos de SQL, toohello **wasb: / / / tutoriales/usesqoop/importeddata** directorio HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ace65-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="ace65-143">campos de Hello en los datos de hello están separados por un carácter de tabulación y líneas de saludo se finalizan con un carácter de nueva línea.</span><span class="sxs-lookup"><span data-stu-id="ace65-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="ace65-144">Una vez completada la importación de hello, utilice Hola después a toolist comando datos hello en el nuevo directorio de hello:</span><span class="sxs-lookup"><span data-stu-id="ace65-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="ace65-145">Uso de SQL Server</span><span class="sxs-lookup"><span data-stu-id="ace65-145">Using SQL Server</span></span>

<span data-ttu-id="ace65-146">También puede utilizar Sqoop tooimport y exportar datos de SQL Server, ya sea en su centro de datos o en una máquina Virtual hospedada en Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="ace65-147">Hola diferencias entre el uso de la base de datos SQL y SQL Server son:</span><span class="sxs-lookup"><span data-stu-id="ace65-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="ace65-148">HDInsight y SQL Server debe estar en Hola misma red Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="ace65-149">Para obtener un ejemplo, vea hello [red local de HDInsight conectar tooyour](./connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="ace65-150">Para obtener más información sobre el uso de HDInsight con una red Virtual de Azure, vea hello [HDInsight ampliar con red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="ace65-151">Para obtener más información sobre la red Virtual de Azure, vea hello [información general de red Virtual](../virtual-network/virtual-networks-overview.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="ace65-152">SQL Server debe estar configurado tooallow autenticación de SQL.</span><span class="sxs-lookup"><span data-stu-id="ace65-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="ace65-153">Para obtener más información, vea hello [elegir un modo de autenticación](https://msdn.microsoft.com/ms144284.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="ace65-154">Puede que tenga las conexiones remotas de tooconfigure SQL Server tooaccept.</span><span class="sxs-lookup"><span data-stu-id="ace65-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="ace65-155">Para obtener más información, vea hello [cómo tootroubleshoot conexión toohello SQL Server base de datos motor](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="ace65-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="ace65-156">Crear hello **sqooptest** base de datos de SQL Server mediante una utilidad como **SQL Server Management Studio** o **tsql**.</span><span class="sxs-lookup"><span data-stu-id="ace65-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="ace65-157">pasos de Hello para el uso de hello Azure CLI sólo funcionan para la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="ace65-158">Hola de uso después de hello de toocreate de instrucciones de Transact-SQL **mobiledata** tabla:</span><span class="sxs-lookup"><span data-stu-id="ace65-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

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

* <span data-ttu-id="ace65-159">Cuando se conecte toohello SQL Server desde HDInsight, puede tener dirección IP de hello toouse del programa Hola a SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ace65-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="ace65-160">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ace65-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="ace65-161">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="ace65-161">Limitations</span></span>

* <span data-ttu-id="ace65-162">La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.</span><span class="sxs-lookup"><span data-stu-id="ace65-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="ace65-163">Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop realiza varias inserciones en lugar de procesamiento por lotes las operaciones de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ace65-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ace65-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ace65-164">Next steps</span></span>

<span data-ttu-id="ace65-165">Ahora que ha aprendido cómo toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="ace65-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="ace65-166">toolearn más información, vea:</span><span class="sxs-lookup"><span data-stu-id="ace65-166">toolearn more, see:</span></span>

* <span data-ttu-id="ace65-167">[Uso de Oozie con HDInsight][hdinsight-use-oozie]: use la acción de Sqoop en un flujo de trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="ace65-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="ace65-168">[Analizar datos de retrasos de vuelos con HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze flight retrasar datos y, a continuación, usar base de datos de Sqoop tooexport datos tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="ace65-169">[Cargar datos tooHDInsight][hdinsight-upload-data]: dar con otros métodos para cargar el almacenamiento de blobs de datos tooHDInsight o SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ace65-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

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
