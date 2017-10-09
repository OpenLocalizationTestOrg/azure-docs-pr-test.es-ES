---
title: Coordinador basado en tiempo de Hadoop Oozie de aaaUse en HDInsight | Documentos de Microsoft
description: "Uso del coordinador de Oozie de Hadoop basado en tiempo en HDInsight, un servicio de big data. Obtenga información acerca de cómo toodefine Oozie flujos de trabajo y coordinadores de y enviar trabajos."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Usar coordinador basado en tiempo de Oozie con Hadoop en flujos de trabajo de HDInsight toodefine y coordinar los trabajos
En este artículo, aprenderá cómo toodefine flujos de trabajo y los coordinadores, y cómo tootrigger Hola trabajos de coordinador, según el tiempo. Resulta útil toogo a través de [Oozie de uso con HDInsight] [ hdinsight-use-oozie] antes de leer este artículo. Además tooOozie, también puede programar trabajos mediante Data Factory de Azure. toolearn Data Factory de Azure, consulte [uso de Pig y Hive con factoría de datos](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> En este artículo se requiere un clúster de HDInsight basado en Windows. Para obtener información sobre el uso de Oozie, incluidas las tareas basadas en tiempo, en un clúster basado en Linux, consulte [Oozie de uso con Hadoop toodefine y ejecutar un flujo de trabajo de HDInsight basados en Linux](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>¿Qué es Oozie?
Oozie de Apache es un sistema de coordinación o flujo de trabajo que administra trabajos de Hadoop. Se integra con la pila de Hadoop de Hola y admite trabajos de Hadoop MapReduce Apache, Pig Apache, Apache Hive y Sqoop de Apache. También puede ser tooschedule usado trabajos que el sistema tooa específico, como programas Java o secuencias de comandos de shell.

Hello siguiente imagen muestra flujo de trabajo de hello que implementará:

![Diagrama de flujo de trabajo][img-workflow-diagram]

flujo de trabajo de Hello contiene dos acciones:

1. Una acción de subárbol ejecuta un hello toocount de script de HiveQL apariciones de cada tipo de nivel de registro en un archivo de registro log4j. Cada registro log4j consta de una línea de campos que contenga una [nivel de registro] campo tooshow Hola hello y tipo de gravedad, por ejemplo:

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    es similar a la salida del script de Hive Hola:

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    Para más información sobre Hive, consulte [Uso de Hive con HDInsight][hdinsight-use-hive].
2. Una acción de Sqoop exporta hello HiveQL acción salida tooa tabla en una base de datos de SQL Azure. Para obtener más información sobre Sqoop, consulte [Uso de Sqoop con HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Para versiones compatibles de Oozie en clústeres de HDInsight, vea [cuáles son las novedades en las versiones de clúster Hola proporcionadas por HDInsight?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una estación de trabajo con Azure PowerShell**.

    > [!IMPORTANT]
    > La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y desaparecerá por completo el 1 de enero de 2017. Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.
    >
    > Siga los pasos de hello en [instalar y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs) versión más reciente de hello tooinstall de PowerShell de Azure. Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.

* **Un clúster de HDInsight**. Para obtener más información sobre cómo crear un clúster de HDInsight, consulte [Creación de clústeres de Hadoop basados en Windows en HDInsight][hdinsight-provision] o [Tutorial de Hadoop: Introducción al uso de Hadoop en HDInsight basado en Linux][hdinsight-get-started]. Necesitará Hola después toogo datos tutorial Hola:

    <table border = "1">
    <tr><th>Propiedad del clúster</th><th>Nombre de variable de Windows PowerShell</th><th>Valor</th><th>Description</th></tr>
    <tr><td>Nombre del clúster de HDInsight</td><td>$clusterName</td><td></td><td>clúster de HDInsight de Hello en el que se ejecutará este tutorial.</td></tr>
    <tr><td>Nombre de usuario del clúster de HDInsight</td><td>$clusterUsername</td><td></td><td>nombre de usuario de clúster de HDInsight Hola. </td></tr>
    <tr><td>Contraseña del usuario del clúster de HDInsight </td><td>$clusterPassword</td><td></td><td>contraseña de usuario de clúster de HDInsight Hola.</td></tr>
    <tr><td>Nombre de la cuenta de almacenamiento de Azure</td><td>$storageAccountName</td><td></td><td>Un clúster de HDInsight toohello disponibles de cuenta de almacenamiento de Azure. Para este tutorial, utilice cuenta de almacenamiento predeterminada de Hola que haya especificado durante el proceso de aprovisionamiento de clúster de Hola.</td></tr>
    <tr><td>Nombre del contenedor de blobs de Azure</td><td>$containerName</td><td></td><td>En este ejemplo, utilice el contenedor de almacenamiento de blobs de Azure de Hola que se usa para el sistema de archivos de clúster de HDInsight de hello predeterminado. De manera predeterminada, tiene Hola mismo nombre como clúster de HDInsight Hola.</td></tr>
    </table>
* **Una base de datos SQL de Azure**. Debe configurar una regla de firewall para hello tooallow acceso de base de datos de SQL server desde la estación de trabajo. Para obtener instrucciones sobre cómo crear una base de datos de SQL Azure y cómo configurar firewall de hello, consulte [empezar a usar la base de datos de SQL Azure] [sqldatabase get-iniciado]. En este artículo se proporciona un script de Windows PowerShell para crear la tabla de base de datos de SQL Azure Hola que necesite para este tutorial.

    <table border = "1">
    <tr><th>Propiedad de la base de datos SQL</th><th>Nombre de variable de Windows PowerShell</th><th>Valor</th><th>Description</th></tr>
    <tr><td>Nombre del servidor de base de datos SQL</td><td>$sqlDatabaseServer</td><td></td><td>toowhich de servidor de base de datos SQL de Hello Sqoop exportará los datos. </td></tr>
    <tr><td>Nombre de inicio de sesión de la base de datos SQL</td><td>$sqlDatabaseLogin</td><td></td><td>Nombre de inicio de sesión de la base de datos SQL.</td></tr>
    <tr><td>Contraseña de inicio de sesión de la base de datos SQL</td><td>$sqlDatabaseLoginPassword</td><td></td><td>Contraseña de inicio de sesión de la base de datos SQL.</td></tr>
    <tr><td>Nombre de la base de datos SQL</td><td>$sqlDatabaseName</td><td></td><td>toowhich de base de datos de SQL Azure Hello Sqoop exportará los datos. </td></tr>
    </table>

  > [!NOTE]
  > De forma predeterminada, una base de datos SQL de Azure permite realizar conexiones desde servicios de Azure, como HDInsight de Azure. Si se deshabilita esta configuración de firewall, debe habilitarla de hello Portal de Azure. Para obtener instrucciones sobre la creación de una base de datos SQL y la configuración de las reglas de firewall, consulte [Creación y configuración de una base de datos SQL][sqldatabase-get-started].

> [!NOTE]
> Valores de hello de rellenar en las tablas de Hola. Le resultará útil para completar el tutorial.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Definir el flujo de trabajo de Oozie y Hola relacionados con script de HiveQL
Las definiciones de los flujos de trabajo de Oozie se escriben en hPDL (un lenguaje de definición de procesos XML). es el nombre de archivo de flujo de trabajo predeterminado de Hello *workflow.xml*.  Se guardar archivo de flujo de trabajo de hello localmente y, a continuación, implementarlo clúster de HDInsight toohello mediante Azure PowerShell más adelante en este tutorial.

acción de Hive en el flujo de trabajo de Hola Hola llama a un archivo de script de HiveQL. El archivo de script contiene tres instrucciones de HiveQL:

1. **instrucción DROP TABLE de Hello** eliminaciones Hola log4j Hive tabla si existe.
2. **instrucción CREATE TABLE de Hello** crea una tabla externa de Hive log4j, que señala toohello ubicación del archivo de registro de hello log4j;
3. **Hola ubicación del archivo de registro de hello log4j**. delimitador de campo de Hello es ",". delimitador de línea de saludo predeterminado es "\n". Una tabla externa de subárbol es el archivo de datos de Hola de tooavoid utilizado que se va a quitar de la ubicación original de hello, en caso de que desea que el flujo de trabajo de toorun hello Oozie varias veces.
4. **Hola instrucción INSERT SOBRESCRIBIR** recuentos de apariciones de Hola de cada tipo de nivel de registro de hello log4j tabla de Hive y guarda ubicación de almacenamiento de blobs de Azure de hello salida tooan.

> [!NOTE]
> Hay un problema conocido de la ruta de acceso de Hive. Se producirá este problema cuando envíe un trabajo de Oozie. Hola instrucciones para corregir el problema de hello puede encontrarse en hello Wiki de TechNet: [Hive de HDInsight de error: no se puede toorename][technetwiki-hive-error].

**llamado por el flujo de trabajo de hello toodefine hello HiveQL script archivo toobe**

1. Cree un archivo de texto con hello siguiente contenido:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Hay tres variables utilizadas en el script de Hola:

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     archivo de definición de flujo de trabajo de Hello (workflow.xml en este tutorial) pasará estos toothis valores script de HiveQL en tiempo de ejecución.
2. Guardar archivo de hello como **C:\Tutorials\UseOozie\useooziewf.hql** usando la codificación ANSI (ASCII). (Use el Bloc de notas si el editor de texto no proporciona esta opción.) El archivo de script será clúster de HDInsight implementado toohello más adelante en el tutorial Hola.

**toodefine un flujo de trabajo**

1. Cree un archivo de texto con hello siguiente contenido:

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
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

    Hay dos acciones definidas en el flujo de trabajo de Hola. Hola inicio-tooaction es *RunHiveScript*. Si se ejecuta la acción de hello *Aceptar*, la acción siguiente hello es *RunSqoopExport*.

    Hola RunHiveScript tiene varias variables. Valores de hello pasará al enviar trabajo de Oozie Hola desde su estación de trabajo mediante el uso de PowerShell de Azure.

    Variables de flujo de trabajo

    <table border = "1">
    <tr><th>Variables de flujo de trabajo</th><th>Description</th></tr>
    <tr><td>${jobTracker}</td><td>Especifique la dirección URL de Hola de seguimiento de trabajo de Hadoop de Hola. Use <strong>jobtrackerhost:9010</strong> en la versión del clúster de HDInsight 3.0 y 2.0.</td></tr>
    <tr><td>${nameNode}</td><td>Especifique la dirección URL de hello del nodo de nombre de Hadoop de Hola. Usar wasb de sistema de archivos de hello predeterminado: / / dirección, por ejemplo, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
    <tr><td>${queueName}</td><td>Especifica el nombre de la cola de Hola que Hola trabajo se enviarán a. Use el <strong>valor predeterminado</strong>.</td></tr>
    </table>

    Variables de acción de Hive

    <table border = "1">
    <tr><th>Variable de acción de Hive</th><th>Description</th></tr>
    <tr><td>${hiveDataFolder}</td><td>directorio de origen de Hola de hello comando Hive Create Table.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>carpeta de salida de Hello de hello instrucción INSERT SOBRESCRIBIR.</td></tr>
    <tr><td>${hiveTableName}</td><td>nombre de Hola de tabla de Hive de Hola que hace referencia a archivos de datos de log4j Hola.</td></tr>
    </table>

    Variables de acción de Sqoop

    <table border = "1">
    <tr><th>Variable de acción de Sqoop</th><th>Description</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Cadena de conexión de Base de datos SQL.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>se exportarán Hello Azure base de datos tabla toowhere Hola de datos de SQL.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>carpeta de salida de Hello de hello instrucción Hive insertar SOBRESCRIBIR. Se trata de hello misma carpeta para la exportación de Sqoop Hola (export-dir).</td></tr>
    </table>

    Para obtener más información sobre el flujo de trabajo de Oozie y el uso de las acciones de flujo de trabajo de hello, consulte [documentación de Apache Oozie 4.0] [ apache-oozie-400] (con la versión de clúster de HDInsight 3.0) o [Apache Oozie 3.3.2 documentación] [ apache-oozie-332] (para la versión 2.1 del clúster de HDInsight).

1. Guardar archivo de hello como **C:\Tutorials\UseOozie\workflow.xml** usando la codificación ANSI (ASCII). (Use el Bloc de notas si el editor de texto no proporciona esta opción.)

**toodefine coordinador**

1. Cree un archivo de texto con hello siguiente contenido:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Hay cinco variables utilizadas en el archivo de definición de hello:

   | Variable | Description |
   | --- | --- |
   | ${coordFrequency} |Hora de pausa del trabajo. La frecuencia se expresa siempre en minutos. |
   | ${coordStart} |Hora de inicio del trabajo. |
   | ${coordEnd} |Hora de finalización del trabajo. |
   | ${coordTimezone} |Oozie procesa los trabajos del coordinador en una zona horaria fija sin horario de verano (representado normalmente mediante UTC). Esta zona horaria se conoce como Hola "Oozie procesamiento timezone." |
   | ${wfPath} |ruta de acceso de Hola para workflow.xml Hola.  Si el nombre de archivo de flujo de trabajo de hello no es nombre de archivo predeterminado de hello (workflow.xml), debe especificarlo. |
2. Guardar archivo de hello como **C:\Tutorials\UseOozie\coordinator.xml** usando la codificación de hello ANSI (ASCII). (Use el Bloc de notas si el editor de texto no proporciona esta opción.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Implementar proyecto de Oozie hello y preparar el tutorial Hola
Se ejecutará una siguiente de hello Azure PowerShell tooperform de secuencia de comandos:

* Copia Hola almacenamiento de blobs de HiveQL (useoozie.hql) de la secuencia de comandos tooAzure, wasb:///tutorials/useoozie/useoozie.hql.
* Copie el archivo workflow.xml toowasb:///tutorials/useoozie/workflow.xml.
* Copie coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* Archivo de datos de copia hello (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Cree una tabla de base de datos SQL de Azure para el almacenamiento de datos de exportación de Sqoop. es el nombre de la tabla de Hello *log4jLogCount*.

**Descripción del almacenamiento de HDInsight**

HDInsight usa el almacenamiento de blobs de Azure para almacenar datos. wasb: / / es la implementación de sistema de archivos distribuido de Hadoop Hola (HDFS) en almacenamiento de blobs de Azure de Microsoft. Para obtener más información, consulte [Uso de Azure Blob Storage con HDInsight][hdinsight-storage].

Cuando se aprovisiona un clúster de HDInsight, una cuenta de almacenamiento de blobs de Azure y un contenedor específico de esa cuenta se designa como sistema de archivos predeterminado de hello, al igual que en HDFS. Además toothis cuenta de almacenamiento, puede agregar cuentas de almacenamiento adicional de hello misma suscripción de Azure o desde diferentes suscripciones de Azure durante el proceso de aprovisionamiento de Hola. Para obtener instrucciones sobre cómo agregar más cuentas de almacenamiento, consulte [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision]. script de PowerShell de Azure de toosimplify Hola usado en este tutorial, todos de hello archivos se almacenan en el contenedor de sistema de archivos de hello predeterminado se encuentran en */tutoriales/useoozie*. De forma predeterminada, este contenedor tiene Hola mismo nombre como nombre de clúster de HDInsight Hola.
Hola sintaxis es:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Hola solo *wasb: / /* la sintaxis es compatible con la versión 3.0 del clúster de HDInsight. Hola anterior *asv: / /* se admiten la sintaxis de 1.6 clústeres y 2.1 de HDInsight, pero no se admite en clústeres de HDInsight 3.0.
>
> Hola wasb: / / ruta de acceso es una ruta de acceso virtual. Para obtener más información, consulte [Uso de Azure Blob Storage con HDInsight][hdinsight-storage].

Un archivo que se almacena en el contenedor de sistema de archivos de hello predeterminado puede tener acceso desde HDInsight mediante cualquiera de hello después a URI (utilizo workflow.xml como ejemplo):

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Si desea tooaccess Hola archivo directamente desde la cuenta de almacenamiento de hello, nombre de blob de hello para el archivo hello es:

    tutorials/useoozie/workflow.xml

**Descripción de las tablas internas y externas de Hive**

Hay algunas cosas que debe tooknow acerca de las tablas internas y externas de Hive:

* Hola comando CREATE TABLE crea una tabla interna, también conocido como una tabla administrada. archivo de datos de Hello debe estar ubicado en el contenedor predeterminado de Hola.
* Hola comando CREATE TABLE mueve datos Hola archivotoohello/hive/almacenamiento/<TableName> carpeta en el contenedor predeterminado de Hola.
* Hola comando CREATE TABLE externo crea una tabla externa. archivo de datos de Hello puede encontrarse fuera del contenedor predeterminado Hola.
* Hola comando CREATE TABLE externo no mueve los archivos de datos de Hola.
* Hola comando CREATE TABLE externo no permite que las subcarpetas de la carpeta de Hola que se especifica en la cláusula de ubicación de Hola. Se trata de motivo Hola ¿por qué tutorial Hola realiza una copia del archivo de hello sample.log.

Para obtener más información, consulte [HDInsight: introducción de tablas internas y externas de Hive][cindygross-hive-tables].

**tutorial de hello tooprepare**

1. Hola abrir Windows PowerShell ISE (en la pantalla de inicio de Windows 8 de bienvenida, escriba **PowerShell_ISE**y, a continuación, haga clic en **Windows PowerShell ISE**. Consulte [Iniciar Windows PowerShell en Windows 8 y Windows][powershell-start] para obtener más información.
2. En el panel de la parte inferior de hello, ejecute hello después comando tooconnect tooyour suscripción de Azure:

    ```powershell
    Add-AzureAccount
    ```

    También será tooenter solicitada sus credenciales de cuenta de Azure. Este método para agregar una conexión a una suscripción expire y después de 12 horas, tendrá toorun Hola cmdlet nuevo.

   > [!NOTE]
   > Si tiene varias suscripciones de Azure y suscripción predeterminada de hello no es hello uno desea toouse, usar hello <strong>Select-AzureSubscription</strong> tooselect cmdlet una suscripción.

3. Copie Hola siguiente secuencia de comandos en el panel de scripts de hello y, a continuación, establezca las variables de seis primeros hello:

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    Para obtener más descripciones de las variables de hello, vea hello [requisitos previos](#prerequisites) sección en este tutorial.

4. Anexar Hola siguiente secuencia de comandos toohello en el panel de scripts de hello:

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create hello log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. Haga clic en **ejecutar Script** o presione **F5** secuencia de comandos de toorun Hola. salida de Hello será similar al:

    ![Resultado de preparación del tutorial][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Ejecute hello Oozie proyecto
Azure PowerShell no proporciona actualmente cmdlets para la definición de trabajos de Oozie. Puede usar hello **Invoke-RestMethod** servicios web de cmdlet tooinvoke Oozie. Hola Oozie API para servicios web es una API de JSON de REST de HTTP. Para obtener más información sobre los servicios web de Oozie Hola API, consulte [documentación de Apache Oozie 4.0] [ apache-oozie-400] (con la versión de clúster de HDInsight 3.0) o [documentación de Apache Oozie 3.3.2] [ apache-oozie-332] (para la versión 2.1 del clúster de HDInsight).

**toosubmit un trabajo de Oozie**

1. Hola abrir Windows PowerShell ISE (en la pantalla de inicio de Windows 8, escriba **PowerShell_ISE**y, a continuación, haga clic en **Windows PowerShell ISE**. Consulte [Iniciar Windows PowerShell en Windows 8 y Windows][powershell-start] para obtener más información.
2. Script siguiente de Hola de copia en el panel de scripts de hello y, a continuación, conjunto Hola variables primero catorce (sin embargo, omitir **$storageUri**).

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    Para obtener más descripciones de las variables de hello, vea hello [requisitos previos](#prerequisites) sección en este tutorial.

    $coordstart y $coordend son de flujo de trabajo a partir de Hola y hora de finalización. toofind hora UTC/GMT de hello, busque "hora utc" en bing.com. Hola $coordFrequency es la frecuencia en minutos que desea que el flujo de trabajo de toorun Hola.
3. Anexar Hola siguiente secuencia de comandos de toohello. Este elemento define la carga de Oozie Hola:

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
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
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > archivo de carga de envío de flujo de trabajo de diferencia importante en comparación con toohello Hello es variable hello **oozie.coord.application.path**. Al enviar una tarea de flujo de trabajo, se usa **oozie.wf.application.path** .

4. Anexar Hola siguiente secuencia de comandos de toohello. Esta parte comprueba el estado del servicio de hello Oozie web:

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. Anexar Hola siguiente secuencia de comandos de toohello. En esta parte se crea un trabajo de Oozie:

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > Cuando se envía un trabajo de flujo de trabajo, debe realizar otro trabajo web servicio llamada toostart Hola después de que se crea el trabajo de Hola. En este caso, el trabajo de coordinador de Hola se desencadena por tiempo. trabajo de Hola se iniciará automáticamente.

6. Anexar Hola siguiente secuencia de comandos de toohello. Este elemento comprueba el estado del trabajo de Hola Oozie:

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. (Opcional) Anexar Hola siguiente secuencia de comandos de toohello.

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. Anexar Hola siguiente secuencia de comandos de toohello:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Quitar signos de hello # si desea que las funciones adicionales de toorun Hola.
9. Si el clúster de HDinsight es la versión 2.1, reemplace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" por "https://$clusterName.azurehdinsight.net:443/oozie/v1/". Versión de clúster de HDInsight 2.1 no no admite la versión 2 de servicios web de Hola.
10. Haga clic en **ejecutar Script** o presione **F5** secuencia de comandos de toorun Hola. salida de Hello será similar al:

     ![Resultado del flujo de trabajo de ejecución del tutorial][img-runworkflow-output]
11. Conectar tooyour hello que exporta datos de base de datos SQL toosee.

**registro de errores de trabajo de hello toocheck**

tootroubleshoot un flujo de trabajo, archivo de registro de hello Oozie puede encontrarse en C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log desde el nodo principal del clúster de Hola. Para obtener información acerca de RDP, consulte [clústeres de HDInsight de administración con Hola portal de Azure][hdinsight-admin-portal].

**tutorial de hello toorerun**

flujo de trabajo de toorerun hello, debe realizar Hola siguientes tareas:

* Elimine el archivo de salida de script de Hive Hola.
* Eliminar datos de hello en la tabla de log4jLogsCount Hola.

Aquí tiene un script de Windows PowerShell de ejemplo que puede usar:

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, se habrá aprendido cómo toodefine un flujo de trabajo de Oozie y un coordinador de Oozie y cómo toorun un coordinador de Oozie de trabajo mediante el uso de PowerShell de Azure. toolearn más información, vea Hola siguientes artículos:

* [Introducción a HDInsight][hdinsight-get-started]
* [Uso de Azure Blob Storage con HDInsight][hdinsight-storage]
* [Administración de HDInsight con Azure PowerShell][hdinsight-admin-powershell]
* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Uso de Sqoop con HDInsight][hdinsight-use-sqoop]
* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Pig con HDInsight][hdinsight-use-pig]
* [Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-java-mapreduce]

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
