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
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Usar Apache Sqoop tooimport y exportar datos entre la base de datos de SQL y Hadoop en HDInsight

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Obtenga información acerca de cómo agrupar toouse Apache Sqoop tooimport y exportación entre un Hadoop en HDInsight de Azure y base de datos de Microsoft SQL Server o base de datos de SQL Azure. Hola los pasos de este Hola de uso de documento `sqoop` comando directamente desde el nodo principal de hello del clúster de Hadoop de Hola. Utilice el nodo principal de SSH tooconnect toohello y ejecutar comandos de hello en este documento.

> [!IMPORTANT]
> Hello pasos descritos en este documento solo funcionan con clústeres de HDInsight que utilizan Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="install-freetds"></a>Instalación de FreeTDS

1. Use el clúster de HDInsight de toohello tooconnect SSH. Por ejemplo, hello siguiente comando conecta toohello de nodo principal principal de un clúster denominado `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Usar hello siguiendo el uso del comando tooinstall:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    Uso se utiliza en varios pasos tooconnect tooSQL base de datos.

## <a name="create-hello-table-in-sql-database"></a>Crear tabla de hello en la base de datos SQL

> [!IMPORTANT]
> Si usas clúster de HDInsight de Hola y base de datos de SQL se crea en [crear clúster y la base de datos SQL](hdinsight-use-sqoop.md), omita los pasos de hello en esta sección. Hello base de datos y tabla se han creado como parte del programa Hola a los pasos de hello [crear clúster y la base de datos SQL](hdinsight-use-sqoop.md) documento.

1. Desde la sesión de SSH de hello, usar hello después el servidor de base de datos SQL de comandos tooconnect toohello.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Recibir toohello similar de salida siguiente texto:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. En hello `1>` símbolo del sistema, escriba Hola después de consulta:

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

    Cuando Hola `GO` instrucción se haya especificado, se evalúan en las instrucciones anteriores Hola. En primer lugar, Hola **mobiledata** se crea la tabla, a continuación, se agrega un índice agrupado tooit (requerido por la base de datos SQL).

    Hola de uso después de tooverify de consulta que Hola tabla se ha creado:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Vea toohello similar de salida siguiente texto:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Escriba `exit` en hello `1>` solicitar utilidad de tooexit Hola tsql.

## <a name="sqoop-export"></a>Exportación de Sqoop

1. Del clúster de toohello de conexión de SSH hello, utilice Hola después tooverify de comando que Sqoop puede ver la base de datos de SQL:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    Cuando se le solicite, escriba la contraseña de Hola para inicio de sesión de base de datos SQL de Hola.

    Este comando devuelve una lista de bases de datos, incluidos hello **sqooptest** base de datos que creó anteriormente.

2. datos de tooexport de **hivesampletable** toohello **mobiledata** tablas, utilice el siguiente comando de hello:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    Este comando indica a Sqoop tooconnect toohello **sqooptest** base de datos. Sqoop, a continuación, exporta los datos de **wasb: / / / hive/almacenamiento/hivesampletable** toohello **mobiledata** tabla.

    > [!IMPORTANT]
    > Use `wasb:///` si almacenamiento predeterminado de hello para el clúster es una cuenta de almacenamiento de Azure. Use `adl:///` si es una instancia de Azure Data Lake Store.

3. Una vez completado el comando de hello, utilice Hola después comandos tooconnect toohello base de datos mediante TSQL:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Una vez conectado, Hola de uso después de tooverify instrucciones que Hola datos fue exportado toohello **mobiledata** tabla:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Debería ver una lista de datos de tabla de Hola. Tipo `exit` utilidad de tooexit Hola tsql.

## <a name="sqoop-import"></a>Importación de Sqoop

1. Siguiente Hola de uso del comando tooimport datos de hello **mobiledata** tabla de base de datos de SQL, toohello **wasb: / / / tutoriales/usesqoop/importeddata** directorio HDInsight:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    campos de Hello en los datos de hello están separados por un carácter de tabulación y líneas de saludo se finalizan con un carácter de nueva línea.

2. Una vez completada la importación de hello, utilice Hola después a toolist comando datos hello en el nuevo directorio de hello:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Uso de SQL Server

También puede utilizar Sqoop tooimport y exportar datos de SQL Server, ya sea en su centro de datos o en una máquina Virtual hospedada en Azure. Hola diferencias entre el uso de la base de datos SQL y SQL Server son:

* HDInsight y SQL Server debe estar en Hola misma red Virtual de Azure.

    Para obtener un ejemplo, vea hello [red local de HDInsight conectar tooyour](./connect-on-premises-network.md) documento.

    Para obtener más información sobre el uso de HDInsight con una red Virtual de Azure, vea hello [HDInsight ampliar con red Virtual de Azure](hdinsight-extend-hadoop-virtual-network.md) documento. Para obtener más información sobre la red Virtual de Azure, vea hello [información general de red Virtual](../virtual-network/virtual-networks-overview.md) documento.

* SQL Server debe estar configurado tooallow autenticación de SQL. Para obtener más información, vea hello [elegir un modo de autenticación](https://msdn.microsoft.com/ms144284.aspx) documento.

* Puede que tenga las conexiones remotas de tooconfigure SQL Server tooaccept. Para obtener más información, vea hello [cómo tootroubleshoot conexión toohello SQL Server base de datos motor](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) documento.

* Crear hello **sqooptest** base de datos de SQL Server mediante una utilidad como **SQL Server Management Studio** o **tsql**. pasos de Hello para el uso de hello Azure CLI sólo funcionan para la base de datos de SQL Azure.

    Hola de uso después de hello de toocreate de instrucciones de Transact-SQL **mobiledata** tabla:

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

* Cuando se conecte toohello SQL Server desde HDInsight, puede tener dirección IP de hello toouse del programa Hola a SQL Server. Por ejemplo:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Limitaciones

* La exportación masiva - basados en Linux con HDInsight, Hola Sqoop conector utilizado tooexport datos tooMicrosoft SQL Server o base de datos de SQL Azure no es compatible con las inserciones masivas.

* Procesamiento por lotes: con HDInsight basados en Linux, cuando se usa hello `-batch` cambiar cuando se realizan inserciones, Sqoop realiza varias inserciones en lugar de procesamiento por lotes las operaciones de inserción de Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo toouse Sqoop. toolearn más información, vea:

* [Uso de Oozie con HDInsight][hdinsight-use-oozie]: use la acción de Sqoop en un flujo de trabajo de Oozie.
* [Analizar datos de retrasos de vuelos con HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze flight retrasar datos y, a continuación, usar base de datos de Sqoop tooexport datos tooan SQL Azure.
* [Cargar datos tooHDInsight][hdinsight-upload-data]: dar con otros métodos para cargar el almacenamiento de blobs de datos tooHDInsight o SQL Azure.

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
