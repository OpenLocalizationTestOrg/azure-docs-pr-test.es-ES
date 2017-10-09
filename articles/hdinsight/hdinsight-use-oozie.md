---
title: aaaUse Hadoop Oozie en HDInsight | Documentos de Microsoft
description: "Use Oozie de Hadoop en HDInsight, un servicio de big data. Obtenga información acerca de cómo toodefine un flujo de trabajo de Oozie y enviar un trabajo de Oozie."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="fb3e2-104">Usar Oozie con Hadoop toodefine y ejecutar un flujo de trabajo en HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb3e2-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="fb3e2-105">Obtenga información acerca de cómo toouse Apache Oozie toodefine un flujo de trabajo y ejecutar Hola flujo de trabajo de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="fb3e2-106">toolearn sobre Coordinador de Oozie hello, consulte [usar basado en tiempo coordinador de Oozie de Hadoop con HDInsight][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="fb3e2-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="fb3e2-107">toolearn Data Factory de Azure, consulte [uso de Pig y Hive con factoría de datos][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="fb3e2-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="fb3e2-108">Oozie de Apache es un sistema de coordinación o flujo de trabajo que administra trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="fb3e2-109">Se integra con la pila de Hadoop de Hola y admite trabajos de Hadoop MapReduce Apache, Pig Apache, Apache Hive y Sqoop de Apache.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="fb3e2-110">También puede ser tooschedule usado trabajos que el sistema tooa específico, como programas Java o secuencias de comandos de shell.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="fb3e2-111">flujo de trabajo de Hello que implementar siguiendo las instrucciones de hello en este tutorial contiene dos acciones:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Diagrama de flujo de trabajo][img-workflow-diagram]

1. <span data-ttu-id="fb3e2-113">Una acción de subárbol ejecuta un hello toocount de script de HiveQL apariciones de cada tipo de nivel de registro en un archivo log4j.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="fb3e2-114">Cada archivo log4j consta de una línea de campos que contiene un campo [nivel de registro] que muestra el tipo de Hola y la gravedad de hello, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="fb3e2-115">es similar a la salida del script de Hive Hola:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="fb3e2-116">Para más información sobre Hive, consulte [Uso de Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="fb3e2-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="fb3e2-117">Una acción de Sqoop exporta la tabla de tooa de salida de hello HiveQL en una base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="fb3e2-118">Para obtener más información sobre Sqoop, consulte [Uso de Hadoop Sqoop con HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="fb3e2-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="fb3e2-119">Para versiones compatibles de Oozie en clústeres de HDInsight, vea [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="fb3e2-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="fb3e2-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb3e2-120">Prerequisites</span></span>
<span data-ttu-id="fb3e2-121">Antes de comenzar este tutorial, debe tener Hola siguiente elemento:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="fb3e2-122">**Una estación de trabajo con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="fb3e2-123">Definir el flujo de trabajo de Oozie y Hola relacionados con script de HiveQL</span><span class="sxs-lookup"><span data-stu-id="fb3e2-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="fb3e2-124">Las definiciones de los flujos de trabajo de Oozie se escriben en hPDL (un lenguaje de definición de proceso XML).</span><span class="sxs-lookup"><span data-stu-id="fb3e2-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="fb3e2-125">es el nombre de archivo de flujo de trabajo predeterminado de Hello *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="fb3e2-126">Hola aquí te mostramos archivo de flujo de trabajo de Hola que se usa en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-126">hello following is hello workflow file you use in this tutorial.</span></span>

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

<span data-ttu-id="fb3e2-127">Hay dos acciones definidas en el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="fb3e2-128">Hola inicio-tooaction es *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="fb3e2-129">Si acción de Hola se ejecuta correctamente, acción siguiente hello es *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="fb3e2-130">Hola RunHiveScript tiene varias variables.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="fb3e2-131">Pasar valores de hello al enviar trabajo de Oozie Hola desde su estación de trabajo mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="fb3e2-132">Variables de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="fb3e2-132">Workflow variables</span></span></th><th><span data-ttu-id="fb3e2-133">Description</span><span class="sxs-lookup"><span data-stu-id="fb3e2-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="fb3e2-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-134">${jobTracker}</span></span></td><td><span data-ttu-id="fb3e2-135">Especifica la dirección URL de Hola de seguimiento de trabajo de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="fb3e2-136">Use <strong>jobtrackerhost: 9010</strong> en HDInsight versión 3.0 y 2.1.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="fb3e2-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-137">${nameNode}</span></span></td><td><span data-ttu-id="fb3e2-138">Especifica la dirección URL de hello del nodo de nombre de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="fb3e2-139">Use la dirección del sistema de archivos de Hola de forma predeterminada, por ejemplo, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="fb3e2-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-140">${queueName}</span></span></td><td><span data-ttu-id="fb3e2-141">Especifica el nombre de la cola de Hola que Hola trabajo se envía a.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="fb3e2-142">Hola de uso <strong>predeterminado</strong>.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="fb3e2-143">Variable de acción de Hive</span><span class="sxs-lookup"><span data-stu-id="fb3e2-143">Hive action variable</span></span></th><th><span data-ttu-id="fb3e2-144">Description</span><span class="sxs-lookup"><span data-stu-id="fb3e2-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="fb3e2-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="fb3e2-146">Especifica el directorio de origen de Hola de hello comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="fb3e2-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="fb3e2-148">Especifica la carpeta de salida de hello de hello instrucción INSERT SOBRESCRIBIR.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="fb3e2-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-149">${hiveTableName}</span></span></td><td><span data-ttu-id="fb3e2-150">Especifica el nombre de Hola de tabla de Hive de Hola que hace referencia a archivos de datos de log4j Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="fb3e2-151">Variable de acción de Sqoop</span><span class="sxs-lookup"><span data-stu-id="fb3e2-151">Sqoop action variable</span></span></th><th><span data-ttu-id="fb3e2-152">Description</span><span class="sxs-lookup"><span data-stu-id="fb3e2-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="fb3e2-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="fb3e2-154">Especifica la cadena de conexión de base de datos de SQL Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="fb3e2-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="fb3e2-156">Especifica la tabla de base de datos de SQL Azure Hola que se exportan datos de Hola a.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="fb3e2-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="fb3e2-158">Especifica la carpeta de salida de hello de hello instrucción Hive insertar SOBRESCRIBIR.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="fb3e2-159">Se trata de hello misma carpeta para la exportación de Sqoop Hola (export-dir).</span><span class="sxs-lookup"><span data-stu-id="fb3e2-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="fb3e2-160">Para obtener más información sobre el flujo de trabajo de Oozie y el uso de acciones de flujo de trabajo, consulte la [documentación de Oozie 4.0 de Apache (en inglés)][apache-oozie-400] (para la versión del clúster de HDInsight 3.0) o la [documentación de Oozie 3.3.2 de Apache (en inglés)][apache-oozie-332] (para la versión del clúster de HDInsight 2.1).</span><span class="sxs-lookup"><span data-stu-id="fb3e2-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="fb3e2-161">acción de Hive en el flujo de trabajo de Hola Hola llama a un archivo de script de HiveQL.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="fb3e2-162">El archivo de script contiene tres instrucciones de HiveQL:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="fb3e2-163">**instrucción DROP TABLE de Hello** eliminaciones Hola log4j Hive tabla si existe.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="fb3e2-164">**instrucción CREATE TABLE de Hello** crea una tabla externa del subárbol log4j que señala toohello ubicación del archivo de registro de hello log4j.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="fb3e2-165">delimitador de campo de Hello es ",".</span><span class="sxs-lookup"><span data-stu-id="fb3e2-165">hello field delimiter is ",".</span></span> <span data-ttu-id="fb3e2-166">delimitador de línea de saludo predeterminado es "\n".</span><span class="sxs-lookup"><span data-stu-id="fb3e2-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="fb3e2-167">Una tabla externa de subárbol es el archivo de datos de Hola de tooavoid utilizado está quitando de la ubicación original de hello si desea que el flujo de trabajo de toorun hello Oozie varias veces.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="fb3e2-168">**Hola instrucción INSERT SOBRESCRIBIR** recuentos de apariciones de Hola de cada tipo de nivel de registro de la tabla de Hive log4j hello y guarda el blob de tooa de salida de hello en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="fb3e2-169">Hay tres variables utilizadas en el script de Hola:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="fb3e2-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-170">${hiveTableName}</span></span>
* <span data-ttu-id="fb3e2-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="fb3e2-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="fb3e2-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="fb3e2-173">archivo de definición de flujo de trabajo de Hello (workflow.xml en este tutorial) pasa estos valores toothis script de HiveQL en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="fb3e2-174">Archivo de flujo de trabajo de Hola y archivo de hello HiveQL se almacenan en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="fb3e2-175">script de PowerShell usar más adelante en este tutorial Hola copia ambos cuenta de almacenamiento de archivos toohello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="fb3e2-176">Enviar trabajos de Oozie mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb3e2-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="fb3e2-177">Azure PowerShell no proporciona actualmente cmdlets para la definición de trabajos de Oozie.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="fb3e2-178">Puede usar hello **Invoke-RestMethod** servicios web de cmdlet tooinvoke Oozie.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="fb3e2-179">Hola Oozie API para servicios web es una API de JSON de REST de HTTP.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="fb3e2-180">Para obtener más información sobre los servicios web de Oozie Hola API, consulte [documentación de Apache Oozie 4.0] [ apache-oozie-400] (para HDInsight versión 3.0) o [documentación de Apache Oozie 3.3.2] [ apache-oozie-332] (para HDInsight versión 2.1).</span><span class="sxs-lookup"><span data-stu-id="fb3e2-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="fb3e2-181">Hola script de PowerShell de esta sección realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="fb3e2-182">Conectar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="fb3e2-183">Cree un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-183">Create an Azure resource group.</span></span> <span data-ttu-id="fb3e2-184">Para más información, vea [Usar Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fb3e2-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="fb3e2-185">Cree un servidor de Base de datos SQL de Azure, una base de datos SQL de Azure y dos tablas.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="fb3e2-186">Utiliza estos nombres Hola Sqoop acción en el flujo de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="fb3e2-187">es el nombre de la tabla de Hello *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="fb3e2-188">Crear un toorun de clúster utiliza HDInsight Oozie trabajos.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="fb3e2-189">clúster de hello tooexamine, puede usar Hola portal de Azure o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="fb3e2-190">Copie el archivo de flujo de trabajo de oozie hello y sistema de archivos predeterminado de hello HiveQL script archivos toohello.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="fb3e2-191">Ambos archivos se almacenan en un contenedor de blobs público.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="fb3e2-192">Copie hello HiveQL script (useoozie.hql) tooAzure (wasb:///tutorials/useoozie/useoozie.hql) de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="fb3e2-193">Copie el archivo workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="fb3e2-194">Archivo de datos de copia hello (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="fb3e2-195">Envíe un trabajo de Oozie.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="fb3e2-196">resultados del trabajo de tooexamine hello OOzie, use Visual Studio u otra toohello de tooconnect de herramientas base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="fb3e2-197">Este es el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-197">Here is hello script.</span></span>  <span data-ttu-id="fb3e2-198">Puede ejecutar el script de Hola desde Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="fb3e2-199">Solo necesita tooconfigure Hola primero 7 variables.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

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
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="fb3e2-200">**tutorial de ejecución toore Hola**</span><span class="sxs-lookup"><span data-stu-id="fb3e2-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="fb3e2-201">flujo de trabajo de ejecución toore hello, debe eliminar Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="fb3e2-202">Hola archivo de salida del script de Hive</span><span class="sxs-lookup"><span data-stu-id="fb3e2-202">hello Hive script output file</span></span>
* <span data-ttu-id="fb3e2-203">datos de Hello en la tabla de hello log4jLogsCount</span><span class="sxs-lookup"><span data-stu-id="fb3e2-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="fb3e2-204">Aquí tiene un script de PowerShell de ejemplo que puede usar:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="fb3e2-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb3e2-205">Next steps</span></span>
<span data-ttu-id="fb3e2-206">En este tutorial, se habrá aprendido cómo toodefine una Oozie flujo de trabajo y cómo toorun una Oozie de trabajo mediante el uso de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb3e2-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="fb3e2-207">toolearn más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="fb3e2-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="fb3e2-208">[Uso del coordinador de Oozie de tiempo con HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="fb3e2-209">[Empezar a trabajar con Hadoop Hive en el uso de auriculares móviles de tooanalyze de HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="fb3e2-210">[Uso de Azure Blob Storage con HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="fb3e2-211">[Administración de HDInsight con PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="fb3e2-212">[Carga de datos para trabajos de Hadoop en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="fb3e2-213">[Uso de Sqoop con Hadoop en HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="fb3e2-214">[Uso de Hive con Hadoop en HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="fb3e2-215">[Uso de Pig con Hadoop en HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="fb3e2-216">[Desarrollo de programas MapReduce de Java para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="fb3e2-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
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
