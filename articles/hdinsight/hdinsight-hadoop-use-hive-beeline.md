---
title: aaaUse Beeline con Apache Hive - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo las consultas toouse hello Beeline cliente toorun Hive con Hadoop en HDInsight. Beeline es una utilidad para trabajar con HiveServer2 sobre JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive,hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Usar el cliente de hello Beeline con Apache Hive

Obtenga información acerca de cómo toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) consultas toorun Hive en HDInsight.

BEELINE es un cliente de Hive que está incluido en los nodos principales del saludo de su clúster de HDInsight. BEELINE usa JDBC tooconnect tooHiveServer2, un servicio hospedado en el clúster de HDInsight. También puede utilizar Beeline tooaccess Hive en HDInsight de forma remota en Hola internet. Hello en la tabla siguiente proporciona las cadenas de conexión para su uso con Beeline:

| Desde dónde se ejecuta Beeline | parameters |
| --- | --- | --- |
| Un nodo de nodo principal o de borde del tooa de conexión de SSH | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Clúster de hello exterior | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Reemplace `admin` con la cuenta de inicio de sesión de clúster de hello para el clúster.
>
> Reemplace `password` con contraseña de Hola de cuenta de inicio de sesión de clúster de Hola.
>
> Reemplace `clustername` con el nombre de Hola de su clúster de HDInsight.

## <a id="prereq"></a>Requisitos previos

* Un clúster de Hadoop basado en Linux en HDInsight.

  > [!IMPORTANT]
  > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un cliente de SSH o un cliente de Beeline local. La mayoría de los pasos de hello en este documento se supone que está usando Beeline desde un clúster de toohello de sesión SSH. Para obtener información acerca de cómo ejecutar Beeline de clúster fuera de hello, vea hello [usar de forma remota Beeline](#remote) sección.

    Para obtener más información sobre cómo usar SSH, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Uso de BeeLine

1. Cuando Beeline se inicia, hay que proporcionar una cadena de conexión de HiveServer2 en el clúster de HDInsight. comando de hello toorun de clúster fuera de hello, debe proporcionar un nombre de cuenta de inicio de sesión de clúster de hello (valor predeterminado `admin`) y la contraseña. Usar hello después de la tabla toofind Hola conexión cadena formato y los parámetros toouse:

    | Desde dónde se ejecuta Beeline | parameters |
    | --- | --- | --- |
    | Un nodo de nodo principal o de borde del tooa de conexión de SSH | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Clúster de hello exterior | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Por ejemplo, hello siguiente comando puede ser usado toostart Beeline desde un clúster de toohello de sesión SSH:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Este comando inicia a hello Beeline cliente y conecta tooHiveServer2 en el nodo principal del clúster Hola. Cuando se completa el comando hello, llega a un `jdbc:hive2://headnodehost:10001/>` símbolo del sistema.

2. Los comandos de Beeline empiezan con un carácter `!`. Por ejemplo `!help` muestra la ayuda. Sin embargo Hola `!` puede omitirse en algunos comandos. Por ejemplo, `help` también funciona.

    Hay un `!sql`, que es usado tooexecute instrucciones de HiveQL. Sin embargo, HiveQL es lo más frecuente que puede omitir Hola anterior `!sql`. Hola siguiendo dos instrucciones es equivalente:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    En un nuevo clúster, solo debe aparecer una tabla: **hivesampletable**.

3. Usar hello después de esquema comando toodisplay Hola Hola hivesampletable:

    ```hiveql
    describe hivesampletable;
    ```

    Este comando devuelve Hola siguiente información:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Esta información describe las columnas de hello en la tabla de Hola. Mientras se pueden llevar a cabo algunas consultas con estos datos, vamos a en su lugar, crear una nueva toodemonstrate tabla cómo datos tooload en Hive y aplicar un esquema.

4. Escriba Hola siguiendo las instrucciones toocreate una tabla denominada **log4jLogs** mediante el uso de datos de ejemplo proporcionados con clúster de HDInsight de hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Estas instrucciones realizan Hola siguientes acciones:

    * `DROP TABLE`-Si existe en la tabla de hello, se elimina.

    * `CREATE EXTERNAL TABLE`: crea una tabla **externa** en Hive. Tablas externas solo almacenan definición de la tabla de hello en el subárbol. Hola datos permanecen en la ubicación original de Hola.

    * `ROW FORMAT`-Cómo se da formato a los datos de Hola. En este caso, los campos de hello en cada registro están separados por un espacio.

    * `STORED AS TEXTFILE LOCATION`-Donde se almacenan los datos de Hola y en qué formato de archivo.

    * `SELECT`-Selecciona un recuento de todas las filas donde columna **t4** contiene el valor de hello **[ERROR]**. Esta consulta devuelve un valor de **3** ya que hay tres filas que contienen este valor.

    * `INPUT__FILE__NAME LIKE '%.log'`-Subárbol intenta tooapply Hola esquema tooall archivos hello del directorio. En este caso, el directorio de hello contiene archivos que no coinciden con el esquema de Hola. tooprevent los datos de elementos no utilizados en los resultados de hello, esta instrucción indica Hive que solo debemos devolver datos de archivos que finalizan con. registro.

  > [!NOTE]
  > Tablas externas deben utilizarse cuando se espera Hola subyacente datos toobe actualizado a través de un origen externo. Por ejemplo, un proceso de carga de datos automatizado o una operación de MapReduce.
  >
  > Quitar una tabla externa **no** eliminar datos de hello, solo la definición de tabla Hola.

    Hola de salida de este comando es similar toohello siguiente texto:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. usar tooexit Beeline, `!exit`.

## <a id="file"></a>Usar Beeline toorun un archivo de HiveQL

Usar hello siguiendo los pasos toocreate un archivo, a continuación, ejecutarlo mediante Beeline.

1. Comando de uso Hola siguiente toocreate un archivo denominado **query.hql**:

    ```bash
    nano query.hql
    ```

2. Usar hello después de texto como contenido de Hola de archivo hello. Esta consulta crea una nueva tabla "interna" denominada **errorLogs**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Estas instrucciones realizan Hola siguientes acciones:

    * **Crear tabla IF NOT EXISTS** -si aún no existe la tabla de hello, se crea. Desde hello **externo** no se utiliza la palabra clave, esta instrucción crea una tabla interna. Las tablas internas se almacenan en el almacén de datos de Hive de Hola y se administran completamente por el subárbol.
    * **ALMACENA AS ORC** -almacena los datos de hello en formato optimizado fila columnas (ORC). ORC es un formato altamente optimizado y eficiente para almacenar datos de Hive.
    * **INSERT OVERWRITE ... Seleccione** -selecciona las filas de hello **log4jLogs** tabla que contenga **[ERROR]**, a continuación, inserta Hola datos en hello **registros de errores de** tabla.

    > [!NOTE]
    > A diferencia de las tablas externas, al quitar una tabla interna, eliminan datos subyacente de saludo.

3. archivo de hello toosave, use **Ctrl**+**_X**, a continuación, escriba **Y**y, finalmente, **ENTRAR**.

4. Usar hello toorun Hola archivo mediante Beeline siguiente:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Hola `-i` parámetro Beeline inicia, se ejecuta Hola instrucciones en el archivo de hello query.hql. Cuando se completa la consulta de hello, llegan hello `jdbc:hive2://headnodehost:10001/>` símbolo del sistema. También puede ejecutar un archivo mediante hello `-f` parámetro, que Beeline se cierra después de completarse Hola consulta.

5. tooverify que Hola **registros de errores de** se creó la tabla, use Hola después tooreturn instrucción todos Hola filas de **registros de errores de**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Se deben devolver tres filas de datos y todas ellas deben contener **[ERROR]** en la columna t4.

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Usar Beeline de forma remota

Si tiene Beeline instalado localmente, o esté utilizándolo a través de una imagen de Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), debe usar Hola parámetros siguientes:

* __Cadena de conexión__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Nombre de inicio de sesión del clúster__: `-n admin`

* __Contraseña de inicio de sesión del clúster__`-p 'password'`

Reemplace hello `clustername` en cadena de conexión de hello con nombre Hola de su clúster de HDInsight.

Reemplace `admin` con el nombre de Hola de su inicio de sesión de clúster y `password` con la contraseña de hello para el inicio de sesión de clúster.

## <a id="sparksql"></a>Uso de Beeline con Spark

Spark proporciona su propia implementación de HiveServer2, que a menudo es servidor Thrift de Spark de usan tooas Hola. Este servicio utiliza las consultas de tooresolve Spark SQL en lugar de Hive y puede proporcionar un mejor rendimiento en función de la consulta.

servidor de tooconnect toohello Thrift de Spark de un Spark en clúster de HDInsight, uso del puerto `10002` en lugar de `10001`. Por ejemplo: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> servidor Thrift de Spark de Hello es no directamente accesible over Hola internet. Solo puede conectarse tooit desde una sesión de SSH o dentro de Hola misma red Virtual de Azure como Hola clúster de HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Pasos siguientes

Para obtener información general de Hive en HDInsight, vea Hola siguiente documento:

* [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md)

Para obtener más información sobre otras maneras de trabajar con Hadoop en HDInsight, vea Hola siguientes documentos:

* [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md)

Si usas Tez con Hive, vea Hola siguientes documentos:

* [Usar hello Tez UI en HDInsight basados en Windows](hdinsight-debug-tez-ui.md)
* [Usar hello vista Ambari Tez en HDInsight basados en Linux](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
