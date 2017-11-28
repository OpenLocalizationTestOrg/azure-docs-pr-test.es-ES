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
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="5443b-104">Usar Oozie con Hadoop toodefine y ejecutar un flujo de trabajo de HDInsight basados en Linux</span><span class="sxs-lookup"><span data-stu-id="5443b-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="5443b-105">Obtenga información acerca de cómo toouse Oozie Apache con Hadoop en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5443b-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="5443b-106">Oozie de Apache es un sistema de coordinación o flujo de trabajo que administra trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5443b-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="5443b-107">Oozie se integra con la pila de Hadoop de Hola y admite Hola siguientes trabajos:</span><span class="sxs-lookup"><span data-stu-id="5443b-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="5443b-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="5443b-108">Apache MapReduce</span></span>
* <span data-ttu-id="5443b-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="5443b-109">Apache Pig</span></span>
* <span data-ttu-id="5443b-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="5443b-110">Apache Hive</span></span>
* <span data-ttu-id="5443b-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="5443b-111">Apache Sqoop</span></span>

<span data-ttu-id="5443b-112">Oozie también puede ser trabajos tooschedule usado que el sistema tooa específico, como programas Java o secuencias de comandos de shell</span><span class="sxs-lookup"><span data-stu-id="5443b-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="5443b-113">Otra opción para definir los flujos de trabajo con HDInsight es Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5443b-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="5443b-114">toolearn más información acerca de la factoría de datos de Azure, consulte [uso de Pig y Hive con factoría de datos][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="5443b-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5443b-115">Oozie no está habilitado en HDInsight unido a un dominio.</span><span class="sxs-lookup"><span data-stu-id="5443b-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5443b-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5443b-116">Prerequisites</span></span>

* <span data-ttu-id="5443b-117">**Un clúster de HDInsight**: Consulte [Introducción a HDInsight en Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="5443b-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5443b-118">pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="5443b-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5443b-119">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="5443b-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5443b-120">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5443b-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="5443b-121">Flujo de trabajo de ejemplo</span><span class="sxs-lookup"><span data-stu-id="5443b-121">Example workflow</span></span>

<span data-ttu-id="5443b-122">flujo de trabajo de Hello usado en este documento contiene dos acciones.</span><span class="sxs-lookup"><span data-stu-id="5443b-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="5443b-123">Las acciones son definiciones de tareas, como la ejecución de Hive, Sqoop, MapReduce o cualquier otro proceso:</span><span class="sxs-lookup"><span data-stu-id="5443b-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagrama de flujo de trabajo][img-workflow-diagram]

1. <span data-ttu-id="5443b-125">Una acción de Hive ejecuta un script de HiveQL tooextract registros de hello **hivesampletable** incluido con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5443b-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="5443b-126">Cada fila de datos describe una visita de un dispositivo móvil específico.</span><span class="sxs-lookup"><span data-stu-id="5443b-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="5443b-127">formato de registro de Hello aparece toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5443b-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="5443b-128">Hola usado en este documento de script de Hive recuentos de visitas total de Hola para cada plataforma (por ejemplo, Android o iPhone) y almacena los recuentos de hello tooa nueva tabla de Hive.</span><span class="sxs-lookup"><span data-stu-id="5443b-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="5443b-129">Para más información sobre Hive, consulte [Uso de Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="5443b-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="5443b-130">Una acción de Sqoop exporta contenido Hola de hello nueva tabla tooa tabla de Hive en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5443b-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="5443b-131">Para obtener más información sobre Sqoop, consulte [Uso de Hadoop Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="5443b-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="5443b-132">Para versiones compatibles de Oozie en clústeres de HDInsight, vea [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="5443b-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="5443b-133">Crear el directorio de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-133">Create hello working directory</span></span>

<span data-ttu-id="5443b-134">Oozie espera recursos necesarios para una toobe de trabajo almacenados en hello mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="5443b-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="5443b-135">Este ejemplo usa **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="5443b-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="5443b-136">Usar hello después toocreate de comando este directorio y el directorio de datos de Hola que contiene la nueva tabla de Hive Hola creado por este flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="5443b-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="5443b-137">Hola `-p` parámetro hace que todos los directorios en hello toobe de ruta de acceso creado.</span><span class="sxs-lookup"><span data-stu-id="5443b-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="5443b-138">Hola **datos** directorio es datos de uso toohold utilizados por hello **useooziewf.hql** secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="5443b-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="5443b-139">Ejecutar Hola siguiente comando, lo que garantiza que Oozie puede suplantar la cuenta de usuario al ejecutar los trabajos de Hive y Sqoop.</span><span class="sxs-lookup"><span data-stu-id="5443b-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="5443b-140">Reemplace **USERNAME** por su nombre de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="5443b-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="5443b-141">Puede omitir los errores de ese usuario Hola ya es miembro de hello `users` grupo.</span><span class="sxs-lookup"><span data-stu-id="5443b-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="5443b-142">Adición de un controlador de base de datos</span><span class="sxs-lookup"><span data-stu-id="5443b-142">Add a database driver</span></span>

<span data-ttu-id="5443b-143">Dado que este flujo de trabajo usa Sqoop tooexport datos tooSQL base de datos, debe proporcionar que una copia del controlador JDBC de hello usa tootalk tooSQL base de datos.</span><span class="sxs-lookup"><span data-stu-id="5443b-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="5443b-144">Use Hola siguientes comando toocopy lo toohello directorio de trabajo:</span><span class="sxs-lookup"><span data-stu-id="5443b-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="5443b-145">Si el flujo de trabajo utiliza otros recursos, como un archivo jar que contiene una aplicación de MapReduce, necesitaría tooadd también estos recursos.</span><span class="sxs-lookup"><span data-stu-id="5443b-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="5443b-146">Definir la consulta de Hive Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-146">Define hello Hive query</span></span>

<span data-ttu-id="5443b-147">Usar hello siguiendo los pasos toocreate un script de HiveQL que define una consulta, que se usa en un flujo de trabajo de Oozie más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="5443b-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="5443b-148">Conecte el clúster toohello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="5443b-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="5443b-149">Hola comando siguiente es un ejemplo del uso de hello `ssh` comando.</span><span class="sxs-lookup"><span data-stu-id="5443b-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="5443b-150">Reemplace __nombre de usuario__ con el usuario SSH de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="5443b-151">Reemplace __CLUSTERNAME__ con el nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5443b-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="5443b-152">Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5443b-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5443b-153">Desde Hola conexión SSH, use Hola después toocreate un archivo de comandos:</span><span class="sxs-lookup"><span data-stu-id="5443b-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="5443b-154">Una vez que abre el editor de nano hello, utilice Hola después de consulta como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="5443b-155">Hay dos variables utilizadas en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="5443b-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="5443b-156">**${hiveTableName}**: contiene nombre Hola de hello tabla toobe creado</span><span class="sxs-lookup"><span data-stu-id="5443b-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="5443b-157">**${hiveDataFolder}**: contiene archivos de datos de hello ubicación toostore hello para la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="5443b-158">archivo de definición de flujo de trabajo de Hello (workflow.xml en este tutorial) pasa estos valores toothis script de HiveQL en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="5443b-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="5443b-159">editor de hello tooexit, presione Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="5443b-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="5443b-160">Cuando se le pida, seleccione **Y** toosave Hola archivo y luego use **ENTRAR** toouse hello **useooziewf.hql** nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="5443b-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="5443b-161">Siguiente de hello use comandos toocopy **useooziewf.hql** demasiado**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="5443b-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="5443b-162">Estos comandos almacenan hello **useooziewf.hql** archivo en almacenamiento de hello HDFS compatible para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="5443b-163">Definir el flujo de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-163">Define hello workflow</span></span>

<span data-ttu-id="5443b-164">Las definiciones de los flujos de trabajo de Oozie se escriben en hPDL (un lenguaje de definición de procesos XML).</span><span class="sxs-lookup"><span data-stu-id="5443b-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="5443b-165">Usar hello siguiendo el flujo de trabajo de pasos toodefine hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="5443b-166">Usar hello después de la instrucción toocreate y editar un archivo nuevo:</span><span class="sxs-lookup"><span data-stu-id="5443b-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="5443b-167">Una vez que abre el editor de nano hello, escriba Hola continuación de XML como contenido del archivo hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

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

    <span data-ttu-id="5443b-168">Hay dos acciones definidas en el flujo de trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="5443b-169">**RunHiveScript**: esta acción es la acción de inicio de Hola y se ejecuta hello **useooziewf.hql** de script de Hive</span><span class="sxs-lookup"><span data-stu-id="5443b-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="5443b-170">**RunSqoopExport**: esta acción exporta datos de hello creados a partir de hello Hive script tooSQL con Sqoop de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="5443b-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="5443b-171">Esta acción solo se ejecuta si hello **RunHiveScript** acción es correcta.</span><span class="sxs-lookup"><span data-stu-id="5443b-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="5443b-172">flujo de trabajo de Hello tiene varias entradas, como `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="5443b-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="5443b-173">Estas entradas se reemplazan por valores que se usa en la definición del trabajo Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="5443b-174">se crea la definición del trabajo Hello más adelante en este documento.</span><span class="sxs-lookup"><span data-stu-id="5443b-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="5443b-175">Hola de nota también `<archive>sqljdbc4.jar</arcive>` entrada Hola Sqoop sección.</span><span class="sxs-lookup"><span data-stu-id="5443b-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="5443b-176">Esta entrada indica Oozie toomake este archivo disponible para Sqoop cuando se ejecuta la acción.</span><span class="sxs-lookup"><span data-stu-id="5443b-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="5443b-177">Utilice Ctrl-X, a continuación, **Y** y **ENTRAR** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5443b-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="5443b-178">Siguiente Hola de uso del comando hello toocopy **workflow.xml** archivo demasiado**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="5443b-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="5443b-179">Crear base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-179">Create hello database</span></span>

<span data-ttu-id="5443b-180">toocreate una base de datos de SQL Azure, siga los pasos de Hola Hola [crear una base de datos de SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5443b-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="5443b-181">Al crear la base de datos de hello, use `oozietest` como nombre de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="5443b-182">También tome nota del nombre de hello del servidor de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="5443b-183">Crear tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="5443b-184">Hay muchas maneras tooconnect tooSQL base de datos toocreate una tabla.</span><span class="sxs-lookup"><span data-stu-id="5443b-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="5443b-185">Hola a consecuencia del uso de pasos [uso](http://www.freetds.org/) de clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="5443b-186">Usar hello siguiendo el uso del comando tooinstall en clúster de HDInsight de hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="5443b-187">Una vez que se ha instalado el uso, utilice Hola después el servidor de base de datos SQL de comandos tooconnect toohello que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="5443b-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="5443b-188">Recibir toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5443b-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="5443b-189">En hello `1>` símbolo del sistema, escriba Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="5443b-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="5443b-190">Cuando Hola `GO` instrucción se haya especificado, se evalúan en las instrucciones anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="5443b-191">Estas instrucciones crean una tabla denominada **mobiledata** utilizado por el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="5443b-192">Hola de uso después de tooverify que Hola tabla se ha creado:</span><span class="sxs-lookup"><span data-stu-id="5443b-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="5443b-193">Vea toohello similar de salida siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5443b-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="5443b-194">Escriba `exit` en hello `1>` solicitar utilidad de tooexit Hola tsql.</span><span class="sxs-lookup"><span data-stu-id="5443b-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="5443b-195">Crear definición de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-195">Create hello job definition</span></span>

<span data-ttu-id="5443b-196">definición del trabajo Hola describe dónde toofind Hola workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="5443b-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="5443b-197">También se describe dónde toofind otros archivos usados por el flujo de trabajo de hello (por ejemplo, useooziewf.hql.) También define los valores de hello para propiedades utilizan en el flujo de trabajo de Hola y los archivos asociados.</span><span class="sxs-lookup"><span data-stu-id="5443b-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="5443b-198">Usar hello sigue dirección completa Hola del comando tooget de almacenamiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="5443b-199">Esta dirección se utiliza en el archivo de configuración de hello en unos momentos:</span><span class="sxs-lookup"><span data-stu-id="5443b-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="5443b-200">Este comando devuelve información toohello similar continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="5443b-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="5443b-201">Si el clúster de HDInsight de hello usa el almacenamiento de Azure como almacenamiento predeterminado de hello, Hola `<value>` contenido del elemento comienzan por `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="5443b-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="5443b-202">Si se usa Azure Data Lake Store en su lugar, comenzará por `adl://`.</span><span class="sxs-lookup"><span data-stu-id="5443b-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="5443b-203">Guardar el contenido de Hola de hello `<value>` elemento, tal y como se utiliza en los pasos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="5443b-204">Usar hello después comando tooget FQDN del nodo principal del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="5443b-205">Esta información se usa para hello JobTracker dirección de clúster de hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="5443b-206">Esto devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5443b-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="5443b-207">Hello puerto usado para hello JobTracker es 8050, por lo que es Hola dirección completa toouse para hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="5443b-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="5443b-208">Usar hello siguiente configuración de definición de trabajo de toocreate Hola Oozie:</span><span class="sxs-lookup"><span data-stu-id="5443b-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="5443b-209">Una vez que abre el editor de nano hello, utilice Hola continuación de XML como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

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

   * <span data-ttu-id="5443b-210">Reemplace todas las instancias de  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  con valor Hola recibidos con anterioridad para el almacenamiento de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5443b-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="5443b-211">Si la ruta de acceso de hello es un `wasb` ruta de acceso, debe usar la ruta de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="5443b-212">No acortar toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="5443b-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="5443b-213">Reemplace **JOBTRACKERADDRESS** con hello dirección JobTracker/ResourceManager recibidos con anterioridad.</span><span class="sxs-lookup"><span data-stu-id="5443b-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="5443b-214">Reemplace **YourName** por el nombre de inicio de sesión por clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="5443b-215">Reemplace **serverName**, **adminLogin**, y **adminPassword** con información de hello para la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5443b-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="5443b-216">La mayoría de hello información de este archivo es valores de hello toopopulate usado utilizados en hello workflow.xml o ooziewf.hql archivos (por ejemplo, ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="5443b-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="5443b-217">Hola **oozie.wf.application.path** entrada define dónde se ejecutó el archivo de toofind Hola workflow.xml, que contiene el flujo de trabajo de Hola este trabajo.</span><span class="sxs-lookup"><span data-stu-id="5443b-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="5443b-218">Utilice Ctrl-X, a continuación, **Y** y **ENTRAR** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5443b-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="5443b-219">Enviar y administrar el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-219">Submit and manage hello job</span></span>

<span data-ttu-id="5443b-220">Hello pasos siguientes utilice hello Oozie comando toosubmit y administración flujos de trabajo de Oozie en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="5443b-221">Hola Oozie comando es una interfaz sencilla sobre hello [API de REST de Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="5443b-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5443b-222">Al usar comandos de hello Oozie, debe usar Hola FQDN para el nodo principal de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="5443b-223">Este FQDN solo es accesible desde el clúster de hello, o si hello clúster se encuentra en una red Virtual de Azure, desde otras máquinas en hello misma red.</span><span class="sxs-lookup"><span data-stu-id="5443b-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="5443b-224">Usar hello después tooobtain Hola URL toohello Oozie servicio:</span><span class="sxs-lookup"><span data-stu-id="5443b-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="5443b-225">Esto devuelve información toohello similar continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="5443b-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="5443b-226">Hola `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` parte es hello toouse de dirección URL con hello Oozie comando.</span><span class="sxs-lookup"><span data-stu-id="5443b-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="5443b-227">Hola uso siga toocreate una variable de entorno para la dirección URL de hello, por lo que no tiene tootype para cada comando:</span><span class="sxs-lookup"><span data-stu-id="5443b-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="5443b-228">Sustituir la URL de hello con hello recibió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5443b-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="5443b-229">Usar hello siguiendo el trabajo de Hola toosubmit:</span><span class="sxs-lookup"><span data-stu-id="5443b-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="5443b-230">Este comando carga la información de trabajo de Hola de **job.xml** y lo envía tooOozie, pero no se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="5443b-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="5443b-231">Cuando se completa el comando hello, debe devolver Hola identificador de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="5443b-232">Por ejemplo: `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="5443b-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="5443b-233">Este identificador es trabajo de hello toomanage usado.</span><span class="sxs-lookup"><span data-stu-id="5443b-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="5443b-234">Ver el estado de Hola de trabajo de hello mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5443b-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="5443b-235">Reemplace `<JOBID>` con hello identificador devuelto en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="5443b-236">Esto devuelve información toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5443b-236">This returns information similar toohello following text:</span></span>

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

    <span data-ttu-id="5443b-237">Este trabajo tiene un estado de `PREP`.</span><span class="sxs-lookup"><span data-stu-id="5443b-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="5443b-238">Este estado indica que el trabajo de Hola se ha creado, pero no inicia.</span><span class="sxs-lookup"><span data-stu-id="5443b-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="5443b-239">Usar hello siguiendo el trabajo de hello toostart de comando:</span><span class="sxs-lookup"><span data-stu-id="5443b-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="5443b-240">Reemplace `<JOBID>` con hello identificador devuelto anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5443b-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="5443b-241">Si se comprueba el estado de hello después este comando, se encuentra en un estado de ejecución y se devuelve información sobre las acciones de hello en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="5443b-242">Una vez completada correctamente la tarea hello, puede comprobar que datos de Hola se generaron y exportan toohello tabla de base de datos SQL mediante Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="5443b-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="5443b-243">En hello `1>` símbolo del sistema, escriba Hola después de consulta:</span><span class="sxs-lookup"><span data-stu-id="5443b-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="5443b-244">información de Hello devuelta es similar toohello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="5443b-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="5443b-245">Para obtener más información sobre hello Oozie comando, consulte [herramienta de línea de comandos de Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="5443b-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="5443b-246">API de REST de Oozie</span><span class="sxs-lookup"><span data-stu-id="5443b-246">Oozie REST API</span></span>

<span data-ttu-id="5443b-247">Hola API de REST de Oozie permite toobuild sus propias herramientas que funcionan con Oozie.</span><span class="sxs-lookup"><span data-stu-id="5443b-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="5443b-248">siguiente Hola es HDInsight información específica acerca del uso de hello Oozie API de REST:</span><span class="sxs-lookup"><span data-stu-id="5443b-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="5443b-249">**URI**: Hola API de REST puede tener acceso desde el clúster fuera de hello en`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="5443b-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="5443b-250">**Autenticación**: autenticar API toohello con cuenta de clúster HTTP hello (Administrador) y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="5443b-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="5443b-251">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="5443b-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="5443b-252">Para obtener más información sobre el uso de API de REST de Oozie hello, consulte [API de servicios Web de Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="5443b-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="5443b-253">Interfaz de usuario web de Oozie</span><span class="sxs-lookup"><span data-stu-id="5443b-253">Oozie Web UI</span></span>

<span data-ttu-id="5443b-254">Hola Oozie interfaz de usuario Web proporciona una vista basada en web en el estado de los trabajos de Oozie hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="5443b-255">interfaz de usuario web de Hello permite hello tooview siguiente información:</span><span class="sxs-lookup"><span data-stu-id="5443b-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="5443b-256">Estado del trabajo</span><span class="sxs-lookup"><span data-stu-id="5443b-256">Job status</span></span>
* <span data-ttu-id="5443b-257">Definición del trabajo</span><span class="sxs-lookup"><span data-stu-id="5443b-257">Job definition</span></span>
* <span data-ttu-id="5443b-258">Configuración</span><span class="sxs-lookup"><span data-stu-id="5443b-258">Configuration</span></span>
* <span data-ttu-id="5443b-259">Un gráfico de acciones de hello en el trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="5443b-260">Registros del trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-260">Logs for hello job</span></span>

<span data-ttu-id="5443b-261">También puede ver detalles de las acciones dentro de un trabajo.</span><span class="sxs-lookup"><span data-stu-id="5443b-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="5443b-262">tooaccess Hola de interfaz de usuario de Web de Oozie, usar hello pasos:</span><span class="sxs-lookup"><span data-stu-id="5443b-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="5443b-263">Crear un clúster de HDInsight de toohello de túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5443b-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="5443b-264">Para obtener información, vea hello [uso SSH túnel con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5443b-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="5443b-265">Una vez que se ha creado un túnel, abra interfaz de usuario de web de Ambari hello en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="5443b-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="5443b-266">Hola URI para el sitio de hello Ambari es **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="5443b-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="5443b-267">Reemplace **CLUSTERNAME** con el nombre de Hola de su clúster de HDInsight basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="5443b-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="5443b-268">Desde la parte izquierda de la página de Hola de hello, seleccione **Oozie**, a continuación, **vínculos rápidos**y, finalmente, **Oozie interfaz de usuario Web**.</span><span class="sxs-lookup"><span data-stu-id="5443b-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![imagen de los menús de Hola](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="5443b-270">Hola toodisplaying de los valores predeterminados de interfaz de usuario de Web de Oozie trabajos de flujo de trabajo en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5443b-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="5443b-271">toosee todos los trabajos de flujo de trabajo, seleccione **todos los trabajos**.</span><span class="sxs-lookup"><span data-stu-id="5443b-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Todos los trabajos mostrados](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="5443b-273">Seleccione un trabajo tooview obtener más información sobre el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-273">Select a job tooview more information about hello job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="5443b-275">Desde la ficha de información del trabajo de hello, puede ver información sobre el trabajo básico y las acciones individuales de hello en el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="5443b-276">Con pestañas de Hola princip Hola. puede ver Hola definición de trabajo configuración del trabajo, Hola acceso registro de trabajo o ver un dirigen acíclico gráfico (DAG) de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="5443b-277">**Registro de trabajo**: Hola seleccione **GetLogs** botón tooget todos los registros de trabajo de Hola o usar hello **escriba el filtro de búsqueda** campo toofilter registros</span><span class="sxs-lookup"><span data-stu-id="5443b-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Registro de trabajo](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="5443b-279">**JobDAG**: Hola DAG es una visión general gráfica de rutas de acceso de datos de hello realizada a través del flujo de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="5443b-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![DAG del trabajo](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="5443b-281">Seleccionar una de las acciones de Hola de hello **información del trabajo** ficha muestra información para la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="5443b-282">Por ejemplo, seleccione hello **RunHiveScript** acción.</span><span class="sxs-lookup"><span data-stu-id="5443b-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Información de acción](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="5443b-284">Puede ver detalles de la acción de hello, como un vínculo toohello **dirección URL de consola**.</span><span class="sxs-lookup"><span data-stu-id="5443b-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="5443b-285">Este vínculo puede ser información de JobTracker tooview usado para el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="5443b-286">Programación de trabajos</span><span class="sxs-lookup"><span data-stu-id="5443b-286">Scheduling jobs</span></span>

<span data-ttu-id="5443b-287">Coordinador de Hello permite toospecify una frecuencia de inicio y finalización, repetición de trabajos.</span><span class="sxs-lookup"><span data-stu-id="5443b-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="5443b-288">toodefine una programación de flujo de trabajo de hello, Hola uso pasos:</span><span class="sxs-lookup"><span data-stu-id="5443b-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="5443b-289">Hola de uso después de un archivo denominado toocreate **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="5443b-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="5443b-290">Usar hello continuación de XML como contenido de Hola de archivo hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-290">Use hello following XML as hello contents of hello file:</span></span>

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
    > <span data-ttu-id="5443b-291">Hola `${...}` variables se reemplazan por valores en la definición del trabajo hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="5443b-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="5443b-292">Hola variables son:</span><span class="sxs-lookup"><span data-stu-id="5443b-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="5443b-293">`${coordFrequency}`: El tiempo entre las instancias del trabajo de hello en ejecución.</span><span class="sxs-lookup"><span data-stu-id="5443b-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="5443b-294">** `${coordStart}`: hora de inicio del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="5443b-295">`${coordEnd}`: hora de finalización del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="5443b-296">`${coordTimezone}`: los trabajos del coordinador se encuentran en una zona horaria fija sin horario de verano (representado normalmente mediante UTC).</span><span class="sxs-lookup"><span data-stu-id="5443b-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="5443b-297">Esta zona horaria se conoce como Hola "Oozie procesamiento timezone."</span><span class="sxs-lookup"><span data-stu-id="5443b-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="5443b-298">`${wfPath}`: Hola workflow.xml toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="5443b-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="5443b-299">Hola toosave de archivos, use Ctrl-X **Y**, y **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="5443b-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="5443b-300">Usar hello siguiendo el directorio de trabajo de toohello archivo Hola de toocopy comando para este trabajo:</span><span class="sxs-lookup"><span data-stu-id="5443b-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="5443b-301">Hola de uso después de hello toomodify **job.xml** archivo:</span><span class="sxs-lookup"><span data-stu-id="5443b-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="5443b-302">Asegúrese de hello siguientes cambios:</span><span class="sxs-lookup"><span data-stu-id="5443b-302">Make hello following changes:</span></span>

   * <span data-ttu-id="5443b-303">archivo tooinstruct oozie toorun hello coordinador en lugar de flujo de trabajo de hello, cambio `<name>oozie.wf.application.path</name>` demasiado`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="5443b-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="5443b-304">Hola tooset `workflowPath` variable utilizada por el Coordinador de hello, agregar Hola continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="5443b-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="5443b-305">Reemplace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` texto con el valor de hello utilizado en otras entradas de archivo de hello job.xml.</span><span class="sxs-lookup"><span data-stu-id="5443b-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="5443b-306">inicio de hello toodefine, final y frecuencia de coordinador de hello, agreguen Hola continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="5443b-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

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

       <span data-ttu-id="5443b-307">Estos valores establecen too12 de tiempo de inicio de hello: 00 P.M. del 10 de mayo de 2017 Hola final tiempo tooMay 12, de 2017.</span><span class="sxs-lookup"><span data-stu-id="5443b-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="5443b-308">intervalo de saludo para ejecutar este trabajo diariamente.</span><span class="sxs-lookup"><span data-stu-id="5443b-308">hello interval for running this job daily.</span></span> <span data-ttu-id="5443b-309">frecuencia de Hola se expresa en minutos, por lo que 24 horas a 60 minutos = 1440 minutos.</span><span class="sxs-lookup"><span data-stu-id="5443b-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="5443b-310">Por último, zona horaria de Hola se establece tooUTC.</span><span class="sxs-lookup"><span data-stu-id="5443b-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="5443b-311">Utilice Ctrl-X, a continuación, **Y** y **ENTRAR** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5443b-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="5443b-312">trabajo de hello toorun, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5443b-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="5443b-313">Este comando se envía e inicia el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="5443b-314">Si visite hello Oozie interfaz de usuario Web y seleccione hello **trabajos de coordinador** pestaña, verá información toohello similar después de imagen:</span><span class="sxs-lookup"><span data-stu-id="5443b-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![pestaña de trabajos de coordinador](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="5443b-316">Hola **materialización siguiente** entrada contiene Hola próxima vez que Hola ejecuciones de los trabajos.</span><span class="sxs-lookup"><span data-stu-id="5443b-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="5443b-317">Toohello similar anterior del flujo de trabajo, selección de entrada del trabajo hello en la interfaz de usuario web de hello muestra información sobre el trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="5443b-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![información de trabajos de coordinador](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="5443b-319">Esta imagen muestra solo correcta ejecuciones del trabajo de hello, acciones no individuales de flujo de trabajo de hello programado.</span><span class="sxs-lookup"><span data-stu-id="5443b-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="5443b-320">toosee que seleccione uno de hello **acción** entradas.</span><span class="sxs-lookup"><span data-stu-id="5443b-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Información de acción](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="5443b-322">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5443b-322">Troubleshooting</span></span>

<span data-ttu-id="5443b-323">Hola Oozie UI permite tooview Oozie registros.</span><span class="sxs-lookup"><span data-stu-id="5443b-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="5443b-324">También contiene registros de tooJobTracker vínculos para tareas de MapReduce iniciadas por el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="5443b-325">patrón de Hola para solucionar el problema debe ser:</span><span class="sxs-lookup"><span data-stu-id="5443b-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="5443b-326">Ver el trabajo de hello en la interfaz de usuario de Oozie Web.</span><span class="sxs-lookup"><span data-stu-id="5443b-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="5443b-327">Si hay un error o un error de una acción específica, seleccione Hola toosee acción si hello **mensaje de Error** campo proporciona más información sobre el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="5443b-328">Si está disponible, utilice URL Hola de hello acción tooview más detalles (por ejemplo, registros de JobTracker) para la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="5443b-329">Hello siguientes son errores específicos que pueden producirse, y cómo tooresolve ellos.</span><span class="sxs-lookup"><span data-stu-id="5443b-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="5443b-330">JA009: No se puede inicializar el clúster</span><span class="sxs-lookup"><span data-stu-id="5443b-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="5443b-331">**Síntomas**: Hola cambios de estado del trabajo demasiado**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="5443b-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="5443b-332">Detalles de trabajo de hello Mostrar estado de RunHiveScript de hello como **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="5443b-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="5443b-333">Selecciona la acción de hello muestra hello mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="5443b-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="5443b-334">**Causa**: Hola direcciones WASB que se usan en hello **job.xml** archivos no contienen el contenedor de almacenamiento de Hola o nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="5443b-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="5443b-335">formato de dirección de Hello WASB debe ser `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="5443b-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="5443b-336">**Resolución**: cambiar hello WASB direcciones usadas Hola trabajo.</span><span class="sxs-lookup"><span data-stu-id="5443b-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="5443b-337">JA002: Oozie no se permite tooimpersonate &lt;usuario ></span><span class="sxs-lookup"><span data-stu-id="5443b-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="5443b-338">**Síntomas**: Hola cambios de estado del trabajo demasiado**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="5443b-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="5443b-339">Detalles de trabajo de hello Mostrar estado de RunHiveScript de hello como **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="5443b-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="5443b-340">Selecciona la acción de hello muestra hello mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="5443b-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="5443b-341">**Causa**: configuración de permiso actual no permite Oozie hello tooimpersonate cuenta de usuario especificada.</span><span class="sxs-lookup"><span data-stu-id="5443b-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="5443b-342">**Resolución**: Oozie se permite a los usuarios de tooimpersonate en hello **usuarios** grupo.</span><span class="sxs-lookup"><span data-stu-id="5443b-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="5443b-343">Hola de uso `groups USERNAME` grupos de hello toosee que Hola cuenta de usuario es miembro de.</span><span class="sxs-lookup"><span data-stu-id="5443b-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="5443b-344">Si el usuario de hello no es un miembro del programa Hola a **usuarios** grupo, use Hola después del grupo de comandos tooadd Hola usuario toohello:</span><span class="sxs-lookup"><span data-stu-id="5443b-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="5443b-345">Puede tardar varios minutos antes de HDInsight reconoce que el usuario Hola se ha agregado el grupo toohello.</span><span class="sxs-lookup"><span data-stu-id="5443b-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="5443b-346">ERROR del selector (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="5443b-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="5443b-347">**Síntomas**: Hola cambios de estado del trabajo demasiado**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="5443b-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="5443b-348">Detalles de trabajo de hello Mostrar estado de RunSqoopExport de hello como **ERROR**.</span><span class="sxs-lookup"><span data-stu-id="5443b-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="5443b-349">Selecciona la acción de hello muestra hello mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="5443b-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="5443b-350">**Causa**: Sqoop es tooload no se puede Hola controlador necesario tooaccess Hola de base.</span><span class="sxs-lookup"><span data-stu-id="5443b-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="5443b-351">**Resolución**: al utilizar Sqoop desde un trabajo de Oozie, debe incluir controladores de base de datos de hello con hello otros recursos (por ejemplo, hello workflow.xml) utilizados por el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="5443b-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="5443b-352">Hacer referencia a archivo Hola que contiene el controlador de la base de datos de Hola de hello `<sqoop>...</sqoop>` sección de hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="5443b-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="5443b-353">Por ejemplo, para el trabajo de hello en este documento, usaría Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="5443b-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="5443b-354">Copie el directorio /tutorials/useoozie toohello de hello sqljdbc4.1.jar archivos:</span><span class="sxs-lookup"><span data-stu-id="5443b-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="5443b-355">Modificar el siguiente XML en una nueva línea anterior de Hola workflow.xml tooadd Hola `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="5443b-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="5443b-356">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5443b-356">Next steps</span></span>

<span data-ttu-id="5443b-357">En este tutorial, se habrá aprendido cómo toodefine un flujo de trabajo de Oozie y cómo toorun un trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="5443b-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="5443b-358">toolearn más acerca de cómo trabajar con HDInsight, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="5443b-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="5443b-359">[Uso del coordinador de Oozie de tiempo con HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="5443b-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="5443b-360">[Carga de datos para trabajos de Hadoop en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="5443b-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="5443b-361">[Uso de Sqoop con Hadoop en HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="5443b-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="5443b-362">[Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="5443b-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="5443b-363">[Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="5443b-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="5443b-364">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="5443b-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
