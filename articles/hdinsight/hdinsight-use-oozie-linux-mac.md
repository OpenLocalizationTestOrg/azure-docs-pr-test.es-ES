---
title: flujos de trabajo de aaaUse Oozie de Hadoop de HDInsight basados en Linux | Documentos de Microsoft
description: "Use Oozie de Hadoop en HDInsight basado en Linux. Obtenga información acerca de cómo toodefine un flujo de trabajo de Oozie y enviar un trabajo de Oozie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a>Usar Oozie con Hadoop toodefine y ejecutar un flujo de trabajo de HDInsight basados en Linux

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Obtenga información acerca de cómo toouse Oozie Apache con Hadoop en HDInsight. Oozie de Apache es un sistema de coordinación o flujo de trabajo que administra trabajos de Hadoop. Oozie se integra con la pila de Hadoop de Hola y admite Hola siguientes trabajos:

* Apache MapReduce
* Apache Pig
* Apache Hive
* Apache Sqoop

Oozie también puede ser trabajos tooschedule usado que el sistema tooa específico, como programas Java o secuencias de comandos de shell

> [!NOTE]
> Otra opción para definir los flujos de trabajo con HDInsight es Azure Data Factory. toolearn más información acerca de la factoría de datos de Azure, consulte [uso de Pig y Hive con factoría de datos][azure-data-factory-pig-hive].

> [!IMPORTANT]
> Oozie no está habilitado en HDInsight unido a un dominio.

## <a name="prerequisites"></a>Requisitos previos

* **Un clúster de HDInsight**: Consulte [Introducción a HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

  > [!IMPORTANT]
  > pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="example-workflow"></a>Flujo de trabajo de ejemplo

flujo de trabajo de Hello usado en este documento contiene dos acciones. Las acciones son definiciones de tareas, como la ejecución de Hive, Sqoop, MapReduce o cualquier otro proceso:

![Diagrama de flujo de trabajo][img-workflow-diagram]

1. Una acción de Hive ejecuta un script de HiveQL tooextract registros de hello **hivesampletable** incluido con HDInsight. Cada fila de datos describe una visita de un dispositivo móvil específico. formato de registro de Hello aparece toohello similar siguiente texto:

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    Hola usado en este documento de script de Hive recuentos de visitas total de Hola para cada plataforma (por ejemplo, Android o iPhone) y almacena los recuentos de hello tooa nueva tabla de Hive.

    Para más información sobre Hive, consulte [Uso de Hive con HDInsight][hdinsight-use-hive].

2. Una acción de Sqoop exporta contenido Hola de hello nueva tabla tooa tabla de Hive en una base de datos de SQL Azure. Para obtener más información sobre Sqoop, consulte [Uso de Hadoop Sqoop con HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Para versiones compatibles de Oozie en clústeres de HDInsight, vea [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight][hdinsight-versions].

## <a name="create-hello-working-directory"></a>Crear el directorio de trabajo de Hola

Oozie espera recursos necesarios para una toobe de trabajo almacenados en hello mismo directorio. Este ejemplo usa **wasb:///tutorials/useoozie**. Usar hello después toocreate de comando este directorio y el directorio de datos de Hola que contiene la nueva tabla de Hive Hola creado por este flujo de trabajo:

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> Hola `-p` parámetro hace que todos los directorios en hello toobe de ruta de acceso creado. Hola **datos** directorio es datos de uso toohold utilizados por hello **useooziewf.hql** secuencia de comandos.

Ejecutar Hola siguiente comando, lo que garantiza que Oozie puede suplantar la cuenta de usuario al ejecutar los trabajos de Hive y Sqoop. Reemplace **USERNAME** por su nombre de inicio de sesión:

```
sudo adduser USERNAME users
```

> [!NOTE]
> Puede omitir los errores de ese usuario Hola ya es miembro de hello `users` grupo.

## <a name="add-a-database-driver"></a>Adición de un controlador de base de datos

Dado que este flujo de trabajo usa Sqoop tooexport datos tooSQL base de datos, debe proporcionar que una copia del controlador JDBC de hello usa tootalk tooSQL base de datos. Use Hola siguientes comando toocopy lo toohello directorio de trabajo:

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

Si el flujo de trabajo utiliza otros recursos, como un archivo jar que contiene una aplicación de MapReduce, necesitaría tooadd también estos recursos.

## <a name="define-hello-hive-query"></a>Definir la consulta de Hive Hola

Usar hello siguiendo los pasos toocreate un script de HiveQL que define una consulta, que se usa en un flujo de trabajo de Oozie más adelante en este documento.

1. Conecte el clúster toohello mediante SSH. Hola comando siguiente es un ejemplo del uso de hello `ssh` comando. Reemplace __nombre de usuario__ con el usuario SSH de hello para el clúster de Hola. Reemplace __CLUSTERNAME__ con el nombre de Hola Hola del clúster de HDInsight.

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Desde Hola conexión SSH, use Hola después toocreate un archivo de comandos:

    ```
    nano useooziewf.hql
    ```

3. Una vez que abre el editor de nano hello, utilice Hola después de consulta como contenido de Hola de archivo hello:

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    Hay dos variables utilizadas en el script de Hola:

    * **${hiveTableName}**: contiene nombre Hola de hello tabla toobe creado

    * **${hiveDataFolder}**: contiene archivos de datos de hello ubicación toostore hello para la tabla de Hola

    archivo de definición de flujo de trabajo de Hello (workflow.xml en este tutorial) pasa estos valores toothis script de HiveQL en tiempo de ejecución

4. editor de hello tooexit, presione Ctrl-X. Cuando se le pida, seleccione **Y** toosave Hola archivo y luego use **ENTRAR** toouse hello **useooziewf.hql** nombre de archivo.

5. Siguiente de hello use comandos toocopy **useooziewf.hql** demasiado**wasb:///tutorials/useoozie/useooziewf.hql**:

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    Estos comandos almacenan hello **useooziewf.hql** archivo en almacenamiento de hello HDFS compatible para clúster Hola.

## <a name="define-hello-workflow"></a>Definir el flujo de trabajo de Hola

Las definiciones de los flujos de trabajo de Oozie se escriben en hPDL (un lenguaje de definición de procesos XML). Usar hello siguiendo el flujo de trabajo de pasos toodefine hello:

1. Usar hello después de la instrucción toocreate y editar un archivo nuevo:

    ```
    nano workflow.xml
    ```

2. Una vez que abre el editor de nano hello, escriba Hola continuación de XML como contenido del archivo hello:

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    Hay dos acciones definidas en el flujo de trabajo de hello:

   * **RunHiveScript**: esta acción es la acción de inicio de Hola y se ejecuta hello **useooziewf.hql** de script de Hive

   * **RunSqoopExport**: esta acción exporta datos de hello creados a partir de hello Hive script tooSQL con Sqoop de la base de datos. Esta acción solo se ejecuta si hello **RunHiveScript** acción es correcta.

     flujo de trabajo de Hello tiene varias entradas, como `${jobTracker}`. Estas entradas se reemplazan por valores que se usa en la definición del trabajo Hola. se crea la definición del trabajo Hello más adelante en este documento.

     Hola de nota también `<archive>sqljdbc4.jar</arcive>` entrada Hola Sqoop sección. Esta entrada indica Oozie toomake este archivo disponible para Sqoop cuando se ejecuta la acción.

3. Utilice Ctrl-X, a continuación, **Y** y **ENTRAR** archivo de hello toosave.

4. Siguiente Hola de uso del comando hello toocopy **workflow.xml** archivo demasiado**/tutorials/useoozie/workflow.xml**:

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a>Crear base de datos de Hola

toocreate una base de datos de SQL Azure, siga los pasos de Hola Hola [crear una base de datos de SQL](../sql-database/sql-database-get-started.md) documento. Al crear la base de datos de hello, use `oozietest` como nombre de la base de datos de Hola. También tome nota del nombre de hello del servidor de base de datos de Hola.

### <a name="create-hello-table"></a>Crear tabla de Hola

> [!NOTE]
> Hay muchas maneras tooconnect tooSQL base de datos toocreate una tabla. Hola a consecuencia del uso de pasos [uso](http://www.freetds.org/) de clúster de HDInsight Hola.


1. Usar hello siguiendo el uso del comando tooinstall en clúster de HDInsight de hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. Una vez que se ha instalado el uso, utilice Hola después el servidor de base de datos SQL de comandos tooconnect toohello que creó anteriormente:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    Recibir toohello similar de salida siguiente texto:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. En hello `1>` símbolo del sistema, escriba Hola siguientes líneas:

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    Cuando Hola `GO` instrucción se haya especificado, se evalúan en las instrucciones anteriores Hola. Estas instrucciones crean una tabla denominada **mobiledata** utilizado por el flujo de trabajo de Hola.

    Hola de uso después de tooverify que Hola tabla se ha creado:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Vea toohello similar de salida siguiente texto:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. Escriba `exit` en hello `1>` solicitar utilidad de tooexit Hola tsql.

## <a name="create-hello-job-definition"></a>Crear definición de trabajo de Hola

definición del trabajo Hola describe dónde toofind Hola workflow.xml. También se describe dónde toofind otros archivos usados por el flujo de trabajo de hello (por ejemplo, useooziewf.hql.) También define los valores de hello para propiedades utilizan en el flujo de trabajo de Hola y los archivos asociados.

1. Usar hello sigue dirección completa Hola del comando tooget de almacenamiento predeterminado de Hola. Esta dirección se utiliza en el archivo de configuración de hello en unos momentos:

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    Este comando devuelve información toohello similar continuación de XML:

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > Si el clúster de HDInsight de hello usa el almacenamiento de Azure como almacenamiento predeterminado de hello, Hola `<value>` contenido del elemento comienzan por `wasb://`. Si se usa Azure Data Lake Store en su lugar, comenzará por `adl://`.

    Guardar el contenido de Hola de hello `<value>` elemento, tal y como se utiliza en los pasos siguientes de Hola.

2. Usar hello después comando tooget FQDN del nodo principal del clúster de Hola. Esta información se usa para hello JobTracker dirección de clúster de hello:

    ```
    hostname -f
    ```

    Esto devuelve información toohello similar siguiente texto:

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    Hello puerto usado para hello JobTracker es 8050, por lo que es Hola dirección completa toouse para hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.

3. Usar hello siguiente configuración de definición de trabajo de toocreate Hola Oozie:

    ```
    nano job.xml
    ```

4. Una vez que abre el editor de nano hello, utilice Hola continuación de XML como contenido de Hola de archivo hello:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * Reemplace todas las instancias de  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  con valor Hola recibidos con anterioridad para el almacenamiento de forma predeterminada.

     > [!WARNING]
     > Si la ruta de acceso de hello es un `wasb` ruta de acceso, debe usar la ruta de acceso completa de Hola. No acortar toojust `wasb:///`.

   * Reemplace **JOBTRACKERADDRESS** con hello dirección JobTracker/ResourceManager recibidos con anterioridad.
   * Reemplace **YourName** por el nombre de inicio de sesión por clúster de HDInsight Hola.
   * Reemplace **serverName**, **adminLogin**, y **adminPassword** con información de hello para la base de datos de SQL Azure.

     La mayoría de hello información de este archivo es valores de hello toopopulate usado utilizados en hello workflow.xml o ooziewf.hql archivos (por ejemplo, ${nameNode}.)

     > [!NOTE]
     > Hola **oozie.wf.application.path** entrada define dónde se ejecutó el archivo de toofind Hola workflow.xml, que contiene el flujo de trabajo de Hola este trabajo.

5. Utilice Ctrl-X, a continuación, **Y** y **ENTRAR** archivo de hello toosave.

## <a name="submit-and-manage-hello-job"></a>Enviar y administrar el trabajo de Hola

Hello pasos siguientes utilice hello Oozie comando toosubmit y administración flujos de trabajo de Oozie en clúster de Hola. Hola Oozie comando es una interfaz sencilla sobre hello [API de REST de Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

> [!IMPORTANT]
> Al usar comandos de hello Oozie, debe usar Hola FQDN para el nodo principal de HDInsight de Hola. Este FQDN solo es accesible desde el clúster de hello, o si hello clúster se encuentra en una red Virtual de Azure, desde otras máquinas en hello misma red.


1. Usar hello después tooobtain Hola URL toohello Oozie servicio:

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    Esto devuelve información toohello similar continuación de XML:

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    Hola `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` parte es hello toouse de dirección URL con hello Oozie comando.

2. Hola uso siga toocreate una variable de entorno para la dirección URL de hello, por lo que no tiene tootype para cada comando:

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    Sustituir la URL de hello con hello recibió anteriormente.
3. Usar hello siguiendo el trabajo de Hola toosubmit:

    ```
    oozie job -config job.xml -submit
    ```

    Este comando carga la información de trabajo de Hola de **job.xml** y lo envía tooOozie, pero no se ejecuta.

    Cuando se completa el comando hello, debe devolver Hola identificador de trabajo de Hola. Por ejemplo: `0000005-150622124850154-oozie-oozi-W`. Este identificador es trabajo de hello toomanage usado.

4. Ver el estado de Hola de trabajo de hello mediante Hola siguiente comando:

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > Reemplace `<JOBID>` con hello identificador devuelto en el paso anterior de Hola.

    Esto devuelve información toohello similar siguiente texto:

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    Este trabajo tiene un estado de `PREP`. Este estado indica que el trabajo de Hola se ha creado, pero no inicia.

5. Usar hello siguiendo el trabajo de hello toostart de comando:

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > Reemplace `<JOBID>` con hello identificador devuelto anteriormente.

    Si se comprueba el estado de hello después este comando, se encuentra en un estado de ejecución y se devuelve información sobre las acciones de hello en el trabajo de Hola.

6. Una vez completada correctamente la tarea hello, puede comprobar que datos de Hola se generaron y exportan toohello tabla de base de datos SQL mediante Hola siguientes comandos:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    En hello `1>` símbolo del sistema, escriba Hola después de consulta:

    ```
    SELECT * FROM mobiledata
    GO
    ```

    información de Hello devuelta es similar toohello siguiente texto:

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

Para obtener más información sobre hello Oozie comando, consulte [herramienta de línea de comandos de Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).

## <a name="oozie-rest-api"></a>API de REST de Oozie

Hola API de REST de Oozie permite toobuild sus propias herramientas que funcionan con Oozie. siguiente Hola es HDInsight información específica acerca del uso de hello Oozie API de REST:

* **URI**: Hola API de REST puede tener acceso desde el clúster fuera de hello en`https://CLUSTERNAME.azurehdinsight.net/oozie`

* **Autenticación**: autenticar API toohello con cuenta de clúster HTTP hello (Administrador) y la contraseña. Por ejemplo:

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

Para obtener más información sobre el uso de API de REST de Oozie hello, consulte [API de servicios Web de Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).

## <a name="oozie-web-ui"></a>Interfaz de usuario web de Oozie

Hola Oozie interfaz de usuario Web proporciona una vista basada en web en el estado de los trabajos de Oozie hello en clúster de Hola. interfaz de usuario web de Hello permite hello tooview siguiente información:

* Estado del trabajo
* Definición del trabajo
* Configuración
* Un gráfico de acciones de hello en el trabajo de Hola
* Registros del trabajo de Hola

También puede ver detalles de las acciones dentro de un trabajo.

tooaccess Hola de interfaz de usuario de Web de Oozie, usar hello pasos:

1. Crear un clúster de HDInsight de toohello de túnel SSH. Para obtener información, vea hello [uso SSH túnel con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

2. Una vez que se ha creado un túnel, abra interfaz de usuario de web de Ambari hello en el explorador web. Hola URI para el sitio de hello Ambari es **https://CLUSTERNAME.azurehdinsight.net**. Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight basados en Linux.

3. Desde la parte izquierda de la página de Hola de hello, seleccione **Oozie**, a continuación, **vínculos rápidos**y, finalmente, **Oozie interfaz de usuario Web**.

    ![imagen de los menús de Hola](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. Hola toodisplaying de los valores predeterminados de interfaz de usuario de Web de Oozie trabajos de flujo de trabajo en ejecución. toosee todos los trabajos de flujo de trabajo, seleccione **todos los trabajos**.

    ![Todos los trabajos mostrados](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. Seleccione un trabajo tooview obtener más información sobre el trabajo de Hola.

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. Desde la ficha de información del trabajo de hello, puede ver información sobre el trabajo básico y las acciones individuales de hello en el trabajo de Hola. Con pestañas de Hola princip Hola. puede ver Hola definición de trabajo configuración del trabajo, Hola acceso registro de trabajo o ver un dirigen acíclico gráfico (DAG) de trabajo de Hola.

   * **Registro de trabajo**: Hola seleccione **GetLogs** botón tooget todos los registros de trabajo de Hola o usar hello **escriba el filtro de búsqueda** campo toofilter registros

       ![Registro de trabajo](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * **JobDAG**: Hola DAG es una visión general gráfica de rutas de acceso de datos de hello realizada a través del flujo de trabajo de Hola

       ![DAG del trabajo](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. Seleccionar una de las acciones de Hola de hello **información del trabajo** ficha muestra información para la acción de Hola. Por ejemplo, seleccione hello **RunHiveScript** acción.

    ![Información de acción](./media/hdinsight-use-oozie-linux-mac/action.png)

8. Puede ver detalles de la acción de hello, como un vínculo toohello **dirección URL de consola**. Este vínculo puede ser información de JobTracker tooview usado para el trabajo de Hola.

## <a name="scheduling-jobs"></a>Programación de trabajos

Coordinador de Hello permite toospecify una frecuencia de inicio y finalización, repetición de trabajos. toodefine una programación de flujo de trabajo de hello, Hola uso pasos:

1. Hola de uso después de un archivo denominado toocreate **coordinator.xml**:

    ```
    nano coordinator.xml
    ```

    Usar hello continuación de XML como contenido de Hola de archivo hello:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > Hola `${...}` variables se reemplazan por valores en la definición del trabajo hello en tiempo de ejecución. Hola variables son:
    >
    > * `${coordFrequency}`: El tiempo entre las instancias del trabajo de hello en ejecución.
    > ** `${coordStart}`: hora de inicio del trabajo de Hola.
    > * `${coordEnd}`: hora de finalización del trabajo de Hola.
    > * `${coordTimezone}`: los trabajos del coordinador se encuentran en una zona horaria fija sin horario de verano (representado normalmente mediante UTC). Esta zona horaria se conoce como Hola "Oozie procesamiento timezone."
    > * `${wfPath}`: Hola workflow.xml toohello de ruta de acceso.

2. Hola toosave de archivos, use Ctrl-X **Y**, y **ENTRAR**.

3. Usar hello siguiendo el directorio de trabajo de toohello archivo Hola de toocopy comando para este trabajo:

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. Hola de uso después de hello toomodify **job.xml** archivo:

    ```
    nano job.xml
    ```

    Asegúrese de hello siguientes cambios:

   * archivo tooinstruct oozie toorun hello coordinador en lugar de flujo de trabajo de hello, cambio `<name>oozie.wf.application.path</name>` demasiado`<name>oozie.coord.application.path</name>`.

   * Hola tooset `workflowPath` variable utilizada por el Coordinador de hello, agregar Hola continuación de XML:

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       Reemplace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` texto con el valor de hello utilizado en otras entradas de archivo de hello job.xml.

   * inicio de hello toodefine, final y frecuencia de coordinador de hello, agreguen Hola continuación de XML:

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       Estos valores establecen too12 de tiempo de inicio de hello: 00 P.M. del 10 de mayo de 2017 Hola final tiempo tooMay 12, de 2017. intervalo de saludo para ejecutar este trabajo diariamente. frecuencia de Hola se expresa en minutos, por lo que 24 horas a 60 minutos = 1440 minutos. Por último, zona horaria de Hola se establece tooUTC.

5. Utilice Ctrl-X, a continuación, **Y** y **ENTRAR** archivo de hello toosave.

6. trabajo de hello toorun, Hola de uso siguiente comando:

    ```
    oozie job -config job.xml -run
    ```

    Este comando se envía e inicia el trabajo de Hola.

7. Si visite hello Oozie interfaz de usuario Web y seleccione hello **trabajos de coordinador** pestaña, verá información toohello similar después de imagen:

    ![pestaña de trabajos de coordinador](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    Hola **materialización siguiente** entrada contiene Hola próxima vez que Hola ejecuciones de los trabajos.

8. Toohello similar anterior del flujo de trabajo, selección de entrada del trabajo hello en la interfaz de usuario web de hello muestra información sobre el trabajo de hello:

    ![información de trabajos de coordinador](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > Esta imagen muestra solo correcta ejecuciones del trabajo de hello, acciones no individuales de flujo de trabajo de hello programado. toosee que seleccione uno de hello **acción** entradas.

    ![Información de acción](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a>Solución de problemas

Hola Oozie UI permite tooview Oozie registros. También contiene registros de tooJobTracker vínculos para tareas de MapReduce iniciadas por el flujo de trabajo de Hola. patrón de Hola para solucionar el problema debe ser:

1. Ver el trabajo de hello en la interfaz de usuario de Oozie Web.

2. Si hay un error o un error de una acción específica, seleccione Hola toosee acción si hello **mensaje de Error** campo proporciona más información sobre el error de Hola.

3. Si está disponible, utilice URL Hola de hello acción tooview más detalles (por ejemplo, registros de JobTracker) para la acción de Hola.

Hello siguientes son errores específicos que pueden producirse, y cómo tooresolve ellos.

### <a name="ja009-cannot-initialize-cluster"></a>JA009: No se puede inicializar el clúster

**Síntomas**: Hola cambios de estado del trabajo demasiado**SUSPENDED**. Detalles de trabajo de hello Mostrar estado de RunHiveScript de hello como **START_MANUAL**. Selecciona la acción de hello muestra hello mensaje de error siguiente:

    JA009: Cannot initialize Cluster. Please check your configuration for map

**Causa**: Hola direcciones WASB que se usan en hello **job.xml** archivos no contienen el contenedor de almacenamiento de Hola o nombre de la cuenta de almacenamiento. formato de dirección de Hello WASB debe ser `wasb://containername@storageaccountname.blob.core.windows.net`.

**Resolución**: cambiar hello WASB direcciones usadas Hola trabajo.

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a>JA002: Oozie no se permite tooimpersonate &lt;usuario >

**Síntomas**: Hola cambios de estado del trabajo demasiado**SUSPENDED**. Detalles de trabajo de hello Mostrar estado de RunHiveScript de hello como **START_MANUAL**. Selecciona la acción de hello muestra hello mensaje de error siguiente:

    JA002: User: oozie is not allowed tooimpersonate <USER>

**Causa**: configuración de permiso actual no permite Oozie hello tooimpersonate cuenta de usuario especificada.

**Resolución**: Oozie se permite a los usuarios de tooimpersonate en hello **usuarios** grupo. Hola de uso `groups USERNAME` grupos de hello toosee que Hola cuenta de usuario es miembro de. Si el usuario de hello no es un miembro del programa Hola a **usuarios** grupo, use Hola después del grupo de comandos tooadd Hola usuario toohello:

    sudo adduser USERNAME users

> [!NOTE]
> Puede tardar varios minutos antes de HDInsight reconoce que el usuario Hola se ha agregado el grupo toohello.

### <a name="launcher-error-sqoop"></a>ERROR del selector (Sqoop)

**Síntomas**: Hola cambios de estado del trabajo demasiado**KILLED**. Detalles de trabajo de hello Mostrar estado de RunSqoopExport de hello como **ERROR**. Selecciona la acción de hello muestra hello mensaje de error siguiente:

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

**Causa**: Sqoop es tooload no se puede Hola controlador necesario tooaccess Hola de base.

**Resolución**: al utilizar Sqoop desde un trabajo de Oozie, debe incluir controladores de base de datos de hello con hello otros recursos (por ejemplo, hello workflow.xml) utilizados por el trabajo de Hola. Hacer referencia a archivo Hola que contiene el controlador de la base de datos de Hola de hello `<sqoop>...</sqoop>` sección de hello workflow.xml.

Por ejemplo, para el trabajo de hello en este documento, usaría Hola pasos:

1. Copie el directorio /tutorials/useoozie toohello de hello sqljdbc4.1.jar archivos:

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. Modificar el siguiente XML en una nueva línea anterior de Hola workflow.xml tooadd Hola `</sqoop>`:

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, se habrá aprendido cómo toodefine un flujo de trabajo de Oozie y cómo toorun un trabajo de Oozie. toolearn más acerca de cómo trabajar con HDInsight, vea Hola siguientes artículos:

* [Uso del coordinador de Oozie de tiempo con HDInsight][hdinsight-oozie-coordinator-time]
* [Carga de datos para trabajos de Hadoop en HDInsight][hdinsight-upload-data]
* [Uso de Sqoop con Hadoop en HDInsight][hdinsight-use-sqoop]
* [Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]
* [Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]
* [Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
