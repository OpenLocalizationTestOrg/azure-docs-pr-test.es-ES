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
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Copia de datos entre Almacén de Data Lake y Base de datos SQL de Azure mediante Sqoop
Obtenga información acerca de cómo toouse Apache Sqoop tooimport y exportar datos entre la base de datos de SQL Azure y almacén de Data Lake.

## <a name="what-is-sqoop"></a>¿Qué es Sqoop?
Las aplicaciones de macrodatos son una opción natural para procesar datos no estructurados y semiestructurados, como registros y archivos. Sin embargo, también puede haber una necesidad de datos tooprocess estructurado que se almacenan en bases de datos relacionales.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) es una herramienta diseñada tootransfer datos entre bases de datos relacionales y un repositorio de grandes cantidades de datos, como almacén de Data Lake. Puede usarlo tooimport datos desde un sistema de administración de bases de datos relacionales (RDBMS) como base de datos de SQL Azure en el almacén de Data Lake. Puede transformar, a continuación y analizar los datos de hello con cargas de trabajo de grandes cantidades de datos y, a continuación, exportar datos de hello en un RDBMS. En este tutorial, utilizará una base de datos de SQL Azure como tooimport y exportación de la base de datos relacional de.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md)
* **Clúster de HDInsight de Azure** con acceso tooa cuenta de almacén de Data Lake. Consulte [Creación de un clúster de HDInsight con Data Lake Store mediante el Portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md). En este artículo se supone que tiene un clúster de HDInsight Linux con acceso a Almacén de Data Lake.
* **Base de datos de SQL Azure**. Para obtener instrucciones sobre cómo toocreate un, consulte [crear una base de datos de SQL Azure](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>¿Obtener información más rápidamente con vídeos?
[Vea este vídeo](https://mix.office.com/watch/1butcdjxmu114) acerca de cómo toocopy datos entre los Blobs de almacenamiento de Azure y almacén de Data Lake mediante DistCp.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Crear tablas de ejemplo Hola base de datos de SQL Azure
1. toostart, cree dos tablas de ejemplo Hola base de datos de SQL Azure. Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello base de datos de SQL Azure y, a continuación, ejecución Hola siguiendo las consultas.

    **Crear Tabla1**

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

    **Crear Tabla2**

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
2. En **Tabla1**, agregue algunos datos de ejemplo. Deje **Tabla2** vacía. Los datos de **Tabla1** se importarán a Almacén de Data Lake. Luego se importarán los datos de Almacén de Data Lake a **Tabla2**. Ejecute hello siguiente fragmento de código.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Sqoop de uso de un clúster de HDInsight con acceso tooData Lake almacén
Un clúster de HDInsight ya tiene paquetes de Sqoop Hola disponibles. Si ha configurado el almacén de hello HDInsight clúster toouse Data Lake como un almacenamiento adicional, puede utilizar Sqoop (sin los cambios de configuración) tooimport o exportar datos entre una base de datos relacional (en este ejemplo, la base de datos de SQL Azure) y un almacén de Data Lake cuenta.

1. Para este tutorial, se supone que ha creado un clúster de Linux, por lo que debe utilizar SSH tooconnect toohello clúster. Vea [clúster de HDInsight basados en Linux de conectar tooa](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Compruebe si tiene acceso a cuenta de almacén de Data Lake Hola de clúster de Hola. Ejecute hello siguiente comando desde el símbolo del sistema de hello SSH:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    Esto debería proporcionar una lista de archivos o carpetas en hello cuenta de almacén de Data Lake.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Importación de datos de Base de datos SQL de Azure a Almacén de Data Lake
1. Navegue directorio toohello donde Sqoop paquetes están disponibles. Normalmente, se encuentran en `/usr/hdp/<version>/sqoop/bin`.
2. Importar datos de Hola de **Table1** en hello cuenta de almacén de Data Lake. Usar la sintaxis de hello:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Tenga en cuenta que **sql-base de datos-server-name** marcador de posición representa el nombre de Hola de servidor hello donde se ejecuta la base de datos de SQL Azure Hola. **nombre de base de datos de SQL** marcador de posición representa el nombre de la base de datos real de Hola.

    Por ejemplo,


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Comprobar que Hola datos ha sido transferido toohello cuenta de almacén de Data Lake. Ejecute el siguiente comando de hello:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Debería ver Hola después de salida.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Cada **parte-m -*** archivo corresponde tooa fila en la tabla de origen de hello, **Table1**. Puede ver Hola contenido de parte de hello - m-* archivos tooverify.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Exportación de datos de Almacén de Data Lake a Base de datos SQL de Azure
1. Exportar datos de Hola de tabla vacía de almacén de Data Lake cuenta toohello, **Table2**, Hola base de datos de SQL Azure. Usar la sintaxis de hello.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Por ejemplo,


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Compruebe que Hola datos eran cargado toohello tabla de base de datos SQL. Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) o Visual Studio tooconnect toohello base de datos de SQL Azure y, a continuación, Hola ejecución después de consulta.

        SELECT * FROM TABLE2

    Esto debe tener Hola después de salida.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Consideraciones de rendimiento sobre el uso de Sqoop

Para su Sqoop de optimización del rendimiento de trabajos toocopy datos tooData Lake almacén, vea [documento de rendimiento de Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Otras referencias
* [Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData](data-lake-store-copy-data-azure-storage-blob.md)
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Uso de Análisis de Azure Data Lake con el Almacén de Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
